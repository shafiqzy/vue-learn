<script setup>
import { ref } from 'vue';

const movie = ref(0);
const date = ref(0);
const time = ref(0);

var message = '';
const seats = ([]);
const array = ([]);

  function receipt(){
      
    message = movie.value + ',' + date.value + ',' + time.value + ',' + seats;
    array.push(message);
    console.log(message);
    console.log(seats);
  }

  function Tekan(cell){
    seats.push(cell);
  }
</script>
<script>
export default{
  data() {
    return {
      numCols: 3, // Number of columns in the 2D array
      twoDArray: [
                  ['A1','A2','A3','A4','A5','A6','A7','A8','A9','A10'],
                  ['B1','B2','B3','B4','B5','B6','B7','B8','B9','B10'],
                  ['C1','C2','C3','C4','C5','C6','C7','C8','C9','C10']
                ]
    };
  },
  methods:{

  }
};
</script>

<template>
  <h1>Booking Movie Ticket</h1>
  <form @submit.prevent="receipt">
    <div class="movie-container">
      <label>Pick a movie:</label>
      <select id="movie" v-model="movie">
        <option value="Avengers">Avengers: Endgame ($10)</option>
        <option value="Joker">Joker ($12)</option>
        <option value="Toy Story 4">Toy Story 4 ($8)</option>
        <option value="The Lion King">The Lion King ($9)</option>
      </select>
    </div>

    <div class="movie-container">
      <label>Pick a Date:</label>
        <input type="date" id="date" v-model="date">
    </div>

    <div class="movie-container">
      <label>Pick a Time:</label>
      <select id="time" v-model="time">
        <option value="11am">11.00 AM</option>
        <option value="1pm">1.00 PM</option>
        <option value="3pm">3.00 PM</option>
        <option value="8pm">8.00 PM</option>
      </select>
    </div>
    <ul class="showcase">
      <li>
        <div class="seat"></div>
        <small>N/A</small>
      </li>

      <li>
        <div class="seat selected"></div>
        <small>Selected</small>
      </li>

      <li>
        <div class="seat occupied"></div>
        <small>Occupied</small>
      </li>
    </ul>
    <table>
      <tr v-for="(row, rowIndex) in twoDArray" :key="rowIndex">
        <!-- {{ row }} -->
        <td v-for="(cell, colIndex) in row" :key="colIndex">
          <button class="seat" :v-model="cell" @click="Tekan(cell)">{{ cell }} </button> </td>
      </tr>
    </table>
    
    <input type="submit">
  </form>
  <table>
    <tr></tr>
    <tr v-for="(val, index) in array">
      index -> {{ index }} || array -> {{ val }}

    </tr>
  </table>
  <table class="table">
      <thead>
        <tr>
          <th>Movie</th>
          <th>Date</th>
          <th>Time</th>
          <th>seat</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(val, index) in array">
          <td>{{ index }}</td>
          <td>{{ val }}</td>
          <td>{{ seats }}</td>
        </tr>
      </tbody>
    </table>

</template>
<style> 

</style>
