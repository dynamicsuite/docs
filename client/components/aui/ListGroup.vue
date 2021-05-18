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
      <aui-list-group :list="list" />
    </template>
    <template #notes>
      <p>
        On click of a group in the list, the "value" of the group will be emitted. You must handle this event
        on the parent.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
export default {
  data() {
    return {
      list: [
        {
          title: 'Row 1',
          subtext: 'This is row 1',
          value: 1
        },
        {
          icon: 'fas fa-box',
          title: 'Row 2',
          subtext: 'This is row 2',
          value: 2
        },
        {
          title: 'Row 3',
          subtext: 'This is row 3',
          value: 3
        }
      ],
      options: {
        syntax_html:
            '<div id="#test">\n' +
            '  <aui-list-group :list="list" />\n' +
            '</div>',
        syntax_js:
            "new Vue({\n" +
            "  el: '#test'\n" +
            "  data: {\n" +
            "    list: [\n" +
            "      {\n" +
            "        title: 'Row 1',\n" +
            "        subtext: 'This is row 1',\n" +
            "        value: 1\n" +
            "      },\n" +
            "      {\n" +
            "        icon: 'fas fa-box',\n" +
            "        title: 'Row 2',\n" +
            "        subtext: 'This is row 2',\n" +
            "        value: 2\n" +
            "      },\n" +
            "      {\n" +
            "        title: 'Row 3',\n" +
            "        subtext: 'This is row 3',\n" +
            "        value: 3\n" +
            "      }\n" +
            "    ]\n" +
            "  }\n" +
            "});",
        events: {
          'click(value)': 'On click of an group (payload is the group value)'
        },
        props: [
          {
            prop: 'list',
            type: 'Array',
            required: true,
            default: 'null',
            usage:
              'The list of groups to render. Each child of the array must be an object and each object ' +
              'must contain a "title" of type "string", and "value" of any type. The "value" will be ' +
              'emitted on click of the group. You may also include a "subtext" of type "string" which ' +
              'will be subtext displayed on the row below the title. If an "icon" of type "string" is' +
              'present, the icon will be appended before the text values. The "icon" value must be a ' +
              'valid Font Awesome icon class.'
          }
        ]
      }
    }
  }
}
</script>