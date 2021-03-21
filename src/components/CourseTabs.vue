<template>
  <article>
    <span
      class="tab"
      v-for="(tab, index) in tabs"
      :key="index"
      @click="selectTab(tab)"
      :class="{ activeTab: selectTab === tab }"
    >
      {{ tab }}
    </span>
    <hr class="tab-separator" />
    <section class="review-section" v-show="selectedTab === 'Review'">
      <p v-if="!reviews.length">There are no reviews yet!</p>
      <ol v-else>
        <li v-for="review in reviews" :key="review.name">
          {{ review.name }}: {{ review.message }} ({{ review.rating }}/5)
        </li>
      </ol>
    </section>
    <section v-show="selectedTab === 'Give Review'">
      <CourseReview @message-submitted="addMessage" />
    </section>
  </article>
</template>

<script>
import CourseReview from './CourseReview';

export default {
  name: 'CourseTabs',
  components: { CourseReview },
  data() {
    return {
      selectedTab: 'Review',
      reviews: [],
      tabs: ['Review', 'Give Review'],
    };
  },
  methods: {
    addMessage(courseReview) {
      this.reviews.push(courseReview);
      let sumRating = 0;
      for (let i = 0; i < this.reviews.length; i += 1) {
        sumRating += this.reviews[i].rating;
        const avgRating = sumRating / this.reviews.length;
        this.$emit('get-avg-feedback', avgRating);
      }
    },
    selectTab(tab) {
      this.selectedTab = tab;
    },
  },
};
</script>

<style></style>
