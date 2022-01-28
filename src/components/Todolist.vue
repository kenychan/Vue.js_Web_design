<template>

<div v-for="(list,index) in todo[usernr_child_data].lists" :key="list.name" class ="window">
  <div class="topbar"><h2>{{list.name}} 
  <input class="delete" type='button' value='X' @click="showModal = true; listnum=index"   /></h2></div>
  <Modal_Sicherheit v-if="showModal" @close="showModal = false" />
  <ol :id="list.listID">
  <li v-for="item in list.items" :key="item.name">
  <Aufgabe :data="item.name" :check="item.done" />
  </li>
  </ol>
  <Inputbox :listnumber ="index" :usernr_childchild="usernr_child_data" />
</div>
</template>


<script>
import Aufgabe from '@/components/Aufgabe';
import Inputbox from '@/components/Input';
import Modal_Sicherheit from '@/components/Modal_Sicherheit';

export default {
  name: 'Todilist',
  props:['usernr_child'],
  components:{
    Aufgabe,
    Inputbox,
    Modal_Sicherheit
  },
  data(){
    return {
      todo: this.$parent.parentData,
      message:'',
      showModal : false,
      listnum : 0,
      usernr_child_data: this.usernr_child  //save props to data
    }
  },
  methods:{
  taskid : function(){
    let listarr = new Array();
    this.todo[this.usernr_child_data].lists.forEach(element => element.items.forEach(item => listarr.push(item.taskID)));
    //https://stackoverflow.com/questions/6979276/select-random-value-not-in-array
    let list2 = new Array();
    for(let i=1; i<201; i++){
      if(!listarr.includes(i)){
      list2.push(i);}
      }

      return list2[Math.floor(Math.random() * list2.length)];

  },
  deletelist : function(){
    this.todo[this.usernr_child_data].lists.splice(this.listnum,1);
        console.log("list number :"+this.listnum);

  }

  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Kanit:wght@500&display=swap');
h2{

  height : 30px;
  border-style: solid ;
  border-width: 4px;
  border-color: black;

  margin-left: 10px;
  margin-right: 30px;
  padding-left: 5px;
  padding-top:2px;

  font-family: 'Bree Serif', serif;
}

.delete {
  display: inline-block;
  margin-top:1px;
  margin-right:3px;
  padding-bottom:3px;
  padding-top:3px;
  padding-left:7px;
  font-family: 'Kanit', sans-serif;
  float:right;
  width:26px;
  background-color: #333333;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}
.delete:hover{
  background-color: #999999;

}

</style>
