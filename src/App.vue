<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

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

onMounted(() => {
  console.log('a')
  notifyMe()
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
    <button @click="onClick">test</button>
    <button @click="clickStart">start</button>
    <button @click="clickStop">stop</button>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
