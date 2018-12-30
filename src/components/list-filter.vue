<template>
  <div class="filter">
    Filter
  </div>
</template>

<script>
import store from '../store'

export default {
  name: 'listFilter',
  data() {
    return {
      store: store,
      airlines: []
    }
  },
  beforeMount() {
    this.store.frontList = this.store.backList
  }
}
</script>

<style lang="scss">
</style>
