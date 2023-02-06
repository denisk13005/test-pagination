<template>
  <div class="container">
    <input 
    class="input" 
    type="text" 
    placeholder="choose an option" 
    v-model="optionValue" 
    @keyup="filterOptions"    
    @click="edit"/>
    <div v-show="showOptions" class="optionsContainer">
      <div class="option" v-for="(el,index) in getOptions" :key="index" @click="chooseOption(el)" > {{ el.value }}, {{ el.id }} </div>
    </div>
  </div>
</template>

<script>
  export default {
    props : {
      options : {
        type : Array,
        required : true
      }
      
    },
    mounted(){
      this.optionsToShow = this.options
    },
      data() {
        return {
          showOptions : false,
          optionValue :"",
          optionsToShow : []
        }
      },
      methods : {
        edit(){
          this.showOptions = !this.showOptions
        },
        chooseOption(el){
          console.log(el)         
          this.optionValue = el.value          
          this.showOptions = false
          this.$emit('choosenOption', el)
        },
        filterOptions(e){
          this.showOptions = true
          let search = e.target.value
          console.log(search)
           this.optionsToShow =  this.options.filter(el => el.value.includes(search))
        }
      },
      computed:{
        getOptions(){
          return this.optionsToShow
        }
      }
    
  }
</script>

<style  scoped>
  .container {
    background: rgb(163, 126, 126);
    width: max-content;
    text-align: right;
  }
  .optionsContainer {
    padding: 10px;
    height : 80px;
    overflow: auto;
    scrollbar-width: thin;
  }
  .option {
    padding: 5px;

  }
  .option:hover {
    background-color: red ;
    cursor : pointer;

  }
</style>