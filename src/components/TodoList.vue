<template>
  <div>
    <v-toolbar dark color="indigo">
          <v-toolbar-title class="white--text">Todo LIST</v-toolbar-title>
    </v-toolbar>
    <v-list>
        <template v-for="(todo, i) in todos">
            <!--  Duplicate keys detected を解決する -->
            <!-- https://qiita.com/ysKuga/items/fa2ba12b10bade86da36 -->
            <v-list-tile v-bind:key="`first-${i}`">
                <v-list-tile-content>
                （なまえ）: {{ todo.name }}, （しょうさい）: {{ todo.detail }}
                </v-list-tile-content>
                <v-list-tile-action>
                    <v-btn id="deleteCircleBtn" flat icon v-on:click="deleteTodo(i)">Delete</v-btn>
                </v-list-tile-action>
            </v-list-tile>
            <v-divider v-bind:key="`second-${i}`"></v-divider>
        </template>
    </v-list>

    <div class="bottom-right">
        <v-btn fab color="indigo" v-on:click="addTodo">
            <v-icon id="addBtn" color="white">ADD</v-icon>
        </v-btn>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            todos: []
        }
    },
    created(){
        this.todos = JSON.parse(localStorage.getItem('todos')) || [];
    },
    methods: {
      deleteTodo(i){
        let res = confirm('本当に消しますか？？')
        if(res == true){
        this.todos.splice(i, 1);
        localStorage.setItem('todos', JSON.stringify(this.todos));
        } else {
            alert("消すのをやめましたー！！")
        }
      },
      addTodo(){
          this.$router.push('/todos/add');
      }
    }
  }
</script>

<style scoped>
.bottom-right {
    position: fixed;
    bottom: 0px;
    right: 0px;
}
#deleteCircleBtn{
    /* padding-right: 60px; */
    width: 140px;
    color:red;
}
v-btn__contetnt {
    text-align: center;
}
#addBtn {
    font-size: 20px;
}
</style>