<template>
  <div class="calculator">
    <span class="display">{{ current || "0" }}</span>
    <span v-on:click="clear" class="btn">C</span>
    <span v-on:click="sign" class="btn">+/-</span>
    <span class="btn">%</span>
    <span class="btn operator">÷</span>
    <span class="btn">7</span>
    <span class="btn">8</span>
    <span class="btn">9</span>
    <span class="btn operator">x</span>
    <span class="btn">4</span>
    <span class="btn">5</span>
    <span class="btn">6</span>
    <span class="btn operator">-</span>
    <span class="btn">1</span>
    <span class="btn">2</span>
    <span class="btn">3</span>
    <span class="btn operator">+</span>
    <span class="btn zero">0</span>
    <span class="btn">.</span>
    <span class="btn operator">=</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "1234",
    };
  },

  methods: {
    // funcion de borrado de calculadora
    clear: function () {
      this.current = "";
    },

    // funcion alterna el signo
    sign: function () {
      // operador condicional ternario :)
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
      /* --- usando if tradicional ---
      if (this.current.charAt(0) === "-") {
        this.current = this.current.slice(1);
      } else this.current = `-${this.current}`; */
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
  user-select: none;
  background-color: #f2f2f2;
  border: 1px solid #999;
}

.operator {
  background: orange;
  color: white;
}
</style>
