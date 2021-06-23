<template>
  <div class="px-28 px-5">
    <div class="flex justify-between items-center py-6 md:py-5">
      <div
        class="
          flex
          items-center
          font-sans
          text-base
          font-normal
          text-gray-767
          leading-tight
        "
      >
        <nuxt-link
          to="/"
          class="
            font-para
            text-xs
            leading-normal
            font-normal
            text-gray-767
            mr-2
            nuxt-link-active
          "
        >
          Home
        </nuxt-link>
        <div class="inline-flex items-center">
          <span class="inline-flex items-center">
            /
            <span
              class="
                inline-block
                font-para
                text-xs
                font-normal
                text-black
                ml-2
                capitalize
              "
            >
              {{ productName }}
            </span>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default { props: { productName: { type: String, default: '' } } };
</script>
