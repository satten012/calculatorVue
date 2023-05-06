<template >
  <div class="container">
      <div class="calculator">
          <div>
              <div>
                  <div class="preveusResult">{{ preveusResult.join(", ") }}</div>

              </div>
              <div class="value" @click="calculate"> {{ value }} </div>

              <div class="buttons">
                  <div class = "clear" @click="clear">ac</div>
                  <div class = "polarityInverter" @click="polarityInverter">+/-</div>
                  <div class = "percent" @click="percent">%</div>
                  <div class ="operate" @click="operate">/</div>
                  <div class="number" @click="addValue">7</div>
                  <div class="number" @click="addValue">8</div>
                  <div class="number" @click="addValue">9</div>
                  <div class ="operate" @click="operate">x</div>
                  <div class="number" @click="addValue">4</div>
                  <div class="number" @click="addValue">5</div>
                  <div class="number" @click="addValue">6</div>
                  <div class ="operate" @click="operate">-</div>
                  <div class="number" @click="addValue">1</div>
                  <div class="number" @click="addValue">2</div>
                  <div class="number" @click="addValue">3</div>
                  <div class ="operate" @click="operate">+</div>
                  <div class="number" id="zero" @click="addValue">0</div>
                  <div class="addDislake" @click="addDislake">.</div>
                  <div class ="equal" @click="resulult">=</div>
              </div>
          </div>


      </div>
  </div>
</template>

<script>
  export default {
      data() {
          return {
              value: 0,
              preveusResult: [],
              previousValue: "",
              secondValue: false,
              finalResult: ""
          }
      },
      methods: {
          addValue(event) {
              const dataAfterClick = (event.target.innerHTML)
              if (this.previousValue != "" && this.secondValue == false) {
                  this.value = dataAfterClick
                  this.secondValue = true
              }
              else if (this.previousValue != "" && this.secondValue == true) {
                  this.value += dataAfterClick
              }
              else if (this.previousValue != "") {
                  this.value = dataAfterClick
              }

              else if (this.value == 0) {
                  this.value = dataAfterClick
              }
              else {
                  this.value += dataAfterClick
              }
              console.log("первое число" + this.value)
              console.log("второе число" + this.previousValue)
          },

          operate(event) {
              if (this.finalResult == "") {
                  this.previousValue = this.value

              }
              this.operator = event.target.innerHTML
              console.log(this.operator)
          },

          resulult() {
              let finalResult = 0

              switch (this.operator) {
                  case '+':
                      finalResult = Number(this.previousValue) + Number(this.value);
                      break;
                  case '-':
                      finalResult = this.previousValue - this.value;
                      break;
                  case 'x':
                      finalResult = this.previousValue * this.value;
                      break;
                  case '/':
                      finalResult = this.previousValue / this.value;
                      break;
                  default:
                      return;
                  
              }
              this.value = finalResult.toFixed(2)
              this.previousValue = finalResult
              
              this.secondValue = false
              console.log(this.previousValue)


              if (this.preveusResult.length < 4) {
                  this.preveusResult.unshift(this.value)
              }
              else {
                  this.preveusResult.unshift(this.value)
                  this.preveusResult.pop()
              }


          },
          polarityInverter() {
              if (this.value != 0 && this.value != "") {
                  this.value = this.value * -1
              }
          },
          percent() {
              this.value = this.value / 100
          },
          clear() {
              this.value = 0,
                  this.preveusResult = [],
                  this.finalResult = "",
                  this.secondValue = false,
                  this.previousValue = ""
          },
          addDislake(){
            if (this.value % 1 == 0 && this.value[this.value.length - 1] != "." && this.secondValue == ""){
              this.value += "."
            }
            if (this.value % 1 == 0 && this.value[this.value.length - 1] != ".") {
                    this.value += "."
                }
          }


      }
  }
</script>

<style>
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }

  .container {
      width: 100vw;
      height: 100vh;
      background-color: #E9E8E8;
      overflow: auto;
      overflow-x: hidden;
      padding: 0;
      margin: 0;
  }

  .calculator {
      width: 390px;
      height: 850px;
      background-color: white;
      margin: auto;
      border-radius: 25px;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
      align-items: center;
  }

  .value {

    text-align: right;
    margin-bottom: 35px;
    border-bottom: 5px solid gray;
    height: 80px;
    vertical-align: middle;
    line-height: auto;
    line-height: 70px;
    font-size: 60px;
    padding-right: 27px;
  }

  .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
      grid-auto-rows: minmax(100px, auto);

      width: 85%
  }

  .buttons>div {
      text-align: center;
      height: 40px;
      width: 71px;
      height: 83px;
      border-radius: 50%;
      line-height: 83px;
      font-size: 25px;
  }

  #zero {
      grid-column: 1/3;
      width: 163px;
      border-radius: 44px;
  }

  .number,
  #zero,
  .addDislake {
      color: #585252;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
      background: #F7F3F3;
  }

  .operate, .equal, .clear,.polarityInverter, .percent {
    background-color: #745D5D;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    color: white;
  }
  .preveusResult{
    height: 170px;
    font-size: 20px;
  }

</style>
