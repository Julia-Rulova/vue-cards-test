<template>
  <section class="app">
    <form-component />
    <cards />
  </section>
</template>

<script>
  import FormComponent from './FormComponent.vue';
  import Cards from './Cards.vue';


  export default {
    components: { FormComponent },

  }
</script>

<style>
  @font-face {
    font-family: 'Source Sans Pro';
    src: url("../assets/fonts/SourceSansPro-Regular.woff") format("woff"),
      url("../assets/fonts/SourceSansPro-Regular.woff2") format("woff2");
  }

  * {
    font-family: 'Source Sans Pro';
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .app {
    width: 100%;
    max-width: 1440px;
    height: 100%;
    margin: 32px auto 0;
    padding: 0 32px;
    background-color: rgba(255, 254, 251, 0.8);
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
</style>
