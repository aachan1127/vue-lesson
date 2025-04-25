<script setup>
import { ref } from 'vue' // ref 関数を呼び出すことで、priceのデータが再レンダリングされる

const title = ref('Vue.js Course')
let price = ref(9.99) // refオブジェクト
function increment() {
  price.value += 1 // .valueをつけることで、 priceの値が再レンダリングされる
  // console.log(price.value)
}
const info = ref({
  student: 1000,
  rating: 4,
})
console.log(info.value.student)
</script>

<template>
  <h1>Title: {{ title }}</h1>
  <h2>Price: {{ price }}</h2>
  <button @click="increment">button</button>
  <h2>Students: {{ info.student }}</h2>
</template>

<style>
h1 {
  color: red;
}
</style>
ß
