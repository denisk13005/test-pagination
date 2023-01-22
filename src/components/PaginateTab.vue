<template>
  <div :style="{background : 'blue'}" class="container">
   <tr v-for="el in listesToShow" :key="el.id" >
    <td>{{ el.value }}</td>
   </tr>
   <div class="pagination">
    <button @click="firstPage">First Page</button>
    <button @click="previous" >-</button>
    <div class="numberCtn">
      <div class="notActivNumber" @click="goTo">{{ page === 1 ?null :page -1  }}</div>
      <div class="activNumber">{{ page }}</div>
      <div class="notActivNumber" @click="goTo">{{ page === numberOfPages ? null : page + 1  }}</div>
    </div>
      <span>page {{ page}} / {{ numberOfPages }}</span>
    <button @click="next">+</button>
    <button @click="lastPage">LastPage</button>
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
      
      elPerPage: 5,
      page :1,
      numberOfPages : 1,
      startIndex:0,
      endIndex : 6
     
    }
  },
  mounted(){
    console.log(this.array,'array')
    console.log(this.array.length)
    console.log(this.numberOfPages);
    this.getPaginatedArray()
 
  },
 
  methods : {
    goTo(e){
      console.log(e.target.textContent)
      this.page = parseInt(e.target.textContent)
      this.getPaginatedArray()
    },
    firstPage(){
      
      this.page = 1
      this.getPaginatedArray()
    },
    lastPage() {
      this.page = this.numberOfPages
      this.getPaginatedArray()
    },
    changeElPerPage() {
      this.elPerPage = parseInt(this.elPerPage)
      this.page = 1
      this.getPaginatedArray()
    },
    getPaginatedArray(){
     console.log(this.elPerPage,"elPP", typeof this.elPerPage)
     this.numberOfPages = Math.ceil(this.array.length / this.elPerPage)
      this.startIndex = (this.page * this.elPerPage) - this.elPerPage
      this.endIndex = this.startIndex + this.elPerPage 
      console.log(this.array.slice(this.startIndex, this.endIndex))
  
    
      
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
  computed : {
    listesToShow(){
      return  this.array.slice(this.startIndex, this.endIndex)
    }
  }
  
};
</script>

<style  scoped>
.container {
  display: flex;
  flex-direction: column;
  width: 500px;
  height: 500px;
  margin: auto
}
.pagination {
  width: 100%;
  background: rgb(42, 139, 79);
  display: flex;
  justify-content: center;
}
.numberCtn{
  flex-grow: 2;
  border: 1px solid red;
  text-align: center;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
.activNumber {
  background: rgb(44, 67, 197);
  flex-grow: 2;
}
.notActivNumber {
  flex-grow: 1;
  font-size: 12px;
  cursor: pointer;

}

</style>
