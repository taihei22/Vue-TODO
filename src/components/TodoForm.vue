<template>
  <div>
    <v-toolbar dark color="indigo">
        <router-link to="/">
            <v-icon>arrow_back</v-icon>
        </router-link>
        <v-toolbar-title class="white--text">Todo ADD</v-toolbar-title>
    </v-toolbar>
    <v-text-field v-model="newTodo.name" placeholder=" Input Name here ..."></v-text-field>
    <v-text-field v-model="newTodo.detail" placeholder=" Input Detail here ..."></v-text-field>
    <v-btn dark color="indigo" v-on:click="addTodo()" class="white--text">Add</v-btn>
  </div>
</template>

<script>
  export default {
    data(){
      return{
        newTodo: {name:'', detail:''}
      }
    },
    methods: {
      addTodo(){
        // 何も入力されていなければ、処理をしない
        if(this.newTodo === "") return;
        const todos = JSON.parse(localStorage.getItem('todos')) || [];
        todos.push(this.newTodo);
        localStorage.setItem('todos', JSON.stringify(todos));
        this.newTodo = "";
        this.$router.push('/');
      }
    }
  }
</script>

<style scoped>
a {
    text-decoration: none;
}
.v-text-field {
    margin-left: 10px
}
</style>