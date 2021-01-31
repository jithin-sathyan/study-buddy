<template>
  <div id="app">
    <div class="course-container">
      <div class="header">
        <span class="brand">Study Buddy</span>
        <div class="total-enrollments" title="Your enrollments">
          {{ currentEnrollments }}
        </div>
      </div>
      <div class="course">
        <div class="course-main">
          <div class="course-title" :title="description">{{ name }}</div>
        </div>
      </div>
    </div>
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
    };
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
