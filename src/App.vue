<template>
  <div id="app">
    <!-- <tab-with-paginate :array="listToShow" @update="updateArray" />
    <EditableSelect :options="list" /> -->
    <EditableDropbox />
    <multiselect v-model="value" :options="options" @click="cli"
      >test</multiselect
    >
  </div>
</template>

<script>
// import TabWithPaginate from "./components/TabWithPaginate.vue";
// import EditableSelect from "./components/EditableSelect.vue";
import EditableDropbox from "./components/EditableDropbox.vue";
import Multiselect from "vue-multiselect";
export default {
  name: "App",
  components: {
    // TabWithPaginate,
    // EditableSelect,
    EditableDropbox,
    Multiselect,
  },
  data() {
    return {
      value: null,
      options: ["list", "of", "options"],
      list: [
        { value: "r", id: 0 },
        { value: "france", id: 1 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "dd", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "itaeelie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
        { value: "italie", id: 2 },
      ],
      chooseOption: "",
      optionId: "",
      test: "",
      test2: "",
      array: [
        { test: "test", test2: "tests3", name: 1 },
        { test: "test", test2: "tests2", name: 2 },
        { test: "test1", test2: "tests2", name: 3 },
        { test: "test", test2: "tests", name: 4 },
      ],
      filter: [
        {
          test: "test1",
        },
        { test2: "tests3" },
      ],
      arrayToShow: [],
      filterList: [],
      filterArray: [],
    };
  },
  mounted() {
    this.arrayToShow = Array.from(this.array);
    this.filterArticles(this.array, this.filter);
    console.log(this.filterArray, "filter array");
  },
  methods: {
    cli(e) {
      console.log(e.target);
    },
    filterArticles(array, filter) {
      let keys = Object.keys(array[0]);
      console.log(keys);
      filter.forEach((el) => {
        array.forEach((element) => {
          keys.forEach((key) => {
            if (element[key] === el[key]) {
              this.filterArray.push(element);
            }
          });
        });
      });
    },
    updateArray(payload) {
      console.log(payload, "in  app");
      this.list = payload;
      console.log(this.listToShow, " list to show in app");
    },
    choosenOption(payload) {
      this.chooseOption = payload.value;
      this.optionId = payload.id;
    },
    inputFilterList(e) {
      let selectField = e.target.id;
      let fieldValue = e.target.value;
      let obj = {};
      obj[selectField] = fieldValue;

      this.filterList.push(obj);
      let t = Array.from(new Set(this.filterList));
      this.filteredArrayToShow(t);
    },
    filteredArrayToShow(filterList) {
      let a = Array.from(this.array);
      console.log(a);
      filterList.forEach((el) => {
        a.filter((element) => element[Object.key(el)] === Object.key(el));
      });
    },
  },
  computed: {
    listToShow() {
      if (this.chooseOption !== "") {
        console.log("titi");
        return this.list.filter((el) => el.value === this.chooseOption);
      } else {
        console.log("toto");
        return this.list;
      }
    },
  },
};
</script>
