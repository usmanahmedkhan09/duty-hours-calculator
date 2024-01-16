<template>
  <div>
    <h1>Duty Hours Checker</h1>

    <div class="time-inputs">
      <div>
        <label for="startTime">Duty Start Time:</label>
        <input type="time" v-model="startTime" id="startTime" placeholder="Enter start time" />
      </div>

      <div>
        <label for="endTime">Duty End Time:</label>
        <input type="time" v-model="endTime" id="endTime" placeholder="Enter end time" />
      </div>
    </div>
    <div class="time-input">
      <label for="requiredHours">Required Duty Hours:</label>
      <input type="number" v-model="requiredHours" id="requiredHours" class="styled-input" />
    </div>

    <button @click="checkDutiesCompletion" style="margin-top: 32px">Check Completion</button>

    <p v-if="totalWorkedHours !== null">
      {{
        `Total hours worked: ${totalWorkedHours.hours} hours and ${totalWorkedHours.minutes} minutes`
      }}
    </p>

    <p v-if="result !== null" style="color: red">
      {{
        result
          ? 'Congratulations! You have completed your duty hours.'
          : 'You still have some duty hours to complete.'
      }}
    </p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const startTime = ref(null)
const endTime = ref(null)
const requiredHours = ref(9.5)
const result = ref(null)
const totalWorkedHours = ref(null)

const checkDutiesCompletion = () => {
  if (startTime.value !== null && endTime.value !== null) {
    const start = convertToDecimalHours(startTime.value)
    const end = convertToDecimalHours(endTime.value)

    const totalHours = end - start
    const hours = Math.floor(totalHours)
    const minutes = Math.round((totalHours - hours) * 60)

    result.value = end - start >= requiredHours.value
    totalWorkedHours.value = { hours, minutes }
  } else {
    alert('Please enter both start and end times.')
  }
}

const convertToDecimalHours = (timeString) => {
  const [hours, minutes] = timeString.split(':').map(Number)
  return hours + minutes / 60
}
</script>

<style scoped>
/* Your existing styles */
div {
  text-align: center;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f8f8f8;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
  color: #333;
}

label {
  display: block;
  margin-bottom: 8px;
}

input {
  padding: 8px;
  margin-bottom: 16px;
}

button {
  padding: 10px;
  font-size: 16px;
  cursor: pointer;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
}

button:hover {
  background-color: #45a049;
}

p {
  font-size: 18px;
  margin-top: 15px;
  color: #333;
}

.time-inputs {
  display: flex;
  justify-content: space-around;
  margin-bottom: 16px;
}

.time-inputs div {
  flex: 1;
  margin-right: 10px;
}

.time-inputs {
  display: flex;
  justify-content: space-around;
  margin-bottom: 16px;
}

.time-input {
  position: relative;
  margin-right: 10px;
}

.styled-input {
  width: 120px;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #3498db;
  border-radius: 5px;
  background-color: #ecf0f1;
  color: #333;
  outline: none;
}

.styled-input:focus {
  border-color: #2ecc71;
}

label {
  display: block;
  margin-bottom: 6px;
  font-size: 14px;
  color: #555;
}

.time-inputs {
  display: flex;
  justify-content: space-around;
  margin-bottom: 16px;
}

.time-input {
  position: relative;
  margin-right: 10px;
}

.styled-input {
  width: 120px;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #3498db;
  border-radius: 5px;
  background-color: #ecf0f1;
  color: #333;
  outline: none;
}

.styled-input:focus {
  border-color: #2ecc71;
}

label {
  display: block;
  margin-bottom: 6px;
  font-size: 14px;
  color: #555;
}
</style>
