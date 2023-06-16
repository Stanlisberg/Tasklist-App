<template>
<!-- <div v-if='showModal' ref='modalRef' class='modal-background'>
  <div class='modal'>
    <div class='modal-wrapper'>
      <p>Are you sure you want to delete this task?</p>
      <div class='btn-div'>
        <button @click='deleteTask(task.id)' class='btn-1'>Delete</button>
        <button @click='displayModal' class='btn-2'>Cancel</button>
      </div>
    </div>
  </div>
</div> -->
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
    <font-awesome-icon icon="fa-regular fa-trash-can" size="xl" color='crimson' @click='displayModal' class='logo'/>
      <div v-if='showModal' ref='modalRef' class='modal-background'>
      <div class='modal'>
        <div class='modal-wrapper'>
          <p>Are you sure you want to delete this task?</p>
          <div class='btn-div'>
            <button @click='deleteTask(task.id)' class='btn-1'>Delete</button>
            <button @click='displayModal' class='btn-2'>Cancel</button>
          </div>
        </div>
      </div>
      </div>

  </div>
</template>

<script>
import { ref } from 'vue'
export default {
    setup() {
       const showModal = ref(false)
       const modalRef = ref()

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

        const displayModal = () => {
          showModal.value = !showModal.value
          // modalRef.value.classList.add("active");
          // taskInfo.value = taskInfo.value.filter(item => ( 
          //    item.id !== data
          // ))
        }

        const deleteTask = (data) => {
            taskInfo.value = taskInfo.value.filter(item => ( 
             item.id !== data
            ))
        }

        return {taskInfo, displayModal, deleteTask, showModal, modalRef }
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

.modal-background {
  background:  rgba(0,0,0,.1);
  height: 100%;
  width: 100%;
  top:0;
  left: 0;
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  padding: 30px 45px;
  background-color: #fff;
  border-radius: 24px;
  box-shadow: 0 6px 58px rgba(121,145,173,.196);
  width: 40%;
  display: flex;
  justify-content: center;
}

.modal-wrapper {
   border: 1px solid blue;
   width: 250px;
}

.modal-wrapper p {
  font-size: 22px;
  font-weight: 600;
  line-height: 1.5;
  margin: 0 auto 40px auto;
  color: #000;
  text-align: center;
}

.btn-div {
  justify-content: center;
  display: flex;
}

.btn-1 {
  margin-right: 10px;
  padding: 13px 30px;
  background: rgb(113, 63, 255);
  box-shadow: 0 1px 2px rgba(184,200,224,.222);
  color: #fff;
  font-weight: 400;
  font-size: 17px;
}

.btn-2 {
  margin-left: 10px;
  padding: 13px 30px;
  color: #7d8592;
  background: #fff;
  border: 1px solid #d8e0f0;
  box-shadow: 0 1px 2px rgba(184,200,224,.222);
  font-weight: 400;
  font-size: 17px
}

/* -------media query----------- */

@media(width <= 605px) {
 .modal {
    width: 90%;
    margin: -50px auto 0 auto;
  }
}
</style>