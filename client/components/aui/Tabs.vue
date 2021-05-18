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
      <aui-tabs :tabs="tabs" :tab.sync="tab" />
    </template>
    <template #notes>
      <p>
        Tabs are designed by default to be used on a "whitesmoke" backdrop, the same backdrop as the default
        container. You must override the style when used on any other background.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
export default {
  data() {
    return {
      tabs: {
        tab1: 'Tab 1',
        tab2: 'Tab 2',
        tab3: 'Tab 3',
        tab4: 'Tab 4',
        tab5: 'Tab 5'
      },
      tab: 'tab1',
      options: {
        syntax_js:
            "new Vue({\n" +
            "  el: '#test'\n" +
            "  data: {\n" +
            "    tabs: {\n" +
            "      tab1: 'Tab 1',\n" +
            "      tab2: 'Tab 2',\n" +
            "      tab3: 'Tab 3',\n" +
            "      tab4: 'Tab 4',\n" +
            "      tab5: 'Tab 5'\n" +
            "    },\n" +
            "    tab: 'tab1'\n" +
            "  }\n" +
            "});",
        syntax_html:
            '<div id="#test">\n' +
            '  <aui-tabs :tabs="tabs" :tab.sync="tab" />\n' +
            '</div>',
        events: {
          'update:tab(tab)': 'Update for "tab" (sync required)',
          'change(tab)': 'When the tabs change'
        },
        props: [
          {
            prop: 'tabs',
            type: 'Object',
            required: true,
            default: 'null',
            usage:
              'The tabs to render. This must be a simple string-string key-value object where the ' +
              'key is the tab name and the value is the name to display.'
          },
          {
            prop: 'tab',
            type: 'String | Number',
            required: true,
            default: 'null',
            usage: 'The current tab (key).'
          },
          {
            prop: 'disabled',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage: 'If the tabs are disabled and non-interactive.'
          }
        ]
      }
    }
  }
}
</script>