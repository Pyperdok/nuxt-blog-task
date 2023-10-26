<template>
  <div class="flex post">
    <img :src="post.image">
    <div class="post-text">
      <p class="title">{{ post.title }}</p>
      <p>{{ post.description }}</p>
      <br>
      <nuxt-content :document="post" />
      <br>
      <nuxt-link to="/">Back to post list</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, route }) {
    const post = await $content('blog', route.params.post).fetch();
    return { post };
  }
}
</script>