<template>
  <div id="app">
    <header>
      Demo app for Aviata.kz
    </header>
    <section>
      <div>Filter</div>
      <div>List</div>
    </section>
    <footer>
      <div class="author">Author: Nikolay Pyatayev</div>
      <div class="year">2018</div>
    </footer>
  </div>
</template>

<script>

export default {
  name: 'app',
  components: {
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Open+Sans:400,700&subset=cyrillic');

  // Global styles
  // Palette
  $light-blue: #DFF0FF;
  $blue: #397FBF;
  $dark-blue: #212C5B;
  $orange: #FE9922;
  $grey: #979797;

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
