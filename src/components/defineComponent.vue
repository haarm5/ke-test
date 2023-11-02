<script lang="ts">
import { constants } from 'buffer'
import { defineComponent, ref } from 'vue'
const myname = ref('Nok')
const msg = ref('Hello World!')
</script>

<template>
  <h1>สวัสดีชาวโลก</h1>
  <h2>นี่ Vue นะจะใครละ</h2>
  <h3>นี้เรา {{ myname }} นะ</h3>
  <h1>{{ msg }}</h1>
</template>
