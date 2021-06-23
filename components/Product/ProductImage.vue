<template>
  <nuxt-link
    :to="`/products/${product.handle}`"
    no-prefetch
    class="flex justify-center"
  >
    <img
      :src="image.src"
      :alt="image.altText"
      :width="image.width"
      :height="image.height"
      loading="lazy"
    />
  </nuxt-link>
</template>

<script>
export default {
  props: { product: { type: Object, default: () => {} } },
  computed: {
    image() {
      return {
        src: this.product.images.edges[0].node.w_300_h_300,
        alt: this.product.images.edges[0].node.altText,
        width: this.product.images.edges[0].node.width,
        height: this.product.images.edges[0].node.height,
      };
    },
  },
};
</script>

<style lang="scss" scoped></style>
