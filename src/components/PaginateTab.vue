<template>
  <div  class="container">
   <tr v-for="(el,index) in listesToShow" :key="index" >
    <td>{{ el.value }}</td>
   </tr>
   <div class="pagination">
    <button @click="firstPage">First Page</button>
    <button @click="previous" >-</button>
    <div class="numberCtn">
      <div class="notActivNumber" @click="goTo">{{ page === 1 || page ===2?null :page -2  }}</div>
      <div class="notActivNumber" @click="goTo">{{ page === 1 ?null :page -1  }}</div>
      <div class="activNumber"><span>{{ page }}</span> </div>
      <div class="notActivNumber" @click="goTo">{{ page === numberOfPages ? null : page + 1  }}</div>
      <div class="notActivNumber" @click="goTo">{{ page === numberOfPages || page === numberOfPages -1?null :page +2  }}</div>
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
button {
  background-color: blue;
  color: white;
  outline: none;
  border: 1px solid whitesmoke;
  border-radius: 3px ;
  font-weight: 700;
}
button:hover{
  color: blue;
  background-color: white;
  cursor: pointer;
  border-color: blue;
}
.container {
  display: flex;
  flex-direction: column;
  width: 500px;
  height: 500px;
  margin: auto
}
.pagination {
  width: 100%;
  display: flex;
  justify-content: center;
}
.numberCtn{
  flex-grow: 2;
  text-align: center;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
.activNumber {
  position: relative;
}
.activNumber span{
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 50%;
  left: 50%;
  transform: translate(-50% ,-50%);
  background-color: rgb(0, 68, 255);
  width: 30px;
  height: 30px;
  text-align: center;
  border-radius: 50%;
  color: white;
}
.notActivNumber {
  font-size: 10px;
  cursor: pointer;

}

</style>
