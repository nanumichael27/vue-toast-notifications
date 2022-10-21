<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref } from "@vue/reactivity";
import Toast from "./components/toast/Toast.vue";
let showToast = ref(false)
let position = ref('top-left')
let message = ref('hello this is a message for you')
let type = ref('success')

const toast = (pos) => {
  position.value = pos;
  showToast.value = true;
}

</script>

<template>
  <div class="heading">
    <h2>Toast Notifications by Nanotek</h2>
  </div>
  <div class="button-panel">
    <button @click="toast('top-left')">Top Left</button>
    <button @click="toast('bottom-left')">Bottom Left</button>
    <button @click="toast('top-right')">Top Right</button>
    <button @click="toast('bottom-right')">Bottom Right</button>
  </div>
  <div class="customization-panel">
    <select name="type" id="" v-model="type">
      <option value="success">Success</option>
      <option value="warning">Warning</option>
      <option value="error">Error</option>
    </select>
    <div>
      <label for="message">Customize Message</label>
      <input type="text" v-model="message">
    </div>
  </div>
  <Toast
    :message="message"
    :show="showToast"
    @hide="showToast = false"
    :type="type"
    :position="position"
  />
</template>

<style scoped>

.heading{
  text-align: center;
  border: 1px solid green;
  margin-bottom: 10px;
  border-radius: 50px;
}
.button-panel{
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 100px;
  border-radius: 50px;
  border: 1px solid green
}

.button-panel button{
  padding: 10px;
  box-shadow: none;
  border: none;
  background: rgb(44, 44, 168);
  color: white;
  cursor: pointer;
  border-radius: 35px;
}

.customization-panel{
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  border-radius: 50px;
  border: 1px solid green;
  padding: 30px;
  margin-top: 10px;
  font-size: large;
  align-items: center;
}

.customization-panel select{
  padding: 10px;
  font-size: large;
  border-radius: 20px;
}

.customization-panel div input{
  font-size: large;
  margin-left: 20px;
  padding: 10px;
  border-radius: 20px;
  border-width: 1px;
}
</style>
