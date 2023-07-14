<template>
  <section
    class="is-flex is-align-items-center is-justify-content-space-between"
  >
    <Cronometro :tempoEmSegundos="tempoEmSegundos" />
    <BotaoTemporizador
      @clicado="iniciar"
      icone="fas fa-play"
      texto="play"
      :desabilitado="cronometroRodando"
    />

    <BotaoTemporizador
      @clicado="finalizar"
      icone="fas fa-stop"
      texto="stop"
      :desabilitado="!cronometroRodando"
    />
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Cronometro from "./Cronometro.vue";
import BotaoTemporizador from "./BotaoTemporizador.vue";

export default defineComponent({
  name: "TemporizadorComponent",
  components: {
    Cronometro,
    BotaoTemporizador,
  },
  emits: ["aoTemporizadorFinalizar"],
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },
  methods: {
    iniciar() {
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
      this.cronometroRodando = true;
    },
    finalizar() {
      clearInterval(this.cronometro);
      this.cronometroRodando = false;
      this.$emit("aoTemporizadorFinalizar", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>
