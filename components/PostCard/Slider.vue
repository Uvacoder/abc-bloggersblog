<template>
  <div class="flex justify-center">
    <nuxt-link
      :to="{
        name: 'post-slug',
        params: { slug: getPostMeta.slug },
      }"
    >
      <img :src="getPostMeta.image" class="relative hw filter blur-sm opacity-30" />
      <div class="absolute bottom-10 left-5">
      <h1 class="text-gray-200 font-bold">
        {{ getPostMeta.title }}
      </h1>
      <p class="text-gray-100 hover:text-gray-700 hover:animate-pulse font-semibold text-lg">
        {{ getPostMeta.description }}
      </p>
      </div>
    </nuxt-link>
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
     * @returns {{title: string, description: string, image: string, slug: string}}
     */
    getPostMeta() {
      const image = `images/${this.post?.image}`;

      return {
        title: this.post.title || "",
        description: this.post.description || "",
        slug: this.post.slug || "",
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