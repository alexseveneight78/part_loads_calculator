<template>
  <div>
    <h3>ROAD TRANPSORT : Calculator of cargo space for part loads</h3>
    <app-table></app-table>
  </div>
</template>

<script>
import Table from './content/Table.vue';
export default {
  name: 'app',
  data () {
    return {
      
    }
  },
  components: {
    'app-table': Table
  }
}
</script>

<style lang="scss">
#app {
  margin: 50px auto;
}
h3 {
  text-align: center;
}

</style>
