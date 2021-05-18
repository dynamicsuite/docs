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
      <aui-alert
        title="Demo Alert"
        text="This is a demo alert"
        :show.sync="show"
        :closeable="true"
      />
      <p>Alerts come in the following styles:</p>
      <aui-alert type="primary" text="primary (default)" />
      <aui-alert type="secondary" text="secondary" />
      <aui-alert type="success" text="success" />
      <aui-alert type="warning" text="warning" />
      <aui-alert type="failure" text="failure" />
    </template>
    <template #notes>
      <p>
        Alerts display as flex full-width by default.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
export default {
  data() {
    return {
      show: true,
      options: {
        syntax_js:
          "new Vue({\n" +
          "  el: '#test',\n" +
          "  data: {\n" +
          "    show: true\n" +
          "  }\n" +
          "});",
        syntax_html:
          '<div id="#test">\n' +
          '  <aui-alert\n' +
          '    title="Demo Alert"\n' +
          '    text="This is a demo alert"\n' +
          '    :show.sync="show"\n' +
          '    :closeable="true"\n' +
          '  />\n' +
          '  <p>Alerts come in the following styles:</p>\n' +
          '  <aui-alert type="primary" text="primary (default)" />\n' +
          '  <aui-alert type="secondary" text="secondary" />\n' +
          '  <aui-alert type="success" text="success" />\n' +
          '  <aui-alert type="warning" text="warning" />\n' +
          '  <aui-alert type="failure" text="failure" />\n' +
          '</div>',
        events: {
          'update:show(show)': 'Update for "show" (sync required)',
          'close': 'When the close button is clicked (when closeable)'
        },
        slots: {
          'default': 'Any content in this slot will go in the alert message body'
        },
        props: [
          {
            prop: 'type',
            type: 'string',
            required: false,
            default: 'primary',
            usage:
              'The type of the alert determines which style class will be applied. Accepted values ' +
              'are: none, primary, secondary, success, warning, failure. Type "none" will not apply ' +
              'any additional style classes. All other types will add the type as a style class.'
          },
          {
            prop: 'title',
            type: 'string',
            required: false,
            default: 'null',
            usage: 'An optional title for the alert to display above the alert message.'
          },
          {
            prop: 'text',
            type: 'string | null',
            required: false,
            default: 'null',
            usage:
              'The body of the alert. This is an alias for the slot content when using ' +
              'plaintext. Slot should be used if custom HTML is required.'
          },
          {
            prop: 'show',
            type: 'boolean | string | null',
            required: false,
            default: 'true',
            usage: 'If the alert is shown and rendered on the DOM.'
          },
          {
            prop: 'closeable',
            type: 'boolean',
            required: false,
            default: 'false',
            usage: 'If the alert is closeable by the user.'
          }
        ]
      }
    }
  }
}
</script>