<template>
  <div id="app" class="bg-theme-blue py-1">
    <div class="container mx-auto">
      <div class="mx-auto -mb-56 ">
        <div class="my-16">
          <h1 class="text-2xl text-blue-300">The Next Generation Notebook For Students</h1>
        </div>
      <form class="bg-white shadow-xl rounded-lg px-8 pt-6 pb-8 mb-4 relative">
        <div class="mb-4">
          <label class="block text-gray-600 text-left font-medium mb-2" for="username">
            Question:
          </label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:bg-blue-100 focus:shadow-md" id="username" type="text" placeholder="What is the name of our Prime Minister?, etc.">
        </div>
        <div class="mb-6">
          <label class="block text-gray-600 text-left font-medium mb-2" for="answer">
            Answer:
          </label>
          <textarea name="answer" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:bg-blue-100 focus:shadow-md"  cols="30" rows="5"></textarea>
        </div>
        <div class="absolute right-0 bottom-0 mb-5 mr-10 ">
          <button class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-1 px-10 rounded focus:outline-none" type="button">
           SAVE
          </button>
        </div>
      </form>
    </div>
    </div>
        <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import './assets/css/main.css';

export default {
  name: 'App',
  components: {
    HelloWorld,
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
</style>
