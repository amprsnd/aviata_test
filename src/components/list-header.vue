<template>
  <div class="list-header">
    <div class="airline-cell">Авиакомпания</div>
    <div class="type-cell">Рейс</div>
    <div class="more-cell">Выбор времени</div>
    <div class="time-cell">Вылет - посадка</div>
    <div class="duration-cell">Время в пути</div>
    <div class="buy-cell"></div>
  </div>
</template>

<script>
export default {
  name: 'listHeader'
}
</script>

<style lang="scss">
  // shared for header and items
  .airline-cell {
    width: calc(110px + 2.8rem);
  }
  .type-cell {
    width: 100%;
    max-width: 150px;
  }
  .more-cell {
    width: 100%;
    max-width: 180px;
  }
  .time-cell {
    width: 100%;
    max-width: 135px;
  }
  .duration-cell {
    width: 100%;
    max-width: 90px;
  }
  .buy-cell {
    flex-grow: 1;
  }

  .list-header {
    display: flex;
    flex-direction: row;
    
    background: $blue;

    color: $white;
    font-size: 1.1rem;

    padding: 0.5rem 1.34rem;


  }
</style>