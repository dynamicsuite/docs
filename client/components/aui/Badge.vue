<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <docs-aui-component v-bind="options" class="docs-aui-badge docs-container ds-container primary">
    <template #examples>
      <p>Badges come in the following styles:</p>
      <aui-badge type="primary" text="primary (default)" />
      <aui-badge type="secondary" text="secondary" />
      <aui-badge type="success" text="success" />
      <aui-badge type="warning" text="warning" />
      <aui-badge type="failure" text="failure" />
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
          '  <p>Badges come in the following styles:</p>\n' +
          '  <aui-badge type="primary" text="primary (default)" />\n' +
          '  <aui-badge type="secondary" text="secondary" />\n' +
          '  <aui-badge type="success" text="success" />\n' +
          '  <aui-badge type="warning" text="warning" />\n' +
          '  <aui-badge type="failure" text="failure" />\n' +
          '</div>',
        slots: {
          'default': 'Any content in this slot will go in the badge body'
        },
        props: [
          {
            prop: 'type',
            type: 'string',
            required: false,
            default: 'primary',
            usage:
              'The type of the badge determines which style class will be applied. Accepted values ' +
              'are: none, primary, secondary, success, warning, failure. Type "none" will not apply ' +
              'any additional style classes. All other types will add the type as a style class.'
          },
          {
            prop: 'text',
            type: 'string',
            required: false,
            default: 'null',
            usage:
              'The text body of the badge. This is an alias for the slot content when using ' +
              'plaintext. Slot should be used if custom HTML is required.'
          }
        ]
      }
    }
  }
}
</script>

<style lang="sass">

/* Space badges */
.docs-aui-badge

  .badge:not(:last-of-type)
    margin-right: 1rem

  .examples
    margin-bottom: 1rem

</style>