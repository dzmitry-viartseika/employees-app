<template>
  <div id="app" class="app-container">
    <h1 class="app__title">Employees</h1>
    <employee-form @submitHandle="submitHandle"
                   :validateFields.sync="validateFields"
                   :sendForm.sync="sendForm"
                   :itemsLenght="itemsLenght"
    />
    <employee-table :items="items"
                    @deleteItem="deleteItem"
    />
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
    items: [],
    validateFields: false,
    sendForm: false,
  }),
  computed: {
    itemsLenght() {
      return this.items.length;
    },
  },
  methods: {
    submitHandle(data) {
      this.sendForm = true;
      setTimeout(() => {
        this.sendForm = false;
      }, 2000);
      this.items = [...this.items, data];
      localStorage.setItem('employees', JSON.stringify(this.items));
    },
    deleteItem(id) {
      this.items = this.items.filter(
        (employee) => employee.id !== id,
      );
      localStorage.setItem('employees', JSON.stringify(this.items));
    },
  },
  beforeMount() {
    const items = JSON.parse(localStorage.getItem('employees'));
    if (items === null) {
      this.items = [];
    } else this.items = items;
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
