<template>
  <div class="ticket-body">
    <div class="ticket-body__info">
      <div class="ticket-body__main-info">
        <img class="ticket-body__airline-icon" :src="require(`../assets/airlines-icons/${$props.ticket.itineraries[0][0].carrier}.png`)" width="15" height="20">
				<p class="ticket-body__airline-name">{{ $props.ticket.itineraries[0][0].carrier_name }}</p>
        <div class="departure-time">
          <p class="departure-time__date">{{ departureDate }}</p>
					<p class="departure-time__time">{{ departureTime }}</p>
        </div>
        <div class="timeline">
					<div class="timeline-codes">
						<span class="airport-code">{{ $props.ticket.itineraries[0][0].segments[0].origin_code }}</span>
						<span class="traveltime">{{ convertHMS($props.ticket.itineraries[0][0].traveltime) }}</span>
						<span class="airport-code">{{ $props.ticket.itineraries[0][0].segments[0].dest_code }}</span>
					</div>
					<div class="timeline-image">
						<span class="circle"></span>
						<span class="circle" v-if="$props.ticket.itineraries[0][0].stops > 0"></span>
						<span class="circle"></span>
					</div>
					<p class="timeline-stops" v-if="$props.ticket.itineraries[0][0].stops > 0">через Шымкент, 1 ч 50 м</p>
        </div>
        <div class="arrival-time">
					<p class="arrival-time__date">{{ arrivalDate }}</p>
					<p class="arrival-time__time">{{ arrivalTime }}</p>
        </div>
      </div>
      <div class="ticket-body__additional-info">
        <a href="">Детали перелета</a>
        <a href="">Условия тарифа</a>
        <div class="refundability" v-if="!$props.ticket.refundable">
          <img src="../assets/icons/icon-non-refundeble.svg" alt="">
          <p>невозвратный</p>
        </div>
      </div>
    </div>
    <div class="ticket-body__price">
      <p class="ticket-body__pricetag">{{ $props.ticket.price }} &#8376;</p>
      <button>Выбрать</button>
      <p class="ticket-body__passengers-price">цена за всех пассажиров</p>
      <div class="ticket-body__baggage-info">
				<p v-if="baggageValue > 0">Багаж: {{ baggageValue }} кг</p>
				<p v-else>Нет багажа</p>
				<button v-if="baggageValue === 0">+ Добавить багаж</button>
			</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Ticket',
	data() {
		return {
			baggageValue: this.$props.ticket.itineraries[0][0].segments[0].baggage_options[0].value,
		}
	},
	props: {
		ticket: Object
	},
	methods: {
		convertHMS(value) {
			const sec = parseInt(value, 10); // convert value to number if it's string

			let hours   = Math.floor(sec / 3600); // get hours
			let minutes = Math.floor((sec - (hours * 3600)) / 60); // get minutes

			if (minutes < 10) {minutes = "0"+minutes;}

			return hours+' ч '+minutes+' м'; // Return is HH : MM : SS
		}
	},
	computed: {
		departureDate() {
			const departure = this.$props.ticket.itineraries[0][0].segments[0].dep_time
			const commaIndex = departure.indexOf(',')
			return departure.slice(0, commaIndex + 4)
		},

		departureTime() {
			const departure = this.$props.ticket.itineraries[0][0].segments[0].dep_time
			const commaIndex = departure.indexOf(',')

			return departure.slice(commaIndex + 5)
		},

		arrivalDate() {
			const arrival = this.$props.ticket.itineraries[0][0].segments[0].arr_time
			const commaIndex = arrival.indexOf(',')
			return arrival.slice(0, commaIndex + 4)
		},

		arrivalTime() {
			const arrival = this.$props.ticket.itineraries[0][0].segments[0].arr_time
			const commaIndex = arrival.indexOf(',')

			return arrival.slice(commaIndex + 5)
		}
	}
}
</script>

<style>

.timeline-stops {
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 12px;
	line-height: 16px;
	text-align: center;
	color: #FF9900;
	}

.circle {
	height: 3px;
	width: 3px;
	border-radius: 50%;
	border: 1px solid #B9B9B9; 
	background-color: #FFFFFF;
}

.timeline-image {
	width: 100%;
	height: 1px;
	display: flex;
	flex-direction: row;
	align-items: center;
	justify-content: space-between;
	background-color: #B9B9B9;
	border: none;
	margin-top: 4px;
}

.timeline {
	width: 170px;
	margin: 0 30px;
}

.timeline-codes {
	width: 100%;
	display: flex;
	justify-content: space-between;
}

.traveltime {
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 12px;
	line-height: 18px;
	color: #202123;
}

.airport-code {
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 10px;
	line-height: 18px;
	color: #B9B9B9;
}

.departure-time__date{
	margin: 0;
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 12px;
	color: #202123;
}

.departure-time__time {
	margin: 0;
	font-family: Open Sans;
	font-style: normal;
	font-weight: 600;
	font-size: 24px;
	color: #202123;
}

.arrival-time__date{
	margin: 0;
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 12px;
	color: #202123;
}

.arrival-time__time {
	margin: 0;
	font-family: Open Sans;
	font-style: normal;
	font-weight: 600;
	font-size: 24px;
	color: #202123;
}

.departure-time {
	margin: 0 12px;
}

.arrival-time {
	margin: 0 12px;
}

.ticket-body {
	width: 880px;
	height: 168px;
	display: flex;
	flex-direction: row;
	background-color: #FFFFFF;
	box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.15);
	border-radius: 4px;
	margin-bottom: 20px;
}

.ticket-body__info {
	display: flex;
	flex-direction: column;
	width: 640px;
	
}

.ticket-body__main-info {
	display: flex;
	flex-direction: row;
	align-items: center;
	height: 120px;
	margin-left: 43px;
}

.ticket-body__airline-icon {
	margin-right: 7px;
}

.ticket-body__airline-name{
	font-family: Open Sans;
	font-style: normal;
	font-weight: 600;
	font-size: 14px;
	color: #202123;
	width: 100px;
}

.ticket-body__additional-info {
	display: flex;
	flex-direction: row;
	height: 48px;
	margin-left: 21px;
}

.ticket-body__additional-info>a {
	margin-left: 23px;
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 12px;
	color: #7284E4;
	text-decoration: none;
	border-bottom: 1px dashed #7284E4;
}

.ticket-body__price {
	display: flex;
	flex-direction: column;
	width: 240px;
	height: inherit;
	background: #F5F5F5;
	border-radius: 0px 4px 4px 0px;
	align-items: center;
}

.ticket-body__price>button{
	background: #55BB06;
	border-radius: 4px;
	width: 200px;
	height: 40px;
	border: none;
	font-family: Open Sans;
	font-style: normal;
	font-weight: bold;
	font-size: 18px;
	color: #FFFFFF;
}

.ticket-body__pricetag{
	font-family: Arial;
	font-size: 24px;
	text-align: center;
	color: #202123;
	height: 28px;
	margin: 12px;
}

.ticket-body__passengers-price {
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 12px;
	text-align: center;
	color: #707276;
	margin: 8px;
}

.ticket-body__baggage-info {
	display: flex;
	flex-direction: row;
	align-items: center;
}

.ticket-body__baggage-info>p{
	font-family: Open Sans;
	font-style: normal;	
	font-weight: normal;
	font-size: 12px;
	color: #202123;
	margin: 6px;
}

.ticket-body__baggage-info>button{
	background: #EAF0FA;
	border-radius: 2px;
	font-family: Open Sans;
	font-style: normal;
	font-weight: 600;
	font-size: 12px;
	color: #5763B3;
	height: 24px;
	width: 128px;
	border: none;
}

.refundability {
	display: flex;
	flex-direction: row;
	align-items: center;
	margin-left: 40px;
}

.refundability>img {
	margin: 5px;
}

.refundability>p{
	font-family: Arial;
	font-size: 12px;
	text-align: center;
	color: #707276;
}

.ticket-body__additional-info {
	display: flex;
	flex-direction: row;
	align-items: center;
}

</style>