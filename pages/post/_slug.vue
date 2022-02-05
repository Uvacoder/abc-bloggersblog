<template>
  <div class="grid justify-items-center">
    <header
      class="mt-8 grid text-left justify-items-start place-content-center"
    >
      <h1 class="flex items-center">
        <span class="text-gray-200 font-semibold text-4xl">{{
          post.title
        }}</span>
           <Author
          v-for="(author, index) in author"
          :key="`author-${index}`"
          :author="post.author"
          class="ml-2"
        />
      </h1>
      <div class="hw mt-2">
        <p>
          <span class="text-gray-200 text-md">
            {{ post.description }}
          </span>
        </p>
        <div class="mt-3"><h3 class="text-gray-400">5dk okuma süresi</h3></div>
      </div>
    </header>
    <article class="flex items-center hw w-full mx-auto mt-6">
      <nuxt-content :document="post" />
    </article>
        
  </div>
</template>

<script>
//import { Disqus } from "vue-disqus"

//export default {
//  components: {
//    Disqus,
//  },
export default {
 data() {
    return {
      post: {},
      related: [],
      author: [this.post?.author],
    };
  },
  async fetch() {
    const post = await this.$content(this.$route.params.slug).fetch();
    if (!post) return this.$router.push("/");

    this.post = post;

    if (post.related?.length > 0) {
      const array = [];
      for (const key of post.related) {
        const { title } = await this.$content(key).only(["title"]).fetch();
        array.push({
          title,
          slug: key,
        });
      }

      this.related = array;
    }
  },
};
</script>

<style lang="scss">
.hw {
  max-width: 800px;
}
.disqus{
    width:800px;
}
.nuxt-content {
  /* Headings */
  h1,
  h2,
  h3 {
    @apply font-semibold hover:underline text-gray-100;
  }

  h1 {
    @apply text-2xl;
  }

  h2,
  h3 {
    @apply text-lg;
  }
  p {
    @apply text-gray-200;

    &.text-center {
      @apply flex justify-center;
    }

    strong {
      @apply font-medium text-gray-100;
    }

    a {
      @apply text-blue-600 hover:underline;
    }

    code {
      @apply bg-gray-700 rounded-md text-gray-200 px-1 py-px font-sans;
    }

    img {
      @apply rounded;
    }

    &:not(:last-child) {
      @apply mb-5;
    }
  }

  /* Ratings */
  .ratings {
    @apply space-y-px mb-4 text-gray-200;
  }

  /* Pre and code block filenames */

  .nuxt-content-highlight {
    @apply relative mb-5;

    .filename {
      @apply absolute right-0 text-gray-300 font-light z-10 mr-3 mt-3 text-sm;
    }

    pre {
      @apply rounded-md px-6 py-4;
    }
  }

  /* Ordered and Unordered Lists */
  ol,
  ul {
    @apply text-gray-300;

    li:not(:last-child) {
      @apply mb-1;
    }
  }

  ol {
    @apply list-decimal pl-4;

    &:not(:last-child) {
      @apply mb-5;
    }
  }

  ul {
    @apply list-disc pl-5;

    &:not(:last-child) {
      @apply mb-5;
    }

    li::marker {
      @apply text-gray-400;
    }
  }

  /* Horizontal line */
  hr {
    @apply border-gray-700  my-8 border-dashed;
  }
}
</style>
