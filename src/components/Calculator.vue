<template>
  <div class="calculator">
    <div class="display">{{ current || "0"}}</div>
    <div class="btn" @click="clear">AC</div>
    <div class="btn" @click="negate">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn bg-operator" @click="divide">÷</div>
    <div class="btn" @click="append(7)">7</div>
    <div class="btn" @click="append(8)">8</div>
    <div class="btn" @click="append(9)">9</div>
    <div class="btn bg-operator" @click="multiply">x</div>
    <div class="btn" @click="append(4)">4</div>
    <div class="btn" @click="append(5)">5</div>
    <div class="btn" @click="append(6)">6</div>
    <div class="btn bg-operator" @click="extract">-</div>
    <div class="btn" @click="append(1)">1</div>
    <div class="btn" @click="append(2)">2</div>
    <div class="btn" @click="append(3)">3</div>
    <div class="btn bg-operator" @click="sum">+</div>
    <div class="btn zero" @click="append(0)">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn bg-operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "",
      operator: null,
      operatorClicked: false,
      previous: null,
    };
  },
  methods: {
    append: function (number) {
        if (this.operatorClicked) {
          this.operatorClicked = false;
          this.current = number;
        }
        else {
          this.current = this.current === "0" ? number: `${this.current}${number}`;
        }
    },
    clear: function () {
      this.current = "";
    },
    divide: function () {
      this.operator = (a,b) => (a/b)*1;
      this.previous = this.current*1;
      this.operatorClicked = true;
    },
    dot: function () {
      if (this.current.indexOf(".",0) == -1) {
        this.current = this.current + ".";
      }
    },
    extract: function () {
      this.operator = (a,b) => (a-b)*1;
      this.previous = this.current*1;
      this.operatorClicked = true;
    },
    equal: function () {
      this.current = this.operator(this.previous*1,this.current*1)*1;
      this.previous = null;
    },
    multiply: function () {
      this.operator = (a,b) => (a*b)*1;
      this.previous = this.current*1;
      this.operatorClicked = true;
    },
    percent: function () {
        this.current = (parseFloat(this.current)/100)*1
    },
    sum: function () {
      this.operator = (a,b) => (a+b)*1;
      this.previous = this.current*1;
      this.operatorClicked = true;
    },
    negate: function () {
        // this.current = this.current.charAt(0) === "-" ? this.current.slice(1) : `-${this.current}`;
        if(this.current.charAt(0) !== "+"){
          `-${this.current}`;
        }
      }
  }
};
</script>

<style scoped>

.btn {
  background: rgb(65, 64, 64);
  border: 1px solid rgb(46, 44, 44);
  color: white;
  cursor: pointer;
}

.btn:active {
  background: black;
}

.calculator {
  border: 1px solid rgb(46, 44, 44);
  display: grid;
  font-size: 2rem;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  margin: 0 auto;
  text-align: center;
  width: 400px;
}

.display {
  background-color: gray;
  color: white;
  display: grid;
  grid-column: 1/5;
  grid-auto-rows: minmax(50px, auto);
  max-width: 400px;
  overflow-x: hidden;
  padding: auto 16px;
}

.bg-operator {
  background-color: orange;
}

.zero {
  display: grid;
  grid-column: 1/3;
}
</style>