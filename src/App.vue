<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div class="number" @click="clear">c</div>
    <div class="number" @click="Sign">-/+</div>
    <div class="number" @click="precent">%</div>
    <div class="orange number" @click="divide">÷</div>
    <div class="number" @click="append('7')">7</div>
    <div class="number" @click="append('8')">8</div>
    <div class="number" @click="append('9')">9</div>
    <div class="orange number" @click="times">x</div>
    <div class="number" @click="append('4')">4</div>
    <div class="number" @click="append('5')">5</div>
    <div class="number" @click="append('6')">6</div>
    <div class="orange number" @click="minus">-</div>
    <div class="number" @click="append('1')">1</div>
    <div class="number" @click="append('2')">2</div>
    <div class="number" @click="append('3')">3</div>
    <div class="orange number" @click="add">+</div>
    <div class="zero number" @click="append('0')">0</div>
    <div class="number" @click="dot">.</div>
    <div class="orange number" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    Sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    precent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
    },
  },
};
</script>

<style>
body {
  background: #ccc;
}
.calculator {
  width: 350px;
  text-align: center;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
  margin: 60px auto;
  overflow: hidden;
}
.display {
  grid-column: 5 / 1;
  text-align: center;
  background: #888;
  padding: 13px;
}
.zero {
  grid-column: 3 /1;
  padding: 10px;
}
.number {
  cursor: pointer;
  border: 1px solid #f6f6f6;
  padding: 10px;
}
.orange {
  background: #f50;
  padding: 10px;
}
</style>
