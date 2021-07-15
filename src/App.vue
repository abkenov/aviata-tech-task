<template>
  <div>
    {{ currentTickets.length }}
    {{ direct }} {{ baggage }} {{ refundable }}
    {{ checkedAirlines }}
    <TariffOptions 
      @directOption="direct = $event" 
      @baggageOption="baggage = $event" 
      @refundOption="refundable = $event"
      @discardOptionsEvent="discardOptions"
    />
    <AirlinesOptions @checkedAirlines="checkedAirlines = $event" :filter="filter" />
    <a @click="discardOptions">Сбросить все фильтры</a>
  </div>
  <div>
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
    filter() {
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
  // created() {
  //   this.filter()
  // },
  watch: {
    direct() {
      this.filter()
    },
    baggage() {
      this.filter()
    },
    refundable() {
      this.filter()
    },
    checkedAirlines() {
      this.filter()
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
}
</style>
