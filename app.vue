<script setup lang="ts">
import { reactive, ref, defineProps, computed } from "vue";
const state = reactive({ count: 0 });
const increment = () => {
  state.count++;
};

const phrase = reactive({ name: "" });

const sayWords = () => {
  phrase.name = "Rene";
};

const song = ref<string>();
watch(song, (newName) => {
  localStorage.setItem("myName", newName);
});

onMounted(() => {
  song.value = localStorage.getItem("myName");
});
</script>
<template>
  <main>
    <h1>Vue basics</h1>
    <section id="reactive">
      <h2>Reacive</h2>
      <h3>From the vue website</h3>
      <button @click="increment" class="btn btn-blue">Update count</button>
      <p aria-live="polite">Current count is {{ state.count }}</p>
      <hr />
      <h3>My example</h3>
      <button @click="sayWords">Say hello</button>
      <p>Hello {{ phrase.name }}</p>
    </section>
    <section id="v-model">
      <h2>V-model</h2>
      <h3>My example</h3>
      What is your favourite song?
      <input type="text" name="my-model" v-model="song" />
      <p>Text will appear here {{ song }}</p>
    </section>
  </main>
</template>

<style lang="sass" scoped>
hr
  width: 100%

main
  display: flex
  flex-flow: column wrap
  align-items: center

#reactive
  .btn
    margin-inline: auto
    height: 1.75rem
    width: auto
    border: none
    border-radius: 5px
    cursor: pointer
    &.btn-blue
      color: #fff
      background-color: #369
      filter: grayscale(0)
      transition: filter 350ms ease-in, scale 250ms ease-out
      &:hover
        filter: grayscale(50%)
        scale: 1.1
      &:active
        background-color: #345698
        filter: grayscale(30%)
</style>
