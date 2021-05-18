<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <docs-aui-component v-bind="options" class="docs-aui-button docs-container ds-container primary">
    <template #examples>
      <aui-button text="Demo" />
      <aui-button :disabled="true" text="Disabled" />
      <aui-button :loading="true" text="Loading" />
      <aui-button badge="failure" text="Failed" />
      <p>Buttons come in the following styles:</p>
      <aui-button type="primary" text="primary (default)" />
      <aui-button type="secondary" text="secondary" />
      <aui-button type="success" text="success" />
      <aui-button type="warning" text="warning" />
      <aui-button type="failure" text="failure" />
      <div class="btn-group">
        <aui-button text="1" />
        <aui-button text="2" />
        <aui-button text="3" />
        <aui-button-drop :dropdown="{test: 'Test'}" />
      </div>
    </template>
    <template #notes>
      <p>
        When running a local api, you may tie the disabled/loading state to the api's calling state. Usually the
        return of this API is so fast that it causes a "flashing" effect on the form. To get around this you
        should create a delayed overlay property on your form to initiate the disabled/loading state if an API
        takes longer than ~300ms.
      </p>
      <p>
        Buttons may be grouped with a special AUI class <code>btn-group</code> to collapse all shared sides. Simply wrap
        your buttons in a container with the <code>btn-group</code> class.
      </p>
      <p>
        Multiple group nesting levels are not supported.
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
          '  <aui-button text="Demo" />\n' +
          '  <aui-button :disabled="true" text="Disabled" />\n' +
          '  <aui-button :loading="true" text="Loading" />\n' +
          '  <aui-button badge="failure" text="Failed" />\n' +
          '  <p>Buttons come in the following styles:</p>\n' +
          '  <aui-button type="primary" text="primary (default)" />\n' +
          '  <aui-button type="secondary" text="secondary" />\n' +
          '  <aui-button type="success" text="success" />\n' +
          '  <aui-button type="warning" text="warning" />\n' +
          '  <aui-button type="failure" text="failure" />\n' +
          '  <div class="btn-group">\n' +
          '    <aui-button text="1" />\n' +
          '    <aui-button text="2" />\n' +
          '    <aui-button text="3" />\n' +
          '    <aui-button-drop :dropdown="{test: \'Test\'}" />\n' +
          '  </div>\n' +
          '</div>',
        events: {
          'click': 'When the button is clicked'
        },
        slots: {
          'default': 'Any content in this slot will go in the button body'
        },
        props: [
          {
            prop: 'type',
            type: 'string',
            required: false,
            default: 'primary',
            usage:
              'The type of the button determines which style class will be applied. Accepted values ' +
              'are: none, primary, secondary, success, warning, failure. Type "none" will not apply ' +
              'any additional style classes. All other types will add the type as a style class.'
          },
          {
            prop: 'text',
            type: 'string',
            required: false,
            default: 'null',
            usage:
                'The text body of the button. This is an alias for the slot content when using ' +
                'plaintext. Slot should be used if custom HTML is required.'
          },
          {
            prop: 'disabled',
            type: 'boolean',
            required: false,
            default: 'false',
            usage: 'If the button is disabled and non-interactive.'
          },
          {
            prop: 'loading',
            type: 'boolean',
            required: false,
            default: 'false',
            usage: 'If the button is in its loading state.'
          },
          {
            prop: 'loading_text',
            type: 'string',
            required: false,
            default: 'null',
            usage: 'Text to display on the button when in the loading state.'
          },
          {
            prop: 'badge',
            type: 'string | null',
            required: false,
            default: 'null',
            usage:
                'The badge type. If this is NULL, no badge will be displayed. This determines the ' +
                'style class applied for the badge.'
          },
          {
            prop: 'badge_text',
            type: 'string',
            required: false,
            default: '!',
            usage: 'Text to display in the attached badge.'
          }
        ]
      }
    }
  }
}
</script>

<style lang="sass">

/* Space buttons */
.docs-aui-button

  .btn
    margin-right: 1rem

  .examples p
    margin-top: 0

</style>