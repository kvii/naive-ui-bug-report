<script setup lang="ts">
import { NTree } from "naive-ui";
import { ref } from 'vue';

const show = ref(false)

const code = `
<NTree
    v-if="show"
    :data="[]"
    pattern="foo"
/>`
</script>

<template>
  <section class="my-container">
    <div>
      <pre> {{ code }} </pre>
    </div>

    <div>
      <button @click="show = !show">show = !show</button>
    </div>

    <NTree
      v-if="show"
      :data="[]"
      pattern="foo"
    />

    <img src="./error.png">
  </section>
</template>

<style>
.my-container {
  width: 600px;
  padding: 24px;
  margin: auto;
  display: flex;
  flex-direction: column;
}
</style>