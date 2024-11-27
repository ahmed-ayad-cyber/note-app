  <script>
import { ref } from 'vue';

  
  export default {
    name: 'App',
    components: {
  
    },
    setup (){
      const showModule =ref(false);
      const text = ref("")
      const notesArray = ref([])
      const theError = ref("")

      const toggleShowing = ()=> {
        showModule.value = true
      };
      const closeShowing = ()=> {
        showModule.value = false
      };
      const getRandomColor =()=> {
       return "hsl(" + Math.random() * 360 + ", 100%, 75%)"; 
      };

      const addingNote = ()=> {
        if (text.value.length <= 9){
          theError.value = "the note must be at least 10 characters"
          return ;
        }
        notesArray.value.push({
          theText:text.value,
          date:(new Date()).toLocaleDateString(),
          time:(new Date()).toLocaleTimeString(),
          id:Math.floor(Math.random() *1000),
          colorValue: getRandomColor()
        })
        text.value = ""
        showModule.value = false
      };
      return {showModule,toggleShowing, closeShowing ,addingNote, notesArray , text, getRandomColor, theError};
    }
  }
  </script>

<template>
  <div>
    <div class="over-lay" v-if="showModule">
      <div class="module"  >
        <textarea v-model="text" name="new-note" cols="50" rows="10" placeholder="add note"></textarea>
        <p v-if="theError" style="color: red;">{{ theError }}</p>
        <button @click="addingNote">add</button>
        <button @click="closeShowing">close</button>
      </div>
    </div>
    <div class="container">
      <h1>MY NOTES</h1>
      <button @click="toggleShowing">+</button>
    </div>
    <div class="card-container" >
      <div class="card" v-for=" note in notesArray" :key="note.id" :style="{backgroundColor:note.colorValue}">
        <p>{{ note.theText }}</p>
        <p class="date">{{ note.date }}  {{ note.time }}</p>
      </div>
    </div>
  </div>
</template>

<style>
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 auto;
  padding: 20px;
}
.container button {
  border: none;
  background-color: black;
  color: white;
  border-radius: 100%;
  padding: 10px 20px;
}
.card-container {
  background-color: antiquewhite;
  padding: 10px;
  display: flex;
  flex-wrap: wrap;
}
.card {
  width: 22.5%;
  height: 200px;
  background-color: green;
  border-radius: 10px;
  padding: 0 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 1%;
}
.date {
  font-size: 12px;
  font-weight: bold;
}
.over-lay {
  position: absolute;
  background-color: rgba(0, 0, 0, 0.274);
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items:center ;
}
.module {
  display: flex;
  flex-direction: column;
  background-color: white;
  padding: 2%;
  border-radius:15px ;
}
.module button {
  margin: 1%;
  border: none;
  color:red;
  padding: 5px;
  background-color: bisque;
}
body{
  margin: 0;
}
</style>
