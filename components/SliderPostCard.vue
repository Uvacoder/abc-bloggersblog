<template>
      <div class="grid">
        <img :src="getPostMeta.image" class="relative hw"/>
        <h1 class="text-gray-200 font-bold absolute bottom-25 left-5">
          {{ getPostMeta.title }}
        </h1>
        <p class="text-gray-500 absolute bottom-10 text-sm left-5"> 
          {{ getPostMeta.description }}
        </p>
      </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
      default: () => {},
    },
    type: {
      type: String,
      required: false,
      default: "normal",
    },
  },
  computed: {
    /**
     * Returns post meta safely.
     * @returns {{title: string, description: string, image: string}}
     */
    getPostMeta() {
      const image =
      `images/${this.post?.image}`;

      return {
        title: this.post.title || "",
        description: this.post.description || "",
        image,
      };
    },
    /**
     * Returns post formatted post date that is nicer than the pure way.
     * @returns {string} The formatted date.
     */
    getPostDate() {
      return this.$getReadableDate(this.post.createdAt);
    },
  },
};
</script>

<style lang="scss">
</style>