<template>
  <div id="app">
    <div>
      <Questions ></Questions>
    </div>
    <div>
      <b-button style="float:left; margin:40px;" variant="primary">Save</b-button>
    </div>
  </div>
</template>

<script>
import Questions from './components/Questions'

export default {
  name: 'App',
  components: {
    Questions
  }
}
</script>

<style>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
