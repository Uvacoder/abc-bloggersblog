<template>
  <div class="flex items-center">
    <h2 class="mr-2 text-gray-300">Yazar:</h2>
    <img
      :src="getIconName"
      class="w-8 h-8 object-cover my-3 ring-2 ring-gray-400 rounded-full"
    />
    <h2 class="ml-2 text-gray-300">{{ author }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    author: {
      type: String,
      required: true,
      default: "",
    },
    icon: {
      type: String,
      required: false,
      default: null,
    },
  },
  computed: {
    /**
     * Returns possible icon name if icon prop is not passed.
     * @returns {string}
     */
    getIconName() {
      if (this.icon) return this.icon;
      else
        return (
          `/${this.author?.toLowerCase()}.png` || `/${this.author?.toLowerCase()}.jpg`
        );
    },
  },
};
</script>

<style>
</style>