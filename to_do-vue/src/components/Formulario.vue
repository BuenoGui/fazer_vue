<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">

            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required
                    type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
            </div>

            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">
                    Cadastras
                </button>
            </div>

            <div @change="props.trocarFiltro" class="col-md-2">
                <select class="form-control">
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Tarefas Pendentes</option>
                    <option value="finalizadas">Tarefas Feitas</option>
                </select>
            </div>

        </div>
    </form>
</template>