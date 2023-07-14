<template>
  <article>
    <strong class="display">{{ tempoDecorrido }}</strong>
  </article>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "cronometroComponent",

  props: {
    tempoEmSegundos: {
      type: Number,
      default: 0,
    },
  },

  computed: {
    tempoDecorrido(): string {
      return new Date(this.tempoEmSegundos * 1000).toISOString().slice(11, 19);
    },
  },
});
</script>

<style scoped>
.display {
  color: var(--texto-primario);
  background-color: var(--bg-primario);
}
</style>
