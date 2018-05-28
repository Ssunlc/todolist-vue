<template>
  <div id="app">
    <div id="cover"></div>
    <tHeader></tHeader>
    <todo></todo>
    <tFooter></tFooter>
  </div>
</template>

<script>
  import tHeader from './components/t-header.vue'
  import tFooter from './components/t-footer.vue'
  import Todo from './components/todo.vue'
  export default {
    

  components: {
       tHeader,
       tFooter,
       Todo,
    }
  }
</script>

<style lang="scss" scoped>
   #app{
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
   }
   #cover{
     position: absolute;
     top: 0;
     left: 0;
     bottom: 0;
     right: 0;
     background-color: #555;
     opacity: 0.5;
     z-index: -1;
   }
</style>
