<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <div class="docs-config-param" :id="param">

    <!-- Target link -->
    <h3>{{param}} <docs-link :link="param" /></h3>

    <!-- Parameter info -->
    <div class="info">
      <span v-if="required" class="required">required</span>
      <span>Type: <code>{{type}}</code></span>
      <span v-if="default_value">Default: <code>{{default_value}}</code></span>
    </div>

    <!-- Parameter usage -->
    <!--suppress HtmlUnknownTag -->
    <slot v-if="!content" />
    <div v-else v-html="content" />

  </div>
</template>

<script>
// noinspection JSValidateTypes
export default {
  props: {

    /**
     * The parameter name.
     *
     * @type {string | null}
     */
    param: {
      type: String | null,
      default: null
    },

    /**
     * If the parameter is required.
     *
     * @type {boolean}
     */
    required: {
      type: Boolean,
      default: false
    },

    /**
     * The parameter type.
     *
     * @type {string}
     */
    type: {
      type: String,
      default: 'null'
    },

    /**
     * The default value of the parameter.
     *
     * @type {string}
     */
    default_value: {
      type: String,
      default: 'null'
    },

    /**
     * HTML content slot alias.
     *
     * @type {string | null}
     */
    content: {
      type: String | null,
      default: null
    }

  }
}
</script>

<style lang="sass">

/* Include DS colors */
@import "../../../../client/sass/dynamicsuite"

/* Parameter container */
.docs-config-param
  display: flex
  flex-direction: column
  margin: 0.5rem 0
  padding: 0.5rem

  /* Border the target */
  &:target
    outline: 1px dashed $color-success
    scroll-margin-top: calc(#{$size-slim} + 1rem)

  /* Header overrides */
  h3
    margin: 0 0 0.25rem 0

  /* Parameter info */
  .info
    display: flex
    align-items: center
    font-size: 0.7rem
    margin-bottom: 0.5rem

    /* If the parameter is required */
    .required
      display: inline-flex
      line-height: 0.8rem
      font-size: 0.8rem
      font-weight: bold
      padding: 0.25rem 0.4rem
      border-radius: 1rem
      text-align: center
      white-space: nowrap
      background: $color-warning

    /* Space info */
    span
      margin-right: 0.5rem

    /* Info values */
    code
      max-width: 0
      min-width: calc(100% - 1rem)

      &:not(.hljs)
        word-break: break-word

    /* Mobile overrides */
    @media (max-width: 500px)
      flex-direction: column
      align-items: flex-start

  /* Paragraph spacing*/
  p
    margin: 0 0 1rem 0

    &:first-of-type
      margin-top: 0

    &:last-of-type
      margin-bottom: 0

</style>