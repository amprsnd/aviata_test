<template>
  <div>{{flightDuration}}, {{ticket.airline.name}}</div>
</template>

<script>
export default {
  name: 'listItem',
  props: ['flightDuration', 'ticket']
}
</script>

<style lang="scss">

</style>