<template>
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