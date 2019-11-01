<template>
  <div class="calculator"  :class="{ active: isActive }" id="app">
    <div class="display"><span style="font-size:20px;">Vue Calculator</span> <br>{{current || '0'}}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn  operator" @click="times">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn  operator" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn  operator" @click="add">+</div>
    <div class="btn zero" @click="append('0')"  style="border-radius:0 0 0 7px">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn  operator" @click="equal" style="border-radius:0 0 7px 0">=</div>
    
    
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
      isActive: false,
    }
  },
  methods:{
    clear(){
      this.current = '';
      this.isActive=  false
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`; 
    },
    percent(){
      this.current = `${parseFloat(this.current)/100}`
    },
    append(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}` ;
      this.isActive = true;
    },
    dot(){
      if (this.current.indexOf('.') === -1 ){
        this.append('.');
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus(){
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add(){
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal(){
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
      
    }
  }
}
</script>

<style >
body{
  background-color: #fff4e4;
}
.calculator{
  margin: 0 auto;
  width: 400px;
  height: 500px;
  font-size: 40px;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px, auto);
  display: grid;
}
.active{
  border-radius: 7px;
  box-shadow: 0px 0px 8px #d1274b;
}
.zero{
  grid-column: 1/3;
}
.display{
  grid-column: 1/5;
  background-color: #584b42;
  color: white;
  border-radius: 7px 7px 0 0;
}
.btn{
  background-color: #eae9e9;
  border: 1px solid #999;
  cursor: pointer;
}
.operator{
  background-color: #ff502f;
  color: white;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
