<template>
 <div>Dont be stupid</div>
  <div v-for='task in taskInfo' :key='task' class='card'>
    <div>
      <p class='para-up'>Task</p>
      <p class='para-title'>{{ task.title }}</p>
    </div>
    <div class='second-col'>
      <p class='para-up'>Priority</p>
      <p>{{ task.level }}</p>
    </div>
    <button>{{ task.label[0] }}</button>
    <font-awesome-icon icon="fa-regular fa-pen-to-square" size="xl" color='teal' class='logo'/>
    <font-awesome-icon icon="fa-regular fa-trash-can" size="xl" color='crimson' @click='clickButton(task.id)' class='logo'/>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
    setup() {

        const taskInfo = ref([
            { title: 'Go to gym', level: 'high', id:'1', label: ['todo', 'in progress', 'Done'] },
            { title: 'Read a book', level: 'low', id:'2', label: ['todo', 'in progress', 'Done'] },
            { title: 'Go to market', level: 'medium', id:'3', label: ['todo', 'in progress', 'Done']},
            { title: 'Do house chores', level: 'high', id:'4', label: ['todo', 'in progress', 'Done']},
            { title: 'Publish an article', level: 'medium', id:'5', label: ['todo', 'in progress', 'Done'] }
        ])


        // const arrayIndex = 0
        // const buttonArray = ref([ 'Todo', 'In Progress', 'Done'])
        // buttonArray.value = buttonArray.value[arrayIndex]
        // arrayIndex += 1

        const clickButton = (data) => {
          taskInfo.value = taskInfo.value.filter(item => ( 
             item.id !== data
          ))
        }

        return {taskInfo, clickButton }
    }

}
</script>

<style scoped>
.card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #ffffff;
  margin-top: 15px;
  border-radius: 25px;
  padding: 17px 20px;
}

.icon {
  color: green;
}

.para-up {
  color:#91929e;
}
.para-title{
  width: 140px;
  font-size: 17px;
  border: 1px solid red;
}

button {
  padding: 10px 15px;
  border-radius: 10px;
  border: none;
  color:#91929e;
  cursor: pointer;
  font-weight:700;
}

.logo {
  cursor:pointer;
}
</style>