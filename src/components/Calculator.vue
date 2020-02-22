<template>
  <div class="calculator">
    <div class="displayPrev">{{ previous || '0' }}</div>
    <div class="display">{{ current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign"  class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="plus" class="btn operator">+</div>
    <div  @click="append(0)" class="zero btn">0</div>
    <div @click="dot('.')" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
    
  </div>
</template>

<script>
export default {
  data(){
    return {
          previous: '',
          current:'',
          operator:null,
          operatorClicked:false,
      }
  },
  methods: {
    clear(){
     this.current = '';
     this.previous = '';
    },
    sign(){
       if(this.current!=0){
        this.current = this.current.charAt(0) === '-'? this.current.slice(1) : `-${this.current}`
       }
    },
    
    percent(){
    if(this.current!=0){
        this.current = `${parseFloat(this.current) / 100}`;
       }
    },
    append(number){
    if(this.operatorClicked){
        this.current = number;
        this.operatorClicked = false;
    }
     else { this.current = `${this.current}${number}`}
    },
    dot(dot){
    if(!this.current.includes(dot)){
      this.current = `${this.current}${dot}`;
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.current = '';
      this.operatorClicked = true;
    },

    
    divide(){
     if(this.previous && this.current){
    this.equal()
    }
    else{   this.operator = (a,b) => a/b;
       this.setPrevious();}
    },


    times(){
     if(this.previous && this.current){
    this.equal()
    }

    if(this.previous && !this.current){
    this.current=this.previous
    this.previous = null 
    }
      else{this.operator = (a,b) => a * b;
      this.setPrevious();}
    },


    minus(){
     if(this.previous && this.current){
    this.equal()
    }
    if(this.previous && !this.current){
    this.current=this.previous
    this.previous = null 
    }
     else{ this.operator = (a,b) => a - b;
      this.setPrevious();}
    },


    plus(){
    if(this.previous && this.current){
    this.equal()
    }
    if(this.previous && !this.current){
    this.current=this.previous
    this.previous = null 
    }
     else{ this.operator = (a,b) => a + b;
      this.setPrevious();}
    },


    equal(){
    if(this.previous && this.current){
      this.current = `${this.operator(parseFloat(this.previous),parseFloat(this.current))}`;
      this.previous = null
      }
    }
    
  } 
}
</script>

<style scoped>
  .calculator{
  margin:0 auto;
  width:400px;
  font-size:40px;
  display:grid;
  grid-template-columns: repeat(4,1fr);
  grid-template-rows: minmax(50px;auto);
  border-radius:8px;

  }
  .displayPrev{
    text-align:left;
    grid-column: 1/5;
    background-color:#777;
    color:white;
   }
  .display{
    text-align:right;
    grid-column: 1/5;
    background-color:#333;
    color:white; 
  }
  .zero{
    grid-column:1/3;
  }
  .btn{
    background-color:#eee;
    border:1px solid #999;
    cursor: pointer;
  }
  .operator{
    background-color: orange;
    color:white;
  }
</style>
