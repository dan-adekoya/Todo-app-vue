<template>
  <div id="Todo">
    <h1>Todo-App</h1>
    <form @submit.prevent="add">
      <input v-model="NTodo" @submit="prevent" ref="input" type="text" placeholder="What you doing ?">
      <button class="submit" type="submit">Task</button>
      <button class="clear" type="reset">Clear Input</button>
      <button class="clear" type="reset"  @click="removeAll()">Clear All Todos</button>
    </form>
    <ul>
      <li v-for="todo in todos" :key="todo">{{todo.title}} <button @click="remove(todo)" class="submit">Done</button></li>
      <!-- <li>Walk Dog <button class="submit">Done</button></li>
      <li>Walk Dog <button class="submit">Done</button></li> -->
    </ul>
  </div>
</template>

<script> 
export default {
  data(){
    return{
      NTodo:'',
      todos:[],
    }
  },
  methods: {
    add(){
      this.todos.push({
        title: this.NTodo
      })
      this.NTodo = ''
    },
    remove(todo){
        let todoIndex = this.todos.indexOf(todo)
        this.todos.splice(todoIndex, 1)
    },
    removeAll(){
        this.todos.splice(0)
    },
    clear(){
      this.NTodo = ''
    },
    prevent(){
      if(this.$refs.input.value == ""){
        this.todo = false
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#Todo{
  font-family: 'roboto'
}
h1{
  text-align: center;
  margin: 10px 0;
  font-weight: 500;
  color: #000000;
  opacity: 60%;
}
form{
  width: 80%;
  margin: auto;
  display: flex;
  margin-top: 50px;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap
}
form button{
  margin: 10px;
}
button{
  cursor: pointer;
}
form .submit,.submit{
  padding: 10px 30px;
  border: none;
  font-size: 17px;
  border-radius: 10px;
  color: #FFFFFF;
  background: #25f60091; 
  outline: none;
}
form .clear{
  padding: 10px 30px;
  border: none;
  font-size: 17px;
  border-radius: 10px;
  color: #FFFFFF;
  background: #f6000086; 
  outline: none;
}
::placeholder{
  font-size: 17px;
  color: #B0B0B0;
}
form input{
  padding: 10px 30px;
  border: 1px solid #D7D7D7;
  font-size: 17px;
  border-radius: 10px;
  outline: none;
}
ul{
  width: 80%;
  margin: 50px auto;
}
ul li{
  width: 90%;
  margin: 30px auto;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  padding: 5px;
  transition: all .4s;
  color: #9A9A9A;
  justify-content: space-between;
  border-radius: 10px;
  opacity: 1;
  border: 1px solid #D7D7D7;
  animation: added .4s 0s 1 forwards

}
@keyframes added {
  from{
    opacity: 0;
    transform: translateX(-50px);
  }
  to{
    transform: translateX(0px);
    opacity: 1;
  }
}
@keyframes remove {
  from{
    opacity: 0;
    transform: translateX(0px);
  }
  to{
    transform: translateX(-50px);
    opacity: 1;
  }
}
</style>
