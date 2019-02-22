<template>
  <transition name="fade">
    <div class="fraction-container">
      <div class="fraction">
        <input
          @input="onChangeFractionValue(index, 'numerator', ...arguments)"
          :value="fraction.numerator"
          @keydown="onInputkeyDown(fraction.numerator, ...arguments)"
          maxlength="2"
        >
        <div class="divider"/>
        <input
          @input="onChangeFractionValue(index, 'denominator', ...arguments)"
          :value="fraction.denominator"
          @keydown="onInputkeyDown(fraction.denominator, ...arguments)"
          maxlength="2"
        >
      </div>
      <div class="plus-sign" v-if="index < fractionsNumber-1">+</div>
      <img
        :src="require('../assets/delete-icon.png')"
        class="delete-button"
        v-if="fractionsNumber > 2"
        @click="onDeleteFraction(index)"
      >
    </div>
  </transition>
</template>

<script>
export default {
  name: "FractionComponent",
  props: {
    fraction: Object,
    onDeleteFraction: Function,
    onChangeFractionValue: Function,
    onInputkeyDown: Function,
    fractionsNumber: Number,
    index: Number
  }
};
</script>

<style scoped>
.fraction-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  position: relative;
}
.fraction {
  display: flex;
  flex-direction: column;
  width: 70px;
  margin: 0 15px;
}
.divider {
  width: 100%;
  border-bottom: 2px solid black;
  margin: 10px 0;
}
.delete-button {
  position: absolute;
  top: -30px;
  left: 90px;
  width: 20px;
  height: 20px;
  cursor: pointer;
}
input {
  height: 50px;
  font-size: 42px;
}
.plus-sign {
  font-size: 32px;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
