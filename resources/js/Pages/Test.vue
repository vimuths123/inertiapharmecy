<template>
  <div>
    <label for="timeslot">Select a Timeslot:</label>
    <select v-model="selectedTimeslot" id="timeslot">
      <option v-for="timeslot in availableTimeslots" :key="timeslot" :value="timeslot">
        {{ timeslot }}
      </option>
    </select>

    <p>You selected: {{ selectedTimeslot }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const generateTimeSlots = () => {
  const timeSlots = [];
  const startTime = 8; // Start at 8 AM
  const endTime = 18; // End at 6 PM
  const interval = 2; // 2-hour interval

  for (let i = startTime; i < endTime; i += interval) {
    const startTimeString = `${i.toString().padStart(2, '0')}:00`;
    const endTimeString = `${(i + interval).toString().padStart(2, '0')}:00`;
    const timeSlot = `${startTimeString} - ${endTimeString}`;
    timeSlots.push(timeSlot);
  }

  return timeSlots;
};

const availableTimeslots = ref(generateTimeSlots());
const selectedTimeslot = ref(availableTimeslots.value[0]); // Set the default to the first timeslot
</script>
