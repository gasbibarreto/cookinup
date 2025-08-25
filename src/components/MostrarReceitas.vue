<script lang="ts">
import type IReceitas from "@/interfaces/iReceitas";
import BotaoPrincipal from "./BotaoPrincipal.vue";
import { obterReceitas } from "@/http";
import type { PropType } from "vue";

export default {
    props: {
        ingredientes: {
            type: Array as PropType<string[]>,
            required: true
        }
    },
    data() {
        return {
            receitas: [] as IReceitas[],
        }
    },
    async created() {
        const buscarReceitas = await obterReceitas();

        this.receitas = buscarReceitas.filter(receita => {
            return receita.ingredientes.some(ingrediente => 
                this.ingredientes.includes(ingrediente)
            )
        });

    },
    emits: ['selecionarIngredientes'],
    components: { BotaoPrincipal }
}
</script>

<template>
    <section class="mostrar-receitas">
        <h1 class="cabecalho titulo-receitas">
            Receitas
        </h1>
        <p class="paragrafo-lg resultados">
            Resultados encontrados: {{ receitas.length }}
        </p>
        <p class="paragrafo-lg informacoes">
            Veja as opcoes de receitas com os ingredientes que voce tem por ai!
        </p>
        <div v-if="receitas.length">
            <ul class="receitas">
                <li v-for="receita in receitas" :key="receita.nome">
                    <img :src="`/imagens/receitas/${receita.imagem}`" alt="Icones de imagens de cada receita"
                        class="recceitas__imagem" />
                    <h2 class="paragrafo-lg receitas__nome">{{ receita.nome }}</h2>
                </li>
            </ul>
        </div>
        <div v-else class="receitas-nao-encontradas">
            <p class="paragrafo-lg receitas-nao-encontradas__info">
                Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?
            </p>

            <img src="../assets/imagens/sem-receitas.png"
                alt="Desenho de um ovo quebrado. A gema tem um rosto com uma expressão triste.">


        </div>

    </section>

    <BotaoPrincipal :texto="'Editar Lista'" @click="$emit('selecionarIngredientes')" />

</template>

<style scoped>
.mostrar-receitas {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.resultados {
    color: var(--verde-medio, #3D6D4A);
    margin-bottom: 0.5rem;
}   

.titulo-receitas {
    color: var(--verde-medio, #3D6D4A);
    display: block;
    margin-bottom: 1.5rem;
}

.informacoes {
    margin-bottom: 2rem;
}

.receitas {
    margin-bottom: 2rem;
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}

.receitas li {
    padding-bottom: 2.5rem;
    border-radius: 1rem;
    background: var(--branco, #FFF);
    box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
    height: 100%;

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
}

.receitas h2 {
    font-size: medium;
}

.recceitas__imagem {
    width: 20rem;
    border-top-right-radius: 1rem;
    border-top-left-radius: 1rem;
}

.receitas-nao-encontradas {
    margin-bottom: 2rem;
}

.receitas-nao-encontradas__info {
    margin-bottom: 0.5rem;
}
</style>