<template>
  <div id="app">
    <div class="container">
     <div>第{{n}}回合</div>
     <div class="chess">
        <div class="row">
          <Cell @click="greet(0,$event)" :n="n" />
          <Cell @click="greet(1,$event)" :n="n" />
          <Cell @click="greet(2,$event)" :n="n" />
        </div>
        <div class="row">
          <Cell @click="greet(3,$event)" :n="n" />
          <Cell @click="greet(4,$event)" :n="n" />
          <Cell @click="greet(5,$event)" :n="n" />
        </div>
        <div class="row">
          <Cell @click="greet(6,$event)" :n="n" />
          <Cell @click="greet(7,$event)" :n="n" />
          <Cell @click="greet(8,$event)" :n="n" />
        </div>
    </div>
    <div>结果：{{res===null?"胜负未分":`胜利者为${res}`}}</div>
    </div>
  </div>
</template>

<script>
import Cell from './components/Cell'
export default {
  name: 'App',
  components:{Cell},
  data(){
    return{
      n:0,
      res:null,
      map:[
        //  0 1 2
        [null,null,null], 
        //  3 4 5
        [null,null,null],
        //  6 7 8
        [null,null,null]
      ]
    }
  },
  methods:{
    greet(i,text){
      this.n++;
      // console.log(`${i}被点了，内容为${text}`);
      this.map[Math.floor(i/3)][i%3] = text
      this.tell();
    },
    tell(){
     for(let k=0;k<3;k++){
       if(this.map[k][0]!== null && this.map[k][0] === this.map[k][1] && this.map[k][1] === this.map[k][2])
         this.res = this.map[k][0]
       }
     for(let j=0;j<3;j++){
       if(this.map[0][j]!==null && this.map[0][j] === this.map[1][j] && this.map[1][j]===this.map[2][j])
       this.res = this.map[0][j]
     } 
     if(this.map[0][0]!==null&&this.map[0][0]===this.map[1][1]&&this.map[1][1]===this.map[2][2])
     {this.res = this.map[0][0]}
     if(this.map[0][2]!==null&&this.map[0][2]===this.map[1][1]&&this.map[1][1]===this.map[2][0])
     {this.res = this.map[0][2]}
   },
   clean(){
     this.n=''
   }
  } 
}
</script>
  
<style>
  .row {
    display: flex;
  }
  .container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
</style>
