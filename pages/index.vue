<template>
  <main class="w-full">
    <section class="main w-4/5 my-0">
      <h1 class="font-normal text-xl">Product List</h1>
      <div>
        <div v-if="!products.length">No Products</div>
        <div v-else class="flex justify-between">
          <product-tile
            v-for="product of products"
            :key="product.id"
            :product="product.node"
          />
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import { pathOr } from 'ramda';
// import { Products } from '~/gql/queries/shopify.gql';
import { Products } from '../../gql/queries/Shopify.gql'


import ProductTile from '~/components/Product/ProductTile.vue';

export default {
  components: { productTile: ProductTile },
  async asyncData({ app }) {
    const client = app.apolloProvider.defaultClient;
    const response = await client.query({ query: Products });
    const products = pathOr([], ['data', 'products', 'edges'], response);

    return { products };
  },
};
</script>

<style scoped>
.main {
  margin: 0 auto;
}
</style>
