<template>
  <p>Register for the event here</p>
  <button @click="register">Register Me</button>
</template>

<script>
export default {
  props: ['event'],
  methods: {
    register() {
      // There should be a call to API
      this.$router.push({
        name: 'EventDetails'
        // params: { id: this.event.id } - do not need to do this
      })
    }
  }
}
</script>
