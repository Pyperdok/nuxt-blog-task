<template>
  <div class="container mx-auto my-10">
    <div class="flex post">
      <img class="w-36 h-36" :src="post.image">
      <div class="post-text pl-3.5">
        <p class="title font-bold mb-3">{{ post.title }}</p>
        <p class="date mb-3"> {{ formatData(post.createdAt) }}</p>
        <p class="desc mb-3">{{ post.description }}</p>
        <nuxt-content class="content mb-5" :document="post" />
        <button class="mb-5 circle-button">
          <nuxt-link to="/">Back to post list</nuxt-link>
        </button>

        <div class="reviews mb-5" v-for="review in reviews">
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