<script setup>
import Card from "@/components/Card/index.vue";
import Textinput from "@/components/Textinput/index.vue";
import Button from "@/components/Button/index.vue";
import Icon from "@/components/Icon/index.vue"
import { ref, onMounted,watch } from "vue";

const toDOListArray = ref([]);
const task = ref("");
const addTask = () => {
  if (task.value.trim() !== '') {
    toDOListArray.value.push({
      text: task.value,
      completed: false,
    });
    task.value = '';
  }
  localStorage.setItem('toDOList' ,JSON.stringify(toDOListArray.value))
};
function deleteTask(index) {
  toDOListArray.value.splice(index, 1);
}
onMounted(()=>{
  let rr = JSON.parse(localStorage.getItem('toDOList'))
  if(rr)
  toDOListArray.value = rr
})
watch(toDOListArray, () => {
  localStorage.setItem('toDOList' ,JSON.stringify(toDOListArray.value))
},
  { deep: true }
)
</script>

<template>
  <Card className="sm:bg-[#a6b9f7] w-2/4 mx-auto rounded-xl mt-6 p-20">
    <div class="grid grid-cols-12">
      <div class="col-span-10 my-auto">
        <Textinput
          type="text"
          classInput="indent-4 w-3/4 text-xl"
          classLabel="text-lg font-bold my-auto"
          horizontal
          v-model="task" placeholder="Enter a new task" @keyup.enter="addTask" 
        />
      </div>
      <div class="col-span-2">
        <Button btnClass="bg-[#2c465f] text-white px-5 h-11 rounded-lg w-10/12 items-center font-bold text-xl" @click="addTask(),task = ''">
          ADD
        </Button>
      </div>
    </div>
    <ul>
      <li v-for="(task, index) in toDOListArray" :key="index" class="break-all flex  mx-auto h-10 mt-6 w-11/12 items-center text-xl">
       <div class="flex gap-x-5 mt-20 border-b border-slate-500 pb-2 w-full justify-between px-3">
        
        <input type="checkbox" v-model="task.completed" class="w-6"/>
        <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }" class="text-[#1E2933]"> 
          {{ task.text }}
        </span>
        <Icon icon="ic:outline-delete"  @click="deleteTask(index)" class="cursor-pointer"/>
        </div>
      </li>
    </ul>
  </Card>
</template>

