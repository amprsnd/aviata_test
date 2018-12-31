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
          v-for="(item, i) in store.frontList"
          :key="i"
          :item="item"
        ></list-item>
        <div v-if="store.frontList && store.frontList.length === 0" class="nothing">Нет результатов...</div>
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

    width: 100%;
    height: 100%;

    font-family: 'Open Sans', sans-serif;
    font-size: 12px;

    background: $light-blue;
    color: $dark-blue;
  }

  body {
    overflow-y: scroll;
  }

  #app {
    max-width: 1000px;
    min-height: 100%;
    margin: 0 auto;

    display: flex;
    flex-direction: column;

    .nothing {
      text-align: center;
      padding: 1rem 0;
      font-size: 1.5rem;
    }

    header {
      padding: 1rem 1.34rem;
      font-size: 2rem;
    }
    section {
      flex-grow: 1;
    }
    footer {
      padding: 1rem 1.34rem;
    }

  }

</style>
