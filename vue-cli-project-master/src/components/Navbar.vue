<template>
    <nav>
  <slot name="buttons"></slot>
    </nav>
</template>

<script>
export default {
  name: 'my-nav',
  props: [
    'navbar',
    'subreddits',
    'headertext'
  ]
}
</script>

<style>

</style>
