<template>
  <div id="app">
    <article class="course-container">
      <header class="header">
        <section class="brand">Study Buddy</section>
        <section class="total-enrollments" title="Your enrollments">
          {{ currentEnrollments }}
        </section>
      </header>
      <div class="course-card-container">
        <article class="course" @mouseover="highlight_enroll()" @mouseleave="dehighlight_enroll()">
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
              <li v-for="eachPrerequisite in prerequisites" :key="eachPrerequisite.id">
                {{ eachPrerequisite.name }}
              </li>
            </ul>
          </section>
          <section>
            <h4>Enrollments</h4>
            <p>{{currentEnrollments}} / {{enrollments}}</p>
          </section>
          <section class="course-actions">
            <button
              class="action-button enroll"
              :class="enroll_classes"
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
        </article>
      </div>
    </article>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      name: 'Vue.js',
      enrollments: 50,
      currentEnrollments: 0,
      description: 'A basic course to understand the concept of Vue JS',
      enrollmentStatus: 'Fresh',
      prerequisites: [{ name: 'HTML', id: '123' }, { name: 'CSS', id: '234' }, { name: 'JavaScript', id: '345' }],
      enroll_classes: 'action-button enroll',
    };
  },
  methods: {
    enroll() {
      this.enrollmentStatus = 'Enrolled';
      this.currentEnrollments += 1;
    },
    cancel() {
      this.enrollmentStatus = 'Fresh';
      this.currentEnrollments -= 1;
    },
    highlight_enroll() {
      this.enroll_classes = 'action-button enroll enroll-hover';
    },
    dehighlight_enroll() {
      this.enroll_classes = 'action-button enroll';
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

.course {
  background: #9d46ff;
  width: 232px;
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
