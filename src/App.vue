<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <progress-bar :completed-steps="completedSteps" :total-steps="totalSteps" style="width:100%;">
      <template v-slot:footer>
        
      </template>
    </progress-bar>
  </div>
</template>

<script>
import ProgressBar from "./components/ProgressBar.vue";

export default {
  name: "App",
  components: {
    ProgressBar
  },
  data () {
    return {
      completedSteps:1,
      totalSteps:10
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
