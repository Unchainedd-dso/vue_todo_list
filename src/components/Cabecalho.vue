<script setup>
    // Abreviação de proprities
    // Define todos os valores que vem da função principal, como atributos
    const props = defineProps(['numeroJogosPendentes'])
</script>

<template>
    <header class="p-5 my-4 bg-light rounded-3">
        <h1>Meus Jogos</h1>
        <p>
            Você ainda possui {{ props.numeroJogosPendentes}} jogos à completar
        </p>
    </header>
</template>