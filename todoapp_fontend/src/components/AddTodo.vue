<template>
  <form @submit="addItem">
    <div class="form-group form-input mr-1">
      <input
        type="text"
        placeholder="Việc mới..."
        v-model="title"
        class="form-control"
        aria-describedby="helpId"
      />
    </div>
    <div class="form-group form-input mr-1">
      <input
        type="text"
        placeholder="Mô tả tóm tắt..."
        v-model="description"
        class="form-control"
        aria-describedby="helpId"
      />
    </div>
    <input type="submit" value="Thêm" class="btn btn-info" />
  </form>
</template>

<script>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'
export default {
  name: 'AddTodo',
  setup(props, context) {
    const title = ref('')
    const description = ref('')
    const addItem = event => {
      event.preventDefault()
      const newItem = {
        id: uuidv4(),
        name: title.value,
        description: description.value,
        completed: false
      }
      context.emit('add-todo', newItem)
      title.value = ''
      description.value = ''
    }
    return {
      title,
      description,
      addItem
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  width: auto;
  height: 36px;
}
form .form-input {
  flex: 10;
}
</style>