<template>
  <div class="employee-table">
    <b-table striped hover :items="items" :fields="fields"></b-table>
  </div>
</template>

<script>
export default {
  name: 'EmployeeTable',
  props: {
    items: {
      type: Array,
      default: () => [],
    },
    fields: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped lang="scss">
  @import "src/assets/scss/variables";
</style>
