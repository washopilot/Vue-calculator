<template>
  <div class="calculator">
    <span class="display">{{ current || '0' }}</span>
    <span v-on:click="clear()" class="btn">C</span>
    <span v-on:click="sign()" class="btn">+/-</span>
    <span v-on:click="percent()" class="btn">%</span>
    <span v-on:click="divide()" class="btn operator">÷</span>
    <span v-on:click="append('7')" class="btn">7</span>
    <span v-on:click="append('8')" class="btn">8</span>
    <span v-on:click="append('9')" class="btn">9</span>
    <span v-on:click="times()" class="btn operator">x</span>
    <span v-on:click="append('4')" class="btn">4</span>
    <span v-on:click="append('5')" class="btn">5</span>
    <span v-on:click="append('6')" class="btn">6</span>
    <span v-on:click="minus()" class="btn operator">-</span>
    <span v-on:click="append('1')" class="btn">1</span>
    <span v-on:click="append('2')" class="btn">2</span>
    <span v-on:click="append('3')" class="btn">3</span>
    <span v-on:click="add()" class="btn operator">+</span>
    <span v-on:click="append('0')" class="btn zero">0</span>
    <span v-on:click="dot()" class="btn">.</span>
    <span v-on:click="equal()" class="btn operator">=</span>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        previous: null,
        current: '1234',
        operator: null,
        operatorClicked: false,
      };
    },

    methods: {
      // funcion de borrado de calculadora
      clear: function() {
        this.current = '';
      },

      // funcion alterna el signo
      sign: function() {
        // operador condicional ternario :)
        this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
        /* --- usando if tradicional ---
      if (this.current.charAt(0) === "-") {
        this.current = this.current.slice(1);
      } else this.current = `-${this.current}`; */
      },

      percent: function() {
        this.current = `${parseFloat(this.current) / 100}`;
      },

      append: function(number) {
        if (this.operatorClicked) {
          this.current = '';
          this.operatorClicked = false;
        }
        this.current = `${this.current}${number}`;
      },

      dot: function() {
        if (this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },

      setPrevious: function() {
        this.previous = this.current;
        this.operatorClicked = true;
      },

      divide: function() {
        this.operator = (a, b) => a / b;
        this.setPrevious();
      },

      times: function() {
        this.operator = (a, b) => a * b;
        this.setPrevious();
      },

      minus: function() {
        this.operator = (a, b) => a - b;
        this.setPrevious();
      },

      add: function() {
        this.operator = (a, b) => a + b;
        this.setPrevious();
      },

      equal: function() {
        this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`;
        this.previous = null;
      },
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }

  .display {
    grid-column: 1/5;
    background-color: black;
    color: white;
  }

  .zero {
    grid-column: 1/3;
  }

  .btn {
    cursor: pointer;
    user-select: none;
    background-color: #f2f2f2;
    border: 1px solid #999;
  }

  .btn:active {
    transform: scale(0.95);
  }

  .operator {
    background: orange;
    color: white;
  }
</style>
