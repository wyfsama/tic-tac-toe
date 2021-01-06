<template>
  <div id="app">
   <div class="container">
     <div class="header">
      <div class='count'>第{{n}}回合</div>
     <button class='restart' @click="clear">重新开始</button>
    </div>
     <div class="chess">
        <div class="row">
          <Cell @click="greet(0,$event)" :n="n" ref="db1"/>
          <Cell @click="greet(1,$event)" :n="n" ref="db2"/>
          <Cell @click="greet(2,$event)" :n="n" ref="db3"/>
        </div>
        <div class="row">
          <Cell @click="greet(3,$event)" :n="n" ref="db4"/>
          <Cell @click="greet(4,$event)" :n="n" ref="db5"/>
          <Cell @click="greet(5,$event)" :n="n" ref="db6"/>
        </div>
        <div class="row">
          <Cell @click="greet(6,$event)" :n="n" ref="db7"/>
          <Cell @click="greet(7,$event)" :n="n" ref="db8"/>
          <Cell @click="greet(8,$event)" :n="n" ref="db9"/>
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
    clear(){
       this.$refs.db1.text='';
       this.$refs.db2.text='';
       this.$refs.db3.text='';
       this.$refs.db4.text='';
       this.$refs.db5.text='';
       this.$refs.db6.text='';
       this.$refs.db7.text='';
       this.$refs.db8.text='';
       this.$refs.db9.text='';
      // this.$refs.db.clearall()
    },
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
  .chess{
    padding: 1rem 0;
  }
   .restart{
    display:block;
  }
  .header{
    width: 302px;
    display: flex;
    justify-content: space-between;
  }
 

</style>
