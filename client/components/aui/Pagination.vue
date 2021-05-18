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
      <aui-pagination
          :page.sync="page"
          :total="total"
          :limit.sync="limit"
          :list_range_limit="list_range_limit"
      />
    </template>
    <template #notes>
      <p>
        This component default to full width flex.
      </p>
      <p>
        When running a local api, you may tie the disabled state to the api's calling state. Usually the
        return of this API is so fast that it causes a "flashing" effect on the form. To get around this you
        should create a delayed overlay property on your form to initiate the disabled state if an API
        takes longer than ~300ms.
      </p>
      <p>
        Both <code>page</code> and <code>limit</code> must be synced back to the parent.
      </p>
      <p>
        Paginating to the current page or out of range does not trigger a <code>@paginate</code> event.
      </p>
    </template>
  </docs-aui-component>
</template>

<script>
export default {
  data() {
    return {
      page: 1,
      total: 10000,
      limit: 10,
      list_range_limit: [10, 100, 1000],
      options: {
        syntax_js:
            "new Vue({\n" +
            "  el: '#test'\n" +
            "  data: {\n" +
            "    page: 1,\n" +
            "    total: 10000,\n" +
            "    limit: 10,\n" +
            "    list_range_limit: [10, 100, 1000]\n" +
            "  }\n" +
            "});",
        syntax_html:
            '<div id="#test">\n' +
            '  <aui-pagination\n' +
            '    :page.sync="page"\n' +
            '    :total="total"\n' +
            '    :limit.sync="limit"\n' +
            '    :list_range_limit="list_range_limit"\n' +
            '  />\n' +
            '</div>',
        events: {
          'update:page(page)': 'Update for "page" (sync required)',
          'update:limit(limit)': 'Update for "limit" (sync required)',
          'paginate': 'When a valid pagination is triggered'
        },
        props: [
          {
            prop: 'disabled',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage: 'If the buttons are disable and non-interactive.'
          },
          {
            prop: 'page',
            type: 'Number',
            required: true,
            default: 'null',
            usage: 'The current page.'
          },
          {
            prop: 'total',
            type: 'Number',
            required: true,
            default: 'null',
            usage: 'The total number of potential records in the dataset.'
          },
          {
            prop: 'limit',
            type: 'Number',
            required: true,
            default: 'null',
            usage: 'The record limit per page.'
          },
          {
            prop: 'list_range_limit',
            type: 'Number[]',
            required: true,
            default: 'null',
            usage: 'The possible limit options for the dropdown.'
          }
        ]
      }
    }
  }
}
</script>