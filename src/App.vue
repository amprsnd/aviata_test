<template>
  <div id="app">
    <header>
      Demo app for Aviata.kz
    </header>
    <section>
      <list-filter></list-filter>
      <list-header></list-header>
      <list-item></list-item>
    </section>
    <footer>
      <div class="author">Author: Nikolay Pyatayev</div>
      <div class="year">2018</div>
    </footer>
  </div>
</template>

<script>
import listFilter from './components/list-filter'
import listHeader from './components/list-header'
import listItem from './components/list-item'

export default {
  name: 'app',
  components: {
    listFilter,
    listHeader,
    listItem
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Open+Sans:400,700&subset=cyrillic');

  html, body {
    font-family: 'Open Sans', sans-serif;
    font-size: 12px;

    background: $light-blue;
    color: $dark-blue;
  }

  #app {
    max-width: 1000px;
    margin: 0 auto;

    header {}
    section {}
    footer {}

  }

</style>
