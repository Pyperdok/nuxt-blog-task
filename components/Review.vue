<template>
  <div class="review">
    <div class="review-content">
      <p class="content">{{ review.content }}</p>
      <button class="circle-button" @click="showReplyForm = !showReplyForm">Reply</button>
      <button v-if="review.replies.length > 0" class="circle-button" @click="showReplies = !showReplies">{{showReplies ? 'Hide' : 'Show'}} Replies</button>
    </div>

    <div v-if="showReplies">
      <div v-for="reply in review.replies">
        <Review :review="reply" />
      </div>
    </div>

    <div v-if="showReplyForm">
      <form @submit.prevent="submitReply">
        <textarea v-model="replyContent" placeholder="Your reply..."></textarea>
        <button class="circle-button" type="submit">Submit Reply</button>
      </form>
    </div>

  </div>
</template>
  
<script>
export default {
  props: {
    review: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showReplyForm: false,
      showReplies: false
    };
  },
  methods: {
    submitReply() {
      this.review.replies.push({
        content: this.replyContent,
        replies: []
      });
      this.showReplyForm = false;
      this.replyContent = '';
    }
  },
};
</script>
  
<style scoped>
.review {
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 15px;
  margin-bottom: 15px;
}

textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  margin-top: 20px;
}

.content {
  margin-bottom: 15px;
}
</style>