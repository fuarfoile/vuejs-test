<template>
  <table class="table">
    <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Age</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(user, index) in users" :key="index">
      <th scope="row">{{ index + 1 }}</th>
      <td>{{ user.name | toFirstUpperCase}}</td>
      <td>{{ user.email }}</td>
      <td>{{ user.age }}</td>
    </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "UserList",
  props: ['users'],
  filters: {
    toFirstUpperCase(value) {
      return value.charAt(0).toUpperCase() + value.slice(1);
    }
  }
}
</script>

<style scoped>

</style>