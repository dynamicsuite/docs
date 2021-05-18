<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <docs-aui-component v-bind="options" class="docs-aui-button-drop docs-container ds-container primary">
    <template #examples>
      <aui-button-drop :dropdown="{test: 'Test'}" menu_align="left" />
      <aui-button-drop :dropdown="{test: 'Test'}" :disabled="true" />
      <p>relative to example:</p>
      <div style="display: flex; outline: 1px dashed #777; height: 6rem; width: 16rem" id="rel">
        <aui-button-drop
          style="align-self: flex-end"
          text="no"
          :dropdown="{test: 'Test'}"
        />
        <aui-button-drop
          style="align-self: flex-end; margin-left: auto"
          text="yes"
          relative_to="#rel"
          :dropdown="{test: 'Test'}"
        />
      </div>
      <p>Buttons come in the following styles:</p>
      <aui-button-drop type="primary" text="primary (default)" :dropdown="{test: 'Test'}" />
      <aui-button-drop type="secondary" text="secondary" :dropdown="{test: 'Test'}" />
      <aui-button-drop type="success" text="success" :dropdown="{test: 'Test'}" />
      <aui-button-drop type="warning" text="warning" :dropdown="{test: 'Test'}" />
      <aui-button-drop type="failure" text="failure" :dropdown="{test: 'Test'}" />
      <div class="btn-group">
        <aui-button text="1" />
        <aui-button text="2" />
        <aui-button text="3" />
        <aui-button-drop :dropdown="{test: 'Test'}" />
      </div>
    </template>
    <template #notes>
      <p>
        When running a local api, you may tie the disabled state to the api's calling state. Usually the
        return of this API is so fast that it causes a "flashing" effect on the form. To get around this you
        should create a delayed overlay property on your form to initiate the disabled state if an API
        takes longer than ~300ms.
      </p>
      <p>
        Buttons may be grouped with a special AUI class <code>btn-group</code> to collapse all shared sides. Simply wrap
        your buttons in a container with the <code>btn-group</code> class.
      </p>
      <p>
        Multiple group nesting levels are not supported.
      </p>
      <p>
        Click events for menu items must be handled on the parent component/instance. The dropdown is structured
        as a simple String, String key-value pair where the key is the event that will be emitted on click of
        the menu item.
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
            '  <aui-button-drop :dropdown="{test: \'Test\'}" />\n' +
            '  <aui-button-drop :dropdown="{test: \'Test\'}" :disabled="true" />\n' +
            '  <p>relative to example:</p>\n' +
            '  <div style="display: flex; outline: 1px dashed #777; height: 6rem; width: 16rem" id="rel">\n' +
            '    <aui-button-drop\n' +
            '       style="align-self: flex-end"\n' +
            '       text="no"\n' +
            '       :dropdown="{test: \'Test\'}"\n' +
            '    />\n' +
            '    <aui-button-drop\n' +
            '      style="align-self: flex-end; margin-left: auto"\n' +
            '      text="yes"\n' +
            '      relative_to="#rel"\n' +
            '      :dropdown="{test: \'Test\'}"\n' +
            '    />\n' +
            '  </div>\n' +
            '  <p>Buttons come in the following styles:</p>\n' +
            '  <aui-button-drop type="primary" text="primary (default)" :dropdown="{test: \'Test\'}" />\n' +
            '  <aui-button-drop type="secondary" text="secondary" :dropdown="{test: \'Test\'}" />\n' +
            '  <aui-button-drop type="success" text="success" :dropdown="{test: \'Test\'}" />\n' +
            '  <aui-button-drop type="warning" text="warning" :dropdown="{test: \'Test\'}" />\n' +
            '  <aui-button-drop type="failure" text="failure" :dropdown="{test: \'Test\'}" />\n' +
            '  <div class="btn-group">\n' +
            '    <aui-button text="1" />\n' +
            '    <aui-button text="2" />\n' +
            '    <aui-button text="3" />\n' +
            '    <aui-button-drop :dropdown="{test: \'Test\'}" />\n' +
            '  </div>\n' +
            '</div>',
        events: {
          'click': 'When the button is clicked',
          'menu-click(key)': 'When a menu entry is clicked',
          'dropdown*': 'Custom event per menu click, see dropdown prop (*event name may vary)'
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
            prop: 'dropdown',
            type: 'object',
            required: true,
            default: 'null',
            usage:
              'The dropdown list to attach to the button. This is an object where the key is the event ' +
              'name that will be emitted on click of that menu entry and the value is the text to ' +
              'display in the menu. Events must be handled on the parent component.'
          },
          {
            prop: 'disabled',
            type: 'boolean',
            required: false,
            default: 'false',
            usage: 'If the button is disabled and non-interactive.'
          },
          {
            prop: 'icon_inactive',
            type: 'string',
            required: false,
            default: 'fas fa-caret-down',
            usage: 'The Font Awesome icon class for the inactive icon.'
          },
          {
            prop: 'icon_active',
            type: 'string',
            required: false,
            default: 'fas fa-caret-up',
            usage: 'The Font Awesome icon class for the active icon.'
          },
          {
            prop: 'menu_align',
            type: 'string',
            required: false,
            default: 'left',
            usage: 'Where to align the dropdown relative to the button. Accepts: left, right.'
          },
          {
            prop: 'relative_to',
            type: 'string | null',
            required: false,
            default: 'null',
            usage: 'Relative container for the dropdown placement. Used to avoid clipping out of parent element.'
          }
        ]
      }
    }
  }
}
</script>

<style lang="sass">

/* Space buttons */
.docs-aui-button-drop .examples

  & > .btn-drop
    margin-right: 1rem

  p:first-of-type
    margin-top: 0

</style>