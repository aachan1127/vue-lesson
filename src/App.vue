<script setup>
import { ref, reactive } from 'vue'
// ref 関数を呼び出すことで、priceのデータが再レンダリングされる
// reactive 関数 元々オブジェクトになっているやつはreactive関数を使うことで、いちいちオブジェクトを作らなくていい（ここでいうinstructor）

const title = ref('Vue.js Course')
let price = ref(9.99) // refオブジェクト

function increment() {
  //ボタンを降りた時の処理↓
  price.value += 1 // .valueをつけることで、 priceの値が再レンダリングされる
  instructor.age += 1 // reactive関数で作られているので、 .valueつけなくても再レンダリングされる
  instructor.bio = 'hi'
  instructor.sns.twitter = 'hello'
  instructor.email = 'info@examlpe.com'
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
  email: ref('aachan@example.com'),
})
instructor.bio = 'hello'
const items = reactive([ref(1), ref(2), 3])
// 配列の中身を逆にする
items.reverse()

// reactive関数でも、配列の時の場合にのみ、.valueをつけないと取り出せないので注意！
console.log(items[0].value)

// それぞれのプロパティにref関数をつけた時
const courseInfo = {
  sections: ref(10),
  language: ref('Japanese'),
}

console.log(courseInfo.sections.value)

//ref関数なので、.valueをつける
// console.log(info.value.student)

//reactive関数なので、.valueつけなくてもいい
// console.log(instructor.sns)

//reactive関数の中のref関数なので、.valueはつけなくてもいい
// console.log(instructor.email)

// const count = ref(2)
// const count2 = ref(2)

// v-htmlディレクティブ ()の中をHTMLとして表示できるようになる
const message = ref('<h1>Hello</h1>')

// v-bindディレクティブ URLを表示させたい時はこれを使う
const vueURL = 'https://vuejs.org'
const vueId = 'vue-link'

// イベントオブジェクト
const count = ref(0)
function countUp(event, times) {
  count.value = event.clientX * times
}
</script>

<template>
  <h1>Title: {{ title }}</h1>
  <h2>Price: {{ price }}</h2>
  <button @click="increment">button</button>
  <h2>Students: {{ info.student }}</h2>
  <h2>Instructor age: {{ instructor.age }}</h2>
  <h2>Instructor bio: {{ instructor.bio }}</h2>
  <h2>Instructor SNS Twitter: {{ instructor.sns.twitter }}</h2>
  <h2>Instructor email: {{ instructor.email }}</h2>

  <!-- courseInfoが普通のオブジェクトなので、.valueは自動でつかないので、自分でつける必要がある！ -->
  <h2>Course Info Sections: {{ courseInfo.sections.value }}</h2>

  <!-- {{  }}の中には、単一の式だけを書くことができる -->
  <!-- また、if文や、関数の中に定義されているものは使えない -->
  <!-- <div>{{ count + 3 }}</div> -->
  <!-- <div>{{ count + count2 }}</div> -->
  <!-- <div>{{ count > 3 ? 'Yes' : 'No' }}</div> -->

  <!-- この２つは同じ表示になる（ディレクティブ） -->
  <!-- <div>{{ count }}</div> -->
  <div v-text="count"></div>

  <!-- v-htmlディレクティブ (※ XSS攻撃されやすいので注意が必要！)-->
  <div v-html="message"></div>

  <!-- v-bindディレクティブ URLで遷移させたい時-->
  <!-- <a v-bind:id="vueId" v-bind:href="vueURL" :foo>Vue.js</a> -->
  <a v-bind="{ id: vueId, href: vueURL }">Vue.js</a>
  <!-- このようにまとめて書くことも可能 -->

  <!--Boolean属性 NaNやfalseを指定すると、disable属性が消える-->
  <!-- <button :disabled="NaN">button</button> -->

  <!-- v-onディレクティブ  何かが起きた時に何かをさせたい時-->
  <!-- <button v-on:click="count++">button</button> -->
  <!-- 上のv-onを@に省略して記載することも可能 -->
  <button @click="count++">button</button>

  <!-- イベントオブジェクト ボタンをクリックした時のX軸の値を取得して表示させる（.clientX)-->
  <p>{{ count }}</p>
  <button @click="count = $event.clientX">button(イベント)</button>

  <!-- 関数に引数を渡したいときは、（）にインラインハンドラーとして関数呼び出し式を書く -->
  <button @click="countUp($event, 5)">button(イベント)</button>

  <!-- .preventDefault()でデフォルトの挙動が起きなくできる -->
  <!-- 例）hrefで遷移できなくなる -->
  <button @click="$event.preventDefault()">button（イベント修飾子）</button>
  <a href="http://vuejs.org" @click="$event.preventDefault()">Vue.js（イベント修飾子）</a>
  <!-- @click.prevent="" でもOK！ ""の中に追加で挙動させたいコードを書ける-->

  <!-- .stopPropagation()で親の要素にクリックイベントが発生したことを電波させなくできる -->
  <div @click="count++">
    <button @click="$event.stopPropagation()">button(カウントアップしない)</button>
    <!-- @click.stop="" でもOK! ""の中に追加で挙動させたいコードを書ける-->
    <!-- @click.stop.prevent の様に連続して書いてもOK！ -->
  </div>

  <!-- @key.upでキーボードを押された時だけカウントされる .spade(スペースキー) .delete(削除キー) など追加もできる-->
  <div>
    <input type="text" @keyup.space.delete="count++" />
  </div>
</template>

<style>
h1 {
  color: red;
}
</style>
