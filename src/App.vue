<template>
  <div id="app">
    <article class="course-container">
      <header class="header">
        <section class="brand">Study Buddy</section>
        <section class="total-enrollments" title="Your enrollments">
          {{ currentEnrollments.length }}
        </section>
      </header>
      <div class="course-card-container">
        <Course
          :limit="enrollments"
          :courseId="course - vue - 1"
          @course-enroll-event="handleCourseEnroll"
          @course-cancel-event="handleCourseCancel"
        />
        <Course
          :limit="enrollments"
          :courseId="course - vue - 2"
          @course-enroll-event="handleCourseEnroll"
          @course-cancel-event="handleCourseCancel"
        />
      </div>
    </article>
  </div>
</template>

<script>
import Course from './components/Course';

export default {
  name: 'App',
  components: { Course },
  data() {
    return {
      enrollments: 50,
      currentEnrollments: [],
    };
  },
  methods: {
    handleCourseEnroll(courseId) {
      this.currentEnrollments.push(courseId);
    },
    handleCourseCancel(courseId) {
      const courseIdIndex = this.currentEnrollments.indexOf(courseId);
      if (courseIdIndex) {
        this.currentEnrollments.splice(courseIdIndex, 1);
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Blinker", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #ede7f6;
}

.course-container {
  height: 100vh;
}

.header {
  display: flex;
  justify-content: space-between;
  padding: 8px 12px;
  background: #6200ea;
  height: 60px;
}

.brand {
  font-size: 40px;
  color: #ffffff;
  font-weight: 800;
  height: inherit;
  line-height: 60px;
}

.total-enrollments {
  font-size: 28px;
  font-weight: 700;
  color: #ffffff;
  text-align: center;
  height: inherit;
  line-height: 60px;
}

.course-card-container {
  display: flex;
  padding: 16px 12px;
}
</style>
