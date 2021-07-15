<template>
  <div>
    <TariffOptions 
      @directOption="direct = $event" 
      @baggageOption="baggage = $event" 
      @refundOption="refundable = $event"
      @discardOptionsEvent="discardOptions"
    />
    <AirlinesOptions @checkedAirlines="checkedAirlines = $event" :filterTickets="filterTickets" />
    <a class="discard-filters" @click="discardOptions">Сбросить все фильтры</a>
  </div>
  <div class="tickets">
    <Ticket v-for="ticket in currentTickets" :key="ticket.id" :ticket="ticket" />
  </div>
</template>

<script>
import TariffOptions from './components/TariffOptions.vue'
import AirlinesOptions from './components/AirlinesOptions.vue'
import Ticket from './components/Ticket.vue'

const data = require('../src/assets/results.json')

export default {
  name: 'App',
  data() {
    return {
      results: data,
      allTickets: [...data.flights],
      currentTickets: [...data.flights],
      direct: false,
      baggage: false,
      refundable: false,
      checkedAirlines: Object.keys(data.airlines),
    }
  },
  methods: {
    filterTickets() {
      this.currentTickets = this.allTickets

      if(this.direct) {
        this.currentTickets = this.currentTickets.filter(flight => flight.itineraries[0][0]['stops'] === 0)
      }

      if(this.baggage) {
        this.currentTickets = this.currentTickets.filter(flight => flight.itineraries[0][0].segments[0].baggage_options[0].value > 0)
      }

      if(this.refundable) {
        this.currentTickets = this.currentTickets.filter(flight => flight.refundable === true)
      }
      
      this.currentTickets = this.currentTickets.filter(flight => this.checkedAirlines.includes(flight.itineraries[0][0].carrier))
      
    },
    discardOptions() {
      this.direct = false
      this.baggage = false
      this.refundable = false
    }
  },
  computed: {

  },
  watch: {
    direct() {
      this.filterTickets()
    },
    baggage() {
      this.filterTickets()
    },
    refundable() {
      this.filterTickets()
    },
    checkedAirlines() {
      console.log('second');
      this.filterTickets()
    }
  },
  components: {
    TariffOptions,
    AirlinesOptions,
    Ticket
  },
  emits: ['directOption', 'baggageOption', 'refundOption', 'discardOptions', 'checkedAirlines']
}
</script>

<style>
html {
  background: #D7D7D7
}

#app {
  display: flex;
  flex-direction: row;
}

button:hover {
  transition-duration: 0.2s;
  opacity: 85%;
}

.tickets {
	display: flex;
	flex-direction: column;
  margin-top: 50px;
}

.discard-filters {
  font-family: Open Sans;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 16px;
  color: #7284E4;
  cursor: pointer;
  border-bottom: 1px dashed;
  margin: 20px auto auto 149px;
}
</style>
