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
      <aui-select label="demo" :options="opt" />
      <aui-select label="disabled" :disabled="true" :options="opt" />
      <aui-select label="success" success="success" :options="opt" />
      <aui-select label="failure" failure="failure" :options="opt" />
      <aui-select label="subtext" subtext="subtext" :options="opt" />
      <aui-select label="leading cap" leading_cap="leading cap" :options="opt" />
      <aui-select label="trailing cap" trailing_cap="trailing cap" :options="opt" />
      <aui-select label="caps with feedback" trailing_cap="trailing cap" failure="oops!" :options="opt" />
      <aui-select label="no feedback icon" :no_feedback_icon="true" failure="oops!" :options="opt" />
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
      opt: {'0': '', '1': 'Option 1', '2': 'Option 2'},
      options: {
        syntax_js:
            "new Vue({\n" +
            "  el: '#test'\n" +
            "  data: {\n" +
            "    opt: {'0': '', '1': 'Option 1', '2': 'Option 2'}\n" +
            "  }\n" +
            "});",
        syntax_html:
            '<div id="#test">\n' +
            '  <aui-select label="demo" :options="opt" />\n' +
            '  <aui-select label="disabled" :disabled="true" :options="opt" />\n' +
            '  <aui-select label="success" success="success" :options="opt" />\n' +
            '  <aui-select label="failure" failure="failure" :options="opt" />\n' +
            '  <aui-select label="subtext" subtext="subtext" :options="opt" />\n' +
            '  <aui-select label="leading cap" leading_cap="leading cap" :options="opt" />\n' +
            '  <aui-select label="trailing cap" trailing_cap="trailing cap" :options="opt" />\n' +
            '  <aui-select label="caps with feedback" trailing_cap="trailing cap" failure="oops!" :options="opt" />\n' +
            '  <aui-select label="no feedback icon" :no_feedback_icon="true" failure="oops!" :options="opt" />\n' +
            '</div>',
        events: {
          'focus($event.target)': 'When the component is focused',
          'blur($event.target)': 'When the component is blurred',
          'input(selected)': 'When input is registered in the component'
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
              'Options to be rendered. This must be an object where the key is the value that will be ' +
              'assigned to the option and the value is the option label.'
          },
          {
            prop: 'multiple',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage: 'If it is possible to select multiple entries.'
          },
          {
            prop: 'size',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'The number of visible options.'
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
          },
          {
            prop: 'us_states',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage:
              'If the component should render US states for its options. The bound value is the ' +
              '2-digit state code.'
          }
        ]
      }
    }
  }
}
</script>