<template>
  <div id="app">
    App page ddd
   <Paginate-Tab :array="list"/>
   <EditableSelect :options="optionsList"/>
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
      optionsList : ["france", "danemark","italie","espagne","canada","senegal"]
     
    }
  },
}
</script>