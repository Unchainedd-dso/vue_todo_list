<script setup>
    // Abreviação de proprities
    // Define todos os valores que vem da função principal, como atributos
    const props = defineProps(['jogosFiltrados', 'removeJogo'])
</script>

<template>
    <!-- list-group-flush remove as bordas lateris e superiores -->
    <ul class="list-group list-group-flush mt-3">
        <li class="list-group-item d-flex" v-for="jogo in props.jogosFiltrados" :key="jogo.id">
            <!-- Todas as alterações são feitas no elemento pai -->
            <input v-model="jogo.finalizado" type="checkbox" class="form-check-input me-3" :id="jogo.id">
            <label :for="jogo.id" class="w-100" :class="{jogoTerminado: jogo.finalizado}">
                {{ jogo.nome }}
            </label>
            <button class="btn-close" @click="props.removeJogo(jogo)"></button>
        </li>
    </ul>
</template>