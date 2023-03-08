<template>
  <div id="app">
    <div class="container">
      <table>
        <tr>
          <td colspan="5">
            <div id="screen">
              <span id="screen_top">M=<span v-text="inputNumber"></span></span>
              <div id="screen_bottom">
                <!-- v-text is a directive that is used to replace the content of HTML tag with private data -->
                <!-- It will update the content automatically when data is changed. It is called data reactive -->
                <span v-text="output" id="operand1">0</span>
                <span id="operator"></span>
                <span id="operand2"></span>
              </div>
              <!-- <span id="screen_bottom">0</span> -->
            </div>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-warning" v-on:click="Clear()">MC</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning" v-on:click="Read()">MR</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning" v-on:click="Minus()">M-</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning" v-on:click="Plus()">M+</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="backspace()">
              <i class="fa fa-long-arrow-right" aria-hidden="true"></i>
            </button>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber(7)">7</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber(8)">8</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber(9)">9</button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary" v-on:click="showOperation(' / ')">÷</button>
          </td>
          <td>
            <button type="button" class="btn btn-light">+/-</button>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber(4)">4</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber(5)">5</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber(6)">6</button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary" v-on:click="showOperation(' * ')">x</button>
          </td>
          <td>
            <button type="button" class="btn btn-secondary" v-on:click="showOperation(' - ')">-</button>
          </td>
        </tr>
        <tr>
          <td>
            <button
              v-on:click="showNumber(1)"
              type="button"
              class="btn btn-light"
            >
              1
            </button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber(2)">2</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber(3)">3</button>
          </td>
          
          <td rowspan="2">

            <button type="button" class="btn btn-secondary long-btn" v-on:click="showOperation(' + ')">+</button>
          </td>
          <td rowspan="2">
            <button type="button" class="btn btn-primary long-btn" v-on:click="calculate()">=</button>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-danger" v-on:click="reset()">C</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber('0')">0</button>
          </td>
          <td>
            <button type="button" class="btn btn-light" v-on:click="showNumber('.')">.</button>
          </td>
        </tr>
      </table>
    </div>
    <div class="alert alert-danger" id="message_panel" role="alert">
      something wrong here
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {},
  data() {
    return {
      // This is the private data section which can be used inside this component
      output: "",
      inputNumber: 0,
    };
  },
  methods: {
    showNumber(number) {
      // Assign number when user click to the inputNumber data
      // To access private data from methods, use (this.)
      this.output += number;
    },
    showOperation(operator) {
      this.output += operator;
    },
    calculate() {
      this.output = eval(this.output);
    },
    reset() {
      this.output = "";
    },
    Plus() {
      this.inputNumber = eval(this.inputNumber+ " + " + this.output);
    },
    Minus() {
      this.inputNumber = eval(this.inputNumber + " - " + this.output);
    },
    Read() {
      if (this.output[(this.output.length) - 2] == "+" || this.output[(this.output.length) - 2] == "-" || this.output[(this.output.length) - 2] == "*" || this.output[(this.output.length) - 2] == "/") {
        this.output += this.inputNumber;
      }
    },
    Clear() {
      this.inputNumber = 0;
    },
    backspace() {
      if (this.output[(this.output.length) - 2] == "+" || this.output[(this.output.length) - 2] == "-" || this.output[(this.output.length) - 2] == "*" || this.output[(this.output.length) - 2] == "/") {
        this.output = this.output.slice(0, -3);
      }
      else {
        this.output = this.output.slice(0, -1);
      }
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  margin-top: 10em;
  width: 300px;
  border: 1px solid black;
  padding-top: 20px;
  padding-bottom: 20px;
}
table {
  border-spacing: 7px;
  border-collapse: separate;
}
#screen {
  border: 1px solid black;
  padding: 7px;
  width: 100%;
  height: 4em;
}
#screen_top {
  display: block;
  font-size: 0.8rem;
}
#screen_bottom {
  font-size: 1.8rem;
  display: block;
  text-align: right;
}
#operand2 {
  background-color: skyblue;
}
#operator {
  background-color: rosybrown;
}
.button-row {
  display: flex;
  justify-content: space-between;
}
button {
  width: 45px;
}
.long-btn {
  display: inline-block;
  height: 80px;
}

/* Message panel */
#message_panel {
  width: 300px;
  margin-top: 1em;
  display: none;
  margin-left: auto;
  margin-right: auto;
}
</style>
