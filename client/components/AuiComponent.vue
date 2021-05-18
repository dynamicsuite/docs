<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <div class="docs-aui-component">

    <!-- Syntax -->
    <div v-if="syntax_js || syntax_html" class="syntax">
      <h2>Syntax:</h2>
      <pre><code class="language-js">{{syntax_js}}</code></pre>
      <pre><code class="language-html">{{syntax_html}}</code></pre>
    </div>

    <!-- Examples -->
    <div class="examples">
      <h2>Example:</h2>
      <slot name="examples"></slot>
    </div>

    <!-- Events -->
    <div v-if="events" class="events">
      <h2>Events:</h2>
      <table>
        <tr v-for="(value, key) in events" :key="'event-' + key">
          <td><pre>@{{key}}</pre></td>
          <td>{{value}}</td>
        </tr>
      </table>
    </div>

    <!-- Slots -->
    <div v-if="slots" class="slots">
      <h2>Slots:</h2>
      <table>
        <tr v-for="(value, key) in slots" :key="'slot-' + key">
          <td><pre>{{key}}</pre></td>
          <td>{{value}}</td>
        </tr>
      </table>
    </div>

    <!-- Notes-->
    <div v-if="$slots.notes" class="notes">
      <h2>Notes:</h2>
      <slot name="notes"></slot>
    </div>

    <!-- Props -->
    <div v-if="props" class="props">
      <h2>Props:</h2>
      <div class="prop" v-for="(value, key) in props" :key="'prop-' + key">
        <docs-config-param
          :param="value.prop"
          :type="value.type"
          :default_value="value.default"
          :required="value.required"
          :content="value.usage"
        />
      </div>
    </div>

  </div>
</template>

<script>
// noinspection JSValidateTypes
export default {
  props: {

    /**
     * Syntax example (Javascript).
     *
     * @type {string | null}
     */
    syntax_js: {
      type: String | null,
      default: null
    },

    /**
     * Syntax example (HTML).
     *
     * @type {string | null}
     */
    syntax_html: {
      type: String | null,
      default: null
    },

    /**
     * Any events emitted by component.
     *
     * @type {object | null}
     */
    events: {
      type: Object | null,
      default: null
    },

    /**
     * Any slots the component has.
     *
     * @type {object | null}
     */
    slots: {
      type: Object | null,
      default: null
    },

    /**
     * The props the component has.
     *
     * @type {array | null}
     */
    props: {
      type: Array | null,
      default: null
    }

  },
  mounted() {
    // noinspection JSUnresolvedVariable
    hljs.initHighlighting.called = false;
    // noinspection JSUnresolvedVariable
    hljs.initHighlighting();
  }
}
</script>

<style lang="sass">

/* Import the core DS colors */
@import "../../../../client/sass/dynamicsuite"

/* Documentation container */
.docs-aui-component

  /* AUI generic padding */
  .examples > .aui, .examples > .btn-group
    margin-bottom: 1rem

  /* Property margin override */
  .props > .prop:last-of-type > .docs-config-param
    margin-bottom: 0

  /* Article headers */
  & > * > h2
    display: flex
    align-content: center
    margin: 0 0 1rem 0
    padding-bottom: 0.25rem
    border-bottom: 1px solid $color-border

</style>