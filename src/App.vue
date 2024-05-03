<template>
  <div class="d-flex justify-content-center align-items-start">
    <div class="card p-3" v-if="!showCode">
      <div class="card-body">
        <div class="card-title">Number Guessing Game</div>
        <div class="d-flex">
          <button class="btn btn-primary" @click="showMeCode">
            Show the code.
          </button>
        </div>
      </div>
    </div>

    <div class="card p-3" v-else>
      <div class="card-body">
        <div class="card-title">Number Guessing Game</div>
        <VCodeBlock :code="code" highlightjs lang="javascript"></VCodeBlock>
        <div class="d-flex">
          <button class="btn btn-primary" @click="showMeCode">
            Hide the code.
          </button>
        </div>
      </div>
    </div>
  </div>
  <div class="d-flex justify-content-center align-items-center h-100">
    <div class="card p-3" v-if="start">
      <div class="card-body">
        <div class="card-title">Number Guessing Game</div>
        Enter the range the numbers should have
        <form @submit="startGame()">
          <div class="d-flex">
            <input
              min="0"
              max="1000"
              type="number"
              class="form-control"
              v-model="firstRangeNumber"
            />
            <input
              min="0"
              max="1000"
              type="number"
              class="form-control"
              v-model="secondRangeNumber"
            />
            <button class="btn btn-primary">Submit</button>
          </div>
        </form>
      </div>
    </div>

    <div class="card p-3" v-else-if="!win && !start">
      <div class="card-body">
        <div class="card-title">Number Guessing Game</div>
        <span v-if="!guessMessage">Guess the random number</span>
        <span v-else>{{ guessMessage }}</span>
        <form @submit.prevent="guess()">
          <div class="d-flex">
            <input
              step="1"
              type="number"
              v-model="guessNumber"
              class="form-control"
            />
            <button class="btn btn-primary">Submit</button>
          </div>
        </form>
      </div>
    </div>

    <div class="card p-3" v-else>
      <div class="card-body">
        <div class="card-title">Number Guessing Game</div>
        <div>You guessed right!!</div>
        <div>The solution was: {{ solutionNumber }}</div>
        <div class="d-flex justify-content-end">
          <button class="btn btn-primary" @click="restart">Restart</button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
<script setup lang="ts">
import { ref } from "vue";
import { VCodeBlock } from "@wdns/vue-code-block";

const showCode = ref(false);
const start = ref(true);
const win = ref(false);
const firstRangeNumber = ref(0);
const secondRangeNumber = ref(0);
const solutionNumber = ref(0);
const guessNumber = ref(0);
const guessMessage = ref("");

function startGame() {
  solutionNumber.value = Math.floor(
    Math.random() * (secondRangeNumber.value - firstRangeNumber.value) +
      firstRangeNumber.value
  );
  start.value = false;
}

function guess() {
  if (guessNumber.value == solutionNumber.value) {
    guessMessage.value = "you won!";
    win.value = true;
  } else if (guessNumber.value < solutionNumber.value) {
    guessMessage.value = "the solution is bigger";
  } else {
    guessMessage.value = "the solution is smaller";
  }
  guessNumber.value = 0;
}
function restart() {
  start.value = true;
  win.value = false;
  firstRangeNumber.value = 0;
  secondRangeNumber.value = 0;
  solutionNumber.value = 0;
  guessNumber.value = 0;
  guessMessage.value = "";
}
function showMeCode() {
  showCode.value = !showCode.value;
}
const code = ref(`<template>
  <div class="d-flex justify-content-center align-items-center h-100">
    <div class="card p-3" v-if="start">
      <div class="card-body">
        <div class="card-title">Number Guessing Game</div>
        Enter the range the numbers should have
        <form @submit="startGame()">
          <div class="d-flex">
            <input
              min="0"
              max="1000"
              type="number"
              class="form-control"
              v-model="firstRangeNumber"
            />
            <input
              min="0"
              max="1000"
              type="number"
              class="form-control"
              v-model="secondRangeNumber"
            />
            <button class="btn btn-primary">Submit</button>
          </div>
        </form>
      </div>
    </div>

    <div class="card p-3" v-else-if="!win && !start">
      <div class="card-body">
        <div class="card-title">Number Guessing Game</div>
        <span v-if="!guessMessage">Guess the random number</span>
        <span v-else>{{ guessMessage }}</span>
        <form @submit.prevent="guess()">
          <div class="d-flex">
            <input
              step="1"
              type="number"
              v-model="guessNumber"
              class="form-control"
            />
            <button class="btn btn-primary">Submit</button>
          </div>
        </form>
      </div>
    </div>

    <div class="card p-3" v-else>
      <div class="card-body">
        <div class="card-title">Number Guessing Game</div>
        <div>You guessed right!!</div>
        <div>The solution was: {{ solutionNumber }}</div>
        <div class="d-flex justify-content-end">
          <button class="btn btn-primary" @click="restart">Restart</button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
<script setup lang="ts">
import { ref } from "vue";

const start = ref(true);
const win = ref(false);
const firstRangeNumber = ref(0);
const secondRangeNumber = ref(0);
const solutionNumber = ref(0);
const guessNumber = ref(0);
const guessMessage = ref("");

function startGame() {
  solutionNumber.value = Math.floor(
    Math.random() * (secondRangeNumber.value - firstRangeNumber.value) +
      firstRangeNumber.value
  );
  start.value = false;
}

function guess() {
  if (guessNumber.value == solutionNumber.value) {
    guessMessage.value = "you won!";
    win.value = true;
  } else if (guessNumber.value < solutionNumber.value) {
    guessMessage.value = "the solution is bigger";
  } else {
    guessMessage.value = "the solution is smaller";
  }
  guessNumber.value = 0;
}
function restart() {
  start.value = true;
  win.value = false;
  firstRangeNumber.value = 0;
  secondRangeNumber.value = 0;
  solutionNumber.value = 0;
  guessNumber.value = 0;
  guessMessage.value = "";
}
/script>
`);
</script>
