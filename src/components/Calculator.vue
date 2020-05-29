<template>
  <div class="calculator">
    <div class= "display">{{current || 0}}</div>
    <button @click="clear"  class="btn">C</button>
    <button @click="sign" class="btn">+/-</button>
    <button @click="percent" class="btn">%</button>
    <button @click="divide" class="btn-operator">÷</button>
    <button @click="append('7')" class="btn">7</button>
    <button @click="append('8')" class="btn">8</button>
    <button @click="append('9')" class="btn">9</button>
    <button @click="times" class="btn-operator">x</button>
    <button @click="append('4')" class="btn">4</button> 
    <button @click="append('5')" class="btn">5</button>
    <button @click="append('6')" class="btn">6</button>
    <button @click="minus" class="btn-operator">-</button>
    <button @click="append('1')"  class="btn">1</button>
    <button @click="append('2')"  class="btn">2</button>
    <button @click="append('3')"  class="btn">3</button>
    <button @click="add" class="btn-operator">+</button>
    <button @click="append('0')" class="zero">0</button>
    <button @click="dot" class="btn">.</button>
    <button  @click="equal" class="btn-operator">=</button>

  

  </div>
</template>

<script>
export default {
  data(){
    return {
   
      current: "",
      previous: null,
      operator: null,
      operatorClicked: false
    }
  },
  name: 'Calculator',
  props: {
    msg: String
  },
  methods:{
    clear(){
      this.current = '';
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ? 
      this.current.slice(1) : `-${this.current}`;
    },
    percent(){
      this.current = (parseFloat(this.current) / 100).toString()
    },
    append(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`
    },
    dot(){
      if(this.current.indexOf('.') === -1){
        this.append('.')
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;  
    },
    divide(){ 
      this.operator = (a, b) => b / a;
      this.setPrevious();      
    },
    minus(){
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    times(){
      console.log("times")
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    add(){
     
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal(){
      this.current = this.operator(
        parseFloat(this.current),  
        parseFloat(this.previous)
        );
        this.previous = null
    }
  }
}
</script>

<style scoped>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: (50px, auto);
  font-size: 30px;
  width: 500px;
  height: 600px;
  margin: 0 auto;
}
.display {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  grid-column: 1/5;
  color: black;
  background-color: lightgrey;
  padding: 5px

}
.zero{
  grid-column: 1/3;
   font-size: 30px;
  font-weight: 50px;
}
.btn{
   font-size: 30px;
  font-weight: 50px;
}
.btn-operator{
  background-color: orange;
  color:white;
  font-size: 30px;
  font-weight: 50px;
}

</style>
