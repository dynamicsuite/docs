<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <docs-aui-component v-bind="options" class="docs-aui-checkbox docs-container ds-container primary">
    <template #examples>
      <p>
        The CRUD list component is quite large and complex, far too much to document here. Resources available:
      </p>
      <p>
        <a href="https://github.com/dynamicsuite/aui-crud-demo">Crud Demo Package Repository</a>
      </p>
    </template>
    <template #notes>
      <p>
        The CRUD list component is designed to read incremental data from a DS API and render it on the page, either as
        a list group or table.
      </p>
      <p>
        Primary features include sorting and filtering of incremental data.
      </p>
      <p>
        The server-side class <code>CrudRead</code> should be consulted for implementation.
      </p>
      <p>
        Error in API calls must be handled externally via the <code>@error</code> event.
      </p>
      <p>
        By default, all CRUD list components will use the same GET keys for saving state to the URL. If you have more
        than one CRUD list component on the page, you must change each GET key to something unique.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
export default {
  data() {
    return {
      options: {
        events: {
          'update:calling(calling)': 'Update for "calling" (sync required)',
          'error': 'When there is a server-side error',
          'show-create': 'When the "create" button is clicked',
          'list-interaction(storable_key)': 'When there is an interaction with a storable in the list'
        },
        slots: {
          'actions': 'Additional action components to go in the header preceding all default actions.',
          'pre-data': 'Additional content to go before the data',
        },
        props: [
          {
            prop: 'title',
            type: 'String',
            default: 'CRUD List',
            usage: 'Title of the list.'
          },
          {
            prop: 'show_create',
            type: 'Boolean',
            default: 'true',
            usage: 'If the create button should be shown.'
          },
          {
            prop: 'create_icon',
            type: 'String',
            default: 'fas fa-plus',
            usage: 'The FontAwesome icon class to show on the create button (if visible).'
          },
          {
            prop: 'show_filter',
            type: 'Boolean',
            default: 'true',
            usage: 'If the filter should be shown.'
          },
          {
            prop: 'filter_placeholder',
            type: 'String',
            default: 'Filter',
            usage: 'Placeholder for the filter input (if visible).'
          },
          {
            prop: 'no_data_icon',
            type: 'String',
            default: 'fas fa-ban',
            usage: 'The FontAwesome icon class to show when there is no data.'
          },
          {
            prop: 'no_data_text',
            type: 'String',
            default: 'No data',
            usage: 'The text to display under the icon when there is no data.'
          },
          {
            prop: 'loading_icon',
            type: 'String',
            default: 'fas fa-circle-notch fa-spin',
            usage: 'The FontAwesome icon class to show when the list is loading.'
          },
          {
            prop: 'loading_text',
            type: 'String | null',
            default: 'Loading...',
            usage: 'The text to display under the icon when the list is loading.'
          },
          {
            prop: 'calling',
            type: 'Boolean',
            default: 'false',
            usage: 'Calling state of any APIs. Must be synced to parent.'
          },
          {
            prop: 'overlay',
            type: 'Boolean',
            default: 'false',
            usage: 'Overlay state for disabling elements. Must be synced to parent.'
          },
          {
            prop: 'type',
            type: 'String',
            default: 'table',
            usage: 'The type of the list. Supports "group" or "table".'
          },
          {
            prop: 'storable_key',
            type: 'String',
            default: 'id',
            usage: 'Storable key for entries.'
          },
          {
            prop: 'group_icon_key',
            type: 'String',
            default: 'icon',
            usage: 'Icon column to use in the data when in group mode.'
          },
          {
            prop: 'group_title_key',
            type: 'String',
            default: 'title',
            usage: 'Title column to use in the data when in group mode.'
          },
          {
            prop: 'group_subtext_key',
            type: 'String',
            default: 'subtext',
            usage: 'Subtext column to use in the data when in group mode.'
          },
          {
            prop: 'table_default_columns',
            type: 'Array',
            default: '[]',
            usage: 'The default columns to show on the table when in table mode.'
          },
          {
            prop: 'table_column_names',
            type: 'Object',
            default: '{}',
            usage:
                'Column name map when in table mode. This is an object where each key is the true column name and ' +
                'the value is the displayed value.'
          },
          {
            prop: 'table_column_format',
            type: 'Object',
            default: '{}',
            usage:
                'Column value format map when in table mode. This is an object where each key is the true column ' +
                'name and the value is a function. The function may take one "value" where this is the true value, ' +
                'and returns the displayed value.'
          },
          {
            prop: 'table_storage_key',
            type: 'String | null',
            default: 'null',
            usage:
                'Storage key for when saving the table layout for the client. Saving the layout will be set on in ' +
                'local storage and then broadcast to the root instance for handling saving via external source. ' +
                'Layouts saved on the server may go in window.dynamicsuite["custom"]["aui_table"][storage_key]. If ' +
                'not set or NULL, the layout will not be saved across refreshes.'
          },
          {
            prop: 'read_api',
            type: 'String',
            required: true,
            usage: 'Read API for reading the list data.'
          },
          {
            prop: 'read_optional_data',
            type: 'Object',
            default: '{}',
            usage: 'Optional data to send along with the read API.'
          },
          {
            prop: 'range_limit',
            type: 'Array',
            default: '[20, 50, 100]',
            usage: 'Number of records to limit the list to. Defaults to the first value.'
          },
          {
            prop: 'filter_delay',
            type: 'Number',
            default: '300',
            usage: 'The delay from inactivity in the filter box until the list refreshes (in milliseconds).'
          },
          {
            prop: 'refresh_interval',
            type: 'Number | null',
            default: 'null',
            usage:
                'Refresh interval for refreshing the list automatically (re-runs the read API). Given in seconds, a ' +
                'value of NULL will never refresh.'
          },
          {
            prop: 'get_key_limit',
            type: 'String',
            default: 'limit',
            usage: 'URL GET key for list limit.'
          },
          {
            prop: 'get_key_page',
            type: 'String',
            default: 'page',
            usage: 'URL GET key for list page.'
          },
          {
            prop: 'get_key_filter',
            type: 'String',
            default: 'filter',
            usage: 'URL GET key for list filter.'
          },
          {
            prop: 'get_key_sort',
            type: 'String',
            default: 'sort',
            usage: 'URL GET key for list sort.'
          }
        ]
      }
    }
  }
}
</script>