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
            default: 'Eau'
        }
    },
    methods: {
        sendData() {
            this.$emit('drink-of-the-user', { drink: this.name });
        }
    }
}
</script>

<style lang="scss" scoped>

</style>