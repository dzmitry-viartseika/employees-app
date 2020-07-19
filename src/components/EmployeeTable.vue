<template>
  <div class="employee-table">
    <p v-if="!items.length" class="empty-table">
      No employees
    </p>
    <table v-else class="employee-table__table">
      <tbody>
      <tr v-for="employee in items" :key="employee.id">
        <td v-if="editing === employee.id">
          <b-form-input
            class="input"
            v-model="employee.name"
            type="text"
          ></b-form-input>
        </td>
        <td v-else>
          {{ employee.name }}
        </td>
        <td v-if="editing === employee.id">
          <b-form-input
            class="input"
            v-model="employee.email"
            type="text"
          ></b-form-input>
        </td>
        <td v-else>
          {{ employee.email }}
        </td>
        <td v-if="editing === employee.id"
            class="employee-table__table-btn"
        >
          <b-button class="employee-form__btn"
                    type="submit"
                    variant="success"
                    @click="editEmployee(employee)"
          >
            Save
          </b-button>
          <b-button class="employee-form__btn"
                    type="submit"
                    variant="outline-success"
                    @click="editing = null"
          >
            Cancel
          </b-button>
        </td>
        <td v-else
            class="employee-table__table-btn"
        >
          <b-button class="employee-form__btn"
                    type="submit"
                    variant="success"
                    @click="editMode(employee.id)"
          >
            Edit
          </b-button>
          <b-button class="employee-form__btn"
                    type="submit"
                    variant="success"
                    @click="deleteItem(employee.id)"
          >Delete</b-button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'EmployeeTable',
  data: () => ({
    editing: null,
  }),
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
  methods: {
    editMode(id) {
      this.editing = id;
    },
    deleteItem(id) {
      this.$emit('deleteItem', id);
    },
    editEmployee(employee) {
      if (employee.name === '' || employee.email === '') return false;
      this.$emit('edit:employee', employee.id, employee);
      this.editing = null;
      localStorage.setItem('employees', JSON.stringify(this.items));
      return true;
    },
  },
};
</script>

<style scoped lang="scss">
  @import "src/assets/scss/variables";
  .employee-table {
    margin-top: calc(1rem + 5px);
    td {
      border: 1px solid rgba($color-black, .3);
      width: 33%;
      padding: 10px;
    }
    &__table {
      width: 100%;
      &-btn {
        display: flex;
        justify-content: space-between;
        width: 100% !important;
      }
    }
  }
</style>
