<template>
  <div class="calculator">
    <div class="result">
      <h2>{{userInput}}</h2>
      <p>{{userExpression}}</p>
    </div>
    <div class="dial">
      <div class="row">
        <input type="button" value="%" class="function-button btn-action" @click="addSimbol('%')"/>
        <input type="button" value="CE" class="function-button btn-action" @click="clear('all')"/>
        <input type="button" value="C" class="function-button btn-action" @click="clear('one')"/>
        <input type="button" value="/" class="function-button btn-action" @click="addSimbol('/')"/>
      </div>
      <div class="row">
        <input type="button" value="7" class="number-button btn-action" @click="addSimbol('7')"/>
        <input type="button" value="8" class="number-button btn-action" @click="addSimbol('8')"/>
        <input type="button" value="9" class="number-button btn-action" @click="addSimbol('9')"/>
        <input type="button" value="*" class="function-button btn-action" @click="addSimbol('*')"/>
      </div>
      <div class="row">
        <input type="button" value="4" class="number-button btn-action" @click="addSimbol('4')"/>
        <input type="button" value="5" class="number-button btn-action" @click="addSimbol('5')"/>
        <input type="button" value="6" class="number-button btn-action" @click="addSimbol('6')"/>
        <input type="button" value="-" class="function-button btn-action" @click="addSimbol('-')"/>
      </div>
      <div class="row">
        <input type="button" value="1" class="number-button btn-action" @click="addSimbol('1')"/>
        <input type="button" value="2" class="number-button btn-action" @click="addSimbol('2')"/>
        <input type="button" value="3" class="number-button btn-action" @click="addSimbol('3')"/>
        <input type="button" value="+" class="function-button btn-action" @click="addSimbol('+')"/>
      </div>
      <div class="row">
        <input type="button" value="0" class="number-button btn-action" @click="addSimbol('0')"/>
        <input type="button" value="." class="number-button btn-action" @click="addSimbol('.')"/>
        <input type="button" value="=" class="equal-function btn-action" @click="solveExpression()"/>
      </div>
    </div>
  </div>
</template>

<script>
import { evaluate } from 'mathjs';

export default {
  name: 'CalculatorComponent',
  data(){
    return{
      userInput: '',
      userExpression: '',
    }
  },
  methods:{
    addSimbol(value){
      const operationSigns = ['+', '-', '*', '/'];
      if (operationSigns.includes(value)){
        this.userInput = value;
        this.userExpression += ` ${value} `;
      }
      else{
        if (operationSigns.includes(this.userInput)){
          this.userInput = '';
        }
        this.userInput += value;
        this.userExpression += value;
      }
    },
    solveExpression(){
      this.userInput = evaluate(this.userExpression);
      this.userExpression = '';
    },
    clear(clearType){
      if (clearType === 'all'){
        this.userExpression = '';
        this.userInput = '';
      }
      else if (clearType === 'one'){
        let deleteNum = 1;
        if (this.userExpression.at(-1) == ' '){
          deleteNum = 3;
        }
        this.userExpression = this.userExpression.substring(0, this.userExpression.length - deleteNum);
        this.userInput = this.userInput.substring(0, this.userInput.length - 1);
      }
    }
  },
}
</script>

<style scoped>
  .calculator{
    width: 330px;
    height: 667px;
  }
  .result{
    height: 217px;
    background-color: #D9D9D9;
    text-align: right;
  }
  .result p{
    padding: 10px 10px;
  }
  .result h2{
    padding: 10px 10px;
    margin: 0px;
  }
  .dial{
    background-color: #3A3535;
    text-align: center;
    padding: 10px 0px;
  }
  .function-button{
    width: 70px;
    height: 70px;
    background-color: #818181;
    border: 0px;
    border-radius: 90px;
    margin: 5px 5px;
  }
  .number-button{
    width: 70px;
    height: 70px;
    background-color: #D9D9D9;
    border: 0px;
    border-radius: 90px;
    margin: 5px 5px;
  }
  .equal-function{
    width: 144px;
    height: 70px;
    background-color: #CF6300;
    border: 0px;
    border-radius: 90px;
    margin: 5px 5px;
  }
  .btn-action:hover{
    border: 2px solid rgb(43, 42, 42);
  }
  .btn-action:active{
    opacity: .6;
  }
</style>
