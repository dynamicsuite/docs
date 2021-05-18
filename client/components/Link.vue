<!--
This file is part of the Dynamic Suite Docs package.

For the full copyright and license information, please view the LICENSE
file that was distributed with this source code.

@package DynamicSuite\Docs
@author Grant Martin <commgdog@gmail.com>
@copyright 2021 Dynamic Suite Team
-->

<template>
  <a class="docs-link" :href="'#' + link" @click="copy(link)" title="Copy to Clipboard">
    <i class="fas fa-link" />
  </a>
</template>

<script>
// noinspection JSValidateTypes
export default {
  props: {

    /**
     * The link name (ID).
     *
     * @type {string | null}
     */
    link: {
      type: String | null,
      default: null
    }

  },
  methods: {

    /**
     * Copy the name link to the clipboard.
     *
     * @param {string} link - The link (ID) to copy.
     */
    copy(link) {
      const dummy = document.createElement('textarea');
      document.body.appendChild(dummy);
      dummy.value = `${location.origin}${location.pathname}#${link}`;
      dummy.select();
      document.execCommand('copy');
      document.body.removeChild(dummy);
    }

  }
}
</script>

<style lang="sass">

/* Include DS colors */
@import "../../../../client/sass/dynamicsuite"

/* Link container */
.docs-link
  color: $color-secondary !important
  cursor: pointer
  font-size: 0.8rem
  margin-left: 0.5rem

  &:hover
    color: $color-primary !important

</style>