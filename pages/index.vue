<template>
  <div class="container">
    <h1>Posts</h1>
    <div class="posts">
      <div v-for="post in posts" :key="post.slug">
        <nuxt-link class="flex post" :to="'/posts/' + post.slug">
          <img :src="post.image">
          <div class="flex post-text">
            <p class="title">{{ post.title }}</p>
            <p>{{ post.description }}</p>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const posts = await $content('blog').fetch();
    return { posts };
  }
}
</script>

<style scoped>
.container {
  font-family: 'Arial', sans-serif;
  max-width: 800px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f9f9f9;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

h1,
h2 {
  font-weight: bold;
}

img {
  width: 150px;
  height: 150px;
}

.title {
  font-weight: bold;
}

.post-text {
  flex-direction: column;
  justify-content: center;
  margin-left: 15px;
}

.post {
  border: solid black 1px;
  margin: auto;
  justify-content: start;
  max-width: 700px;
  margin-bottom: 50px;
  flex-grow: 0;
}
</style>
