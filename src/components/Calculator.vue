<template>
  <div class="calculator">
    <div class="display">{{result || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="times" class="btn operator">X</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append(0)" class="zero btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data(){
  return{
  result:'',
  operator:null,
  previous:null,
  operatorClicked:false,
  }
},
methods:{
  clear(){
  this.result='';
  },
  sign(){
  this.result=this.result.charAt(0) === '-' ?  this.result.slice(1) : `-${this.result}`;
  },
  percent(){
  this.result= `${parseFloat(this.result)/100}`
  },
  append(number){
	if(this.operatorClicked){
	this.result = '';
	this.operatorClicked = false;

}
  this.result=`${this.result}${number}`
  },
  dot(){
  if(this.result.indexOf('.') === -1){
  this.append('.');
  }
  },
  setPrevious(){
	this.operatorClicked=true;
	this.previous=this.result;
},
  divide(){
	this.operator=(a, b) => a/b;
	operatorClicked=true;
	this.setPrevious();

  },
  times(){
	this.operator=(a, b) => a*b;
	this.setPrevious();

  },
  minus(){
	this.operator=(a, b) => a-b;
	this.setPrevious();
  },
  add(){
this.operator=(a, b) => a+b;
this.setPrevious();

  },
  equal(){
	this.result=`${this.operator(parseFloat(this.result), parseFloat(this.previous))}`;
  this.previous=null;
  }

}

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
width:400px;
margin:0 auto;
display:grid;
font-size:40px;
grid-template-columns:repeat(4, 1fr);
grid-auto-rows: minmax(50px, auto);
}
.display{
grid-column: 1/5;
background-color:skyblue;
color:#fff;
}
.zero{
grid-column:1/3
}
.btn{
background-color:blue;
border:solid 1px #999;
color:#fff;
}
.operator{
background-color:green;
}

</style>
