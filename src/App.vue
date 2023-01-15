<template>
  <div id="app">
    choosen option :{{chooseOption}} <br/>
    id:{{ optionId }}
   <Paginate-Tab :array="list"/>
   <EditableSelect :options="optionsList" @choosenOption="choosenOption"/>
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
      list: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22],
      optionsList : [{value : 'france', id: 1},{value:"italie",id:2}],
      chooseOption : '',
      optionId : ''
     
    }
  },
  methods : {
    choosenOption (payload){
      this.chooseOption = payload.value
      this.optionId = payload.id
      console.log(payload.value)
      console.log(payload.id)
    }
  }
}
</script>