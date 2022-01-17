<template>
  <div class="about container mt-5">
    <h4 class="mx-3">Todos</h4>
    
   
    <div class="row">
      <div class=" col-lg-6 col-sm-12">
       <div class="row">
          <div class="col-12 my-3">
            <div class="mx-3 shadow my-3 py-4 p-3 align-self-center text-dark" 
            v-for="(todo,index) in todos" :key="index"
            :class="{'bg-green' : todo.done}">
              <div class="row">
                <div class="col-9">
                  <span><b>{{todo.text}}</b></span> <br>
                  <small>{{todo.createdAt.toString()}}</small>
                </div>
                <div class="col-3 align-self-center">
                    <div class="row justify-content-center">
                        <div class="col-4 align-self-center text-success" v-if="!todo.done" @click="markAsDone(index)"><i>&check;</i></div>
                        <div class="col-4 align-self-center text-warning" v-else  @click="markAsunDone(index)"><i>re</i></div>
                        <div class="col-4 align-self-center text-danger" @click="remove(index)"><i>&times;</i></div>
                    </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-12 my-3" v-if="todos.length === 0">
            <div class="mx-3 card p-5 align-self-center text-dark">
              <span>You don't Have any Task To-Do</span>
            </div>
          </div>
       </div>
      </div>
      <div class=" col-lg-6 col-sm-12 my-3 py-4">
          <div class="shadow py-3 p-3 mx-3">
              <form action="" v-on:dubmit.prevent="onSubmit">
                <div class="mb-3">
                  <label for="addTodos" class="col-sm-12 col-form-label"><b>Add new Todos</b></label>
                  <div class="col-sm-12">
                    <input type="text" class="form-control" id="addTodos" v-model="todoText">
                  </div>
                </div>
                <button class="btn btn-success" @click.prevent="addTodo">Add Todos</button>
              </form>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
  import {defineComponent, reactive,ref} from "vue"
  export default defineComponent({

    setup() {

      const todoText = ref("")
      const todos = reactive([])

      function addTodo(){ 
        if (todoText.value === "") {
          alert('Input Can not be empty')
          return;
        }else{
           todos.unshift({
            text: todoText.value,
            createdAt: new Date(),
            done: false
          })
        }
       
        todoText.value = "";

        
      }

      function markAsDone(index){
          todos[index].done = true
      }

      function markAsunDone(index){
         todos[index].done = false
      }

      function remove(index){
        todos.splice(index,1)
      }
      
      return{
        todos,
        todoText,
        addTodo,
        markAsDone,
        markAsunDone,
        remove,
      }
    } 
    
  })
</script>