<script setup>
import { reactive } from 'vue';
import  Cabecalho  from './components/Cabeca.vue'
import  Formulario  from './components/Formulario.vue'
import  ListaTarefas  from './components/ListaTarefas.vue'

  const estado = reactive ({
    filtro: 'todas',
    tarefaTemp: '',

    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false
      },
      {
        titulo: 'Estudar SASS',
        finalizada: true
      },
      {
        titulo: 'Estudar JAVA',
        finalizada: false
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estado;

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
      finalizada: false
    }

    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = ''
  }


</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value" />
    <ListaTarefas :tarefas="getTarefasFiltradas()" />

  </div>
</template>
