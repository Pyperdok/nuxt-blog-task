<template>
  <div class="review mb-5 p-2 border-2 border-[#ccc]">
    <div class="review-content mb-3">
      <p class="mb-5">{{ review.content }}</p>
      <button class="circle-button" @click="showReplyForm = !showReplyForm">Reply</button>
      <button v-if="review.replies.length > 0" class="circle-button" @click="showReplies = !showReplies">{{showReplies ? 'Hide' : 'Show'}} Replies</button>
    </div>

    <div v-if="showReplies">
      <div v-for="reply in review.replies">
        <Review :review="reply" />
      </div>
    </div>

    <div class="mt-5" v-if="showReplyForm">
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