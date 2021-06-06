<template>
  <textarea @change="convert" v-model="inputText"></textarea>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { pulldown_cmark } from '../wasm-markdown/pkg/wasm_markdown';

let wasmContainer: { pulldown_cmark: typeof pulldown_cmark };
import('../wasm-markdown/pkg').then(wasm => (wasmContainer = wasm));

export default defineComponent({
  name: 'App',
  components: {},
  setup() {
    const inputText = ref('');
    const convert = () => {
      console.log(wasmContainer?.pulldown_cmark(inputText.value));
    };
    return { convert, inputText };
  },
});
</script>