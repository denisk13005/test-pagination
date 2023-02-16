<template>
  <!-- <div class="container">
    <input type="text" v-model="searchValue" @click="show" @blur="bluring" />
    <ul v-if="showOptions">
      <li
        v-for="option in filteredOptions"
        @click="selectOption(option)"
        :key="option"
      >
        {{ option }}
      </li>
    </ul>
  </div> -->
  <div class="dropdown">
    <input
      @blur="closeDropdown"
      tabindex="0"
      ref="dropdown"
      @click="toggleDropdown"
      class="select"
      type="text"
      @change="test"
      v-model="selectedOption"
    />

    <div class="options" :style="{ 'max-height': open ? '300px' : '0px' }">
      <div
        v-for="option in filteredOptions"
        @mousedown="selectOption(option)"
        class="option"
        :key="option"
      >
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      open: false,
      options: ["BMW", "Fiat", "Citroen", "Audi", "Tesla"],
      selectedOption: "",
      searchValue: "",
      showOptions: true,
    };
  },
  computed: {
    filteredOptions() {
      return this.options.filter((option) =>
        option.toLowerCase().includes(this.selectedOption.toLowerCase())
      );
    },
  },
  methods: {
    // bluring(e) {
    //   console.log(e, "ttttt");
    // },
    // show(e) {
    //   console.log(this.showOptions);
    //   this.showOptions = !this.showOptions;
    //   console.log(this.showOptions);
    //   console.log(e.target.parentElement, "el");
    // },
    // selectOption(option) {
    //   this.selectedOption = option;
    //   this.searchValue = option;
    //   this.showOptions = false;
    // },
    // closeOptions() {
    //   this.showOptions = false;
    // },
    test() {
      console.log(this.selectedOption, "so");
    },
    toggleDropdown() {
      this.open = !this.open;
    },
    closeDropdown() {
      this.open = false;
    },
    selectOption(option) {
      // this.$emit("input", option);
      this.selectedOption = option;
    },
  },
};
</script>
<style>
.dropdown {
  width: 200px;
  position: relative;
}

.select {
  height: 40px;
  position: absolute;
  left: 0;
  width: 100%;
  background: green;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  cursor: pointer;
}
.option {
  width: 100%;
  height: 40px;
  background: darkgreen;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.option:hover {
  background: green;
}
.options {
  overflow: hidden;
  transition: max-height 200ms;
}
</style>
