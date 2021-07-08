<template>
  <div class="container">
    <div class="columns is-centered">
      <div class="column is-6">
        <div class="box">
          <div class="content">
              <h1 class="title">Lista de Tarefas</h1>
              <label class="label">Tarefa</label>
              <div class="field has-addons">
                <input class="input" v-model="text" placeholder="Todo">
                <button class="button is-primary" v-on:click="addTodo(text)">Adicionar Tarefa</button>
              </div>
          </div>

          <table class="table is-fullwidth is-bordered">
            <thead>
              <tr>
                <th>Tarefa</th>
                <th>Status</th>
                <th>#</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(todo, index) in todos" :key="index">
                <td :class="{'is-success': todo.status === 'Concluída',
                              'is-warning ': todo.status ==='Em Progresso'}">
                    {{todo.text}}
                </td>
                <td style="width: 140px">
                  <div @click="changeStatus(index)" class="is-clickable">
                    {{todo.status}}
                  </div>
                </td>
                <td>
                  <div @click="deleteTodo(index)">
                    <i class="fas fa-trash"></i>
                  </div>
                </td>
              </tr>
              
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

  
</template>

<script>
export default {
  data() {
    return {
      availableStatus: ['Pendente', 'Em Progresso', 'Concluída'],

      todos: [{
        text: "Aprender VueJs",
        status: "Pendente",
      }],

    };

  },
  methods: {
    addTodo(text) {
      if (text !== " ") {
        this.todos.push({
          text,
          status: 'Pendente'
        });
      }
    },
    
    deleteTodo(index){
      this.todos.splice(index, 1);
    },

    changeStatus(index){
      let newIndex = this.availableStatus.indexOf(this.todos[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.todos[index].status = this.availableStatus[newIndex];
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .container {
    margin-top: 10%;
    
  }

  .is-clickable {
    cursor: pointer;
  }

</style>
