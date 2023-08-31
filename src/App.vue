<script setup>
import { ref, computed } from "vue";

const nombre = "vue dinamico";

const counter = ref(0);
const arrayFav = ref([]);

const increment = () => {
  counter.value++;
};

const decrement = () => {
  counter.value--;
};

const reset = () => {
  counter.value = 0;
};

const add = () => {
  arrayFav.value.push(counter.value);
};

const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  } else if (counter.value > 0) {
    return "positive";
  } else counter.value < 0;
  return "negative";
});

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFav.value.find((num) => num === counter.value);
  console.log(numSearch);
  if (numSearch === 0) return true;
  return numSearch ? true : false;
});
</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ nombre }}!</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="decrement" class="btn btn-danger fw-bold">Restar</button>
      <button @click="reset" class="btn btn-warning fw-bold">Resetear</button>
      <button @click="increment" class="btn btn-success fw-bold">Sumar</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary fw-bold">
        Favorito
      </button>
    </div>
    <ul class="list-group">
      <li v-for="(num, index) in arrayFav" :key="index" class="list-group-item">
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<style>
h1 {
  color: purple;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: #ffc107;
}
</style>
