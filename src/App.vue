<template>
  <div id="app">
    <h1>Сложение дробей</h1>
    <div class="container">
      <FractionComponent
        v-for="(fraction, index) in fractions"
        :key="fraction"
        :index="index"
        :fraction="fraction"
        :onDeleteFraction="deleteFraction"
        :onInputkeyDown="inputkeyDown"
        :onChangeFractionValue="changeFractionValue"
        :fractionsNumber="fractions.length"
      />
      <div class="equality-sign">=</div>
      <div class="result-text">{{ fractionsAddition }}</div>
    </div>
    <button @click="addFraction">Добавить дробь</button>
  </div>
</template>

<script>
import FractionComponent from "./components/FractionComponent.vue";

export default {
  name: "app",
  methods: {
    inputkeyDown: function(inputValue, e) {
      const symbol = event.key;
      if (isNaN(symbol) && symbol !== "Backspace") {
        event.preventDefault();
      } else if (inputValue.length === 0 && symbol == 0) {
        event.preventDefault();
      }
    },
    changeFractionValue: function(index, property, e) {
      this.$data.fractions[index][property] = e.target.value;
    },
    addFraction: function() {
      if (this.$data.fractions.length < 5) {
        this.$data.fractions.push({
          numerator: "",
          denominator: ""
        });
      }
    },
    deleteFraction: function(index) {
      this.$data.fractions.splice(index, 1);
    }
  },
  data: function() {
    return {
      fractions: [
        {
          numerator: "",
          denominator: ""
        },
        {
          numerator: "",
          denominator: ""
        }
      ]
    };
  },
  computed: {
    fractionsAddition: function() {
      if (
        this.$data.fractions.some(item => !item.numerator || !item.denominator)
      ) {
        return "Заполните все поля";
      }

      return this.$data.fractions.reduce(
        (result, item) => result + item.numerator / item.denominator,
        0
      );
    }
  },
  components: {
    FractionComponent
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  margin: 70px 0;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.result-text {
  margin: 0 20px;
  font-size: 30px;
  font-weight: bold;
}
.equality-sign {
  font-size: 32px;
}
</style>
