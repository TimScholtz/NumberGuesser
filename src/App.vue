<template>
  {{ solutionNumber }}
  <div class="d-flex justify-content-center align-items-center h-100">
    <div class="card p-3" v-if="start">
      <div class="card-title">Number Guessing Game</div>
      <div class="card-body">
        Enter the range the numbers should have
        <form @submit="startGame()">
          <div class="d-flex">
            <input
              type="number"
              class="form-control"
              v-model="firstRangeNumber"
            />
            <input
              type="number"
              class="form-control"
              v-model="secondRangeNumber"
            />
            <button class="btn btn-primary">Submit</button>
          </div>
        </form>
      </div>
    </div>

    <div class="card p-3" v-else>
      <div class="card-title">Number Guessing Game</div>
      <div class="card-body">
        Guess the random number
        <form @submit="guess()">
          <div class="d-flex">
            <input type="number" class="form-control" />
            <button class="btn btn-primary">Submit</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
<script setup lang="ts">
import { ref } from "vue";

const start = ref(true);
const firstRangeNumber = ref(0);
const secondRangeNumber = ref(0);
const solutionNumber = ref(0);

function startGame() {
  solutionNumber.value = Math.floor(
    Math.random() * (secondRangeNumber.value - firstRangeNumber.value) +
      firstRangeNumber.value
  );
  start.value = false;
}

function guess() {}
</script>
