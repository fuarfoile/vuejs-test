<template>
  <div v-if="errors.length && showError" class="alert alert-danger" role="alert">
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Error",
  props: ['errors', 'showError'],
}
</script>

<style scoped>

</style>