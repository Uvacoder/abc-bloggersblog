<template>
  <div>
    <header class="grid justify-items-center bg-gray-900">
      <h1 class="text-gray-300 font-semibold text-2xl py-4">Son Gönderiler</h1>
      <Slider class="pb-4" />
      <div class="grid justify-items-center bg-gray-900">
        <h1 class="text-gray-300 text-lg mt-4">Gönderiler</h1>
        <div>
          <PostCardMain
            v-for="(post, index) in posts.all"
            :key="`latest-${index}`"
            :post="post"
            class="m-8"
          />
        </div>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: {
        all: [],
      },
    };
  },
  async fetch() {
    const allPosts = await this.$content()
      .sortBy("createdAt")
      .limit(10)
      .without(["body"])
      .fetch();

    this.posts = {
      all: allPosts || [],
    };
  },
};
</script>

<style>
</style>