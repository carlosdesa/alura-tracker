<template>
  <button
    class="button"
    @click="emitAction"
    :disabled="cronometroRodandoComputed"
  >
    <span>{{ actionType }}</span>
  </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "BotaoGenerico",

  props: {
    actionType: {
      type: String,
      default: "",
    },
    cronometroRodando: {
      type: Boolean,
      default: false,
    },
  },

  computed: {
    cronometroRodandoComputed() {
      return this.actionType === "play"
        ? this.cronometroRodando
        : !this.cronometroRodando;
    },
  },

  mounted() {},
  emits: ["actionEmitted"],

  methods: {
    emitAction() {
      this.$emit("actionEmitted", this.actionType);
    },
  },
});
</script>

<style lang="scss" scoped></style>
