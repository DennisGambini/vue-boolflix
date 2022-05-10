<template>
  <header>
        <h1>boolflix</h1>
        <app-search/>
  </header>
</template>

<script>
import AppSearch from './AppSearch.vue'
export default {
  components: { AppSearch },
    name: 'AppHeader'
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';

    header{
        padding: $section-pad;
        @include flex-row-between;
        h1{
            color: red;
            text-transform: uppercase;
           
        }
    }
</style>