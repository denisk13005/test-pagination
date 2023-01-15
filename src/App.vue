<template>
  <div id="app">
    choosen option :{{chooseOption}} <br/>
    id:{{ optionId }}
   <PaginateTab :array="listToShow"/>
   <EditableSelect :options="list" @choosenOption="choosenOption"/>
  </div>
</template>

<script>
import PaginateTab from './components/PaginateTab.vue';
import EditableSelect from './components/EditableSelect.vue';
export default {
  name: "App",
  components : {
    PaginateTab,
    EditableSelect
  },
  data() {
    return {
      list: [{value : '', id: 0},{value : 'france', id: 1},{value:"italie",id:2}],
      chooseOption : '',
      optionId : ''
     
    }
  },
  methods : {
    choosenOption (payload){
      this.chooseOption = payload.value
      this.optionId = payload.id
      
    },
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