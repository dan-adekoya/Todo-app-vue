<template>
  <div id="Todo">
    <h1>Todo-App</h1>
    <form @submit.prevent="add">
      <div>
        <input v-model="empty" @submit="add" ref="input" type="text" placeholder="What you doing ?">
        <p v-if="error" class="error">Input a Todo</p>
      </div>
      <button class="submit" type="submit">Task</button>
      <button class="clear" type="reset">Clear Input</button>
      <button class="clear" type="reset"  @click="removeAll()">Clear All Todos</button>
    </form>
    <ul>
      <li v-for="todo in todos" :key="todo">{{todo.title}} <button @click="remove(todo)" class="submit">Done</button></li>
    </ul>
    <a href="https://github.com/devdanielcodes/Todo-app-vue" target="_blank">Repo Link</a>
  </div>
</template>

<script> 
export default {
  data(){
    return{
      empty: '',
      todos:[],
      error: false
    }
  },
  methods: {
    add(){
      if(this.empty == ''){
        this.error = true
      }else{
        this.todos.push({
        title: this.empty
        })
        this.empty = ''
        this.error = false
      }
      
    },
    remove(x){
        let todoIndex = this.todos.indexOf(x)
        this.todos.splice(todoIndex, 1)
    },
    removeAll(){
        this.todos.splice(0)
    },
    clear(){
      this.empty = ''
      this.empty.focus()
    },
    /* prevent(){
      if(this.todos.title == ''){
        this.stop()
      }
    } */
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*{
  font-family: 'roboto', sans-serif;
}
h1{
  text-align: center;
  margin: 10px 0;
  font-weight: 500;
  font-size: 50px;
  color: #000000;
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
  margin-bottom: 10px;
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
.error{
  color: red;
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
a{
  position: fixed;
  bottom: 5px;
  right: 10px;
  padding: 10px;
  color: white;
  text-decoration: none;
  border-radius: 10px;
  background: rgb(0, 174, 255);
}
</style>
