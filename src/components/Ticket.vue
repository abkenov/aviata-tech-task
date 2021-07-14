<template>
  <div class="ticket-body">
    <div class="ticket-body__info">
      <div class="ticket-body__main-info">
        <img class="ticket-body__airline-icon" src="../assets/airlines-icons/KC.png" width="15" height="20">
        <p class="ticket-body__airline-name">Air Astana</p>
        <div class="departure-time">
          <p class="departure-time__date">25 ноя, вс</p>
					<p class="departure-time__time">23:25</p>
        </div>
        <div class="timeline">
            4 hours
        </div>
        <div class="arrival-time">
					<p class="departure-time__date">26 ноя, пн</p>
					<p class="departure-time__time">03:25</p>
        </div>
      </div>
      <div class="ticket-body__additional-info">
        <a href="">Детали перелета</a>
        <a href="">Условия тарифа</a>
        <div class="refundability">
          <img src="../assets/icons/icon-non-refundeble.svg" alt="">
          <p>невозвратный</p>
        </div>
      </div>
    </div>
    <div class="ticket-body__price">
      <p class="ticket-body__pricetag">590 240 &#8376;</p>
      <button>Выбрать</button>
      <p class="ticket-body__passengers-price">цена за всех пассажиров</p>
      <div class="ticket-body__baggage-info">
				<p>Нет багажа</p>
				<button>+ Добавить багаж</button>
			</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Ticket'
}
</script>

<style>
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