<template>
  <div class="about">
    <h1>This is an about page</h1>
    <input type="text" :value="name" @input="handleInput" />
    <h2>{{name}}</h2>
  </div>
</template>
<script>
export default {
  data () {
    return {
      name: ''
    }
  },
  methods: {
    handleInput (e) {
      this.name = e.target.value
    }
  }
}
</script>
<style lang="less" scoped>

</style>
