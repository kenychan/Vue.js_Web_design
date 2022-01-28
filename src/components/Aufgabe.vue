<template>
<input type="checkbox" v-model="ifcheck">
<span>{{data}}</span>
</template>


<script>
export default {
  name: 'Aufgabe',
  props:['data','check'],
  data() {
    return{ifcheck : this.check}
  }

  }




</script>
