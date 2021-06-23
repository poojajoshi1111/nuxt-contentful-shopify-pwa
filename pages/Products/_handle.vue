<template>
  <div v-if="product.title">
    <bread-crumb :product-name="product.title" />
    <div class="flex">
      <div class="w-2/3 pl-28">
        <div
          class="bg-white justify-center flex items-center"
          style="min-height: 765px"
        >
          <img
            :src="image.w_1024_h_767"
            :alt="image.altText"
            loading="lazy"
            :width="image.width"
            :height="image.height"
          />
        </div>
        <div v-if="product.descriptionHtml" class="max-w-none mb-12 px-0">
          {{ product.descriptionHtml }}
        </div>
      </div>
      <div class="w-1/3 pr-28 ml-10">
        <div class="mb-6 px-0">
          <div class="flex items-center justify-between mt-0 mb-10">
            <sale-banner v-if="product.availableForSale" />
            <div>{{ product.vendor }}</div>
          </div>
          <h1 class="text-4xl text-black font-normal leading-10 mt-0 mb-6">
            {{ product.title }}
          </h1>
          <p>{{ product.description }}</p>
          <div class="flex items-center mb-6">
            <span class="text-3xl mr-4 font-normal text-campaign-sale">
              {{ price | currency }}
            </span>
          </div>
          <div class="flex justify-between items-center mb-6 lg:px-0 px-5">
            <app-button label="add to bag" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { pathOr } from 'ramda';
import { ProductByHandle } from '~/gql/queries/shopify.gql';

import BreadCrumb from '~/components/BreadCrumb';
import AppButton from '~/components/common/AppButton.vue';
import SaleBanner from '~/components/ProductDetail/SaleBanner.vue';

export default {
  components: {
    breadCrumb: BreadCrumb,
    appButton: AppButton,
    saleBanner: SaleBanner,
  },
  async asyncData({ app, params: { handle }, error }) {
    const client = app.apolloProvider.defaultClient;
    const response = await client.query({
      query: ProductByHandle,
      variables: { handle },
    });
    const product = pathOr({}, ['data', 'productByHandle'], response);

    if (!product.title) {
      return error({ statusCode: 404, message: 'Page not found!' });
    }
    return { product };
  },
  computed: {
    image() {
      return pathOr('', ['product', 'images', 'edges', [0], 'node'], this);
    },
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
