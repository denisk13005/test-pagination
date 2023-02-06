<template>
  <div @click="closeOptions">
    <input type="text" v-model="searchValue" @click="showOptions = true"/>
    <ul v-if="showOptions">
      <li v-for="option in filteredOptions" @click="selectOption(option)" :key="option">
        {{ option }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: ['Apple', 'Banana', 'Cherry', 'Date', 'Elderberry'],
      selectedOption: '',
      searchValue: '',
      showOptions: false,
    };
  },
  computed: {
    filteredOptions() {
      return this.options.filter((option) => option.toLowerCase().includes(this.searchValue.toLowerCase()));
    },
  },
  methods: {
    selectOption(option) {
      this.selectedOption = option;
      this.searchValue = option;
      this.showOptions = false;
    },
    closeOptions() {
      this.showOptions = false;
    },
  },
};
</script>
