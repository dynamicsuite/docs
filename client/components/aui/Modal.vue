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
      <aui-button text="Show Modal" @click="show = true"/>
      <aui-modal :show.sync="show" title="Test Title">
        <template #content>
          <p>
            This is a test modal!
          </p>
        </template>
        <template #left>
          <aui-button type="secondary">cancel</aui-button>
        </template>
        <template #right>
          <aui-button>proceed</aui-button>
        </template>
      </aui-modal>
    </template>
    <template #notes>
      <p>
        Only one modal may be open at a given time.
      </p>
      <p>
        The modal show property should sync modifier back to the show property on the parent.
      </p>
      <p>
        This component utilizes nested slots. If you just use the default slot, the entire body will be
        overridden with the given content. If you use the slot <code>#content</code> then a footer will be added
        to the bottom of the modal body. To put content in the footer you can use the named slots
        <code>#left</code> and <code>#right</code> to put the content in their respective sides of the footer.
      </p>
      <p>
        Extra padding is stripped by the <code>#content</code> slot, you may override this in delegated styles.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
// noinspection JSValidateTypes
export default {
  data() {
    return {
      show: false,
      options: {
        syntax_js:
            "new Vue({\n" +
            "  el: '#test'\n" +
            "  data: {\n" +
            "    show: false\n" +
            "  }\n" +
            "});",
        syntax_html:
            '<div id="#test">\n' +
            '  <aui-button text="Show Modal" @click="show = true"/>\n' +
            '  <aui-modal :show.sync="show" title="Test Title">\n' +
            '    <template #content>\n' +
            '      <p>\n' +
            '        This is a test modal!\n' +
            '      </p>\n' +
            '    </template>\n' +
            '    <template #left>\n' +
            '      <aui-button type="secondary">cancel</aui-button>\n' +
            '    </template>\n' +
            '    <template #right>\n' +
            '      <aui-button>proceed</aui-button>\n' +
            '    </template><p>\n' +
            '  </aui-modal>\n' +
            '</div>',
        events: {
          'update:show(show)': 'Update for "show" (sync required)',
          'close': 'When the modal is closed'
        },
        slots: {
          'default': 'Anything that goes in this slow will fill the entire body of the modal',
          'content': 'Anything that goes in this slow will fill the content area only of the modal',
          'left': 'Anything that goes in this slot will go on the left side of the footer',
          'right': 'Anything that goes in this slot will go on the right side of the footer',
        },
        props: [
          {
            prop: 'type',
            type: 'String',
            required: false,
            default: 'primary',
            usage:
              'The type of the modal determines which style class will be applied. Accepted values ' +
              'are: none, primary, secondary, success, warning, failure. Type "none" will not apply ' +
              'any additional style classes. All other types will add a style class in the format of ' +
              '<code>modal-${name}</code>.'
          },
          {
            prop: 'show',
            type: 'Boolean',
            required: true,
            default: 'false',
            usage: 'If the modal should be shown.'
          },
          {
            prop: 'title',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'The title bar text of the modal.'
          },
          {
            prop: 'closeable',
            type: 'Boolean',
            required: false,
            default: 'true',
            usage: 'If the modal is closeable.'
          }
        ]
      }
    }
  }
}
</script>