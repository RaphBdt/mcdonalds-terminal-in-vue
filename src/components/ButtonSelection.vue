<template>
  <div class="btn">
      {{ title }}
  </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            default: 'Title'
        }
    }
}
</script>

<style lang="scss" scoped>
    .btn {
        width: 200px;
        height: 125px;
        display: flex;
        justify-content: center;
        align-items: center;
        box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
        color: #333333;
    }
</style>