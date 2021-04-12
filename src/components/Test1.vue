<template>
  <div>
    <h4>{{ todo }}</h4>
    <p>
      {{ user.name }}
      {{ user.age }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'Test1',
  inject: ['todo', 'user']
}
</script>

<style scoped>

</style>
