# Table Column Width Alignment

## Overview
I contribute my code a UI change on table displayed on a modal.  The repository is the open-source project `KaotoIO/kaoto` , which is a visual Integration Designer for Apache Camel,which is an integration framwork that connects your application with services, APIs and data - whether they live in the cloud, on-premise, or both.

You can use  `Kaoto` as a VS Code Extenstion, in a containerized environment with `Podman` or as an Online Testing Instance at `https://kaotoio.github.io/kaoto/`

When you visit catalog section of `Kaoto`(https://kaotoio.github.io/kaoto/#/catalog), it provides a large collection of building blocks for graphical design. These categorized into 4 main groups: `Componenet`,`Processor`,`Entity` and `Kamelet`.
When you click on a building blocks , it display details about it in the from 3-tab modal. Each tab contain a table. 

Before I fix the issue , On `Endpoint Options` tab, the table was rendered by combining two individual tables for Path Parameters and Query Parameters. Infact this was the design approach used for other two parameters as well.  Because , it uses two indipendent tables and as column width depend on the content of the tables, the table widths were different for Path Parameter table and the Query Parameter table. As a result, the main table displayed vertically misaligned. Therfore, my task was to come up with a solution for this misalignemnt. 


## What happened
I picked up Issue #117, which reported a visual alignment bug in this modal:

> "The Endpoint Options tab in the component properties modal contains two tables with path parameters and query parameters. The tables are independent <PropertiesTableSimple> components so they have different formatting from each other which causes the columns to be not vertically aligned"

*Vertically Misaligned Table*
<img width="1879" height="745" alt="misaligned-tables" src="https://github.com/user-attachments/assets/5b9d4fef-58c9-498c-aed8-c5e22dc7d557" />



To reproduce the issue locally, I opened the catalog modal for a component containing both parameter types and inspected the DOM structure on the Endpoint Options tab. I confirmed that rendering two separate <PropertiesTableSimple> components caused each HTML table to size its columns independently based on its own text content, throwing off the vertical column alignment between the two sections.

Next, I checked PropertiesModal.scss and <PropertiesTableSimple> to see if any existing CSS controlled the column widths or table-layout, and found no explicit width rules. Because standard HTML tables calculate column widths per <table> element, trying to force separate tables into alignment with custom CSS widths would be fragile across different screen sizes and parameter names.

This led me to change my approach: instead of styling two separate tables to match, I refactored the component structure to group consecutive parameter tables together. By rendering them inside a single shared <Table> component using multiple row groups (<tbody> elements) and matching the group header styling to the original captions, I ensured that all sections share the exact same column constraints automatically.

*Vertically Aligned Table*
<img width="1895" height="749" alt="vertically-aligned-table" src="https://github.com/user-attachments/assets/1000663f-6ad1-4fc6-8eda-39c9a1194ed6" />


### The Changes I made
```
commit 2e8274162ed24ab3cb44d1e3733e06105536a513
Author: dineshigdd <dineshigdd@gmail.com>
Date:   Fri Nov 6 13:18:20 2026 -0800

    test(ui): cover properties tabs rendering

diff --git a/packages/ui/src/components/PropertiesModal/PropertiesTabs.test.tsx b/packages/ui/src/components/PropertiesModal/PropertiesTabs.test.tsx
new file mode 100644
index 00000000..052d590a
--- /dev/null
+++ b/packages/ui/src/components/PropertiesModal/PropertiesTabs.test.tsx
@@ -0,0 +1,58 @@
+import { render, screen } from '@testing-library/react';
+
+import { IPropertiesTable, PropertiesHeaders, PropertiesTableType } from './PropertiesModal.models';
+import { groupTables, PropertiesTabs } from './PropertiesTabs';
+
+describe('PropertiesTabs', () => {
+  const headers = [PropertiesHeaders.Name, PropertiesHeaders.Description];
+  const row = (name: string) => ({ name, description: name + ' description', type: 'string', rowAdditionalInfo: {} });
+
+  const simpleTable = (caption: string, tableHeaders = headers): IPropertiesTable => ({
+    type: PropertiesTableType.Simple,
+    headers: tableHeaders,
+    rows: [row(caption + '-row')],
+    caption,
+  });
+
+  const treeTable: IPropertiesTable = {
+    type: PropertiesTableType.Tree,
+    headers,
+    rows: [row('tree-row')],
+    caption: 'tree',
+  };
+
+  describe('groupTables', () => {
+    it('groups consecutive simple tables with identical headers', () => {
+      const groups = groupTables([simpleTable('path'), simpleTable('query')]);
+
+      expect(groups).toHaveLength(1);
+      expect(groups[0].startIndex).toBe(0);
+      expect(groups[0].tables.map((table) => table.caption)).toEqual(['path', 'query']);
+    });
+
+    it('keeps simple tables with different headers apart', () => {
+      const groups = groupTables([simpleTable('a'), simpleTable('b', [PropertiesHeaders.Name])]);
+
+      expect(groups.map((group) => group.startIndex)).toEqual([0, 1]);
+    });
+
+    it('never groups tree tables', () => {
+      const groups = groupTables([simpleTable('a'), treeTable, simpleTable('b')]);
+
+      expect(groups.map((group) => group.startIndex)).toEqual([0, 1, 2]);
+      expect(groups[1].tables).toEqual([treeTable]);
+    });
+  });
+
+  it('renders grouped simple tables as one table and a following tree table separately', () => {
+    const tables = [simpleTable('path'), simpleTable('query'), treeTable];
+    const { container } = render(<PropertiesTabs tab={{ rootName: 'tab', tables }} tab_index={0} />);
+
+    expect(container.querySelectorAll('table')).toHaveLength(2);
+    const sharedTable = screen.getByTestId('tab-0-table-0');
+    expect(sharedTable.tagName).toBe('TABLE');
+    expect(screen.queryByTestId('tab-0-table-1')).not.toBeInTheDocument();
+    expect(sharedTable).toContainElement(screen.getByTestId('tab-0-table-1-properties-modal-table-caption'));
+    expect(screen.getByTestId('tab-0-table-2-properties-modal-table-caption')).toHaveTextContent('tree');
+  });
+});

commit 3368db81c0471a809e4c11abb6580dabcc8838af
Author: dineshigdd <dineshigdd@gmail.com>
Date:   Fri Nov 6 13:15:56 2026 -0800

    fix(ui): align endpoint options columns by rendering parameter groups in one table

diff --git a/packages/ui/src/components/PropertiesModal/PropertiesModal.test.tsx b/packages/ui/src/components/PropertiesModal/PropertiesModal.test.tsx
index 91a726e9..2d01e3dc 100644
--- a/packages/ui/src/components/PropertiesModal/PropertiesModal.test.tsx
+++ b/packages/ui/src/components/PropertiesModal/PropertiesModal.test.tsx
@@ -1,6 +1,6 @@
 import catalogLibrary from '@kaoto/camel-catalog/index.json';
 import { CatalogLibrary } from '@kaoto/camel-catalog/types';
-import { screen, waitFor } from '@testing-library/dom';
+import { screen, waitFor, within } from '@testing-library/dom';
 import { act, render } from '@testing-library/react';
 
 import { CatalogContext } from '../../dynamic-catalog/catalog.provider';
@@ -110,11 +110,8 @@ describe('PropertiesModal', () => {
       expect(screen.getByTestId('tab-1-table-1-properties-modal-table-caption')).toHaveTextContent(
         'query parameters (26)',
       );
-      //headers
-      expect(screen.getByTestId('tab-1-table-1-header-name')).toHaveTextContent('name');
-      expect(screen.getByTestId('tab-1-table-1-header-description')).toHaveTextContent('description');
-      expect(screen.getByTestId('tab-1-table-1-header-default')).toHaveTextContent('default');
-      expect(screen.getByTestId('tab-1-table-1-header-type')).toHaveTextContent('type');
+      //headers are shared with table1 (single table, one header row)
+      expect(screen.queryByTestId('tab-1-table-1-header-name')).not.toBeInTheDocument();
       //rows
       expect(screen.getByTestId('tab-1-table-1-row-0-cell-name')).toHaveTextContent(
         'sendEmptyMessageWhenIdle (consumer)',
@@ -144,6 +141,39 @@ describe('PropertiesModal', () => {
       expect(screen.getByTestId('tab-2-table-0-row-0-cell-type')).toHaveTextContent('List');
       expect(screen.getByTestId('tab-2-table-0-row-0-cell-default')).toHaveTextContent('');
     });
+
+    it('renders endpoint options path and query parameters as row groups of a single table', async () => {
+      await renderModal(tile);
+      await waitFor(() => {
+        expect(screen.queryByText('Loading properties...')).not.toBeInTheDocument();
+      });
+      await act(async () => {
+        screen.getByTestId('tab-1').click();
+        await new Promise(process.nextTick);
+      });
+
+      // one shared table instead of one table per parameter group
+      const table = screen.getByTestId('tab-1-table-0');
+      expect(table.tagName).toBe('TABLE');
+      expect(screen.queryByTestId('tab-1-table-1')).not.toBeInTheDocument();
+
+      // both group captions are inside that table and span every column
+      const headerCount = table.querySelectorAll('thead tr th').length;
+      expect(headerCount).toBe(4);
+      const pathCaption = within(table).getByTestId('tab-1-table-0-properties-modal-table-caption');
+      const queryCaption = within(table).getByTestId('tab-1-table-1-properties-modal-table-caption');
+      expect(pathCaption).toHaveTextContent('path parameters (1)');
+      expect(queryCaption).toHaveTextContent('query parameters (26)');
+      expect(pathCaption).toHaveAttribute('colspan', String(headerCount));
+      expect(queryCaption).toHaveAttribute('colspan', String(headerCount));
+
+      // every data row has the same number of cells as the header row
+      const dataRows = table.querySelectorAll('tbody tr[data-testid*="-row-"]');
+      expect(dataRows).toHaveLength(27);
+      dataRows.forEach((row) => {
+        expect(row.querySelectorAll('td')).toHaveLength(headerCount);
+      });
+    });
   });
 
   describe('Component tile with empty properties and no headers/apis', () => {
@@ -205,6 +235,9 @@ describe('PropertiesModal', () => {
       expect(screen.getByTestId('tab-0-table-0-row-0-cell-description')).toHaveTextContent(
         'A short description for the security scheme.',
       );
+      // a single caption-less table renders no group heading row
+      expect(screen.queryByTestId('tab-0-table-0-properties-modal-table-caption')).not.toBeInTheDocument();
+      expect(screen.getByTestId('tab-0-table-0').querySelector('tbody th')).toBeNull();
     });
   });
 
diff --git a/packages/ui/src/components/PropertiesModal/PropertiesTabs.tsx b/packages/ui/src/components/PropertiesModal/PropertiesTabs.tsx
index 72c28604..148e7871 100644
--- a/packages/ui/src/components/PropertiesModal/PropertiesTabs.tsx
+++ b/packages/ui/src/components/PropertiesModal/PropertiesTabs.tsx
@@ -1,6 +1,6 @@
-import { FunctionComponent } from 'react';
+import { FunctionComponent, useMemo } from 'react';
 
-import { IPropertiesTab, PropertiesTableType } from './PropertiesModal.models';
+import { IPropertiesTab, IPropertiesTable, PropertiesTableType } from './PropertiesModal.models';
 import { PropertiesTableSimple, PropertiesTableTree } from './Tables';
 
 interface IPropertiesTabsProps {
@@ -8,28 +8,63 @@ interface IPropertiesTabsProps {
   tab_index: number;
 }
 
+/** A run of tables rendered together, plus the index of its first table within the tab */
+interface ITableGroup {
+  startIndex: number;
+  tables: IPropertiesTable[];
+}
+
+const haveSameHeaders = (a: IPropertiesTable, b: IPropertiesTable): boolean =>
+  a.headers.length === b.headers.length && a.headers.every((header, index) => header === b.headers[index]);
+
+/**
+ * Groups consecutive simple tables with identical headers so they can be rendered as row groups
+ * of a single table, which keeps their columns aligned. Tree tables always stay on their own.
+ */
+export const groupTables = (tables: IPropertiesTable[]): ITableGroup[] => {
+  const groups: ITableGroup[] = [];
+
+  tables.forEach((table, index) => {
+    const lastGroup = groups.at(-1);
+    const lastTable = lastGroup?.tables.at(-1);
+
+    if (
+      lastGroup &&
+      lastTable &&
+      table.type === PropertiesTableType.Simple &&
+      lastTable.type === PropertiesTableType.Simple &&
+      haveSameHeaders(lastTable, table)
+    ) {
+      lastGroup.tables.push(table);
+    } else {
+      groups.push({ startIndex: index, tables: [table] });
+    }
+  });
+
+  return groups;
+};
+
 export const PropertiesTabs: FunctionComponent<IPropertiesTabsProps> = (props) => {
+  const groups = useMemo(() => groupTables(props.tab.tables), [props.tab.tables]);
+
   return (
     <div>
-      {props.tab.tables.map((table, table_index) => {
-        switch (table.type) {
+      {groups.map((group) => {
+        const groupKey = 'tab-' + props.tab_index + '-table-' + group.startIndex;
+        const firstTable = group.tables[0];
+
+        switch (firstTable.type) {
           case PropertiesTableType.Simple:
             return (
               <PropertiesTableSimple
-                key={'tab-' + props.tab_index + '-table-' + table_index}
-                tables={[table]}
+                key={groupKey}
+                tables={group.tables}
                 rootDataTestId={'tab-' + props.tab_index}
-                startTableIndex={table_index}
+                startTableIndex={group.startIndex}
               />
             );
           case PropertiesTableType.Tree:
-            return (
-              <PropertiesTableTree
-                key={'tab-' + props.tab_index + '-table-' + table_index}
-                table={table}
-                rootDataTestId={'tab-' + props.tab_index + '-table-' + table_index}
-              />
-            );
+            return <PropertiesTableTree key={groupKey} table={firstTable} rootDataTestId={groupKey} />;
         }
       })}
     </div>

commit 9f95511c09093b1c52a6a5e3fef36bce6bb6745d
Author: dineshigdd <dineshigdd@gmail.com>
Date:   Fri Nov 6 13:06:28 2026 -0800

    fix(ui): align properties modal table columns

diff --git a/packages/ui/src/components/PropertiesModal/PropertiesModal.scss b/packages/ui/src/components/PropertiesModal/PropertiesModal.scss
index eadb99e9..7164ba96 100644
--- a/packages/ui/src/components/PropertiesModal/PropertiesModal.scss
+++ b/packages/ui/src/components/PropertiesModal/PropertiesModal.scss
@@ -26,6 +26,14 @@
     font-weight: normal;
   }
 
+  // Group heading row inside a shared table; mirrors the look of the former table caption
+  &__group-caption {
+    color: var(--pf-t--global--text--color--subtle);
+    font-size: var(--pf-t--global--font--size--sm);
+    font-weight: normal;
+    text-align: start;
+  }
+
   &__body {
     height: 75vh;
 

commit 3948cd7054fc947d7dda9ce3d45178406ab0273e
Author: dineshigdd <dineshigdd@gmail.com>
Date:   Fri Nov 6 10:43:33 2026 -0800

    refactor(ui): render properties table groups as row groups of one table
    
    PropertiesTableSimple now accepts a list of tables and renders them
    in one table with a shared header and one tbody per group. Group
    captions become rowgroup header rows. Callers still pass one table
    each, so the rendered output is unchanged.

diff --git a/packages/ui/src/components/PropertiesModal/PropertiesTabs.tsx b/packages/ui/src/components/PropertiesModal/PropertiesTabs.tsx
index ab7c7992..72c28604 100644
--- a/packages/ui/src/components/PropertiesModal/PropertiesTabs.tsx
+++ b/packages/ui/src/components/PropertiesModal/PropertiesTabs.tsx
@@ -17,8 +17,9 @@ export const PropertiesTabs: FunctionComponent<IPropertiesTabsProps> = (props) =
             return (
               <PropertiesTableSimple
                 key={'tab-' + props.tab_index + '-table-' + table_index}
-                table={table}
-                rootDataTestId={'tab-' + props.tab_index + '-table-' + table_index}
+                tables={[table]}
+                rootDataTestId={'tab-' + props.tab_index}
+                startTableIndex={table_index}
               />
             );
           case PropertiesTableType.Tree:
diff --git a/packages/ui/src/components/PropertiesModal/Tables/PropertiesTableSimple.tsx b/packages/ui/src/components/PropertiesModal/Tables/PropertiesTableSimple.tsx
index 825f7d7f..754e0490 100644
--- a/packages/ui/src/components/PropertiesModal/Tables/PropertiesTableSimple.tsx
+++ b/packages/ui/src/components/PropertiesModal/Tables/PropertiesTableSimple.tsx
@@ -1,29 +1,61 @@
-import { Caption, Table, Tbody, Thead, Tr } from '@patternfly/react-table';
+import { Table, Tbody, Th, Thead, Tr } from '@patternfly/react-table';
 import { FunctionComponent } from 'react';
 
 import { IPropertiesTable } from '../PropertiesModal.models';
 import { renderHeaders, renderRowData } from './PropertiesTableCommon';
 
 interface IPropertiesTableSimpleProps {
+  /** Tab-level test id prefix, e.g. `tab-1`. Each group gets `<prefix>-table-<index>`. */
   rootDataTestId: string;
-  table: IPropertiesTable;
+  /** Index of the first group within the tab, used to build per-group test ids. */
+  startTableIndex?: number;
+  /** Groups rendered as row groups of a single table. All groups are expected to share the same headers. */
+  tables: IPropertiesTable[];
 }
 
-export const PropertiesTableSimple: FunctionComponent<IPropertiesTableSimpleProps> = (props) => {
+export const PropertiesTableSimple: FunctionComponent<IPropertiesTableSimpleProps> = ({
+  rootDataTestId,
+  startTableIndex = 0,
+  tables,
+}) => {
+  if (tables.length === 0) {
+    return null;
+  }
+
+  const headers = tables[0].headers;
+  const getGroupDataTestId = (groupIndex: number) => `${rootDataTestId}-table-${startTableIndex + groupIndex}`;
+  const firstGroupDataTestId = getGroupDataTestId(0);
+
   return (
-    <Table aria-label="Simple table" variant="compact" data-testid={props.rootDataTestId}>
-      <Caption data-testid={props.rootDataTestId + '-properties-modal-table-caption'}>{props.table.caption}</Caption>
+    <Table aria-label="Simple table" variant="compact" data-testid={firstGroupDataTestId}>
       <Thead>
-        <Tr>{renderHeaders(props.table.headers, props.rootDataTestId)}</Tr>
+        <Tr>{renderHeaders(headers, firstGroupDataTestId)}</Tr>
       </Thead>
-      <Tbody>
-        {props.table.rows.length != 0 &&
-          props.table.rows.map((row, row_index) => (
-            <Tr data-testid={props.rootDataTestId + '-row-' + row_index} key={row.name}>
-              {renderRowData(props.table.headers, row, props.rootDataTestId + '-row-' + row_index, row_index)}
-            </Tr>
-          ))}
-      </Tbody>
+      {tables.map((table, groupIndex) => {
+        const groupDataTestId = getGroupDataTestId(groupIndex);
+
+        return (
+          <Tbody key={groupDataTestId} data-testid={groupDataTestId + '-group'}>
+            {table.caption !== undefined && (
+              <Tr>
+                <Th
+                  colSpan={headers.length}
+                  scope="rowgroup"
+                  className="properties-modal__group-caption"
+                  data-testid={groupDataTestId + '-properties-modal-table-caption'}
+                >
+                  {table.caption}
+                </Th>
+              </Tr>
+            )}
+            {table.rows.map((row, rowIndex) => (
+              <Tr data-testid={groupDataTestId + '-row-' + rowIndex} key={row.name}>
+                {renderRowData(headers, row, groupDataTestId + '-row-' + rowIndex, rowIndex)}
+              </Tr>
+            ))}
+          </Tbody>
+        );
+      })}
     </Table>
   );
 };
```

## Limitations and what's next
When I manually checked the output of these code changes, I focused primarily on the `ActiveMQ 6.x` block on the Endpoint Options tab and a few other blocks. I did not explicitly test the other two tabs (`Component options` or `Message Headers`). While the issue description noted that table misalignments can happen in different tabs whenever two or more tables are rendered within the same tab, and my unified row-group approach should theoretically resolve it globally, I did not verify those other tabs manually or with dedicated unit tests. 

As a next step, I would extend test coverage across the remaining tabs in the properties modal to validate that all multi-table views maintain consistent column alignment and robust rendering across the entire component catalog.
