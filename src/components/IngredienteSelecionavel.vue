<script lang="ts">
import Tag from "./Tag.vue";

export default {
    components: { Tag },
    props: {
        texto: { type: String, required: true }
    },
    data() {
        return {
            selecionado: false
        };
    },
    methods: {
        toggleSelecionado() {
            this.selecionado = !this.selecionado;
            if (this.selecionado) {
                this.$emit('adicionarIngrediente', this.texto)
            } else {
                this.$emit('removerIngrediente', this.texto)
            }
        }
    },
    emits:['adicionarIngrediente', 'removerIngrediente']
}
</script>

<template>
    <button class="ingrediente" @click="toggleSelecionado">
        <Tag :texto="texto" :ativa="selecionado" />
    </button>
</template>

<style scoped>
.ingrediente {
    cursor: pointer;
}

.ingrediente:focus {
    outline: none;
}
</style>