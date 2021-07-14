<template>
  <div class="options-checkboxes">
      <h2 class="options-checkboxes__title">Опции тарифа</h2>
      <img class="options-checkboxes__selection-reset" @mouseover="onHover"/>

      <div class="options-checkboxes__option">
        <input type="checkbox" name="only-direct" v-model="direct" @change="returnDirect">
        <label for="only-direct">Только прямые</label>
      </div>
      <div class="options-checkboxes__option">
        <input type="checkbox" name="only-with-baggage" v-model="baggage" @change="returnBaggage">
        <label for="only-with-baggage">Только с багажом</label>
      </div>
      <div class="options-checkboxes__option">
        <input type="checkbox" name="only-refundable" v-model="refundable" @change="returnRefundable">
        <label for="only-refundable">Только возвратные</label>
      </div>
  </div>
  {{ direct }}
  {{ baggage }}
  {{ refundable }}
</template>

<script>

export default {
  data() {
    return {
      direct: false,
      baggage: false,
      refundable: false,
    }
  },
  methods: {
    returnDirect() {
      this.$emit('directOption', this.direct)
    },
    returnBaggage() {
      this.$emit('baggageOption', this.baggage)
    },
    returnRefundable() {
      this.$emit('refundOption', this.refundable)
    },
  },
  emits: ['directOption', 'baggageOption', 'refundOption'],
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400;0,600;0,700;0,800;1,300;1,400;1,600;1,700;1,800&display=swap');

  .options-checkboxes {
    border-radius: 4px;
    font-family: Open Sans;
    background-color: #F5F5F5;
    display: flex;
    flex-direction: column;
    width: 240px;
    height: 152px;
  }

  .options-checkboxes__title {
    margin: 12px;
    height: 20px;
    font-family: Open Sans;
    font-style: normal;
    font-weight: bold;
    font-size: 14px;
    line-height: 20px;
  }
  
  .options-checkboxes__option {
    height: 32px;
    width: 191px;
    display: flex;
	align-items: center;
  }

  .options-checkboxes__option>input {
    margin: 12px;
    border: 1px solid #B9B9B9;
	box-sizing: border-box;
	border-radius: 2px;
  }

  .options-checkboxes__option>label{
    font-family: Open Sans;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 16px;
  }

</style>