<template>
  <div class="container">
    <div class="flex post">
      <img :src="post.image">
      <div class="post-text">
        <p class="title">{{ post.title }}</p>
        <p class="date"> {{ formatData(post.createdAt) }}</p>
        <br>
        <p>{{ post.description }}</p>
        <br>
        <nuxt-content :document="post" />
        <br>
        <button class="mb-5 circle-button">
          <nuxt-link to="/">Back to post list</nuxt-link>
        </button>

        <div class="reviews" v-for="review in reviews">
          <Review :review="review" />
        </div>
        <ReviewForm @review-submitted="addReview" />
      </div>
    </div>
  </div>
</template>

<script>
import reviews from '~/content/reviews.json';

export default {
  async asyncData({ $content, route }) {
    const post = await $content('blog', route.params.post).fetch();
    return { post, reviews };
  },
  methods: {
    formatData(data) {
      const options = { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit', second: '2-digit' };
      return new Date(data).toLocaleDateString('en-US', options);
    },
    addReview(review) {
      reviews.push(review);
    }
  }
}
</script>

<style scoped>
.container {
  margin: 50px auto;
  padding: 20px;
  background-color: #f9f9f9;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

.title {
  font-weight: bold;
}

.post-text {
  padding-left: 15px;
}

img {
  width: 150px;
  height: 150px;
}

.reviews {
  margin-bottom: 25px;
}
</style>