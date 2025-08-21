<script lang="ts">
import type IReceitas from "@/interfaces/iReceitas";
import BotaoPrincipal from "./BotaoPrincipal.vue";
import { obterReceitas } from "@/http";

export default {
    data() {
        return {
            receitas: [] as IReceitas[]
        }
    },
    async created() {
        this.receitas = await obterReceitas();
    },
    emits: ['selecionarIngredientes'],
    components: { BotaoPrincipal }
}
</script>

<template>
    <section>
        <h1 class="cabecalho titulo-receitas">
            Receitas
        </h1>
        <p class="paragrafo-lg resultado">
            Resultados encontrados:
        </p>
        <p class="paragrafo-lg opcoes">
            Veja as opcoes de receitas com os ingredientes que voce tem por ai!
        </p>
        <ul class="receitas">
            <li v-for="receita in receitas" :key="receita.nome">
                <img :src="`/imagens/receitas/${receita.imagem}`" alt="Icones de imagens de cada receita"
                    class="recceitas__imagem" />
                <h2 class="paragrafo-lg receitas__nome">{{ receita.nome }}</h2>
            </li>
        </ul>

    </section>

    <BotaoPrincipal :texto="'Editar Lista'" @click="$emit('selecionarIngredientes')" />

</template>

<style scoped>

.titulo-receitas {
    color: var(--verde-medio, #3D6D4A);
    display: block;
    margin-bottom: 1.5rem;
}
  
.receitas {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.recceitas__imagem {
  width: 20rem;
}

</style>