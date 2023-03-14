<template>
  <div class="dropdown">
    <input
      @blur="closeDropdown"
      tabindex="0"
      ref="dropdown"
      @click="toggleDropdown"
      class="input"
      type="text"
      v-model="selectedOption"
      :disabled="notEditable"
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
    <i class="icon icon-arrow-down"></i>
  </div>
</template>

<script>
export default {
  props: ["options", "notEditable"],
  created() {
    console.log(this.notEditable, "disabled");
  },
  data() {
    return {
      open: false,
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
    toggleDropdown() {
      this.open = !this.open;
    },
    closeDropdown() {
      this.open = false;
    },
    selectOption(payload) {
      console.log(payload, "payload");
      this.$emit("getField");
      this.selectedOption = payload;
      this.$emit("setValue", payload);
      console.log(this.selectedOption);
    },
  },
  watch: {
    // disabled(value) {
    //   this.notEditable = value;
    // },
  },
};
</script>
<style>
.dropdown {
  width: 150px;
  position: relative;
}

.input {
  height: 30px;
  position: absolute;
  left: 0;
  top: 10px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.input[disabled] {
  background: lightgray;
  cursor: not-allowed;
}
.icon {
  position: absolute;
  right: 10px;
  top: 20px;
  font-size: 11px;
  width: max-content;
}

.option {
  height: 25px;
  color: black;
  cursor: pointer;
  border: 1px solid #00205b;
  display: flex;
  align-items: center;
  justify-content: start;
}
.option:hover {
  background: #00205b;
  color: white;
  border: 1px solid white;
}
.options {
  overflow: hidden;
  transition: max-height 100ms;
  position: absolute;
  top: 45px;
  z-index: 200;
  width: 100%;
  color: white;
  max-height: 80px;
  overflow: auto;
  background: white;
}
</style>
