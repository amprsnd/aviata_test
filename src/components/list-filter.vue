<template>
  <div class="filter">
    <div class="airlines" @click="showHideAirlinesList()">
      <div :class="[{'unfolded': showSelectList}, 'dropdown']">Авиакомпании</div>
      <ul v-if="showSelectList">
        <li
          v-for="(airline, key, i) in airlines"
          :key='i'
          @click="airlines[key] = !airlines[key]"
        >
          <div :class="[{'checked': airline}, 'checkbox']" :key='i'></div>
          {{key
            .replace('all', 'Все')
            .replace('_', ' ')
          }}
        </li>
      </ul>
    </div>
    <div class="direct-only" @click="directOnly = !directOnly">
      <div :class="[{'checked': directOnly}, 'checkbox']"></div>
      Только прямые рейсы
    </div>
  </div>
</template>

<script>
import store from '../store'

export default {
  name: 'listFilter',
  data() {
    return {
      store: store,
      airlines: {
        all: true
      },
      directOnly: false,
      showSelectList: false
    }
  },
  beforeMount() {
    this.airlinesList()
    this.store.frontList = this.store.backList
  },
  watch: {
    'airlines.all': function (val) {
      let isSelected = val ? true : false
      for (let airline in this.airlines) {
        this.airlines[airline] = isSelected
      }
    },
    showSelectList: function (val) {
      if (!val) this.filter()
    },
    directOnly: function () {
      this.filter()
    }
  },
  methods: {
    airlinesList() {
      this.store.backList.forEach((item) => {
        item.flights.forEach((f) => {
          if (this.airlines[f.airline.name] === undefined) {
            let key = f.airline.name.replace(' ', '_')
            this.$set(this.airlines, key, true)
          }
        })
      })
    },
    showHideAirlinesList() {
      this.showSelectList = !this.showSelectList
    },
    filter() {
      if (this.store.frontList) {
        let flights = this.store.backList
        let airlines = []

        // Фильтр по авиакомпаниям
        for (let airline in this.airlines) {
          if (airline !== 'all' && this.airlines[airline]) {
            airlines.push(airline.replace('_', ' '))
          }
        }
        // Две возможные реализации фильтра:
        // some - оставит отфильтрованную авиакампанию в непрямых перелётах
        // every - отфильтрует и стыковочные
        flights = flights.filter((flight) => {
          let hasInclude = flight.flights.every((f) => {
            console.log(f.airline.name)
            console.log(airlines.includes(f.airline.name))
            return airlines.includes(f.airline.name)
          })
          return hasInclude
        })

        // Фильтр по перелётам
        if (this.directOnly) {
          flights = flights.filter((flight) => {
            return flight.flights.length === 1
          })
        }
        this.store.frontList = flights
      }
    }
  },
}
</script>

<style lang="scss">
  .filter {
    display: flex;
    flex-direction: row;
    padding: 0.7rem 0;

    line-height: 21px;
    font-size: 1.2rem;

    .checkbox {
      display: inline-block;
      vertical-align: top;
      width: 21px;
      height: 21px;
      box-sizing: border-box;
      border-radius: 0.5rem;

      margin-right: 1rem;
      border: 1px solid $blue;

      &.checked {
        border: none;
        background: url('/images/checkbox-checked.svg') 50% 50% no-repeat $orange;
      }
    }

    .airlines {
      cursor: pointer;
      padding-right: 55px;

      .dropdown::after {
        content: '';
        display: inline-block;
        width: 11px;
        height: 6px;

        vertical-align: middle;
        margin-left: 4px;

        background: url('/images/down-arrow.svg') 50% 50% no-repeat;
        background-size: contain;

      }
      .dropdown.unfolded::after {
        transform: rotateX(180deg);
      }

      ul {
        position: absolute;
        background:  $white;
        box-sizing: border-box;

        min-width: 170px;

        margin: 0;
        padding:  0.7rem 0;

        border-radius: 0.7rem;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2);

        li {
          list-style: none;
          margin: 0;
          padding: 0.7rem 0.83rem;
          line-height: 21px;

          cursor: pointer;

          &:hover {
            background: $silver;
          }
        }
      }
    }

    .direct-only {
      cursor: pointer;
    }
  }
</style>
