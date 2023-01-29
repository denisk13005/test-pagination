<template>
  <div  class="container">
    

   <TabComponent :listesToShow = "listesToShow"/>
   <div class="pagination">
    
    <div class="numberCtn">
      <div class="leftBtns">

        <button @click="firstPage">First Page</button>
        <button @click="previous" >-</button>
      </div>
      <div class="numbers">

        <div class="notActivNumber" @click="goTo">{{ page === 1 || page ===2?null :page -2  }}</div>
        <div class="notActivNumber" @click="goTo">{{ page === 1 ?null :page -1  }}</div>
        <div class="activNumber"><span>{{ page }}</span> </div>
        <div class="notActivNumber" @click="goTo">{{ page === numberOfPages ? null : page + 1  }}</div>
        <div class="notActivNumber" @click="goTo">{{ page === numberOfPages || page === numberOfPages -1?null :page +2  }}</div>
      </div>
      <div class="rightBtns">

        <button @click="next">+</button>
        <button @click="lastPage">LastPage</button>
      </div>
    </div>
   
    <div class="pageChoice">
      <div >

       
        <select name="" id="elPerPage"  v-model="elPerPage" @change="changeElPerPage">
          <option value= "5" >5</option>
          <option value="10">10</option>
          <option value="50">50</option>
          <option value="100">100</option>
        </select>
        <span>Eléments/page</span>
      </div>
      <span>page {{ page}} / {{ numberOfPages }}</span>
    </div>

   
   </div>
  </div>
</template>

<script>
import TabComponent from './TabComponent.vue';
export default {
  components : {TabComponent},
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
      console.log('ici')
      let tabArray = this.array.slice(this.startIndex, this.endIndex)
      return  tabArray
    }
  }
  
};
</script>

<style  scoped>
button {
  background-color: #011a5c;
  color: white;
  outline: none;
  border: 1px solid white;
  border-radius: 3px ;
  width: 6vw;
  height: 4vh;
  font-size: 16px;
  
}
button:hover{
  color: #011a5c;
  background-color: white;
  cursor: pointer;
  border-color: #011a5c;
}
.leftBtns button{
  margin-right: 10px;
 
}

.rightBtns button{
  margin-left: 10px;
}
.container {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: max-content;
  margin: auto;
  border: 1px solid #011a5c;
  
}
.pagination {
  width: 50%;
  height: 10vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: auto;
  color: #011a5c;
  border: 1px solid #011a5c;

  
}
.numberCtn{
  text-align: center;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width :100%;
  margin: auto;
  height: calc(4vh + 2px);

}
.numbers {
  width:20%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
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
  background-color: rgb(255, 255, 255);
  width: 30px;
  height: 30px;
  text-align: center;
  border-radius: 50%;
  color: #011a5c;
  font-size: 18px;
}
.notActivNumber {
  font-size: 10px;
  cursor: pointer;
  margin-left: 40px;
  margin-right: 40px;
  

}
.pageChoice {
  display: flex;
  justify-content: space-between;
  padding: 5px;
}
#elPerPage{
  margin-right: 15px;  
  background-color: white;
  color: #011a5c;
  border: 1px solid #011a5c;
}

</style>
