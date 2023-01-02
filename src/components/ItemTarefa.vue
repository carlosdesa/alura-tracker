<template>
  <BoxVue>
    <div class="columns">
      <div class="column is-7">
        {{ tarefa.descricao || "Tarefa sem descrição" }}
      </div>
      <div class="column">
        <RelogioCronometro :tempo-em-segundos="tarefa.duracaoEmSegundos" />
      </div>
    </div>
  </BoxVue>
</template>

<script lang="ts">
import type ITarefa from "@/interfaces/ITarefa";
import type { PropType } from "vue";
import { defineComponent } from "vue";
import RelogioCronometro from "./RelogioCronometro.vue";
import BoxVue from "./BoxVue.vue";

export default defineComponent({
  name: "ItemTarefa",

  data() {
    return {};
  },
  components: {
    RelogioCronometro,
    BoxVue,
  },
  props: {
    tarefa: {
      type: Object as PropType<ITarefa>,
      required: true,
    },
  },
  mounted() {},

  methods: {},
});
</script>

<style scoped></style>
