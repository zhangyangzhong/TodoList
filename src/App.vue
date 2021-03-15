<template>
  <div class="container">
    <form @submit.prevent="AddFn">
        <p style="text-align: center">TodoList</p>
        <input type="text" v-model="inputValue" placeholder="list" autofocus>
        <p>{{inputValue}}</p>
        <button>Add to the List</button>
        <p id="loopList" v-for=" (List,idx) in todo.list" :key="idx" @click="removeList(idx)">{{idx+1}}.{{List}}</p>
      </form>
  </div>
</template>

<script>
import { reactive, ref } from 'vue'
export default {
  setup(){

    const inputValue = ref('')
    // using reactive is best for datas
    const todo = reactive({
      list:[],
      })

    const AddFn = () => {
      todo.list.push(inputValue.value)
      inputValue.value = ""
    }

    const removeList = (parameter) => {
      return todo.list.splice(parameter,1),
      (todo.list.length == 0) ? alert("finish todolist"):null
    }
    
    return{
      inputValue,
      AddFn,
      todo,
      removeList,
    }
  }
}
</script>

<style lang="scss">
body,html{
  padding: 0;
  margin: 0;
  user-select: none;
}
  .container{
    box-sizing: border-box;
    padding: 10px;
    display: flex;
    justify-content: center;
    background-color: rgb(221, 221, 221);
    align-items: center;
    height: 100vh;
    width: 100%;
    #loopList{
      display: block;
      cursor: pointer;
    }
    input{
      outline: none;
    }
    button{
      width: 100%;
      padding: 5px 0 5px 0;
      border-radius: 5px;
      outline: none;
      border: none;
      background-color: rgb(39, 118, 182);
      color: white;
      cursor: pointer;
    }
  }
</style>
