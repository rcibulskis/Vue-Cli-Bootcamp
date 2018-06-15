<template>
    
  <b-dropdown id="ddown1" class="m-md-2" :text="headertext">
    <div v-for="(gaming, key) in navbar" :key="gaming">
    <b-dropdown-item :href="navbar[key]" v-text="key" target="_blank">
      <a :href="navbar[key]" v-text="key" target="_blank"></a>
    </b-dropdown-item>
    </div>
  </b-dropdown>
   
</template>

<script>
export default {
  name: 'dropdown',
  props: [
    'navbar',
    'subreddits',
    'headertext'
  ]
}
</script>

<style>

</style>
