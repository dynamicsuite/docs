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
      <aui-input label="demo" placeholder="demo" />
      <aui-input label="datalist" :options="['Option 1', 'Option 2']" />
      <aui-input label="telephone (US)" type="tel" placeholder="(___) ___-____" />
      <aui-input label="disabled" :disabled="true" />
      <aui-input label="success" success="success" />
      <aui-input label="failure" failure="failure" />
      <aui-input label="subtext" subtext="subtext" />
      <aui-input label="leading cap" leading_cap="leading cap" />
      <aui-input label="trailing cap" trailing_cap="trailing cap" />
      <aui-input label="caps with feedback" trailing_cap="trailing cap" failure="oops!" />
      <aui-input label="no feedback icon" :no_feedback_icon="true" failure="oops!" />
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
        control input.
      </p>
      <p>
        Inputs with the type "tel" (telephone) will be masked to standard US format of (000) 000-0000 (14
        characters).
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
            '  <aui-input label="demo" placeholder="demo" />\n' +
            '  <aui-input label="datalist" :options="[\'Option 1\', \'Option 2\']" />\n' +
            '  <aui-input label="telephone (US)" type="tel" placeholder="(___) ___-____" />\n' +
            '  <aui-input label="disabled" :disabled="true" />\n' +
            '  <aui-input label="success" success="success" />\n' +
            '  <aui-input label="failure" failure="failure" />\n' +
            '  <aui-input label="subtext" subtext="subtext" />\n' +
            '  <aui-input label="leading cap" leading_cap="leading cap" />\n' +
            '  <aui-input label="trailing cap" trailing_cap="trailing cap" />\n' +
            '  <aui-input label="caps with feedback" trailing_cap="trailing cap" failure="oops!" />\n' +
            '  <aui-input label="no feedback icon" :no_feedback_icon="true" failure="oops!" />\n' +
            '</div>',
        events: {
          'focus($event.target)': 'When the component is focused',
          'blur($event.target)': 'When the component is blurred',
          'input($event.target.value)': 'When component is registered in the component',
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
            prop: 'type',
            type: 'String',
            required: false,
            default: 'text',
            usage: 'Input type. Supports most HTML5 input types.'
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
            prop: 'options',
            type: 'Array',
            required: false,
            default: '[]',
            usage:
              'Options if a datalist is attached to the component. This must be an array of ' +
              'string/numeric values that should be used to generate the datalist and bind to the model.'
          },
          {
            prop: 'tabindex',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'Input tab index.'
          },
          {
            prop: 'step',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'Input step for numeric inputs.'
          },
          {
            prop: 'max_whole_digits',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'The maximum number of whole digits for numeric inputs.'
          },
          {
            prop: 'max_decimal_digits',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'The maximum number of decimal digits for numeric inputs.'
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
          },
          {
            prop: 'no_feedback_icon',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage: 'If no icon should trail the component on feedback, for use in short length components.'
          }
        ]
      }
    }
  }
}
</script>