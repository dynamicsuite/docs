<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <docs-aui-component v-bind="options" class="docs-aui-number docs-container ds-container primary">
    <template #examples>
      <aui-number :is_currency="true" number="1" />
      <aui-number :padding="0" :is_currency="true" number="-$1" />
      <aui-number number="10.49" />
      <aui-number :padding="2" number="5312.1111" />
      <aui-number :padding="2" number="5312.1" />
      <aui-number :padding="2" number="5312.01" />
      <aui-number :is_currency="true" number="-$99.99" />
      <aui-number :is_currency="true" number="$123" />
    </template>
    <template #notes>
      <p>
        If the number is defined as currency, and a "padding" property is not given, the pad length of the
        number will default to 2. If the "padding" property is given, it will always be used. If the number
        given is not defined as currency and no "padding" property is given, the pad length of the number will
        default to 0.
      </p>
      <p>
        If a number exceeds the number of decimals for padding as defined by the property "padding", the number
        will exceed the padding no matter what, this is so that you can never get clipped values and the model
        will always render as it is set.
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
            '  <aui-number :is_currency="true" number="1" />\n' +
            '  <aui-number :padding="0" :is_currency="true" number="-$1" />\n' +
            '  <aui-number number="10.49" />\n' +
            '  <aui-number :padding="2" number="5312.1111" />\n' +
            '  <aui-number :padding="2" number="5312.1" />\n' +
            '  <aui-number :padding="2" number="5312.01" />\n' +
            '  <aui-number :is_currency="true" number="-$99.99" />\n' +
            '  <aui-number :is_currency="true" number="$123" />\n' +
            '</div>',
        props: [
          {
            prop: 'is_currency',
            type: 'Boolean',
            required: false,
            default: 'false',
            usage: 'If the number should be rendered as currency.'
          },
          {
            prop: 'currency_symbol',
            type: 'String',
            required: false,
            default: '$',
            usage: 'The currency symbol to use if the number is defined as currency.'
          },
          {
            prop: 'padding',
            type: 'Number | null',
            required: false,
            default: 'null',
            usage: 'The number of zeros that should pad the number to the right of the decimal place.'
          },
          {
            prop: 'number',
            type: 'Number | String | null',
            required: true,
            default: 'null',
            usage: 'The number to format and display.'
          }
        ]
      }
    }
  }
}
</script>

<style lang="sass">

/* Space numbers */
.docs-aui-number .examples
  display: flex
  flex-direction: column

</style>