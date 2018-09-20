<template>
  <div class="white elevation-2">
    <v-toolbar flat dark dense color="primary">
      <v-toolbar-title>{{title}}</v-toolbar-title>
        <slot name="action">
        </slot>
      </v-toolbar>

      <div class="pr-4 pl-4">
        <slot>
          No slot content defined
        </slot>
      </div>
  </div>
</template>
<script>
export default {
  props: [
    'title'
  ]
}
</script>
<style scoped>

</style>
