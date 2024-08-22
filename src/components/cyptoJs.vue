<script setup lang="ts">
import { ref } from 'vue'
import CryptoJS from 'crypto-js'

defineProps<{ msg: string }>()

const count = ref(0)
const file1 = ref()
const file2 = ref()

function onFileChange1(e:any) {
  const files = e.target.files;
  if (files && files.length) {
    file1.value = files[0]
  }
}
function onFileChange2(e:any) {
  const files = e.target.files;
  if (files && files.length) {
    file2.value = files[0]
  }
}
async function calculateFileHash(file:any) {  
  return new Promise((resolve, reject) => {  
    // 读取文件的buffer
    const reader = new FileReader();  
    reader.onload = (e:any) => {  
      const wa = CryptoJS.lib.WordArray.create(e.target.result);
      resolve(CryptoJS.SHA256(wa).toString());  
    };  
    reader.onerror = error => reject(error);  
    reader.readAsArrayBuffer(file);  
  });  
}

async function compareFiles() {  
  try {  
    const [file1r, file2r] = await Promise.all(  
      [file1.value,file2.value].map((file:any) => calculateFileHash(file))  
    );
    console.log('%c [ file1r, file2r ]-39', 'font-size:13px; background:pink; color:#bf2c9f;', file1r == file2r)
  } catch (error) {  
    console.error('计算文件哈希时出错:', error);  
  }  
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <input type="file" @change="onFileChange1" ref="fileInput" />
  <input type="file" @change="onFileChange2" ref="fileInput" />

  <button type="button" @click="count++">count is {{ count }}</button>
  <button type="button" @click="compareFiles">比较</button>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
