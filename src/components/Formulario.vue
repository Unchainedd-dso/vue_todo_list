<script setup>
// Define as propriedades que o componente recebe do pai
const props = defineProps(['noEnvio', 'nomeJogo', 'filtro']);

// Define os eventos que o componente pode emitir para o pai
// Em vez de usar o nome da variável em si, o que causaria uma confusão no vue, visto que não podemos mudar o valor de uma prop, convencionou-se em usar 'update:<valor_propriedade>'
// Assim, ela envia o seu valor para a mesma variável sem confusoes, igual no v-model
const emit = defineEmits(['update:nomeJogo', 'update:filtro']);
</script>

<template>
    <!-- Previne o comportamento padrão do formulário (recarregar a página) e chama a função 'noEnvio' recebida como prop -->
    <form @submit.prevent="props.noEnvio">
        <div class="row">
            <div class="col-md-9">
                <!-- Campo de entrada de texto para o nome do jogo -->
                <!-- Define o valor do campo com a prop 'nomeJogo' -->
                <!-- Emite um evento para atualizar 'nomeJogo' no componente pai, visto que a função java está nele -->
                <!-- v-model é substituido pelo :value e pelo @input -->
                <input 
                    :value="props.nomeJogo" 
                    @input="emit('update:nomeJogo', $event.target.value)" 
                    type="text" 
                    class="form-control" 
                    placeholder="Digite o nome do jogo aqui" 
                    required> 
            </div>
            <div class="col-md-3 d-flex">
                <button type="submit" class="btn btn-primary me-2">Cadastrar</button>
                <!-- Define o valor selecionado com a prop 'filtro' -->
                <!-- Emite um evento para atualizar 'filtro' no componente pai -->
                <select 
                    :value="props.filtro"
                    @change="emit('update:filtro', $event.target.value)"  
                    class="form-control w-auto">
                    <option value="todosJogos">Todos os jogos</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="completos">Completos</option>
                </select>
            </div>
        </div>
    </form>
</template>
