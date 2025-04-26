<script setup>
import { ref, reactive } from 'vue'
// ref 関数を呼び出すことで、priceのデータが再レンダリングされる
// reactive 関数 元々オブジェクトになっているやつはreactive関数を使うことで、いちいちオブジェクトを作らなくていい（ここでいうinstructor）

const title = ref('Vue.js Course')
let price = ref(9.99) // refオブジェクト

function increment() {
  price.value += 1 // .valueをつけることで、 priceの値が再レンダリングされる
  instructor.age += 1 // reactive関数で作られているので、 .valueつけなくても再レンダリングされる
  instructor.bio = 'hi'
  instructor.sns.twitter = 'hello'
}

const info = ref({
  student: 1000,
  rating: 4,
})

const instructor = reactive({
  name: 'Akane',
  age: 33,
  sns: {
    //reactive関数の中のオブジェクトは、reactiveになる！
    twitter: '@aachan',
    youtube: '@Akane',
  },
})
instructor.bio = 'hello'
console.log(info.value.student) //ref関数なので、.valueをつける
console.log(instructor.sns) //reactive関数なので、.valueつけなくてもいい
</script>

<template>
  <h1>Title: {{ title }}</h1>
  <h2>Price: {{ price }}</h2>
  <button @click="increment">button</button>
  <h2>Students: {{ info.student }}</h2>
  <h2>Instructor age: {{ instructor.age }}</h2>
  <h2>Instructor bio: {{ instructor.bio }}</h2>
  <h2>Instructor SNS Twitter: {{ instructor.sns.twitter }}</h2>
</template>

<style>
h1 {
  color: red;
}
</style>
ß
