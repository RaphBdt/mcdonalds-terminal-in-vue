<template>
  <div>
      <button @click="newOrder">
          Ajouter un menu
      </button>
  </div>
</template>

<script>
export default {
    props: {
        numberOfTheOrder: {
            type: Number,
            default: 0
        }
    },
    methods: {
        newOrder() {
            this.$emit('new-order');
        }
    }
}
</script>

<style scoped lang="scss">
    button {
        background-color: tomato;
        border: none;
        padding: 10px;
        margin: 30px auto;
        border-radius: 9px;
    }
</style>