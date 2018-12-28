<template>
  <div id="app">
    <header>
      Demo app for Aviata.kz
    </header>
    <section>
      <template v-if="store.backList">
        <list-filter></list-filter>
        <list-header></list-header>
        <list-item
          v-for="(ticket, i) in store.frontList"
          :key="i"
          :flightDuration="ticket.flightDuration"
          :ticket="ticket.flights[0]"
        ></list-item>
      </template>
      <preloader v-else></preloader>
      
    </section>
    <footer>
      <div class="author">Author: Nikolay Pyatayev</div>
      <div class="year">2018</div>
    </footer>
  </div>
</template>

<script>
import store from './store'

import preloader from './components/preloader'
import listFilter from './components/list-filter'
import listHeader from './components/list-header'
import listItem from './components/list-item'

export default {
  name: 'app',
  components: {
    preloader,
    listFilter,
    listHeader,
    listItem
  },
  data() {
    return {
      store: store
    }
  },
  beforeMount() {
    this.getData()
  },
  methods: {
    getData () {
      fetch(this.store.api)
        .then((response) => {
          return response.json()
        }).then((json) => {
          this.store.backList = json
        }).catch((ex) => {
          // TODO: parsing error
        })
    }
  },
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
