<template>
<transition name="modal">
  <div class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container">

        <div class="modal-header">
          <h3><slot name="header">
            New List
          </slot></h3>
        </div>

        <div class="modal-body">

          <div class="listname">List Name:</div> <input type="text" v-model="message" >
        </div>

        <div class="modal-footer">
            <div class="listname">List Item:</div> <input type="text" v-model="message2">

        <div id = "buttonline">
          <button class="cancel" @click="$emit('close')">
            Cancel
          </button>

          <button class="submit" v-on:click="add" @click="$emit('close')">
            Submit
          </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</transition>

</template>

<script>
export default {
  name: 'Modal',
  props:['usernr'],
  data(){
  return{ message:'',
          message2:''}
    },

  methods: {

  listid : function(){
  let listarr = new Array();
  this.$parent.todolistdata[this.usernr].lists.forEach(element => listarr.push(element.listID));
  //https://stackoverflow.com/questions/6979276/select-random-value-not-in-array
  let list2 = new Array();
  for(let i=1; i<101; i++){
  if(!listarr.includes(i)){
  list2.push(i);}}

  return list2[Math.floor(Math.random() * list2.length)];

  },

    add: function(){
    let num = this.listid();
    this.$parent.todolistdata[this.usernr].lists.push({ name: this.message, listID: num , items: [{name:this.message2, done:false, taskID: 22}] });
    }
    //https://stackoverflow.com/questions/40707738/vuejs-accessing-a-method-from-another-method
    }
  }


</script>






<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Alfa+Slab+One&family=Bree+Serif&display=swap');

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0.5, 0, 0, 0.6);
  display: table;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  border-style: solid ;
  border-width: 4px;
  border-color: black;  width: 300px;
  border-radius: 35px;

  margin: 0px auto;
  padding: 10px 30px;
  background-color: #fff;
  font-family: 'Bree Serif', serif;

}

.modal-header{
font-size:20px;
font-family: 'Bree Serif', serif;
}

.listname{
  display:inline-block;
  vertical-align:middle;
  margin-top:8px;
}


.modal-body {
  margin: 1px 0;

}

.modal-footer{
  margin: 20px 0;
}

#buttonline{
    width:100%;
    text-align: center;
    margin-top:30px;
}

.cancel {
  display: inline-block;
  font-family: 'Georgia', serif;
  width: 47%;
  background-color: grey;
  color: white;
  padding: 5px 5px;
  margin-top:2%;
  margin-right:8%;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.cancel:hover{
  background-color: black;
}

.submit {
  display: inline-block;
  font-family: 'Georgia', serif;
  width: 45%;
  background-color: grey;
  color: white;
  padding: 5px 5px;
  margin-top:2%;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.submit:hover{
  background-color: black;

}

input[type=text], select {
  float: right;
  font-family: 'Bree Serif', serif;
  width: 70%;
  padding: 2px;
  text-align: center;
  border: 2px solid black;
  border-radius: 12px;
  box-sizing: border-box;
}




</style>
