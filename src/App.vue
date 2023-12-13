

<script setup>
  import { computed, ref } from 'vue';

  const name = "Vue 3";

  const counter = ref(0);
  const arrayFavoritos = ref([]);

  const increment = () => {
    counter.value ++;
  };

  const decrement = () => {
    counter.value --;
  };

  const reset = () => {
    counter.value = 0;
  };

  const add = () => {
    arrayFavoritos.value.push( counter.value );
  };

  const bloquearBtnAdd = computed( ()=> {

    const numSearch = arrayFavoritos.value.find( num => num === counter.value );
    return numSearch ||  numSearch === 0;

  });
  const classCounter = computed(() => {

    if ( counter.value === 0 ) {
      return 'zero'
    }

    if ( counter.value > 0 ) {
      return 'positive'
    }

    if ( counter.value < 0 ) {
      return 'negative'
    }

  });

</script>

<template>

  <div class="container text-center mt-3">

    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Resetear</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
    </div>
    <ul class="list-group mt-4">
      <li 
        class="list-group-item"
        v-for="(num, index) in arrayFavoritos" 
        :key="index"
      >
        {{ num }}
      </li>
    </ul>
  </div>

</template>

<style>
  h1 {
    color: red;
  }
  .positive {
    color: green
  }
  .negative {
    color: red
  }
  .zero {
    color: peru;
  }
</style>
