<template>
  <RelogioCronometro :tempoEmSegundos="tempoEmSegundos" />
  <BotaoGenerico
    actionType="play"
    :cronometroRodando="cronometroRodando"
    @actionEmitted="executeAction"
  />
  <BotaoGenerico
    actionType="stop"
    :cronometroRodando="cronometroRodando"
    @actionEmitted="executeAction"
  />
  <!-- <button class="button" @click="iniciar" :disabled="cronometroRodando">
    <span>play</span>
  </button>
  <button class="button" @click="finalizar" :disabled="!cronometroRodando">
    <span>stop</span>
  </button> -->
</template>

<script lang="ts">
import { defineComponent } from "vue";
import RelogioCronometro from "@/components/RelogioCronometro.vue";
import BotaoGenerico from "./BotaoGenerico.vue";

export default defineComponent({
  name: "ControladorDeTempo",
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },
  components: {
    RelogioCronometro,
    BotaoGenerico,
  },
  emits: ["aoTempoFinalizado"],
  methods: {
    executeAction(actionType: string): void {
      actionType === "play" ? this.iniciar() : this.finalizar();
    },
    iniciar() {
      this.cronometroRodando = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    finalizar() {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
      this.$emit("aoTempoFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>

<style lang="scss" scoped></style>
