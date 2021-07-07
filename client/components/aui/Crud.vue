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
      <p>
        The CRUD interface is quite large and complex, far too much to document here. Resources available:
      </p>
      <p>
        <a href="https://github.com/dynamicsuite/aui-crud-demo">Crud Demo Package Repository</a>
      </p>
    </template>
    <template #notes>
      <p>
        Every root element in the <code>#form</code> slot will automatically have a 1rem margin-bottom applied.
      </p>
      <p>
        The property <code>overlay</code> is exported by the slot <code>#form</code> and should be used to display
        delayed loading and disabling form control.
      </p>
      <p>
        By default, all CRUD components will use the same GET key for saving state to the URL. If you have more than one
        CRUD component on the page, you must change the GET key to something unique.
      </p>
      <h4>APIs:</h4>
      <p>
        The following are all of the associated APIs and what they can return. Anything else returned will
        result in a failure notice being shown and the page must be refreshed.
      </p>
      <h5>List Read:</h5>
      <ul>
        <li>
          <code>OK</code> - The list data was read. see the class <code>AUICrudRead</code>
        </li>
      </ul>
      <h5>Form Create:</h5>
      <ul>
        <li>
          <code>INPUT_ERROR</code> - Can return a standard input validation array when invalid values were
          found (missing fields, etc).
        </li>
        <li>
          <code>OK</code> - Must return the new storable ID on success.
        </li>
      </ul>
      <h5>Form Read:</h5>
      <ul>
        <li>
          <code>NOT_FOUND</code> - If the storable was not found, this will redirect the user to the list.
        </li>
        <li>
          <code>OK</code> - If the storable was read. Must return the data as defined by the "fields"
          property.
        </li>
      </ul>
      <h5>Form Update:</h5>
      <ul>
        <li>
          <code>INPUT_ERROR</code> - Can return a standard input validation array when invalid values were
          found (missing fields, etc).
        </li>
        <li>
          <code>OK</code> - No additional data is returned on success.
        </li>
      </ul>
      <h5>Form Delete:</h5>
      <ul>
        <li>
          <code>DELETE_PROTECT</code> - Use this if the storable cannot be deleted for a specific reason.
        </li>
        <li>
          <code>OK</code> - No additional data is returned on success.
        </li>
      </ul>
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
          'update:feedback(feedback)': 'Update for "feedback" (sync required)',
          'update:form(form)': 'Update for "form" (sync required)',
          'form-pre-read': 'Right before the form storable is read'
        },
        slots: {
          'list-actions': 'Additional content to go on the list view next to the filter',
          'list-pre-data': 'Additional content to go on the list view before the data',
          'form': 'The content of the form',
          'form-back-button': 'Override for the back button on the form'
        },
        props: [
          {
            prop: 'error_icon',
            type: 'String',
            default: 'fas fa-exclamation-triangle',
            usage: 'FontAwesome icon class to display for the error notice.'
          },
          {
            prop: 'error_text',
            type: 'String',
            default: 'A server error has occurred',
            usage: 'Text to display for the error notice.'
          },
          {
            prop: 'error_subtext',
            type: 'String',
            default: 'Please reload the page',
            usage: 'Subtext to display for the error notice.'
          },
          {
            prop: 'storable_key',
            type: 'String',
            default: 'id',
            usage: 'Storable key for entries.'
          },
          {
            prop: 'get_key_id',
            type: 'String',
            default: 'crud',
            usage:
              'URL GET key for which view CRUD is on. A value of 0 means "show create" where as any other value ' +
              'will read the storable of that value and show the update page.'
          },
          {
            prop: 'calling',
            type: 'Boolean',
            default: 'false',
            usage: 'Calling state of any APIs. Must be synced to parent.'
          },
          {
            prop: 'list_title',
            type: 'String',
            default: 'CRUD List',
            usage: 'Title of the list.'
          },
          {
            prop: 'list_show_create',
            type: 'Boolean',
            default: 'true',
            usage: 'If the create button should be shown on the list.'
          },
          {
            prop: 'list_create_icon',
            type: 'String',
            default: 'fas fa-plus',
            usage: 'The FontAwesome icon class to show on the create button (if visible).'
          },
          {
            prop: 'list_show_filter',
            type: 'Boolean',
            default: 'true',
            usage: 'If the filter should be shown.'
          },
          {
            prop: 'list_filter_placeholder',
            type: 'String',
            default: 'Filter',
            usage: 'Placeholder for the filter input (if visible).'
          },
          {
            prop: 'list_no_data_icon',
            type: 'String',
            default: 'fas fa-ban',
            usage: 'The FontAwesome icon class to show when there is no data.'
          },
          {
            prop: 'list_no_data_text',
            type: 'String',
            default: 'No data',
            usage: 'The text to display under the icon when there is no data.'
          },
          {
            prop: 'list_loading_icon',
            type: 'String',
            default: 'fas fa-circle-notch fa-spin',
            usage: 'The FontAwesome icon class to show when the list is loading.'
          },
          {
            prop: 'list_loading_text',
            type: 'String | null',
            default: 'Loading...',
            usage: 'The text to display under the icon when the list is loading.'
          },
          {
            prop: 'list_type',
            type: 'String',
            default: 'table',
            usage: 'The type of the list. Supports "group" or "table".'
          },
          {
            prop: 'list_group_icon_key',
            type: 'String',
            default: 'icon',
            usage: 'Icon column to use in the data when in group mode.'
          },
          {
            prop: 'list_group_title_key',
            type: 'String',
            default: 'title',
            usage: 'Title column to use in the data when in group mode.'
          },
          {
            prop: 'list_group_subtext_key',
            type: 'String',
            default: 'subtext',
            usage: 'Subtext column to use in the data when in group mode.'
          },
          {
            prop: 'list_table_default_columns',
            type: 'Array',
            default: '[]',
            usage: 'The default columns to show on the table when in table mode.'
          },
          {
            prop: 'list_table_column_names',
            type: 'Object',
            default: '{}',
            usage:
              'Column name map when in table mode. This is an object where each key is the true column name and ' +
              'the value is the displayed value.'
          },
          {
            prop: 'list_table_column_format',
            type: 'Object',
            default: '{}',
            usage:
              'Column value format map when in table mode. This is an object where each key is the true column ' +
              'name and the value is a function. The function may take one "value" where this is the true value, ' +
              'and returns the displayed value.'
          },
          {
            prop: 'list_table_storage_key',
            type: 'String | null',
            default: 'null',
            usage:
              'Storage key for when saving the table layout for the client. Saving the layout will be set on in ' +
              'local storage and then broadcast to the root instance for handling saving via external source. ' +
              'Layouts saved on the server may go in window.dynamicsuite["custom"]["aui_table"][storage_key]. If ' +
              'not set or NULL, the layout will not be saved across refreshes.'
          },
          {
            prop: 'list_read_api',
            type: 'String',
            required: true,
            usage: 'Read API for reading the list data.'
          },
          {
            prop: 'list_read_optional_data',
            type: 'Object',
            default: '{}',
            usage: 'Optional data to send along with the read API.'
          },
          {
            prop: 'list_range_limit',
            type: 'Array',
            default: '[20, 50, 100]',
            usage: 'Number of records to limit the list to. Defaults to the first value.'
          },
          {
            prop: 'list_filter_delay',
            type: 'Number',
            default: '300',
            usage: 'The delay from inactivity in the filter box until the list refreshes (in milliseconds).'
          },
          {
            prop: 'list_refresh_interval',
            type: 'Number | null',
            default: 'null',
            usage:
              'Refresh interval for refreshing the list automatically (re-runs the read API). Given in seconds, a ' +
              'value of NULL will never refresh.'
          },
          {
            prop: 'list_get_key_limit',
            type: 'String',
            default: 'limit',
            usage: 'URL GET key for list limit.'
          },
          {
            prop: 'list_get_key_page',
            type: 'String',
            default: 'page',
            usage: 'URL GET key for list page.'
          },
          {
            prop: 'list_get_key_filter',
            type: 'String',
            default: 'filter',
            usage: 'URL GET key for list filter.'
          },
          {
            prop: 'list_get_key_sort',
            type: 'String',
            default: 'sort',
            usage: 'URL GET key for list sort.'
          },
          {
            prop: 'form',
            type: 'Object',
            default: '{}',
            usage: 'The actual form data sent to APIs.'
          },
          {
            prop: 'form_secure_fields',
            type: 'Array',
            default: '[]',
            usage:
                'Secure fields that are cleared after API calls (such as passwords). This is an array of "field" names.'
          },
          {
            prop: 'feedback',
            type: 'Object',
            default: '{}',
            usage: 'Form feedback'
          },
          {
            prop: 'form_loading_icon',
            type: 'String',
            default: 'fas fa-circle-notch fa-spin',
            usage: 'The FontAwesome icon class to show when the form is loading.'
          },
          {
            prop: 'form_loading_text',
            type: 'String|null',
            default: 'Loading...',
            usage: 'The text to display under the icon when the form is loading.'
          },
          {
            prop: 'form_create_setup_api',
            type: 'String|null',
            default: 'null',
            usage: 'API to call to pre-fill the form when creating a new storable.'
          },
          {
            prop: 'form_create_setup_api_data',
            type: 'Object',
            default: '{}',
            usage: 'Additional data to send along with the form create setup API.'
          },
          {
            prop: 'form_create_api',
            type: 'String|null',
            default: 'null',
            usage: 'API to call to create a new storable.'
          },
          {
            prop: 'form_create_api_data',
            type: 'Object',
            default: '{}',
            usage: 'Additional data to send along with the form create API.'
          },
          {
            prop: 'form_read_api',
            type: 'String|null',
            default: 'null',
            required: true,
            usage: 'API to call to read a storable to pre-fill the form when editing/viewing.'
          },
          {
            prop: 'form_read_api_data',
            type: 'Object',
            default: '{}',
            usage: 'Additional data to send along with the form read API.'
          },
          {
            prop: 'form_update_api',
            type: 'String|null',
            default: 'null',
            usage: 'API to call to update the active storable.'
          },
          {
            prop: 'form_update_api_data',
            type: 'Object',
            default: '{}',
            usage: 'Additional data to send along with the form update API.'
          },
          {
            prop: 'form_delete_api',
            type: 'String|null',
            default: 'null',
            usage: 'API to call to delete the active storable.'
          },
          {
            prop: 'form_delete_api_data',
            type: 'Object',
            default: '{}',
            usage: 'Additional data to send along with the form delete API.'
          },
          {
            prop: 'form_exclude_columns',
            type: 'String[]',
            default: '[]',
            usage: 'Columns to exclude from API calls.'
          },
          {
            prop: 'form_format_columns',
            type: 'Object',
            default: '{}',
            usage:
              'Format specific columns when sent to API calls. This is an object where the key is the column and ' +
              'the value is a function that returns a formatted value. This function takes 1 argument, the actual ' +
              'form value.'
          },
          {
            prop: 'form_show_actions',
            type: 'Boolean',
            default: 'true',
            usage: 'If the form actions should be shown.'
          },
          {
            prop: 'form_show_back_button',
            type: 'Boolean',
            default: 'true',
            usage: 'If the back button should be show on the form actions.'
          },
          {
            prop: 'form_action_back_text',
            type: 'String',
            default: 'Back',
            usage: 'Text to display on the form action for "Back".'
          },
          {
            prop: 'form_action_update_text',
            type: 'String',
            default: 'Update',
            usage: 'Text to display on the form action for "Update".'
          },
          {
            prop: 'form_action_update_loading_text',
            type: 'String',
            default: 'Updating...',
            usage: 'Text to display on the form action for "Update" when loading.'
          },
          {
            prop: 'form_action_create_text',
            type: 'String',
            default: 'Create',
            usage: 'Text to display on the form action for "Create".'
          },
          {
            prop: 'form_action_create_loading_text',
            type: 'String',
            default: 'Creating...',
            usage: 'Text to display on the form action for "Create" when loading.'
          },
          {
            prop: 'form_created_confirmation_icon',
            type: 'String',
            default: 'fas fa-check-circle',
            usage: 'FontAwesome icon class to display on the created confirmation splash screen.'
          },
          {
            prop: 'form_created_confirmation_text',
            type: 'String',
            default: 'Created!',
            usage: 'Text to display on the created confirmation splash screen.'
          },
          {
            prop: 'form_action_delete_cancel_text',
            type: 'String',
            default: 'Cancel',
            usage: 'Text to display on the form action for "Delete" when canceling.'
          },
          {
            prop: 'form_action_delete_text',
            type: 'String',
            default: 'Delete',
            usage: 'Text to display on the form action for "Delete".'
          },
          {
            prop: 'form_action_delete_loading_text',
            type: 'String',
            default: 'Deleting...',
            usage: 'Text to display on the form action for "Delete" when loading.'
          },
          {
            prop: 'form_action_delete_prompt',
            type: 'String',
            default: 'Are you sure you want to delete?',
            usage: 'Text to display on the modal body when deleting a storable.'
          },
          {
            prop: 'form_feedback_success_tick_icon',
            type: 'String',
            default: 'fas fa-check',
            usage: 'FontAwesome icon class to show on the "success" feedback tick.'
          },
          {
            prop: 'form_feedback_failure_tick_icon',
            type: 'String',
            default: 'fas fa-times',
            usage: 'FontAwesome icon class to show on the "failure" feedback tick.'
          },
          {
            prop: 'form_created_to_list',
            type: 'Boolean',
            default: 'true',
            usage: 'If you should be returned to the list view on creation.'
          }
        ]
      }
    }
  }
}
</script>
