<template>
  <div>
    <h2>Submit a Review</h2>
    <form @submit.prevent="submitReview">
        <label>Review:</label>
        <textarea class="review-textarea my-5" v-model="review.content" required></textarea>
      <button class="circle-button" @click.prevent="submitReview">Submit</button>
    </form>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      review: {
        content: ''
      },
    };
  },
  methods: {
    submitReview() {
      this.$emit("review-submitted", { content: this.review.content, replies: [] });
      this.review.content = '';
    },
  },
};
</script>