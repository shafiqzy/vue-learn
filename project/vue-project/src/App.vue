<script setup>
//need to import { ref } from 'vue' for ref();
import { ref } from 'vue';

//ref() is use to obtain value from  v-model (html)
const no1 = ref(0);
const no2 = ref(0);
const result = ref(0);

//array
const array = ref ([]);

function add(){

  if (no1.value < 0 || no2.value < 0) {

    return alert("Negative Number");

  } else {

    result.value = no1.value + no2.value;
    //array.value.push(result.value);//the result data  will add in the array

  }

}

function sub(){

  if (no1.value < 0 || no2.value < 0) {
    return alert("Negative Number");
  } else {
    result.value = no1.value - no2.value;
    //array.value.push(result.value);
  }

}

function multiple(){

if (no1.value < 0 || no2.value < 0) {
  return alert("Negative Number");
} else {
  result.value = no1.value * no2.value;
  //array.value.push(result.value);
}

}

function divide(){

if (no1.value < 0 || no2.value < 0) {
  return alert("Negative Number");
} else {
  result.value = no1.value / no2.value;
  //array.value.push(result.value);
}

}

</script>

<template>
  <div>
    <input type="number" v-model="no1"/>
    <input type="number" v-model="no2"/>
  </div>
  <div>
    <button @click="add">add</button><!--@click to call a function-->
    <button @click="sub">subtract</button>
    <button @click="multiple">multiple</button>
    <button @click="divide">divide</button>
  </div>

  <div>
    <h1>{{ result }}</h1><!--to display data from js-->
  </div>

  <div v-if="result > 5">Lebih dari 5</div><!-- v-if="result > 5" use js error message -->
  <div v-else-if="result < 0">Negative number</div>
  <h1>jawapan array</h1>
    <!--val ialah variable, index is number index-->
    <!--Kalau tukar tempat, value pun akan berubah-->
      <table>
        <tr>
          <th>No.</th>
          <th>Movie Name</th>
          <th>Date and Time</th>
          <th>Seat</th>
        </tr>
        <tr v-for="(val, index) in array">

        </tr>
      </table>
      index -> {{ index }} || array -> {{ val }}

<table>
    <tr v-for="(row, rowIndex) in twoDArray" :key="rowIndex">
      <td v-for="(cell, cellIndex) in row" :key="cellIndex">
        {{ cell }}
      </td>
    </tr>
  </table>

  new Vue({
  el: '#app',
  data: {
    twoDArray: [],
  },
  mounted() {
    // populate the 2D array with data
    this.twoDArray = [
      [1, 2, 3],
      [4, 5, 6],
      [7, 8, 9],
    ];
  },
});

</template>