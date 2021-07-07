<template>
  <div>
    <splide :options="options">
      <splide-slide
        v-for="(post, index) in posts.latest"
        :key="`latest-${index}`"
        :post="post"
        class="flex"
      >
        <PostCardSlider :key="`latest-${index}`" :post="post" class="hw" />
      </splide-slide>
    </splide>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: {
        type: "loop",
        focus: "center",
        width: "800px",
      },
      posts: {
        latest: [],
      },
    };
  },
  async fetch() {
    const latestPosts = await this.$content()
      .sortBy("createdAt", "description")
      .limit(3)
      .without(["body"])
      .fetch();

    this.posts = {
      latest: latestPosts || [],
    };
  },
};
</script>
<style lang="scss">
hw {
  max-width: 800;
  max-height: 600;
}
</style>