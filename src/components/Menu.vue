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
            default: 'Best Of'
        },
        price: {
            type: Number,
            default: 0
        }
    },
    methods: {
        sendData() {
            this.$emit('menu-of-the-user', { menu: this.name, price: this.price });
        }
    }
}
</script>

<style lang="scss" scoped>

</style>