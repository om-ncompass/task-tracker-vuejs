<template>
  <button
    :style="{ backgroundColor: color }"
    class="btn"
    @click="handleClick()"
   >{{ text }}</button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    text: String,
    color: String
  },
  methods: {
    handleClick() {
      console.log('Clicked')
    }
  }
}
</script>