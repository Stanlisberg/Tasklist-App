<template>
  <div ref="btnref1" class="container">
    <div class="wrapper">
      <div class="first-row">
        <h1 @click="doThis" ref="paraRef" class="head">Task List</h1>
        <button @click="displayUpdateModal"><span class="add">+</span> Add Task</button>
      </div>
      <div class="second-row">
        <div v-for="task in taskInfo" :key="task" class="card">
          <div v-if="showModal" class="modal-background">
            <div class="modal">
              <div class="modal-wrapper">
                <p>Are you sure you want to delete this task?</p>
                <div class="btn-div">
                  <button @click="deleteTask" class="btn-1">Delete</button>
                  <button @click="displayModal" class="btn-2">Cancel</button>
                </div>
              </div>
            </div>
          </div>

          <div v-if="showUpdateModal" class="update-background">
            <div class="update-modal">
              <div class="update-first">
                <p>Add Task</p>
                <font-awesome-icon
                  icon="xmark"
                  size="xl"
                  color="#000"
                  class="logo"
                  @click="displayUpdateModal()"
                />
              </div>
              <div class="update-second">
                <p>Task</p>
                <input
                  type="text"
                  class="input"
                  placeholder="Type your task here..."
                  v-model="inputValue"
                />
              </div>
              <div class="update-third">
                <p>Priority</p>
                <button @click="handleActiveButton(1)" :class="highActive()">High</button>
                <button @click="handleActiveButton(2)" :class="mediumActive()">Medium</button>
                <button @click="handleActiveButton(3)" :class="lowActive()">Low</button>
              </div>
              <div class="add-button-div">
                <button
                  @click="addTask"
                  ref="addUpdateRef"
                  :class="disableAdd()"
                  id="add-button-id"
                >
                  Add
                </button>
              </div>
            </div>
          </div>

          <div v-if="editModal" class="edit-background">
            <div class="edit-modal">
              <div class="update-first">
                <p>Edit Task</p>
                <font-awesome-icon
                  icon="xmark"
                  size="xl"
                  color="#000"
                  class="logo"
                  @click="showEditModal"
                />
              </div>
              <div class="update-second">
                <p>Task</p>
                <input
                  type="text"
                  class="input"
                  placeholder="Type your task here..."
                  v-model="editValue"
                />
              </div>
              <div class="update-third">
                <p>Priority</p>
                <button ref="handleButtonRef" @click="handleActiveButton(1)" :class="highActive()">
                  High
                </button>
                <button @click="handleActiveButton(2)" :class="mediumActive()">Medium</button>
                <button @click="handleActiveButton(3)" :class="lowActive()">Low</button>
              </div>
              <div class="add-button-div">
                <button @click="editTask" ref="addUpdateRef" class="add-button" id="add-button-id">
                  Edit
                </button>
              </div>
            </div>
          </div>

          <!-- <div class='hey'> -->
          <div class="card-wrapper">
            <div class="first-col">
              <p class="para-up">Task</p>
              <p class="para-title">{{ task.title }}</p>
            </div>
            <div class="second-col">
              <p class="para-up">Priority</p>
              <p :class="handleLevel(task)">{{ task.level }}</p>
            </div>
          </div>

          <button
            ref="buttonRef"
            id="progress-button"
            :class="changeProgress(task)"
            @click="changeProgressButton(task.label)"
          >
            {{ progressButton }}
          </button>
          <font-awesome-icon
            icon="fa-regular fa-pen-to-square"
            size="xl"
            color="rgb(10, 22, 41)"
            class="logo logo1"
            @click="showEditModal(task)"
          />
          <font-awesome-icon
            icon="fa-regular fa-trash-can"
            size="xl"
            color="crimson"
            @click="showDeleteModal(task)"
            class="logo logo2"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
export default {
  setup() {
    const showModal = ref(false)
    const taskToDelete = ref(null)
    const taskToEdit = ref(null)
    const showUpdateModal = ref(false)
    const editModal = ref(false)
    const activeButton = ref(null)
    const inputValue = ref()
    const editValue = ref()
    const addUpdateRef = ref()
    const addRef = ref()
    const removeRef = ref(false)
    const progressButton = ref()
    const handleButtonRef = ref()
    const paraRef = ref(null)
    const buttonRef = ref(null)
    const buttonValue = ref()

    const myButton = buttonRef

    const doThis = () => {
      if ((taskToEdit.value.level = 'High')) {
        console.log('hey')
      }
    }

    const taskInfo = ref([
      { title: 'Go to gym', level: 'High', id: '1', label: ['To Do', 'In Progress', 'Done'] },
      { title: 'Read a book', level: 'Low', id: '2', label: ['To Do', 'In Progress', 'Done'] },
      { title: 'Go to market', level: 'Medium', id: '3', label: ['To Do', 'In Progress', 'Done'] },
      { title: 'Do house chores', level: 'High', id: '4', label: ['To Do', 'In Progress', 'Done'] },
      {
        title: 'Publish an article',
        level: 'Low',
        id: '5',
        label: ['To Do', 'In Progress', 'Done']
      }
    ])

    // const arrayIndex = 0
    // const buttonArray = ref([ 'Todo', 'In Progress', 'Done'])
    // buttonArray.value = buttonArray.value[arrayIndex]
    // arrayIndex += 1

    //-----Display Delete  modal--------
    const displayModal = () => {
      showModal.value = !showModal.value
    }

    //-----Display Update  modal---------
    const displayUpdateModal = () => {
      showUpdateModal.value = !showUpdateModal.value

      console.log(taskInfo.value)
    }

    //--------Disable add button-------
    const disableAdd = () => {
      if (!inputValue.value) {
        return 'disable-add-button'
      } else {
        return 'add-button'
      }
    }

    //------individual button active & handle active button------

    const handleActiveButton = (id) => {
      activeButton.value = id
    }

    const highActive = () => {
      if (activeButton.value == 1) {
        return 'high-active'
      } else {
        return 'button-high'
      }
    }

    const mediumActive = () => {
      if (activeButton.value == 2) {
        return 'medium-active'
      } else {
        return 'button-medium'
      }
    }

    const lowActive = () => {
      if (activeButton.value == 3) {
        return 'low-active'
      } else {
        return 'button-low'
      }
    }

    //-------delete task--------
    const showDeleteModal = (task) => {
      showModal.value = !showModal.value
      taskToDelete.value = task
    }
    const deleteTask = () => {
      taskInfo.value = taskInfo.value.filter((item) => item.id !== taskToDelete.value.id)
      showModal.value = !showModal.value
    }

    //---------Add task-----------
    let newTask
    const addTask = () => {
      if (activeButton.value === 1) {
        addRef.value = 'High'
      } else if (activeButton.value === 2) {
        addRef.value = 'Medium'
      } else if (activeButton.value === 3) {
        addRef.value = 'Low'
      }

      newTask = {
        title: inputValue.value,
        level: addRef.value,
        id: generateUniqueId(),
        label: ['To Do', 'In Progress', 'Done']
      }

      taskInfo.value.push(newTask)
      showUpdateModal.value = !showUpdateModal.value
      inputValue.value = ''
    }

    //-----------Edit Task---------------
    const showEditModal = (editTask) => {
      editModal.value = !editModal.value
      taskToEdit.value = editTask
      editValue.value = taskToEdit.value.title

      if (taskToEdit.value.level === 'High') {
        handleActiveButton(1)
      } else if (taskToEdit.value.level === 'Medium') {
        handleActiveButton(2)
      } else if (taskToEdit.value.level === 'Low') {
        handleActiveButton(3)
      }
    }

    const editTask = () => {
      taskToEdit.value.title = editValue.value
      editModal.value = !editModal.value

      if (activeButton.value === 1) {
        taskToEdit.value.level = 'High'
      } else if (activeButton.value === 2) {
        taskToEdit.value.level = 'Medium'
      } else if (activeButton.value === 3) {
        taskToEdit.value.level = 'Low'
      }
    }

    //-------Generate unique Id-------------
    const generateUniqueId = () => {
      return Date.now()
    }

    //---------Change Progress----------
    const changeProgress = (task) => {
      progressButton.value = task.label[2]
    }

    // buttonValue.value = 'To Do'
    const changeProgressButton = (task) => {
      const testing = task
        .filter((data) => {
          if (progressButton.value === 'To Do') {
            return data === 'In Progress'
          } else if (progressButton.value === 'In Progress') {
            return data === 'Done'
          } else if (progressButton.value === 'Done') {
            return data === 'To Do'
          }
        })
        .map((item) => {
          // return item
          console.log(item)
          return (progressButton.value = item)
        })

      //  console.log(progressButton.value)
    }

    //--------- Level Test cholor-----------
    const handleLevel = (task) => {
      if (task.level === 'High') {
        return 'high-red'
      } else if (task.level === 'Medium') {
        return 'medium-yellow'
      } else if (task.level === 'Low') {
        return 'low-green'
      }
    }

    return {
      taskInfo,
      displayModal,
      handleButtonRef,
      paraRef,
      doThis,
      buttonRef,
      buttonValue,
      // progressValue,
      changeProgress,
      handleLevel,
      changeProgressButton,
      progressButton,
      deleteTask,
      showDeleteModal,
      taskToDelete,
      taskToEdit,
      removeRef,
      inputValue,
      editValue,
      addTask,
      newTask,
      addUpdateRef,
      disableAdd,
      displayUpdateModal,
      handleActiveButton,
      activeButton,
      showModal,
      showUpdateModal,
      showEditModal,
      editModal,
      editTask,
      highActive,
      mediumActive,
      lowActive
    }
  }
}
</script>

<style scoped>
/*-------Head Section-----------*/
.container {
  font-weight: normal;
  border: 1px solid black;
  min-height: 100vh;
}

.wrapper {
  max-width: 700px;
  margin: 30px auto;
  padding: 0 15px;
}

.first-row {
  display: flex;
  justify-content: space-between;
}

.first-row .head {
  font-size: 35px;
  font-weight: 700;
  margin: 15px 0;
}

.first-row button {
  padding: 12px 27px;
  margin: 20px 0;
  border-radius: 14px;
  font-size: 20px;
  font-weight: 600;
  border: none;
  background: rgb(113, 63, 255);
  color: #fff;
  box-shadow: rgba(113, 63, 255, 0.25) 0px 6px 12px;
}

.add {
  margin-right: 5px;
  font-weight: bold;
}

@media (width <= 605px) {
  .first-row .head {
    line-height: 1;
  }
  .first-row button {
    padding: 10px 25px;
  }
}

/*--------Card Section----------*/
.card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #ffffff;
  margin-top: 15px;
  border-radius: 25px;
  padding: 17px 20px;
}

.card-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.icon {
  color: green;
}

.para-up {
  color: #91929e;
}
.para-title {
  width: 220px;
  font-size: 17px;
}

.high-red {
  color: #f73446;
  font-weight: 700;
}

.medium-yellow {
  font-weight: 700;
  color: #ffbd21;
}

.low-green {
  font-weight: 700;
  color: #0ac947;
}

button {
  padding: 7px 15px;
  border-radius: 9px;
  border: none;
  color: #91929e;
  cursor: pointer;
  font-weight: 700;
}

.logo {
  cursor: pointer;
}

@media (width <= 600px) {
  .para-title {
    width: 160px;
    font-size: 16px;
  }

  .card {
    display: block;
  }

  #progress-button {
    margin-top: 50px;
  }

  .logo2 {
    margin-left: 8%;
  }

  .logo1 {
    margin-left: 8%;
  }
}

/*-----Delete Modal section---------*/
.modal-background {
  background: rgba(0, 0, 0, 0.2);
  height: 100%;
  width: 100%;
  top: 0;
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
  /* box-shadow: 0 6px 58px rgba(121,145,173,.196); */
  width: 40%;
  display: flex;
  justify-content: center;
}

.modal-wrapper {
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
  box-shadow: 0 1px 2px rgba(184, 200, 224, 0.222);
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
  box-shadow: 0 1px 2px rgba(184, 200, 224, 0.222);
  font-weight: 400;
  font-size: 17px;
}

@media (width <= 605px) {
  .modal {
    width: 90%;
    margin: -50px auto 0 auto;
  }
}

/*--------Update Modal Section---------*/
.update-background {
  background: rgba(0, 0, 0, 0.2);
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
}

.update-modal {
  padding: 30px 50px;
  background-color: #fff;
  border-radius: 24px;
  width: 40%;
  justify-content: center;
  border: 1px solid blue;
  line-height: 2;
}

.update-first {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.update-first p {
  font-size: 22px;
  font-weight: 700;
  color: #000;
}

.update-second p,
.update-third p {
  color: rgb(125, 133, 146);
  font-size: 14px;
  font-weight: 700;
}

.update-second input {
  padding: 18px 20px;
  border-radius: 15px;
  width: 100%;
  background: #fff;
  border: 1px solid #d8e0f0;
  font-size: 15px;
  outline: none;
  color: rgb(125, 133, 146);
  margin-top: 8px;
}

.input::placeholder {
  font-size: 15px;
}

.update-second input:focus {
  border: 1px solid #d8e0f0;
}

.update-second,
.update-third {
  margin-top: 10px;
}

.update-third button {
  padding: 13px 0 13px 0;
  width: 24%;
  text-align: center;
  margin-top: 8px;
}
.button-medium,
.button-low {
  margin-left: 10px;
}

.button-high {
  border: 1px solid #f73446;
  color: #f73446;
  background: #fff;
}

.button-medium {
  border: 1px solid #ffbd21;
  color: #ffbd21;
  background: #fff;
}

.button-low {
  color: rgb(10, 201, 71);
  border: 1px solid rgb(10, 201, 71);
  background: #fff;
}

.high-active {
  background: #f73446;
  color: #fff;
}

.medium-active {
  background: #ffbd21;
  color: #fff;
  margin-left: 10px;
}

.low-active {
  background: rgb(10, 201, 71);
  color: #fff;
  margin-left: 10px;
}

.add-button-div {
  display: flex;
  justify-content: end;
}

.add-button {
  padding: 13px 0 13px 0;
  width: 24%;
  text-align: center;
  margin-top: 40px;
  box-shadow: rgba(113, 63, 255, 0.25) 0px 6px 12px;
  color: rgb(255, 255, 255);
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
  background: rgb(113, 63, 255);
}

.disable-add-button {
  background-color: #7d8592;
  cursor: not-allowed;
  color: rgb(255, 255, 255);
  padding: 13px 0 13px 0;
  width: 24%;
  text-align: center;
  margin-top: 40px;
  box-shadow: rgba(113, 63, 255, 0.25) 0px 6px 12px;
  color: rgb(255, 255, 255);
  font-size: 16px;
  font-weight: 600;
}

@media (width <= 605px) {
  .update-modal {
    width: 92%;
    margin: -50px auto 0 auto;
  }

  .update-third button {
    padding: 13px 0 13px 0;
    width: 28%;
    text-align: center;
    margin-top: 8px;
  }

  #add-button-id {
    width: 35%;
  }
}

/*-------Edit modal------------*/
.edit-background {
  background: rgba(0, 0, 0, 0.2);
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
}

.edit-modal {
  padding: 30px 50px;
  background-color: #fff;
  border-radius: 24px;
  width: 40%;
  justify-content: center;
  border: 1px solid blue;
  line-height: 2;
}

@media (width <= 605px) {
  .edit-modal {
    width: 92%;
    margin: -50px auto 0 auto;
  }
}
</style>