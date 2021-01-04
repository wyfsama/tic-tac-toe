<template>
  <div class="cell" @click="changeCell">
      <div>{{ text }}</div>
   </div>
</template>

<script>
export default {
    data(){
        return{
            text:''
        }
    },
    props:["n"],
    methods:{
        changeCell(){      
            if(this.text !== ""){
                return
            }
            this.text = this.n % 2 === 0 ? "x" :"o";   
            this.$emit('click',this.text)
        }
    }
}
</script>

<style>
    .cell {
        width: 100px;
        height: 100px;
        border: solid 1px black;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 80px;
    }
</style>