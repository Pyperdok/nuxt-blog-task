<template>
  <div class="container mx-auto h-full w-[500px]">
    <h1 class="font-bold mb-3">Posts</h1>
    <div class="posts flex flex-col items-center">
      <div v-for="post in posts" :key="post.slug">
        <nuxt-link class="flex post border-2 border-black mb-10 justify-start" :to="'/posts/' + post.slug">
          <img class="w-36 h-36" :src="post.image">
          <div class="post-text flex flex-col justify-center pl-3.5 w-[350px]">
            <p class="title font-bold">{{ post.title }}</p>
            <p style="word-wrap: break-word;">{{ post.description }}</p>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const posts = await $content('blog').sortBy('createdAt', 'asc').fetch();
    return { posts };
  }
}
</script>
