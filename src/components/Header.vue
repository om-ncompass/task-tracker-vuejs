<template>
  <header>
    <h1>{{ title }}</h1>
    <Button 
      v-show="isHomePage"
      :text="display ? 'Close' : 'Add Task'"
      :color="display ? 'red' : 'green'"
      @click="$emit('toggle-form')"
    />
  </header>
</template>

<script>
import Button from './Atoms/Button.vue'

export default {
  name: 'Header',
  props: {
    title: String,
    display: Boolean
  },
  components: {
    Button
  },
  computed: {
    isHomePage() {
      if(this.$route.path === '/') {
        return true;
      } else {
        return false;
      }
    }
  },
  emits: ['toggle-form']
}
</script>

<style scoped>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }
</style>