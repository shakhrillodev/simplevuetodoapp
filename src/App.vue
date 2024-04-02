<script setup>
import { ref } from 'vue';
const modal = ref(false);
const newData = ref("");
const notes = ref([]);
function addNewData(){
  if(newData.value.length<10){
    return 
  }
  notes.value = [...notes.value, {
    id: Math.random()*100000,
    text: newData.value,
    time: (new Date()).toLocaleDateString('en-US'),
    bg: "hsl(" + Math.random() * 360 + ", 100%, 75%)"
  }]
  newData.value = ""
  modal.value = false
}
</script>

<template>
  <main>
    <div v-if="modal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newData" name="data" id="nono" cols="30" rows="10"></textarea>
        <button @click="addNewData">Add Item</button>
        <button @click="modal=false" class="close">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>ToDo APP</h1>
        <button @click="modal=true">+</button>
      </header>
      <div class="todo-list">
        <div v-for="note in notes" class="todo-item" key="note.id" :style="{backgroundColor: note.bg}">
          <p>{{ note.text }}</p>
          <div class="date">{{note.time}}</div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  .overlay{
    position: absolute;
    z-index: 20;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .modal{
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 10px;
    border-radius: 10px;
    background: white;
  }
  .modal textarea{
    resize: none;
  }
  .modal button{
    background: blue;
    color: white;
    outline: none;
    border: none;
    padding: 10px;
    border-radius: 10px;
  }
  .modal .close{
    background: red;
  }
  main{
    width: 100%;
    height: 100vh;
  }
  .container{
    max-width: 1100px;
    padding: 10px;
    margin: 0px auto;
  }
  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .todo-list{
    margin-top: 30px;
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }
  .todo-item{
    width: 200px;
    height: 200px;
    background: green;
    padding: 10px;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between
  }
</style>