<script setup>
import { reactive, watch } from "vue";

let average = "0.0";
let count = 0;

const inputs = reactive({
  5: 0,
  4: 0,
  3: 0,
  2: 0,
  1: 0,
});

watch(inputs, () => {
  let sum = 0;
  count = 0;

  for (let [key, value] of Object.entries(inputs)) {
    value = value || 0;
    sum += key * value;
    count += value;
  }

  average = (sum / count || 0).toFixed(1);
});
</script>

<template>
  <div class="m-a">
    <div class="mt-5 h-10 fs-6 fw-b">리뷰 예보</div>
    <div class="mt-5 h-10 fd-r">
      <img class="h-4" src="/star.png" alt="Star" />
      <div class="ml-1 fw-b">{{ average }} ({{ count }})</div>
    </div>
    <div class="h-10 fd-r" v-for="key in Object.keys(inputs).reverse()" v-bind:key="key">
      <div class="w-15">{{ key }}점</div>
      <progress v-bind:value="inputs[key] / count || 0"></progress>
      <input
        type="number"
        inputmode="numeric"
        v-model.number="inputs[key]"
        v-on:focus="inputs[key] ||= ''"
        v-on:blur="inputs[key] ||= 0"
      />
    </div>
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: "Noto Sans KR", sans-serif;
  font-size: 4vmin;
  line-height: 1;
  touch-action: manipulation;
}

div {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

progress {
  appearance: none;
  width: 55vmin;
  height: 2vmin;
}

progress::-webkit-progress-bar {
  border-radius: 1vmin;
  background-color: #f0f0f0;
}

progress::-webkit-progress-value {
  border-radius: 1vmin;
  background-color: #ffac33;
}

input {
  appearance: none;
  margin-left: 5vmin;
  border: none;
  border-radius: 2vmin;
  padding: 0;
  width: 15vmin;
  height: 8vmin;
  background-color: #f0f0f0;
  font-family: "Noto Sans KR", sans-serif;
  font-size: 4vmin;
  text-align: center;
  line-height: 1;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

.m-a {
  margin: auto;
}

.mt-5 {
  margin-top: 5vmin;
}

.ml-1 {
  margin-left: 1vmin;
}

.w-15 {
  width: 15vmin;
}

.h-4 {
  height: 4vmin;
}

.h-10 {
  height: 10vmin;
}

.fd-r {
  flex-direction: row;
}

.fs-6 {
  font-size: 6vmin;
}

.fw-b {
  font-weight: bold;
}
</style>
