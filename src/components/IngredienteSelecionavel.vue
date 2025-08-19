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
        }
    }
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