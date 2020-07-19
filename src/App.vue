<template>
  <div id="app" class="app-container">
    <h1>Employees</h1>
    <employee-form @submitHandle="submitHandle" :validateFields.sync="validateFields" />
    <employee-table :items="items" :fields="fields" />
  </div>
</template>

<script>
import EmployeeForm from './components/EmployeeForm.vue';
import EmployeeTable from './components/EmployeeTable.vue';

export default {
  name: 'App',
  components: {
    EmployeeTable,
    EmployeeForm,
  },
  data: () => ({
    items: [
      {
        name: 'Richard Hendricks',
        email: 'richard@piedpiper.com',
      },
      {
        name: 'Bertram Gilfoyle',
        email: 'gilfoyle@piedpiper.com',
      },
      {
        name: 'Dinesh Chugtai',
        email: 'dinesh@piedpiper.com',
      },
    ],
    fields: ['name', 'email'],
    validateFields: false,
  }),
  methods: {
    submitHandle(data) {
      console.log('test', data);
    },
  },
};
</script>

<style lang="scss">
  @import "src/assets/scss/style";
  button {
    background: $buttonColor;
    border: 1px solid $buttonColor;
  }
</style>
