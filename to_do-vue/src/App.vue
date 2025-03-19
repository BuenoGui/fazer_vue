<script setup>
import { reactive } from 'vue';

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
    <header class="p-5 mg-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você tem {{  getTarefasPendentes().length }} tarefas pendentes</p>
    </header>

    <form @submit.prevent="cadastraTarefa">
      <div class="row">

        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>

        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">
            Cadastras
          </button>
        </div>

        <div  @change="evento => estado.filtro = evento.target.value" class="col-md-2">
          <select class="form-control">
              <option value="todas">Todas Tarefas</option>
              <option value="pendentes">Tarefas Pendentes</option>
              <option value="finalizadas">Tarefas Feitas</option>
            </select>
        </div>

      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada === true}" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo}}
        </label>
      </li>
    </ul>

  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
