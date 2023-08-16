<template>
    <div>
      <h1>Vue 3 Demo Page</h1>
  
      <!-- Conditional Rendering -->
      <section class="section-box">
        <h2>Conditional Rendering</h2>
        <div class="section-content">
          <div class="control">
            <label for="showMessageCheckbox">Toggle showMessage True/False:</label>
            <input type="checkbox" id="showMessageCheckbox" v-model="showMessage" />
          </div>
          <p v-if="showMessage">v-if rendered and displayed this message when the checkbox is used to toggle the "showMessage" constant to true.</p>
          <p v-else>This message is rendered and displayed when showMessage is false, using v-else.</p>
        </div>
      </section>
  
      <section class="section-box">
        <h2>Conditional Rendering with v-show</h2>
        <div class="section-content">
          <div class="control">
            <label for="messageTwoCheckbox">Toggle messageTwo True/False:</label>
            <input type="checkbox" id="messageTwoCheckbox" v-model="messageTwo" />
          </div>
          <p v-show="messageTwo">This is a message displayed using v-show="messageTwo". Note that it remains rendered in the DOM regardless of whether the "showMessage" constant is set to true or false - it's the display of the message that is toggled</p>
        </div>
      </section>
  
      <section class="section-box">
        <h2>List Rendering with v-for</h2>
        <div class="section-content">
          <p>The following list:</p>
          <img alt="list 1" src="@/assets/list1.jpg" width="400" height="25" />
          <p>has been rendered below as an ordered list, using v-for:</p>
          <ol>
            <li v-for="(item, index) in items" :key="index">{{ item }}</li>
          </ol>
        </div>
      </section>
  
      <section class="section-box">
        <h2>List Rendering with v-for and v-if</h2>
        <div class="section-content">
          <p>The following list:</p>
          <img alt="list 2" src="@/assets/list2.jpg" width="400" height="25" />
          <p>has been rendered below as an ordered list, using v-for, and v-if. Toggle the checkbox to false, and the list will disappear:</p>
          <ol>
            <li v-if="showList" v-for="(item, index) in listItems" :key="index">{{ item }}</li>
          </ol>
          <div class="control">
            <label for="showListCheckbox">Toggle showList True/False:</label>
            <input type="checkbox" id="showListCheckbox" v-model="showList" />
          </div>
        </div>
      </section>
  
      <section class="section-box">
        <h2>Form Input Handling</h2>
        <div class="section-content">
        <p>Enter text below. It will be rendered in real-time as you type:</p>
        <input type="text" v-model="inputText" />

        <p>You typed: {{ inputText }}</p>

        <div class="input-list">
          <p>Enter text and click "Add Input" or press "Enter" to add it to the list:</p>
          <input
            type="text"
            id="inputToAdd"
            v-model="inputToAdd"
            :style="{ border: inputToAddError ? '2px solid red' : '1px solid #ccc' }"
            @keydown.enter="addInput"
          />
          <button @click="addInput">Add Input</button>
          <p v-if="inputToAddError" class="error-message">Please enter some input</p>
        </div>

        <ol>
          <li v-for="(item, index) in inputList" :key="index">{{ item.name }}</li>
        </ol>
      </div>
    </section>
  </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const showMessage = ref(true);
  const messageTwo = ref(true);
  const items = ref(['Apple', 'Banana', 'Cherry']);
  const showList = ref(true);
  const listItems = ref(['Blue', 'Red', 'Yellow']);

const inputText = ref('')
  const inputToAdd = ref('');
  const inputToAddError = ref(false);
  const inputList = ref([]);

  function addInput() {
    if (inputToAdd.value.trim() !== '') {
        inputList.value.push({
            name: inputToAdd.value
        })
            inputToAdd.value = '';
            inputToAddError.value = false;
        
    } else {
        inputToAddError.value = true;
    }
  }
  </script>
  
  <style scoped>
  /* Styling for the demo page */
  h1 {
    text-align: center;
    margin-bottom: 20px;
  }
  
  h2 {
    margin-top: 20px;
  }
  
  .section-box {
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f2f2f2;
    padding: 20px;
    margin: 20px 0;
  }
  
  .section-content {
    margin-top: 10px;
  }
  
  .control {
    margin-bottom: 10px;
  }
  
  ol {
    margin-left: 20px;
  }
  
  input[type="text"] {
    width: 100%;
    padding: 10px;
    font-size: 16px;
  }
  
  p {
    margin: 10px 0;
  }

  .error-message {
  color: red;
  font-size: 16px;
  display: block;
  margin-top: 5px;
}
  </style>
  