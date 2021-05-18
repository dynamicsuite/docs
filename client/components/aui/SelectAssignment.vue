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
      <aui-select-assignment :assigned.sync="assigned" :unassigned.sync="unassigned" />
    </template>
    <template #notes>
      <p>
        Select assignments display as flex full-width by default.
      </p>
      <p>
        This component is intended to be used with "sync" vue modifiers to re-sync the changed lists back to the
        parent.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
export default {
  data() {
    return {
      assigned: {
        1: 'Option 1',
        2: 'Option 2'
      },
      unassigned: {
        3: 'Option 3',
        4: 'Option 4'
      },
      options: {
        syntax_js:
            "new Vue({\n" +
            "  el: '#test'\n" +
            "  data: {\n" +
            "    assigned: {\n" +
            "      1: 'Option 1',\n" +
            "      2: 'Option 2'\n" +
            "    },\n" +
            "    unassigned: {\n" +
            "      3: 'Option 3',\n" +
            "      4: 'Option 4'\n" +
            "    }\n" +
            "  }\n" +
            "});",
        syntax_html:
            '<div id="#test">\n' +
            '  <aui-select-assignment :assigned.sync="assigned" :unassigned.sync="unassigned" />\n' +
            '</div>',
        events: {
          'update:assigned(assigned)': 'Update for "assigned" (sync required)',
          'update:unassigned(unassigned)': 'Update for "unassigned" (sync required)',
        },
        props: [
          {
            prop: 'assigned',
            type: 'Object | null',
            required: true,
            default: 'null',
            usage: 'Key-value list of assigned options.'
          },
          {
            prop: 'assigned_label',
            type: 'String',
            required: false,
            default: 'Assigned',
            usage: 'Label for the "assigned" list.'
          },
          {
            prop: 'unassigned',
            type: 'Object | null',
            required: true,
            default: 'null',
            usage: 'Key-value list of unassigned options.'
          },
          {
            prop: 'unassigned_label',
            type: 'String',
            required: false,
            default: 'Unassigned',
            usage: 'Label for the "unassigned" list.'
          },
          {
            prop: 'disabled',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage: 'If all selects and buttons are disabled non-interactive.'
          },
          {
            prop: 'size',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'The number of visible options.'
          }
        ]
      }
    }
  }
}
</script>