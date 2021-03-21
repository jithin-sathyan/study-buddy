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
  </article>
</template>

<script>
export default {
  name: 'Course',
  props: {
    limit: {
      type: Number,
      required: true,
      default: 20,
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
      this.mouseOnCourse = true;
    },
    dehighlight_enroll() {
      this.mouseOnCourse = false;
    },
  },
  computed: {
    enrollmentStats() {
      return `${this.currentEnrollments}/${this.limit}`;
    },
  },
};
</script>

<style scoped>
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
