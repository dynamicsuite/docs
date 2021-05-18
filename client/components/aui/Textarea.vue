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
      <aui-textarea label="demo" placeholder="demo" rows="5" />
      <aui-textarea label="disabled" :disabled="true" />
      <aui-textarea label="success" success="success" />
      <aui-textarea label="failure" failure="failure" />
      <aui-textarea label="subtext" subtext="subtext" />
      <aui-textarea label="leading cap" leading_cap="leading cap" />
      <aui-textarea label="trailing cap" trailing_cap="trailing cap" />
      <aui-textarea label="caps with feedback" trailing_cap="trailing cap" failure="oops!" />
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
            '  <aui-textarea label="demo" placeholder="demo" rows="5" />\n' +
            '  <aui-textarea label="disabled" :disabled="true" />\n' +
            '  <aui-textarea label="success" success="success" />\n' +
            '  <aui-textarea label="failure" failure="failure" />\n' +
            '  <aui-textarea label="subtext" subtext="subtext" />\n' +
            '  <aui-textarea label="leading cap" leading_cap="leading cap" />\n' +
            '  <aui-textarea label="trailing cap" trailing_cap="trailing cap" />\n' +
            '  <aui-textarea label="caps with feedback" trailing_cap="trailing cap" failure="oops!" />\n' +
            '</div>',
        events: {
          'focus($event.target)': 'When the component is focused',
          'blur($event.target)': 'When the component is blurred',
          'input($event.target.value)': 'When input is registered in the component',
          'keydown($event)': 'When there is a key pressed down while focused'
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
            prop: 'leading_cap',
            type: 'String | null',
            required: false,
            default: 'null',
            usage: 'Content to display in the leading component cap. Free-form HTML.'
          },
          {
            prop: 'trailing_cap',
            type: 'String | null',
            required: false,
            default: 'null',
            usage: 'Content to display in the trailing component cap. Free-form HTML.'
          },
          {
            prop: 'value',
            type: 'String | Number | Boolean | null',
            required: false,
            default: 'null',
            usage: 'The model binding value of the component.'
          },
          {
            prop: 'autocomplete',
            type: 'String | null',
            required: false,
            default: 'null',
            usage: 'Component autocomplete value.'
          },
          {
            prop: 'placeholder',
            type: 'String | null',
            required: false,
            default: 'null',
            usage: 'Component placeholder text.'
          },
          {
            prop: 'disabled',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage: 'If the component is disabled and non-interactive.'
          },
          {
            prop: 'rows',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'The rows (height) of the component.'
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