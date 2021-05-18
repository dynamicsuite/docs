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
      <aui-notice type="primary" icon="fas fa-chess-knight" text="Static Knight" />
      <aui-notice type="secondary" icon="fas fa-snowboarding" text="Nothing to do" />
      <aui-notice type="success" icon="fas fa-smile" text="It worked!" />
      <aui-notice type="warning" icon="fas fa-grimace" text="It kinda worked?" />
      <aui-notice type="failure" icon="fas fa-angry" subtext="Please reload the page" text="It didn't work." />
      <aui-notice icon="fas fa-circle-notch fa-spin" text="Loading" />
    </template>
    <template #notes>
      <p>
        Notices display as flex full-width by default with all content aligned and justified to the center.
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
            '  <aui-notice type="primary" icon="fas fa-chess-knight" text="Static Knight" />\n' +
            '  <aui-notice type="secondary" icon="fas fa-snowboarding" text="Nothing to do" />\n' +
            '  <aui-notice type="success" icon="fas fa-smile" text="It worked!" />\n' +
            '  <aui-notice type="warning" icon="fas fa-grimace" text="It kinda worked?" />\n' +
            '  <aui-notice type="failure" icon="fas fa-angry" subtext="Please reload the page" text="It didn\'t work." />\n' +
            '  <aui-notice icon="fas fa-circle-notch fa-spin" text="Loading" />\n' +
            '</div>',
        slots: {
          'default': 'Any content in this slot will go in the notice message body'
        },
        props: [
          {
            prop: 'type',
            type: 'String',
            required: false,
            default: 'secondary',
            usage:
              'The type of the notice determines which style class will be applied. Accepted values ' +
              'are: primary, secondary, success, warning, failure.'
          },
          {
            prop: 'icon',
            type: 'String',
            required: false,
            default: 'fas fa-cog',
            usage: 'The Font Awesome icon to display for the notice.'
          },
          {
            prop: 'text',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage:
              'The body of the notice. This is an alias for the slot content when using ' +
              'plaintext. Slot should be used if custom HTML is required.'
          },
          {
            prop: 'subtext',
            type: 'String | Number | null',
            required: false,
            default: 'null',
            usage: 'Subtext to display under the notice text.'
          }
        ]
      }
    }
  }
}
</script>