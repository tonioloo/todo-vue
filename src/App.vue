<script setup>
  import { reactive } from "vue";
  import cabecalho from "./components/cabecalho.vue";
  import Formulario from "./components/Form"
  import ListaDeTarefas from "./components/ListaDeTarefas.vue"

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6+',
        finzalizada: false
      },
      {
        titulo: 'Estudar SASS',
        finzalizada: false
      },
      {
        titulo: 'Ir para a academia',
        finzalizada: true,
      },
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finzalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finzalizada)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finzalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = '';
  }  
  
</script>

<template>
  <div class="container">
    <Cabecalho />
    <Formulario />
    <ListaDeTarefas />
  </div>  
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
