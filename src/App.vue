<script setup>
import { ref, reactive } from "vue";
import Modal from "./components/Modal.vue";
import DeleteTask from "./components/DeleteModal.vue";
const deleteShow = ref(false);
const modalShow = ref(false);
const taskIndex = ref();
const tasks = ref([
  { name: "Task 1", time: 60 },
  { name: "Task 2", time: 75 },
])
function removeTask(){
  tasks.value.splice(taskIndex.value, 1);
  deleteShow.value = false;
}
function dataPush(taskData){
  console.log(taskData);
  tasks.value.push({
    name: taskData.value.name,
    time: taskData.value.time,
  });
  modalShow.value = false;
}
function taskDelete(dataIndex){
  taskIndex.value = dataIndex;
  deleteShow.value = true;
}
</script>
<template>
  
  <section class="bg-white p-4 rounded shadow-md">
    <div class="flex flex-col">
      <h1 class="text-2xl font-semibold"> Assignment 1</h1>
      <h2 class="mt-2 text-lg font-bold pt-4">Task List</h2>
      <div class="w-96 m-auto mt-8 flex flex-col items-start">
        <!-- Use the Modal here -->
        
        <div class="flex flex-col mt-2 w-full gap-2">
          <div class="task-container" v-for="(task, index) in tasks" :key="index">
            <div class="task flex justify-between items-center border-b-2 pb-2 mb-2">
                <span class="text-lg">{{ task.name }} - {{ task.time }} mins</span>
                <button @click="removeTask(index)" class="text-red-500 rounded">Remove</button>
            </div>
        </div>
          <h3 v-show="tasks.length<=0" class="text-start mt-2">No task today. Add a new task</h3>
        </div>
      </div>
    </div>
    <button @click="modalShow = true" class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-700">Add Task</button>
  </section>
  <Modal v-show="modalShow" @modal-show="modalShow = false" @get-data="dataPush" />
  <DeleteTask v-show="deleteShow" @modal-hide="deleteShow = false" @delete-item="removeTask" />
</template>

<style scoped>
</style>