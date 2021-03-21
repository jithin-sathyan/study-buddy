<template>
  <article
    class="course"
    @mouseover="highlight_enroll()"
    @mouseleave="dehighlight_enroll()"
  >
    <section class="course-main">
      <header class="course-title" :title="description">
        {{ name }}
      </header>
    </section>
    <section>
      <p class="course-description">{{ description }}</p>
    </section>
    <section>
      <h4>Prerquisites</h4>
      <ul>
        <li
          v-for="eachPrerequisite in prerequisites"
          :key="eachPrerequisite.id"
        >
          {{ eachPrerequisite.name }}
        </li>
      </ul>
    </section>
    <section>
      <h4>Enrollments</h4>
      <p>{{ enrollmentStats }}</p>
    </section>
    <section class="course-actions">
      <button
        class="action-button enroll"
        :class="{ 'enroll-hover': mouseOnCourse }"
        v-if="enrollmentStatus == 'Fresh'"
        v-on:click="enroll()"
      >
        Enroll
      </button>
      <button
        class="action-button enroll"
        v-else-if="enrollmentStatus == 'Enrolled'"
        v-on:click="cancel()"
      >
        Cancel
      </button>
    </section>
    <hr />
    <section class="feedback">
      <p class="feedback-bar">
        <span title="Average Feedback">Feedback: {{ averageFeedback }} </span>
        <span
          v-if="feedbackOpen"
          class="feedback-view"
          v-on:click="feedbackSection(false)"
          >Hide</span
        >
        <span v-else class="feedback-view" v-on:click="feedbackSection(true)"
          >View Feedback</span
        >
      </p>
      <div class="feedback-div" v-show="feedbackOpen">
        <ol>
          <li v-for="review in reviews" :key="review.name">
            {{review.name}}: {{review.message}}: ({{review.rating}}/5)
          </li>
        </ol>
        <CourseReview @message-submitted="addMessage"/>
      </div>
    </section>
  </article>
</template>

<script>
import CourseReview from './CourseReview';

export default {
  name: 'Course',
  components: { CourseReview },
  props: {
    limit: {
      type: Number,
      required: true,
      default: 20,
    },
    courseId: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      name: 'Vue.js',
      currentEnrollments: 0,
      description: 'A basic course to understand the concept of Vue JS',
      enrollmentStatus: 'Fresh',
      prerequisites: [
        { name: 'HTML', id: '123' },
        { name: 'CSS', id: '234' },
        { name: 'JavaScript', id: '345' },
      ],
      mouseOnCourse: false,
      id: 1,
      reviews: [],
      feedbackOpen: false,
    };
  },
  methods: {
    enroll() {
      this.enrollmentStatus = 'Enrolled';
      this.currentEnrollments += 1;
      this.$emit('course-enroll-event', this.courseId);
    },
    cancel() {
      this.enrollmentStatus = 'Fresh';
      this.currentEnrollments -= 1;
      this.$emit('course-cancel-event', this.courseId);
    },
    highlight_enroll() {
      this.mouseOnCourse = true;
    },
    dehighlight_enroll() {
      this.mouseOnCourse = false;
    },
    addMessage(courseReview) {
      this.reviews.push(courseReview);
    },
    feedbackSection(shouldOpen) {
      this.feedbackOpen = shouldOpen;
    },
  },
  computed: {
    enrollmentStats() {
      return `${this.currentEnrollments}/${this.limit}`;
    },
    averageFeedback() {
      if (this.reviews.length === 0) {
        return 'NA';
      }
      let sumRating = 0;
      for (let i = 0; this.reviews.length; i += 1) {
        sumRating += this.reviews[i].rating;
      }
      return `${sumRating} / ${this.reviews.length} /5`;
    },
  },
};
</script>

<style scoped>
.course {
  background: #9d46ff;
  height: max-content;
  width: 420px;
  margin: 12px;
  padding: 12px;
  border-radius: 4px;
}

.course-title {
  font-weight: 600;
  font-size: 32px;
}

.course-description {
  font-family: "Roboto", sans-serif;
}

.action-button {
  width: 100%;
  height: 40px;
  background: #0a00b6;
  color: #ffffff;
  font-family: "Blinker", sans-serif;
  font-weight: 500;
  font-size: 20px;
  border-radius: 4px;
  border: unset;
}

.enroll-hover {
  background: #ffffff;
  color: #0a00b6;
}
</style>
