<template>
  <div class="employee-form">
    <form @submit.prevent="handleSubmit">
      <b-form-group class="employee-form employee-form__name">
        <b-form-input
          class="input"
          v-model="employee.name"
          type="text"
          placeholder="Enter name"
          @focus="clearStatus"
          ref="first"
        ></b-form-input>
      </b-form-group>
      <b-form-group class="employee-form employee-form__email">
        <b-form-input
          class="input"
          v-model="employee.email"
          type="email"
          @focus="clearStatus"
          placeholder="Enter email"
        ></b-form-input>
        <div v-show="validateFields" class="employee-form__text employee-form__text_error">
          Please fill out all required fields
        </div>
        <div v-show="sendForm" class="employee-form__text employee-form__text_success">
          Employee successfully added
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
    sendForm: {
      type: Boolean,
      default: () => false,
    },
    itemsLenght: {
      type: Number,
      default: () => '',
    },
  },
  data() {
    return {
      employee: {
        id: this.itemsLenght + 1,
        name: '',
        email: '',
      },
      success: false,
    };
  },
  methods: {
    handleSubmit() {
      const data = { ...this.employee };
      if (data.name === '' || data.email === '') {
        this.$emit('update:validateFields', true);
      } else {
        this.$emit('update:validateFields', false);
        this.$emit('submitHandle', data);
        this.clearFields();
      }
    },
    clearFields() {
      this.employee.name = '';
      this.employee.email = '';
      this.$refs.first.focus();
    },
    clearStatus() {
      this.success = false;
    },
  },
  beforeMount() {
    this.$nextTick(() => {
      this.$refs.first.focus();
    });
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
      position: absolute;
      font-size: 12px;
      &_error {
        color: $validationColor;
      }
      &_success {
        color: $buttonColor;
      }
    }
  }
</style>
