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
      <aui-wysiwyg label="demo" />
      <aui-wysiwyg label="disabled" :disabled="true" />
      <aui-wysiwyg label="success" success="success" />
      <aui-wysiwyg label="failure" failure="failure" />
      <aui-wysiwyg label="subtext" subtext="subtext" />
    </template>
    <template #notes>
      <p>
        All form control components can be bound with v-model.
      </p>
      <p>
        All form control components default to full width flex.
      </p>
      <p>
        When running a local api, you may tie the disabled state to the api's calling state. Usually the
        return of this API is so fast that it causes a "flashing" effect on the form. To get around this you
        should create a delayed overlay property on your form to initiate the disabled state if an API
        takes longer than ~300ms.
      </p>
      <p>
        When the failure state evaluates to true, a watcher triggers to scroll to the highest failed form
        control component.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
export default {
  data() {
    return {
      options: {
        syntax_js:
            "new Vue({\n" +
            "  el: '#test'\n" +
            "});",
        syntax_html:
            '<div id="#test">\n' +
            '  <aui-wysiwyg label="demo" />\n' +
            '  <aui-wysiwyg label="disabled" :disabled="true" />\n' +
            '  <aui-wysiwyg label="success" success="success" />\n' +
            '  <aui-wysiwyg label="failure" failure="failure" />\n' +
            '  <aui-wysiwyg label="subtext" subtext="subtext" />\n' +
            '</div>',
        events: {
          'input($event.target.value)': 'When input is registered in the component'
        },
        slots: {
          'default': 'Any content in this slot will go in the component label'
        },
        props: [
          {
            prop: 'label',
            type: 'String | null',
            required: false,
            default: 'null',
            usage:
              'Component label. This is an alias for the slot content when using plaintext. Slot ' +
              'should be used if custom HTML is required.'
          },
          {
            prop: 'actions',
            type: 'Array',
            required: false,
            default: ['bold', 'italic', 'underline', 'heading1', 'ulist', 'olist'],
            usage: 'Pell action bar actions.'
          },
          {
            prop: 'default_paragraph_separator',
            type: 'String',
            required: false,
            default: 'p',
            usage: 'Default HTML tag separator for paragraphs.'
          },
          {
            prop: 'style_with_css',
            type: 'Boolean',
            required: false,
            default: 'true',
            usage: 'If the content should be styled with CSS vs tags.'
          },
          {
            prop: 'classes',
            type: 'Object',
            required: false,
            default: {
              actionbar: 'pell-actionbar',
              button: 'pell-btn',
              content: 'pell-content',
              selected: 'pell-button-selected'
            },
            usage: 'Custom Pell widget classes.'
          },
          {
            prop: 'value',
            type: 'String | Number | Boolean | null',
            required: false,
            default: 'null',
            usage: 'The model binding value of the component.'
          },
          {
            prop: 'disabled',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage: 'If the component is disabled and non-interactive.'
          },
          {
            prop: 'success',
            type: 'String | null',
            required: false,
            default: 'null',
            usage:
              'Success subtext to display under the component. Subtext values override each other in ' +
              'the following order, only one may be present at a time: success > failure > subtext.'
          },
          {
            prop: 'failure',
            type: 'String | null',
            required: false,
            default: 'null',
            usage:
              'Failure subtext to display under the component. Subtext values override each other in ' +
              'the following order, only one may be present at a time: success > failure > subtext.'
          },
          {
            prop: 'subtext',
            type: 'String | null',
            required: false,
            default: 'null',
            usage:
              'Subtext to display under the component. Subtext values override each other in ' +
              'the following order, only one may be present at a time: success > failure > subtext.'
          }
        ]
      }
    }
  }
}
</script>