<script setup lang="ts">
import { ref } from 'vue'
import * as fs from 'fs'
import * as path from 'path'

defineProps<{ msg: string }>()

const fileArr = ref<string[]>([])

// 读取文件目录
let _fs: typeof fs = window.require('fs')
let _path: typeof path = window.require('path')
console.log(_path.join(__dirname,'../../'))
const readDir =() =>{
  _fs.readdir(_path.join(__dirname,'../../../../../../../../'),(err: NodeJS.ErrnoException | null, files: string[])=>{
      console.log(files)
      fileArr.value.push(...files)
  })
}
</script>

<template>
  <h1>{{ msg }}</h1>

  <p>
    Recommended IDE setup:
    <a href="https://code.visualstudio.com/" target="_blank">VSCode</a>
    +
    <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
  </p>

  <p>See <code>README.md</code> for more information.</p>

  <p>
    <a href="https://vitejs.dev/guide/features.html" target="_blank">
      Vite Docs
    </a>
    |
    <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Docs</a>
  </p>

  <br>
  <button @click="readDir">read current project dir files</button>
  <p v-for="item,index in fileArr" :key="index">{{item}}</p>
  <p>
    Edit
    <code>components/HelloWorld.vue</code> to test hot module replacement.
  </p>
</template>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
