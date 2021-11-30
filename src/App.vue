<template>

    <the-header tittle="RememberMe"></the-header>
    <the-resources></the-resources>
   
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import LearningResource from './components/learning-resources/LearningResource.vue'
// import StoredResources from './components/learning-resources/StoredResources.vue'
import TheHeader from './components/layouts/TheHeader.vue'
import TheResources from './components/learning-resources/TheResources.vue'
export default {
  name: 'App',
  components: {
    // LearningResource: LearningResource,
    // StoredResources,
    TheHeader,
    TheResources
  },
  
}
</script>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");

    * {
      box-sizing: border-box;
    }

    html {
      font-family: "Roboto", sans-serif;
    }

    body {
      margin: 0;
}
</style>
