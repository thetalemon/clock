<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'

function notifyMe() {
  if (!('Notification' in window)) {
    // このブラウザはデスクトップ通知に対応していない
  } else if (Notification.permission === 'granted') {
    // 許可済
  } else if (Notification.permission !== 'denied') {
    Notification.requestPermission().then((permission) => {
      if (permission === 'granted') {
        // 許可されてないので許可を求める
      }
    })
  }
}

import { onMounted } from 'vue'
import { format } from 'date-fns'
import { ref } from 'vue'
const getCurrentDate = () => {
  const date = format(new Date(), 'yyyy-MM-dd hh:mm:ss')
  return date
}
const currentDate = ref(getCurrentDate())

onMounted(() => {
  notifyMe()
  setInterval(
    () => {
      currentDate.value = getCurrentDate()
    },
    // 1秒ごと
    1000
  )
})

const onClick = function () {
  new Notification('こんにちは！')
}
let a = 0
let id: any = undefined

var fn = function () {
  a += 10
  new Notification(`${a}経過しました`)
  id = setTimeout(fn, tm)
}
var tm = 10000

function clickStart() {
  a = 0
  id = setTimeout(fn, tm)
}

function clickStop() {
  clearTimeout(id)
}
</script>

<template>
  <header>
    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <div>
      <button @click="onClick">test</button>
      <button @click="clickStart">start</button>
      <button @click="clickStop">stop</button>
    </div>
    <p>通知オンオフ</p>
    <p>時報オンオフ</p>

    {{ currentDate }}
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
