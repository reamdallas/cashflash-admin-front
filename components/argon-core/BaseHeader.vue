<template>
  <div
    class="header"
    :class="{[`bg-${type}`]: type}"
  >
    <div class="container-fluid">
      <div class="header-body">
        <slot />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'BaseHeader',
  props: {
    type: {
      type: String,
      default: 'transparent',
      description: 'Header background type',
    },
  },
};
</script>
<style>
</style>
