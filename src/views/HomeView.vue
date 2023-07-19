<script>
export default {
    data() {
      return {
        text:"0",
        text1:"",
        text_check:false,
        Asmd:"",
        calculate:["%", "CE", "C", "+", "1", "2", "3", "-", "4", "5", "6", "*", "7", "8", "9", "/", "+/-", "0", ".", "="],
        calculate1:["%", "+","-","*","/", "="],
        str:""
      }
    },methods: {
        content(abs){
            if(abs==="CE"){this.text="0";return}
            if(abs==="C"){this.text="0";this.text1="";this.Asmd="";return}
            if(abs==="+/-"){
              if(Math.sign(this.text)===1){this.text=-Math.abs(this.text)}
              else{this.text=Math.abs(this.text)}
              //this.text1=this.text;
              return;
            }
            if(this.calculate1.includes(abs)){
                if(this.Asmd==="="){
                  this.text1="";
                }else if(this.text1!=="" && this.text_check===false){
                  this.text=parseFloat(eval(this.text1+this.Asmd+(this.text)));
                }                               
                this.Asmd=abs;
                this.text_check=true;
            }else{
                if(this.text_check){this.text1=this.text;this.text="0";this.text_check=false;}
                if(abs==="." && this.text.includes(abs)){return} // 小數點是否重複典籍
                if(this.text.length>10){return} //長度
                if(this.text==="0" || this.text===0){this.text = abs}else{this.text += abs;}
            }
            
        }
    },
}
</script>

<template lang="">
  <div class="container">
      <h1>{{text}}</h1>
      <div class="computer">
          <button type="button" v-for="(item,index) in calculate" :key="index" v-on:click="content(item)">{{item}}</button>
      </div>
  </div>
</template>

<style lang="scss" scoped>
    .container{
        width: 30rem;
        margin: auto;
        background-color: white;
        padding: 1rem;
        border-radius: 6px;

        h1{
          text-align: end;
          font-size: 5rem;
          padding: 0.5rem;
          margin-bottom: 0.5rem;
          border-bottom: 1px solid black;
          word-wrap: break-word;
        }
        .computer{
          display: flex;
          flex-wrap: wrap;

          button{
            width: 6rem;
            font-size: 3rem;
            padding: 1rem 0;
            margin: 0.5rem;
            border-radius: 4px;
            cursor: pointer;
          }
        }
    }
</style>
