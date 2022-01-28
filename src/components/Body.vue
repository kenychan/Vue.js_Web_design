<template>
<div class="example">
<Todolist :usernr_child="user" />
</div>
</template>



<script>
import Todolist from '@/components/Todolist';


export default {
  name: 'Body',
  props:['user'],
  components:{
    Todolist
  },
  data(){
    return {
      parentData: this.$parent.todolistdata,
    }
  }


};
</script>
