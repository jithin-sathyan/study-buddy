<template>
  <form @submit.prevent="onSubmit" class="review-form">
    <div class="review-div">
      <label for="name">Name:</label><br />
      <input
        class="review-input"
        v-model="name"
        id="name"
        placeholder="Your name please..."
      />
    </div>
    <div class="review-div">
      <label for="message">Feedback:</label><br />
      <textarea
        class="review-input message-area"
        id="message"
        v-model="message"
        placeholder="Your feedback please..."
      />
    </div>
    <div class="review-div">
      <label for="rating">Rating:</label><br />
      <select class="review-select review-input" v-model.number="rating">
        <option value="0" disabled selected>Please rate...</option>
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>
    </div>
    <div class="error-section" v-show="errorState">
      <p>There were a few error while submitting</p>
      <ul class="error-list">
        <li v-show="name === null">Please provide a name</li>
        <li v-show="message === null">Please provide your feedback message</li>
        <li v-show="rating === 0">Please choose a rating</li>
      </ul>
    </div>
    <div class="review-div">
      <input class="review-submit" type="submit" />
    </div>
  </form>
</template>

<script>
export default {
  name: 'CourseReview',
  data() {
    return {
      name: null,
      message: null,
      rating: 0,
      errorState: false,
    };
  },
  methods: {
    onSubmit() {
      this.errorState =
        this.name === null ||
        this.message === null ||
        this.rating === null ||
        this.rating === 0;
      if (!this.errorState) {
        const courseReview = {
          name: this.name,
          message: this.message,
          rating: this.rating,
        };

        this.$emit('message-submitted', courseReview);
        this.name = null;
        this.message = null;
        this.rating = 0;
      }
    },
  },
};
</script>

<style></style>
