<template>
  <div class="employee-form">
    <form @submit.prevent="handleSubmit">
      <b-form-group class="employee-form employee-form__name">
        <b-form-input
          class="input"
          v-model="employee.name"
          type="text"
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>
      <b-form-group class="employee-form employee-form__email">
        <b-form-input
          class="input"
          v-model="employee.email"
          type="email"
          placeholder="Enter email"
        ></b-form-input>
        <div v-show="validateFields" class="employee-form__text">
          Please fill out all required fields
        </div>
      </b-form-group>
      <b-button class="employee-form__btn" type="submit" variant="success">Add Employee</b-button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'employee-form',
  props: {
    validateFields: {
      type: Boolean,
      default: () => false,
    },
  },
  data() {
    return {
      employee: {
        name: '',
        email: '',
      },
    };
  },
  methods: {
    handleSubmit() {
      if (this.employee.name === '' || this.employee.email === '') {
        this.$emit('update:validateFields', true);
      } else {
        this.$emit('update:validateFields', false);
        this.$emit('submitHandle', this.employee);
      }
    },
  },
};
</script>

<style scoped lang="scss">
  @import "src/assets/scss/variables";
  .employee-form {
    &__email {
      position: relative;
    }
    &__btn {
      margin-top: 5px;
    }
    &__text {
      height: 20px;
      color: $validationColor;
      position: absolute;
      font-size: 12px;
    }
  }
</style>
