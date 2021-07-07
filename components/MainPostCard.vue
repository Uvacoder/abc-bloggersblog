<template>
  <nuxt-link
    :to="{
      name: 'post-slug',
      params: { slug: getPostMeta.slug },
    }"
  >
    <div class="flex justify-start bg-gray-700 rounded-md hw h-auto">
      <img :src="getPostMeta.image" class="max-w-48 m-4" />
      <div>
        <h1 class="text-lg text-gray-300 mt-4">
          {{ getPostMeta.title }}
        </h1>
        <p class="text-gray-400 my-4">
          {{ getPostMeta.description }}
        </p>
      </div>
    </div>
  </nuxt-link>
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

<style>
.hw {
  max-width: 800px;
}
</style>