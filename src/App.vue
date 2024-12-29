<template>
   <div class="container">
      <div class="verse-card">
          <div class="flex-container" style="display: flex; justify-content: space-between; align-items: center;">
            <h1 @click="isDatePickerVisible = !isDatePickerVisible">{{ formattedToday }}</h1>
            <small style="width: auto;">No {{ verseIndex }}. / {{ bibleVerses.length }}</small>
          </div>
          <p>{{ todayVerse.text }}</p>
          <small>{{ todayVerse.reference }}</small>
      </div>

      <!-- Hidden Date Picker -->
      <input
        type="date"
        v-show="isDatePickerVisible"
        @change="onDateChange"
        ref="datePicker"
      />


  </div>
</template>

<script>
import { bibleVerses } from './const/verse';
// import bibleVerses from './const/verse.js'
export default {
  name: 'App',
  components: {
  },
  data() {
      return {
        bibleVerses,
        
        today: new Date(), // Current date
        isDatePickerVisible: false,
      };
  },
  mounted(){
    console.clear()
    console.log(this.bibleVerses)
  },
  methods:{
    getDayOfYear(date) {
      const monthDays = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
      const month = date.getMonth();
      const day = date.getDate();
      return monthDays.slice(0, month).reduce((total, days) => total + days, 0) + day;
    },
    isLeapDay(date) {
      return date.getMonth() === 1 && date.getDate() === 29; // Check for Feb 29
    },
    onDateChange(event) {
      // Update `today` with the selected date
      this.today = new Date(event.target.value);
      this.isDatePickerVisible = false;
    },
  },
  computed: {
    formattedToday() {
      const options = { month: "2-digit", day: "2-digit", weekday: "short" };
      return this.today.toLocaleDateString("en-US", options); // Format: MM/DD Day
    },
    verseIndex() {
      const dayOfYear = this.getDayOfYear(this.today);

      if (this.isLeapDay(this.today)) {
        return this.bibleVerses.length - 1; // Last index for leap day
      }

      return (dayOfYear - 1) % this.bibleVerses.length + 1; // Adjust to 1-based index
    },
    todayVerse() {
      return this.bibleVerses[this.verseIndex - 1]; // Get the verse by index (adjusted for 0-based)
    },
  },
}
</script>

<style>
body {
    margin: 0;
    padding: 0;
    background: url('../public/img/bg.jpg') no-repeat center center fixed;
    background-size: cover;
    color: white;
    font-family: Arial, sans-serif;
    height: 100vh;


    position: relative;
    overflow-x: hidden;
    overflow-y: hidden;
}
.container {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.verse-card {
  width: 90vw;
  position: absolute;
  top: 10%;
  left: 50%;
  transform: translateX(-50%);

  background-color: rgba(0, 0, 0, 0.7);
  padding: 20px;
  border-radius: 10px;
  text-align: center;
}
.verse-card h1 {
    font-size: 1.5rem;
}
.verse-card p {
    font-size: 1.2rem;
    text-align: left;
}
small {
  display: block;
    /* position: absolute; */
    bottom: 10px;
    width: 100%;
    text-align: right;
}
</style>
