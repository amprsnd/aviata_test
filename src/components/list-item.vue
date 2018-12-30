<template>
  <div class="list-item">
    <div class="airline-cell">
      <img
        v-for="(flights, i) in item.flights"
        :key="i"
        :src="airlineLogo(flights.airline.code)"
        :alt="flights.airline.name"
      />
    </div>
    <div class="type-cell">{{flightType(item.flights)}}</div>
    <div class="more-cell">
      <a href="#">Выбрать другое время</a>
      <br>
      <a href="#">Поделиться</a>
    </div>
    <div class="time-cell" v-html="flightTime(item.flights)"></div>
    <div class="duration-cell">{{flightDuration(item.flightDuration)}}</div>
    <div class="buy-cell">
      <!-- TODO: Кнопки могут плясать по ширине из-за разных цен. 
      Нужно что-то предпринять, но я уже в пижаме... (c) -->
      <button>Купить за {{formatPrice(item.price)}} kzt</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'listItem',
  props: ['item'],
  methods: {
    airlineLogo(code) {
      return `/images/${code}.svg`
    },
    formatPrice(value) {
      return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
    },
    flightType(flights) {
      return flights.length > 1 ? 'со стыковкой' : 'прямой'
    },
    flightTime(flights) {
      let flightLength = flights.length -1
      // TODO: добавить отображение дат для непрямых рейсов
      return `
        <span>${flights[0].departureTime}</span> - <span>${flights[flightLength].arrivalTime}</span>
      `
    },
    flightDuration(duration) {
      return `${Math.floor(duration / 60)}ч ${duration % 60}м`
    }
  },
}
</script>

<style lang="scss">
  .list-item {
    display: flex;
    flex-direction: row;

    background: $white;
    border-bottom: 1px solid $grey;

    &:last-child {
      border-bottom: none;
    }
    div {
      box-sizing: border-box;
      padding: 1.4rem;
    }

    .airline-cell {

      img {
        display: block;
        width: 100%;
        max-width: 110px;
        height: auto;
        margin-bottom: 0.83rem;

        &:last-child {
          margin-bottom: 0;
        }
      }
    }
    .more-cell {
      a, a:visited {
        color: $dark-blue;
        text-decoration: none;

        border-bottom: 1px dashed $light-grey;

        &:first-child::after {
          content: '';
          display: inline-block;
          width: 8px;
          height: 4px;

          vertical-align: middle;
          margin-left: 4px;

          background: url('/images/down-arrow-small.svg') 50% 50% no-repeat;
          background-size: contain;
        }
        &:last-child {
          line-height: 2;
        }
      }
    }
    .time-cell {
      span:first-child {
        font-weight: 700;
      }
    }

    .buy-cell {
      text-align: right;

      button {
        padding: 0.83rem 1.7rem;
        border: none;
        border-radius: 3px;
        background: $orange;
        color: $white;
        outline: none;

        cursor: pointer;
      }
    }
  }
</style>