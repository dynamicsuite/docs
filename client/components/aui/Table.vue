<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <docs-aui-component v-bind="options" class="docs-container ds-container primary">
    <template #examples>
      <aui-table :table="table" />
    </template>
    <template #notes>
      <p>
        AUI tables are a "proto component" designed to be extended by higher level components.
      </p>
      <p>
        By default, tables only contain some basic styling, but have an assortment of events they can emit to a parent
        component (such as CRUD) to extend their functionality with sorting, interaction, etc.
      </p>
      <p>
        Table column layouts may be saved. By default, the layout is saved an retrieved via localstorage, but these
        values can also be saved on the server. When a save is requested, an event is broadcast back to the root
        instance for "aui-table-save" with the columns to save. You must handle this save by listening for this
        event.
      </p>
      <p>
        Before localstorage saves are requested, the component will look for:
        <code>window.dynamicsuite['custom']['aui_table'][storage_key]</code>
        to load the columns. If not found (set on server), localstorage will be used.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
export default {
  data() {
    return {
      table: [
        {col_1: 'col 1 test 1', col_2: 'col 2 test 1', col_3: 'col 3 test 1'},
        {col_1: 'col 1 test 2', col_2: 'col 2 test 2', col_3: 'col 3 test 2'},
        {col_1: 'col 1 test 3', col_2: 'col 2 test 3', col_3: 'col 3 test 3'},
        {col_1: 'col 1 test 4', col_2: 'col 2 test 4', col_3: 'col 3 test 4'},
        {col_1: 'col 1 test 5', col_2: 'col 2 test 5', col_3: 'col 3 test 5'}
      ],
      options: {
        syntax_js:
            "new Vue({\n" +
            "  el: '#test'\n" +
            "  data: {\n" +
            "    table: [\n" +
            "      {col_1: 'col 1 test 1', col_2: 'col 2 test 1', col_3: 'col 3 test 1'},\n" +
            "      {col_1: 'col 1 test 2', col_2: 'col 2 test 2', col_3: 'col 3 test 2'},\n" +
            "      {col_1: 'col 1 test 3', col_2: 'col 2 test 3', col_3: 'col 3 test 3'},\n" +
            "      {col_1: 'col 1 test 4', col_2: 'col 2 test 4', col_3: 'col 3 test 4'},\n" +
            "      {col_1: 'col 1 test 5', col_2: 'col 2 test 5', col_3: 'col 3 test 5'}\n" +
            "    ]\n" +
            "  },\n" +
            "});",
        syntax_html:
            '<div id="#test">\n' +
            '  <aui-table :table="table" />\n' +
            '</div>',
        events: {
          'update:sort(sort)': 'Update for "sort" (sync required)',
          'row-interaction(interactive_column)': 'When an interactive table row is clicked',
          '$root.aui-table-reset': 'When a table layout reset was requested',
          '$root.aui-table-save(columns)': 'When a table layout save was requested'
        },
        props: [
          {
            prop: 'table',
            type: 'Array',
            default: '[]',
            usage: 'The table data to render in the form of a raw array of rows of data where each row is an object.'
          },
          {
            prop: 'interactive',
            type: 'Boolean',
            default: 'false',
            usage: 'If the table is interactive and should emit something on row click.'
          },
          {
            prop: 'interactive_column',
            type: 'String | null',
            default: 'null',
            usage: 'The column to emit the value of on row interaction.'
          },
          {
            prop: 'default_columns',
            type: 'String[]',
            default: '[]',
            usage: 'The default columns that are visible on the table.'
          },
          {
            prop: 'column_names',
            type: 'Object',
            default: '{}',
            usage:
              'Column name map. This is an object where each key is the true column name and the value is the ' +
              'displayed value.'
          },
          {
            prop: 'column_format',
            type: 'Object',
            default: '{}',
            usage:
              'Column value format map. This is an object where each key is the true column name and the value is ' +
              'a function. The function may take one "value" where this is the true value, and returns the ' +
              'displayed value.'
          },
          {
            prop: 'row_classes',
            type: 'Function',
            default: '() => ({})',
            usage: 'Classes to apply to each row given an argument of the row data. Standard Vue classes object.'
          },
          {
            prop: 'sortable',
            type: 'Boolean',
            default: 'false',
            usage:
              'If the table is sortable. If sortable, icons will be added to the table header and clicking on the ' +
              'header will sort by that column. This component does not handle any of the sorting itself, but ' +
              'emits out a @sort event with which columns to sort by. Actual sorting functionality must be handled ' +
              'by the parent.'
          },
          {
            prop: 'sort',
            type: 'Object',
            default: '{}',
            usage:
              'Key, value pair for sorting. The key is the column to sort and the value is the sorting direction ' +
              '(ascending or descending). Must be synced back to the parent.'
          },
          {
            prop: 'sort_icon_none',
            type: 'String',
            default: 'fas fa-sort',
            usage: 'Column sorting icon (FontAwesome class): no sort on column.'
          },
          {
            prop: 'sort_icon_asc',
            type: 'String',
            default: 'fas fa-sort-amount-down',
            usage: 'Column sorting icon (FontAwesome class): ascending.'
          },
          {
            prop: 'sort_icon_desc',
            type: 'String',
            default: 'fas fa-sort-amount-down-alt',
            usage: 'Column sorting icon (FontAwesome class): descending.'
          },
          {
            prop: 'storage_key',
            type: 'String | null',
            default: 'null',
            usage:
              'Storage key for when saving the table layout for the client. Saving the layout will be set on in ' +
              'local storage and then broadcast to the root instance for handling saving via external source. ' +
              'Layouts saved on the server may go in window.dynamicsuite["custom"]["aui_table"][storage_key]. If ' +
              'not set or NULL, the layout will not be saved across refreshes.'
          },
          {
            prop: 'calling',
            type: 'Boolean',
            default: 'false',
            usage: 'If an API calling state is present for blocking interaction.'
          }
        ]
      }
    }
  }
}
</script>