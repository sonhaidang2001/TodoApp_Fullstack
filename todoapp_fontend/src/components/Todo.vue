<template>
  <div id="todo">
    <AddTodo @add-todo="addTodo" />
    <div class="form d-flex justify-content-between bg-secondary">
      <div>Công việc</div>
      <div>Mô tả</div>
      <div>Hành động</div>
    </div>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todoProps="todo"
      @change-complete="changeComplete"
      @delete-item="deleteItem"
    />
  </div>
</template>

<script>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'
import TodoItem from '../components/TodoItem.vue'
import AddTodo from '../components/AddTodo.vue'
import axios from 'axios'
export default {
  name: 'Todo',
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([])

    const getAllTodos = async () => {
      try {
        const res = await axios.get('http://localhost:5000/works/api/work')
        todos.value = res.data
      } catch (error) {
        console.log(error)
      }
    }
    getAllTodos()

    const changeComplete = id => {
      todos.value = todos.value.map(todo => {
        if (todo._id === id) todo.completed = !todo.completed
        return todo
      })
    }

    const deleteItem = async id => {
      try {
        await axios.delete(`http://localhost:5000/works/api/work/${id}`)
        todos.value = todos.value.filter(todo => todo._id !== id)
      } catch (error) {
        console.log(error)
      }
    }

    const addTodo = async newTodo => {
      try {
        const res = await axios.post(
          'http://localhost:5000/works/api/work',
          newTodo
        )
        todos.value.push(res.data)
      } catch (error) {
        console.log(error)
      }
    }

    return {
      todos,
      changeComplete,
      deleteItem,
      addTodo
    }
  }
}
</script>

<style scoped>
#todo {
  width: 1100px;
  height: auto;
  box-shadow: 0 0 10px #333;
  border-radius: 8px;
  padding: 15px 10px;
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  margin-top: 10px;
}
.form {
  padding: 15px 10px;
  margin-top: 5px;
  color: #fff;
  font-weight: bold;
  font-size: 18px;
}
</style>