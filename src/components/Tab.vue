<template>
  <div v-show="isActive" class="tabs-detail__wrapper">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    props: {
      name: { required: true },
      selected: { default: false }
    },
    data: () => {
      return {
        isActive: false
      }
    },
    mounted() {
      this.isActive = this.selected;
    }
  }
</script>

<style lang="scss">
.tabs-detail {
  &__wrapper {
    > :first-child {
      margin-top: 0;
      padding-top: 0;
    }

    > * {
      margin-bottom: 0;
    }

    > * + * {
      margin-top: 1em;
    }
  }
}
</style>