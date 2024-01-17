<script setup>
import { ref } from "vue"

const tasks= ref([
  {name:'Task 1',time:'60' },
  {name:'Task 2',time:'75'},
  {name:'Task 3',time:'75'},  

]);

const taskName = ref('');
const taskTime=ref('');

function addNewTask(){
  console.log("Hello");

  if(taskName.value ==''){
    alert("please enter your task name");
    //taskName.value.focus();
    
  }else if(taskTime.value ==''){
    alert("please enter your task time");
  }
  else{
    console.log(taskName.value);
    const newTask={
    name: taskName.value,
    time: taskTime.value,
    } 
    tasks.value.push(newTask);  
    taskName.value='';
    taskTime.value='';
  }


}

function DeleteTask(id){
  //console.log(id);
  this.tasks.splice(id, 1);
}

const isShowModal = ref(false)

function showModal () {
  isShowModal.value = true
}
</script>
<template>
  <section class="container mx-auto flex items-center flex-col">
    <h1 class="text-center text-2xl py-10">Task List</h1>

    <!-- <p v-for="task in tasks" :key="task.id">{{ task.name }}</p> -->
    <div class="container mx-auto flex space-x-5 justify-center m-5" v-for="(task,index) in tasks" :key="index" >
      <p> Task Name : {{ task.name }}
          Time : {{ task.time }}
          <button @click="DeleteTask(index)" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" >
            Delete
          </button>
      </p>
    </div>

    <div class="container mx-auto flex space-x-5 justify-center m-5">
      <button @click="showModal" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" >
        Add New Task
      </button>  
      <div v-if="isShowModal">
        
          <p><input type="text" v-model="taskName" class="border border-gray-500 bg-white p-5"  placeholder="Enter Your Task Name" value="" /></p>
          <p><input type="number" v-model="taskTime" class="border border-gray-500 bg-white p-5"  placeholder="Enter Your Task Time" value=""  /></p>
          <p><button @click="addNewTask()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" >
            Save Task
          </button></p>
            
        </div>
    </div>




  </section>
</template>
<style scoped></style>