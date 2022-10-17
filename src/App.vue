<script setup lang="ts">
import {ref} from 'vue'
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup

const intext = ref(null);
const outtext = ref(null);

function tojson(event:Event){
  const retlst = [];
  const arrs = intext.value.value.split("\n")
  const cols:string[] = arrs[0].split(",")
  for (let i = 1; i < arrs.length; i++) {
    let tempobj:Object = {}
    for (let j = 0;j<cols.length;j++){
      tempobj[cols[j] as keyof typeof tempobj]= arrs[i].split(",")[j]

    }
    retlst.push(JSON.stringify(tempobj))
  }
  console.log(retlst)

  outtext.value.value = "[" + retlst.toString() + "]"

}

function tocsv(event:Event){
  const jsarr = JSON.parse(intext.value.value)
  let csvstr = "" + Object.keys(jsarr[0])+"\n"
  for (let i = 0;i<jsarr.length;i++){
    csvstr = csvstr + Object.values(jsarr[i]).join(",") + "\n"
  }
  outtext.value.value = csvstr

}

</script>

<template>

  <p><label for="csvinput">CSV</label></p>
  <textarea title="input" ref="intext" id="input" rows="18" spellcheck="false"></textarea>


  <div>
    <button type="button" @click="tojson">Convert To JSON</button>
    <button type="button" @click="tocsv">Convert To CSV</button>
  </div>
  <div>
    <p><label for="output"> Output</label></p>
    <textarea title="output" ref="outtext" id="result" rows="18" spellcheck="false" disabled></textarea>
  </div>
</template>

<style scoped>

</style>
