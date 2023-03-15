<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemporaria: '',
    tarefas: [
      {
        tarefa: 'Estudar Es6',
        completa: false
      },
      {
        tarefa: 'Estudar SASS',
        completa: false,
      },
      {
        tarefa: 'Ir à academia',
        completa: true
      }
    ]
  })

  const getTarefasPendentes =() => {
    return estado.tarefas.filter(tarefa => tarefa.completa === false)
  }

  const getTarefasFinalizadas =() => {
    return estado.tarefas.filter(tarefa => tarefa.completa === true)
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estado //usando a desestruturação

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes()

      case 'finalizadas':
        return getTarefasFinalizadas()

      default:
        return estado.tarefas
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      tarefa: estado.tarefaTemporaria,
      completa: false
    }

    estado.tarefas.push(tarefaNova)

    estado.tarefaTemporaria = ''
  }

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-5 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" required type="text" placeholder="Digite sua tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.completa = evento.target.checked" :checked="tarefa.completa" :id="tarefa.tarefa" type="checkbox">
        <label :class="{done: tarefa.completa === true}" class="ms-3" :for="tarefa.tarefa">
          {{ tarefa.tarefa }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
