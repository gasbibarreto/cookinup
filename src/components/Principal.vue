<script lang="ts">
import SelecionarIngredientes from "./SelecionarIngredientes.vue";
import SuaLista from "./SuaLista.vue";
import MostrarReceitas from "./MostrarReceitas.vue";

type Pagina = 'SelecionarIngredientes' | 'MostrarReceitas';

export default{
    data() {
        return {
            ingredientes: [] as string[],
            conteudo: 'SelecionarIngredientes' as Pagina
        };
    },
    methods:{
        adicionarIngrediente(ingrediente: string) {
            this.ingredientes.push(ingrediente)
        },
        
        removerIngrediente(ingrediente: string) {
            const newIngredientes = this.ingredientes.filter( el => 
                ingrediente !== el 
            )

            this.ingredientes = newIngredientes            
        },
        navegarPagina(pagina: Pagina) {
            this.conteudo = pagina
        }
    },
    emits: ['adicionarIngrediente', 'removerIngrediente', 'buscarReceitas'],
    components: { SelecionarIngredientes, SuaLista, MostrarReceitas }
}
    
</script>

<template>
<main class="conteudo-principal">
    <SuaLista :ingredientes= "ingredientes" />

    <SelecionarIngredientes v-if="conteudo === 'SelecionarIngredientes'"
        @adicionar-ingrediente="adicionarIngrediente"
        @remover-ingrediente="removerIngrediente"
        @buscar-receitas="navegarPagina('MostrarReceitas')"
        />
    
    <MostrarReceitas v-else-if="conteudo === 'MostrarReceitas'"  />
</main>         
</template>

<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #FFFAF3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}



</style>