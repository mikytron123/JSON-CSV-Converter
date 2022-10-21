<script setup lang="ts">
import {ref} from 'vue'
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup

const intext = ref("");
const outtext = ref("");

function tojson(event:Event){
  const retlst = [];
  const arrs = intext.value.split("\n")
  const cols:string[] = arrs[0].split(",")
  for (let i = 1; i < arrs.length; i++) {
    let tempobj:Object = {}
    for (let j = 0;j<cols.length;j++){
      tempobj[cols[j] as keyof typeof tempobj]= arrs[i].split(",")[j]

    }
    retlst.push(JSON.stringify(tempobj))
  }
  console.log(retlst)

  outtext.value = "[" + retlst.toString() + "]"

}

function tocsv(event:Event){
  const jsarr = JSON.parse(intext.value)
  let csvstr = "" + Object.keys(jsarr[0])+"\n"
  for (let i = 0;i<jsarr.length;i++){
    csvstr = csvstr + Object.values(jsarr[i]).join(",") + "\n"
  }
  outtext.value = csvstr

}

</script>

<template>
  
  <h1>JSON/CSV Data Converter</h1>
  <p><label for="csvinput">Input</label></p>
  <textarea title="input" v-model="intext" id="input" rows="18" spellcheck="false"></textarea>


  <div>
    <button type="button" @click="tojson">Convert To JSON</button>
    <button type="button" @click="tocsv">Convert To CSV</button>
  </div>
  <div>
    <p><label for="output"> Output</label></p>
    <textarea title="output" v-model="outtext" id="result" rows="18" spellcheck="false" disabled></textarea>
  </div>
</template>

<style scoped>

</style>
