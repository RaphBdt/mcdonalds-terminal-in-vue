<template>
  <div @click="sendData()">
      <ButtonSelection :title="name" />
  </div>
</template>

<script>
import ButtonSelection from './ButtonSelection.vue'
export default {
  components: { ButtonSelection },
    props: {
        name: {
            type: String,
            default: 'Sur place'
        }
    },
    methods: {
        sendData() {
            this.$emit('place-of-the-user', { place: this.name });
        }
    }
}
</script>

<style lang="scss" scoped>

</style>