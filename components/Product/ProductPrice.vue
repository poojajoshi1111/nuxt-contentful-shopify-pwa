<template>
  <p class="text-xs font-normal text-red-700">
    <span class="lg:text-lg text-sm font-normal text-gray-800 md:text-gray-900">
      {{ price | currency }}
    </span>
  </p>
</template>

<script>
import { pathOr } from 'ramda';

export default {
  props: { product: { type: Object, default: () => {} } },
  computed: {
    price() {
      return pathOr(
        0,
        ['product', 'priceRange', 'maxVariantPrice', 'amount'],
        this
      );
    },
  },
};
</script>

<style lang="scss" scoped></style>
