<template>
  <div id="app">
    <BidCalculator />
  </div>
</template>

<script>
import BidCalculator from './components/BidCalculator.vue';

export default {
  name: 'App',
  components: {
    BidCalculator
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
