<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';


const estado = reactive({
  filtro:'todas',
  tarefaTemp:"",
  tarefas:[{
    titulo:'Estudar ES6',
    finalizada:false,
  },
  {
    titulo:'Estudar SAAS',
    finalizada:false,
  },
  {
    titulo:'Ir para academia',
    finalizada:true,
  }]
})

const getTarefasPendentes = () => {
  //Filtrar tarefas
  return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
}

const getTarefasFinalizadas = () => {
  //Filtrar tarefas
  return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
}

const getTarefasFiltradas = () => {
  //Recuperar o Filtro
  const filtro = estado.filtro;

  switch(filtro){
    case 'pendentes':
      return  getTarefasPendentes();
    case 'finalizadas':
    return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

//Adicionar tarefa
/*Antes de fazer o push, precisamos armazenar o nome que o usuario digitar no campo para uma propriedade de um estado*/

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo:estado.tarefaTemp,
    finalizada:false,
  }

  estado.tarefas.push(tarefaNova);

  //Limpa input após envio da tarefa nova.
  estado.tarefaTemp="";
}

</script>

<template>
  <div class="container">

    <Cabecalho :tarefaPendente="getTarefasPendentes().length" />
    <Formulario :trocarFiltro="evento => estado.filtro = evento.target.value" :tarefaTemp="estado.tarefaTemp" :editaTarefaTemp="evento => estado.tarefaTemp = evento.target.value"  :cadastraTarefa="cadastraTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>    

  </div>
    
</template>


