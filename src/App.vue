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
        <article class="course">
          <section class="course-main">
            <header class="course-title" :title="description">
              {{ name }}
            </header>
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
    };
  },
};
</script>

<style>
#app {
  font-family: "Blinker", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
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
  height: 180px;
  width: 180px;
  margin: 12px;
  padding: 12px;
}

.course-title {
  font-weight: 600;
  font-size: 32px;
}
</style>
