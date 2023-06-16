<template>
  <div class="container">
    <div class="wrapper">
      <div class="first-row">
        <h1 class="head">Task List</h1>
        <button><span class="add">+</span> Add Task</button>
      </div>
      <div class="second-row">
        <Data />
      </div>
    </div>
  </div>
</template>

<script>
import Data from '../components/Data.vue'
export default {
  components: { Data },
  setup() {}
}
</script>

<style scoped>
.container {
  font-weight: normal;
  border: 1px solid black;
  min-height: 100vh;
}

.wrapper {
  max-width: 700px;
  margin: 50px auto;
  border: 1px solid blue;
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
</style>