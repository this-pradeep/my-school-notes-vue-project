<template>
  <div id="app">
      <QuestionAnswerList/>
  </div>
</template>

<script>
import QuestionAnswerList from './components/QuestionAnswerList.vue';
import './assets/css/main.css';

export default {
  name: 'App',
  components: {
    QuestionAnswerList,
  },
};
</script>

<style lang="scss">
#app {
   font-family: Avenir, Quicksand, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
::-webkit-scrollbar{
width: 12px;
}
::-webkit-scrollbar-track{
  box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
  border-radius: 10px;
}
::-webkit-scrollbar-thumb{
  box-shadow: inset 0 0 6px rgba(3, 55, 104, 0.5);
  border-radius: 10px;
  background-color: rgba(91, 181, 255, 0.5);
}
</style>
