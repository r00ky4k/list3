<template>
  <div id="app">
    <h1>Список заданий</h1>
    <input v-model="message">
    <p></p>
    <button v-on:click="AddTodo"> Добавить задание </button>
    <p></p>

    <hr>

    <div v-for="(message, i) in todos" :key="i">
     <p>
        <span>{{i+1+") "}}</span>
        <span>{{ message+"   " }}</span>
        <button v-on:click="DeleteTodo"> Выполнил </button>
     </p>
    </div>


  </div>

</template>


<script>

export default {
  name: "app",
  components: {

  },
  data: function () {
    return {
      title: "todoapp",
      message: "",
      date: '',
seen: true,
todos: [],
    };
  },

  computed: {

  },

  async mounted () {
    const data = await localStorage.getItem('todos')
    this.todos = JSON.parse(data)
  },

  methods: {
    AddTodo()  {
      let message = this.message+' | '+this.getDate() ;
      this.todos.push(message);
      this.message = "";
      localStorage.setItem('todos',JSON.stringify(this.todos))
      false
    },

    DeleteTodo(index){
      this.todos.splice(index, 1);
      localStorage.setItem('todos',JSON.stringify(this.todos))
    },

    getDate(){
      let date = new Date();
      let formatDate =+date.getHours()+':'+date.getMinutes()+':'+date.getSeconds()+' | '+date.getDate() +'.'+ (date.getMonth()+1)+'.'+ date.getFullYear();

      return formatDate;
    },
  },

  created: function () {

  },

  watch: {},



};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
