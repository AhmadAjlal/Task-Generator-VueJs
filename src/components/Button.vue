<template>
  <button :style="{background: color}" class="btn" @click="onClick()">{{ btnName }}</button>
</template>

<script>
export default {
  name: "ButtonComponent",
  props: {
    btnName: String,
    color: String,
  },
  methods: {
    onClick() {
      this.$emit('btn-click')
    }
  },
}
</script>

<style scoped>

</style>