<template>
  <div id="app">
    choosen option :{{chooseOption}} <br/>
    id:{{ optionId }}
   <PaginateTab :array="listToShow"/>
   <!-- <EditableSelect :options="list" @choosenOption="choosenOption"/> -->
    <!-- <select name="" id="test" v-model="test" @change="inputFilterList">
      <option value="test">test</option>
      <option value="test2">test2</option>
      <option value="test3">test3</option>
    </select> -->
    <!-- <select name="" id="test2" v-model="test2" @change="inputFilterList">
      <option value="tests">tests</option>
      <option value="tests2">tests2</option>
      <option value="tests3">tests3</option>
    </select>
    {{ test }}
    {{ test2 }}

    <div v-for="(el,index) in arrayToShow" :key="index">
    <p>{{ el.name }}</p></div> -->
  </div>
</template>

<script>
import PaginateTab from './components/PaginateTab.vue';
// import EditableSelect from './components/EditableSelect.vue';
export default {
  name: "App",
  components : {
    PaginateTab,
    // EditableSelect
  },
  data() {
    return {
      list: 
      [{value : 'r', id: 0},{value : 'france', id: 1},{value:"italie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"dd",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"itaeelie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      {value:"italie",id:2},
      
    
    ],
      chooseOption : '',
      optionId : '',
    test:'',
    test2:'',
    array:[
      {test:"test",test2:"tests3",name:1},
      {test:"test", test2:'tests2',name:2},
      {test:"test1", test2:'tests2',name:3},
      {test:"test",test2:"tests",name:4},
    ],
    arrayToShow:[],
    filterList:[]
     
    }
  },
  mounted(){
    this.arrayToShow = Array.from(this.array)
  },
  methods : {
    choosenOption (payload){
      this.chooseOption = payload.value
      this.optionId = payload.id
      
    },
    inputFilterList(e){
     
      let selectField = (e.target.id)
      let fieldValue  = (e.target.value)
      let obj = {}
      obj[selectField] = fieldValue
      
      
     this.filterList.push(obj)
      let t =  Array.from(new Set(this.filterList))
     this.filteredArrayToShow(t)
    

    },
    filteredArrayToShow(filterList){
      let a = Array.from(this.array)
      console.log(a)
      filterList.forEach(el => {
        a.filter(element => element[Object.key(el)] === Object.key(el) )
      })
      
    }

  },
  computed: {
    listToShow () {
      if(this.chooseOption !== ''){
        console.log('titi')
        return this.list.filter(el => el.value === this.chooseOption)
      }
      else {
        console.log('toto')
        return this.list 
      }
    }
  }
}
</script>