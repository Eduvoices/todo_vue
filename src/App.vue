<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';


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
    <Cabecalho tarefas-pendentes="10" />
    <Formulario/>
    <ListaDeTarefas/>
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
