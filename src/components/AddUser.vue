<template>
  <div>
    <Error
        :errors="errors"
        :showError="showError"
    />
    <form
        @submit.prevent="addUser"
        novalidate="true"
    >
      <div class="row g-3">
        <div class="col-sm-5">
          <input type="text" v-model="name" class="form-control" placeholder="Ваше имя">
        </div>
        <div class="col-sm-5">
          <input type="email" v-model="email" class="form-control" placeholder="Ваш Email">
        </div>
        <div class="col-sm">
          <input @keypress="onlyNumber" type="text" v-model.number="age" class="form-control" placeholder="Ваш возраст">
        </div>
      </div>
      <br>
      <div class="col">
        <button :disabled="isDisabled" type="submit" class="btn btn-primary">Добавить пользователя</button>
      </div>

    </form>
  </div>

</template>

<script>
import Error from "@/components/Error";
export default {
  name: "AddUser",
  components: {Error},
  data() {
    return {
      errors: [],
      name: null,
      email: null,
      age: null,
      showError: false
    }
  },
  props: ['users'],
  methods: {
    addUser() {
      if(this.checkForm()) {
        this.users.push(
            {id: Date.now(), name: this.name, email: this.email, age: this.age}
        );
        this.showError = false;
        this.name = null;
        this.email = null;
        this.age = null;
      } else {
        this.showError = true;
      }
    },
    checkForm: function () {
      this.errors = [];

      if (!this.name) {
        //this.errors.push('Укажите имя');
        this.emptyField();
        return false;
      } else if (String(this.name).length > 20) {
        this.errors.push('Поле: имя. Длина имени не должна превышать 20 символов');
      }

      if (!this.email) {
        //this.errors.push('Укажите электронную почту');
        this.emptyField();
        return false;
      } else if (!this.validEmail(this.email)) {
        this.errors.push('Поле: email. Укажите корректный адрес электронной почты');
      }

      if (this.age == null || this.age === '') {
        //this.errors.push('Укажите возраст');
        this.emptyField();
        return false;
      } else if (Number.isNaN(Number(this.age)) || Number(this.age) < 0 || Number(this.age) > 999) {
        this.errors.push('Поле: возраст. Укажите корректный возраст');
      }

      if (!this.errors.length) {
        return true;
      }
    },
    emptyField() {
      this.errors = ['Не все поля заполнены']
    },
    validEmail: function (email) {
      let re = /.+@.+\..+/i;
      return re.test(email);
    },
    onlyNumber ($event) {
      let keyCode = $event.keyCode;
      if (keyCode < 48 || keyCode > 57) {
        $event.preventDefault();
      }
    }
  },
  computed: {
    isDisabled() {
      return this.showError && !this.checkForm();
    }
  }
}
</script>

<style scoped>

</style>