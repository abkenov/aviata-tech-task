<template>
  <div class="options-checkboxes">
      <div class="options-checkboxes__header">
        <h2 class="options-checkboxes__title">Опции тарифа</h2>
        <div class="options-checkboxes__selection-reset tooltip" @click="discardOptionsChild">
          <p class="tooltip-text">Сбросить выбор</p>
          <svg width="18" height="14" viewBox="0 0 18 14" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" clip-rule="evenodd" d="M10.6464 6.64648L13.2929 4.00004L10.6464 1.35359L11.3535 0.646484L14 3.29293L16.6464 0.646484L17.3535 1.35359L14.7071 4.00004L17.3535 6.64648L16.6464 7.35359L14 4.70714L11.3535 7.35359L10.6464 6.64648ZM2.91465 4.00003H8C8 4.34074 8.0284 4.67482 8.08296 5.00003H2.91465C2.70873 5.58263 2.15311 6.00003 1.5 6.00003C0.671573 6.00003 0 5.32846 0 4.50003C0 3.6716 0.671573 3.00003 1.5 3.00003C2.15311 3.00003 2.70873 3.41743 2.91465 4.00003ZM7.91465 8.00003H9.52779C9.86799 8.38014 10.2559 8.71661 10.6822 9.00003H7.91465C7.70873 9.58263 7.15311 10 6.5 10C5.84689 10 5.29127 9.58263 5.08535 9.00003H0.5C0.223858 9.00003 0 8.77617 0 8.50003C0 8.22389 0.223858 8.00003 0.5 8.00003H5.08535C5.29127 7.41743 5.84689 7.00003 6.5 7.00003C7.15311 7.00003 7.70873 7.41743 7.91465 8.00003ZM2.91465 12C2.70873 11.4174 2.15311 11 1.5 11C0.671573 11 0 11.6716 0 12.5C0 13.3285 0.671573 14 1.5 14C2.15311 14 2.70873 13.5826 2.91465 13H14.5C14.7761 13 15 12.7762 15 12.5C15 12.2239 14.7761 12 14.5 12H2.91465Z"/>
          </svg>
        </div>
      </div>
      <div class="options-checkboxes__option">
        <input class="custom-checkbox" type="checkbox" name="only-direct" id="only-direct" v-model="direct" @change="returnDirect">
        <label for="only-direct">Только прямые</label>
      </div>
      <div class="options-checkboxes__option">
        <input class="custom-checkbox" type="checkbox" name="only-with-baggage" id="only-with-baggage" v-model="baggage" @change="returnBaggage">
        <label for="only-with-baggage">Только с багажом</label>
      </div>
      <div class="options-checkboxes__option">
        <input class="custom-checkbox" type="checkbox" name="only-refundable" id="only-refundable" v-model="refundable" @change="returnRefundable">
        <label for="only-refundable">Только возвратные</label>
      </div>
  </div>
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
    discardOptionsChild() {
      this.$emit('discardOptionsEvent', false)
      this.direct = false
      this.baggage = false
      this.refundable = false
    }
  },
  emits: ['directOption', 'baggageOption', 'refundOption', 'discardOptionsEvent'],
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
    margin: 50px 20px 12px 149px;
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

  .options-checkboxes__header {
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  
  .options-checkboxes__option {
    height: 32px;
    width: 100%;
    display: flex;
    align-items: center;
  }

  .options-checkboxes__option:hover {
    background: #EBEBEB;
    cursor: pointer;
  }

  .options-checkboxes__option>input {
    margin: 12px;
    border: 1px solid #B9B9B9;
    box-sizing: border-box;
    border-radius: 2px;
    cursor: pointer;
  }

  .options-checkboxes__option>label{
    font-family: Open Sans;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 16px;
    cursor: pointer;
  }

  .options-checkboxes__selection-reset{
    margin: 0 15px 0 auto;
  }

  .options-checkboxes__selection-reset>svg{
    fill: #B9B9B9;
    transition-duration: 0.2s;
  }

  .options-checkboxes__selection-reset>svg:hover {
    fill: #7284E4;
    width: 20px;
    height: 16px;
  }

  .tooltip-text {
    position: absolute;
    visibility: hidden;
    z-index: 1;
    background: #FFFFFF;
    border: 1px solid #E1E1E1;
    box-sizing: border-box;
    border-radius: 6px;
    font-family: Open Sans;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 16px;
    color: #202123;
    padding: 12px;
    top: 5px;
    left: 300px;
  }

  .tooltip:hover .tooltip-text{
    visibility: visible;
  }

</style>