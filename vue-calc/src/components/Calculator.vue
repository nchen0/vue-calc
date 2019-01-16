<template>
  <div class="App">
    <div class="container">
      <div v-if="storedNumber !== 0 && calculation === 0" class="display-screen">{{storedNumber}}</div>
      <div v-else class="display-screen">{{calculation}}</div>
      <div class="buttons">
        <div class="number-buttons">
          <button v-on:click="clear" class="big-button clear-button">Clear</button>
          <button v-on:click="addNumber(7)" class="button">7</button>
          <button v-on:click="addNumber(8)" class="button">8</button>
          <button v-on:click="addNumber(9)" class="button">9</button>
          <button v-on:click="addNumber(4)" class="button">4</button>
          <button v-on:click="addNumber(5)" class="button">5</button>
          <button v-on:click="addNumber(6)" class="button">6</button>
          <button v-on:click="addNumber(1)" class="button">1</button>
          <button v-on:click="addNumber(2)" class="button">2</button>
          <button v-on:click="addNumber(3)" class="button">3</button>
          <button v-on:click="addNumber(0)" class="big-button">0</button>
        </div>
        <div class="action-buttons">
          <button v-on:click="calculate('divide')" class="button action-button">÷</button>
          <button v-on:click="calculate('multiply')" class="button action-button">×</button>
          <button v-on:click="calculate('minus')" class="button action-button">−</button>
          <button v-on:click="calculate('add')" class="button action-button">+</button>
          <button v-on:click="clickEqual('equal')" class="button action-button equal-button">=</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      calculation: 0,
      prevCalculation: 0,
      storedNumber: 0,
      calculateMethod: "",
      prevNumber: false
    };
  },
  methods: {
    addNumber: function(e) {
      if (
        (this.calculation === 0 || this.prevCalculation !== 0) &&
        this.prevNumber === false
      ) {
        this.calculation = e;
      } else {
        this.calculation = Number(this.calculation.toString() + e.toString());
      }
    },
    calculate: function(e) {
      this.calculatedMethod = e;
      this.storedNumber = this.calculation;
      this.prevNumber = true;
      this.calculation = 0;
    },
    clickEqual: function(e) {
      switch (this.calculatedMethod) {
        case "divide":
          this.calculation = Math.round(this.storedNumber / this.calculation);
          this.storedNumber = 0;
          return;
        case "add":
          this.calculation = this.storedNumber + this.calculation;
          this.storedNumber = 0;
          return;
        case "subtract":
          this.calculation = this.storedNumber - this.calculation;
          this.storedNumber = 0;
          return;
        case "multiply":
          this.calculation = this.storedNumber * this.calculation;
          this.storedNumber = 0;
          return;
      }
    },
    clear: function() {
      (this.calculation = 0),
        (this.prevCalculation = 0),
        (this.storedNumber = 0),
        (this.calculateMethod = ""),
        (this.prevNumber = false);
    }
  }
};
</script>

<style scope>
.App {
  text-align: center;
  box-sizing: border-box;
  font-size: 40px;
}

.container {
  height: 620px;
  width: 400px;
  border: 1px solid black;
  display: flex;
  flex-direction: column;
  padding: 0;
  box-sizing: border-box;
}

.display-screen {
  height: 120px;
  background-color: black;
  color: white;
  width: 400px;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  font-size: 65px;
}

/* Buttons */
.buttons {
  display: flex;
}

.number-buttons {
  display: flex;
  flex-wrap: wrap;
}

.big-button {
  height: 100px;
  width: 300px;
  border: 1px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
}

.button {
  height: 100px;
  width: 100px;
  border: 1px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
}

.action-button {
  background-color: #b30000;
  color: white;
  font-size: 50px;
}
.equal-button {
  background-color: #ff8000;
  color: white;
}

/* Hover & Action */
.button:hover,
.big-button:hover {
  background-color: rgb(224, 224, 224);
  cursor: pointer;
}

.button:active,
.big-button:active {
  font-weight: bold;
}

.action-button:hover {
  background-color: #920202;
}

.equal-button:hover {
  background-color: #dd7206;
}

.action-button:focus {
  outline-color: grey;
}
</style>
