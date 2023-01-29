<template>
  <div class="paginatein">
 <tr v-for="(el, index) in listesToShow" :key="index">
      <td>{{ el.value }}</td>
    </tr> 
  </div>
</template>

<script>
export default {
  props: {
    listesToShow: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
</style>