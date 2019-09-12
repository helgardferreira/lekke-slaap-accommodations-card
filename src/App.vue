<template>
  <div id="app">
    <h1>Search Results</h1>

    <div class="appointments-container">
      <accomodations-card msg="Welcome to Your Vue.js App" />
    </div>
  </div>
</template>

<script>
import AccomodationsCard from "./components/AccomodationsCard.vue";

export default {
  name: "app",
  components: {
    accomodationsCard: AccomodationsCard
  }
};
</script>

<style lang="scss">
body {
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
  font-family: "NTR", sans-serif;
  background: #eee;
  h1 {
    text-align: center;
  }
}

#app {
  color: #2c3e50;
}

.appointments {
  display: flex;
  justify-content: center;
  flex-flow: row wrap;
}
</style>
