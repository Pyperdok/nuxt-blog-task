<template>
  <div>
    <h2>Submit a Review</h2>
    <form @submit.prevent="submitReview">
      <div>
        <label for="content">Review:</label>
        <textarea id="content" required></textarea>
      </div>
      <button class="circle-button" @click="submitReview">Submit</button>
    </form>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      review: {
        content: '',
        replies: []
      },
    };
  },
  methods: {
    submitReview() {
      this.$emit("review-submitted", this.review);
      this.review.content = '';
    },
  },
};
</script>
  
<style scoped>
/* You can style your form here. This is just a basic example. */
div {
  margin: 20px;
}

label {
  display: block;
  margin-bottom: 10px;
}

textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
}
</style>