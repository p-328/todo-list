<template>
  <div class="content">
   <!-- TODO: Implement Search functionality for todos -->
    <div class="list-border">
      <h1>Todo List</h1>
      <ul class="list">
        <li v-for="item in todos" v-bind:key="item.id" class="item">
          <p>{{item.task}}</p>
          <button class="btn-submit" @click="removeTodo(item.id)">Delete</button>
        </li>
      </ul>
      <br>
      <input type="text" v-model="todoBuffer">
      <br>
      <button @click="createTodo()" class="btn-submit">Create Todo</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyList',
  data() { 
    return {
      todos: Array(0),
      todoBuffer: '',
      storageKey: 'todos',
      searchResults: [],
      searchRegex: ''
    }
  },
  methods: {
    createTodo() {
      if (this.todoBuffer != '') { 
        this.todos.push({ id: Math.random(), task: this.todoBuffer });
      }
      localStorage.setItem(this.storageKey, JSON.stringify(this.todos));
      this.todoBuffer = '';
    },
    removeTodo(id) { 
      this.todos = this.todos.filter(item => item.id !== id);
      localStorage.setItem(this.storageKey, JSON.stringify(this.todos));
    }
  },
  mounted() { 
    const items = JSON.parse(localStorage.getItem(this.storageKey));
    if (items != null) { 
      this.todos = items;
    }
  }
}
</script>

<style scoped>
  @font-face {
    font-family: 'IBM Plex';
    src: url('../assets/IBMPlexSans-Regular.ttf') format('truetype');
  };
  
  .list-border {
    border-style: solid;
    width: 40%;
    margin: 0 auto;
    font-family: 'IBM Plex';
  };
  .content {
    display: flex;
    justify-content: center;
  }
  .list {
    list-style: none;
    margin: 10px;
  }
  .btn-submit {
    font-family: 'IBM Plex';
    color: rgb(147, 147, 147);
    background-color: black;
    border-radius: 4px;
    width: 40%;
    height: 5%;
    display: flex;
  };
  .btn-submit:hover {
    color: rgb(245, 13, 13);
  };
  .btn-submit:active {
    color: white;
  };
  
  .item {
    border: 4px solid black;
    border-radius: 4px;
  };
  
</style>
