<template>
  <button
    class="
      md:w-full
      lg:pr-10 lg:pl-10
      transition-colors
      duration-500
      ease-in-out
      leading-5
      text-xs text-center
      py-3
      uppercase
      text-white
      bg-black
      hover:bg-gray-700
      px-3
      lg:px-20
      font-bold
      w-full
      md:w-auto
      inline-block
    "
  >
    <span>{{ label }}</span>
  </button>
</template>

<script>
export default {
  props: { label: { type: String, required: true } },
};
</script>

<style lang="scss" scoped></style>
