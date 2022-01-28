<template>

<div class="click">
  <input type='text' v-model="message" />
  <input type='button' id="addbtm" value='ADD' v-on:click="add" />

</div>

</template>


<script>
export default {
  name: 'Inputbox',
  props:['listnumber','usernr_childchild'],
  data(){
    return {
      message:'',
      todo: this.$parent.todo
    }
  },
  methods: {
  //https://stackoverflow.com/questions/43672010/how-to-passing-props-id-into-methods-in-vue-js

    add: function(){
    let num = this.$parent.taskid();
    this.todo[this.usernr_childchild].lists[this.listnumber].items.push({name: this.message, taskID: num, done: false});
    this.message ='';
    }
    //https://stackoverflow.com/questions/40707738/vuejs-accessing-a-method-from-another-method
    }


};
</script>

<style scoped>
#addbtm {
  display: inline-block;
  font-family: 'Bree Serif', serif;
  width:35%;
  background-color: #333333;
  color: white;
  margin-left:7%;
  padding: 5px 10px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}
#addbtm:hover{
  background-color: grey;

}
</style>
