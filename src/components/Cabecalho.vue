<script setup>

    const props = defineProps (['tarefaPendente'])

</script>


<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <p><!-- Acessa o retorno, que é um array. E através dele temos acesso ao atributo length -->
            Você possui {{ props.tarefaPendente }} tarefas pendentes
        </p>
    </header>
</template>