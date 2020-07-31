<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr width="20%">

    <form class="form-group" id="todoForm" @submit.prevent="addTodo()">
      <div class="form-group">
        <label for="newTodo">New Item</label>
        <input type="text" class="form-control" id="newTodo" name="newTodo" aria-describedby="new todo item"
               placeholder="Enter your todo item here..."  v-model="newTodo">
        <small id="emailHelp" class="form-text text-muted">never forget your tasks again.</small>
        <button class="btn btn-primary btn-sm mt-2" type="submit">add</button>
      </div>
    </form>

    <div class="todoList" v-if="this.todoList.length != 0">
      <h6>Todo List</h6>
      <ul class="list-group">
        <li class="list-group-item" v-for="(item, index) in todoList" v-bind:key="item.title">
          <button v-if="!item.done"
                  class="btn btn-primary btn-sm mr-2"
                  @click="markDone(item)"><i class="fa fa-check"></i></button>
          <span :class="{done: item.done}"> {{ item.title }} </span>
          <button class="btn btn-danger btn-sm float-right"
                  @click="removeItem(index)"
          ><i class="fa fa-trash"></i></button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  data() {
    return {
      newTodo: '',
      todoList: JSON.parse(localStorage.todos),
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo !== '') {
        this.todoList.push({
          title: this.newTodo,
          done: false
        });
        this.newTodo = '';
      }
    },
    markDone(todo) {
      todo.done = true;
    },
    removeItem(index) {
      this.todoList.splice(index, 1);
    },
  },
  props: {
    msg: String
  },
  watch: {
    todoList: {
      handler() {
        localStorage.todos = JSON.stringify(this.todoList);
      },
      deep: true
  },
    deep: true
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #todoForm {
    width: 30%;
    margin:  2% auto 0;
    text-align: left;
  }

  .todoList {
    text-align: left;
    width: 30%;
    margin: 2% auto 0;
  }

  .todoList button{
    padding-top: 0;
    padding-bottom: 0;
    margin-top: 0;
    margin-bottom: 0;
  }

  .done {
    text-decoration: line-through ;
  }
</style>
