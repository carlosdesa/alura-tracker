<script lang="ts">
import BarraLateral from "./components/BarraLateral.vue";
import FormularioCentral from "./components/FormularioCentral.vue";
import ItemTarefa from "./components/ItemTarefa.vue";
import type ITarefa from "./interfaces/ITarefa";
import BoxVue from "./components/BoxVue.vue";

import { defineComponent } from "vue";

export default defineComponent({
  name: "RelogioCronometro",
  components: {
    BarraLateral,
    FormularioCentral,
    ItemTarefa,
    BoxVue,
  },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false,
      modoEscuro: "",
    };
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0;
    },
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;
    },
  },
});
</script>

<template>
  <main
    class="columns is-gapless is-multiline"
    :class="{ 'modo-escuro': modoEscuroAtivo }"
  >
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioCentral @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <ItemTarefa
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
        <BoxVue v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(</BoxVue
        >
      </div>
    </div>
  </main>
</template>

<style scoped>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}
.conteudo {
  background-color: var(--bg-primario);
}
</style>
