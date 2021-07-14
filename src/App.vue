<template>
  {{ currentTickets.length }}
  <TariffOptions 
    @directOption="direct = $event" 
    @baggageOption="baggage = $event" 
    @refundOption="refundable = $event" 
  />
  <AirlinesOptions />
  <Ticket />
  
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
      filteredTickets: [...data.flights],
      currentTickets: [...data.flights],
      direct: false,
      baggage: false,
      refundable: false,
    }
  },
  methods: {
    filterDirect() {
      this.currentTickets = this.filteredTickets.filter(flight => flight.itineraries[0][0]['stops'] === 0)
    },
    filterBaggage() {
      this.currentTickets = this.filteredTickets.filter(flight => flight.itineraries[0][0].segments[0].baggage_options[0].value > 0)
    },
    filterRefundable() {
      this.currentTickets = this.filteredTickets.filter(flight => flight.refundable === true)
    },
  },
  computed: {

  },
  watch: {
    direct(newVal) {
      newVal ? this.filterDirect() : this.currentTickets = [...this.filteredTickets]
    },
    baggage(newVal) {
      newVal ? this.filterBaggage() : this.currentTickets = [...this.filteredTickets]
    },
    refundable(newVal) {
      newVal ? this.filterRefundable() : this.currentTickets = [...this.filteredTickets]
    },
  },
  components: {
    TariffOptions,
    AirlinesOptions,
    Ticket
  },
  emits: ['directOption', 'baggageOption', 'refundOption']
}
</script>

<style>
#app {
  background: #D7D7D7;
}
</style>
