<template>

<div class="topbar">
<Header title="Todo List" />
<span class="userid">Current UserID: {{usernumber}}</span>
<button class="show-modal" @click="showModal = true">Add List</button>
<button class="show-modal" @click="adduser">Add User</button>

</div>

<!--update user_id data-->
<button class="user_button" v-for="(user,index) in todolistdata" :key="user"  v-on:click="update(index)" >
User{{user.userID}}</button>


<!--updating data won't make DOM automatically update the props in Component attribute and rerender-->
<div v-for="(user,index) in todolistdata" :key="user" class="user">
<!--create multiple Modal, but only show the correct one, pay attention to the double conditon use-->
<Modal v-if="showModal==true&&usernumber==index" @close="showModal = false" :usernr="index" >
</Modal>
<!--create multiple Body according to the data lenght, and only show the body that == current usernumber. which is updated through fcuntion-->
<Body v-if="usernumber==index" :user="index" />

</div>




<Footer footer="This is a footer." />

</template>

<script>
import Header from './components/Header';
import Body from './components/Body';
import Footer from './components/Footer';
import static_todolistdata from './static_todolistdata.js';
import Modal from './components/Modal';


export default {
  name: 'App',
  components: {
    Header,
    Body,
    Footer,
    Modal
  },
  data() {
  return {todolistdata: static_todolistdata,
          showModal: false,
          usernumber : 0,
          }

  },


  methods: {
    adduser(){
    this.todolistdata.push({user: "default", userID: this.todolistdata.length,lists:[]});
    },
    update(index) {
      this.usernumber = index;


      //old method:
      //https://stackoverflow.com/questions/40957008/how-to-access-to-a-child-method-from-the-parent-in-vue-js
    },

  }
};
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Alfa+Slab+One&family=Bree+Serif&display=swap');
.example {
  display: flex;
  align-items: stretch;
  flex-wrap: wrap;
}

.window{
  flex: 19%;
  /* Make elements inside the container behave like table cells */

  border-style: solid ;
  border-width: 4px;
  border-color: black;

}

body {
  font-size: 12px;
  font-family: 'Georgia', serif;
  font-weight: 400;
  line-height: 1.45;
  color: #333;
  background: #ecf0f1;
  padding: 1em;

}

ol{

  border-style: solid ;
  border-width: 4px;
  border-color: black;

  margin-left: 10px;
  margin-right: 30px;
  padding-left: 18px;
  padding-bottom: 10px;
  padding-top: 10px;
  font-family: 'Bree Serif', serif;
}

.click{
  border-style: solid ;
  border-width: 4px;
  border-color: black;

  margin-left: 10px;
  margin-right: 30px;
  margin-bottom: 10px;
  padding-left: 5px;
  padding-top: 5px;
  padding-bottom: 5px;


}
h1 {
  display:inline-block;
  width:100px;
  font-size: 2em;
  font-family: 'Bree Serif', serif;
}


p {
  margin-bottom: 1.3em;
  text-align: justify;
}

input[type=text], select {
  font-family: 'Bree Serif', serif;
  width: 50%;
  padding: 5px;
  margin-left: 2%;
  margin-top: 2%;
  margin-bottom: 2%;

  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 20px;
  box-sizing: border-box;
}


li{
  list-style: none;
  padding: 2px;
}

span{
  margin-left: 5px;
  padding: 2px;

}

.userid{
ont-size: 2em;
bottom: 0px;
position:relative;
text-decoration: underline;
font-family: 'Bree Serif', serif;
}




footer{
  font-size: 2em;
  bottom: 0px;
  float: right;
  position:relative;
  text-decoration: underline;
}
@media screen and (max-width:1080px) {

  .window{
    flex:100%;

  }
}

.topbar{
white-space: nowrap;
overflow-x: auto;
overflow-y: hidden;
}

.show-modal {

  display: inline-block;
  float:right;
  margin-top:20px;
  margin-right:2px;
  font-family: 'Georgia', serif;
  width: 80px;
  background-color: #333333;
  color: white;
  padding: 5px 5px;

  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.show-modal:hover{
  background-color: black;
}

.user_button{
display: inline-block;
align:center;
margin-right:2px;
margin-bottom:14px;
font-family: 'Georgia', serif;
width: 60px;
background-color: #888888;
color: white;
padding: 5px 5px;

border: none;
border-radius: 10px;
cursor: pointer;
}

.user_button:hover{
background-color: black;

}


</style>
