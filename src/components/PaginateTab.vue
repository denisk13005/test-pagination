<template>
  <div :style="{background : 'blue'}">
   <tr v-for="el in listesToShow" :key="el" :style= "{background: 'yellow', display:'inline-block'}">
    <td>{{ el }}</td>
   </tr>
   <div class="pagination">
    <button @click="previous" >-</button>
      <span>page {{ page}} / {{ numberOfPages }}</span>
    <button @click="next">+</button>
    <select name="" id="elPerPage"  v-model="elPerPage" @change="changeElPerPage">
      <option value= "5" >5</option>
      <option value="10">10</option>
      <option value="50">50</option>
      <option value="100">100</option>
    </select>
   </div>
  </div>
</template>

<script>
export default {
  props : {
    array : {
      type : Array,
      required:true,
    }
  },
  data() {
    return {
      listesToShow: [],
      elPerPage: 5,
      page :1,
      numberOfPages : 1,
     
    }
  },
  mounted(){
    console.log(this.array)
    console.log(this.array.length)
    console.log(this.numberOfPages);
    this.getPaginatedArray()
 
  },
 
  methods : {
    changeElPerPage() {
      this.elPerPage = parseInt(this.elPerPage)
      this.page = 1
      this.getPaginatedArray()
    },
    getPaginatedArray(){
     console.log(this.elPerPage,"elPP", typeof this.elPerPage)
     this.numberOfPages = Math.ceil(this.array.length / this.elPerPage)
      let startIndex = (this.page * this.elPerPage) - this.elPerPage
      let endIndex = startIndex + this.elPerPage
      console.log(startIndex , endIndex,'---------')
  return  this.listesToShow = this.array.slice(startIndex, endIndex)
    
      
    },
    next(){
      if(this.page < this.numberOfPages){
        this.page += 1
        this.getPaginatedArray()        
      }else {
        return
      }
      console.log(this.page);
      console.log(this.page);
    },
    previous(){
      this.page > 1 ? this.page -= 1 : null
      this.getPaginatedArray()
      console.log(this.page);
    }
  },
  
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
