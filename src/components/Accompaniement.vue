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
            default: 'Frites'
        }
    },
    methods: {
        sendData() {
            this.$emit('accompaniement-of-the-user', { accompaniement: this.name });
        }
    }
}
</script>

<style lang="scss" scoped>

</style>