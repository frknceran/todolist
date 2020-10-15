<template>
  <div id="app">
    <AddToDo></AddToDo>
  </div>
</template>

<script>
import AddToDo from './components/AddToDo.vue'


export default {
  name: 'App',

  components: {
    AddToDo
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width:600px;
  margin:auto;
}
</style>
