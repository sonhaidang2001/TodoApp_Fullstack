<template>
  <div class="todo-item pd-3 d-flex">
    <div>
      <input
        type="checkbox"
        :checked="todoProps.completed"
        @change="changComplete"
      />
      <label :class="[todoProps.completed ? 'is-completed' : '']" for="">{{
        todoProps.name
      }}</label>
    </div>
    <p>{{ todoProps.description }}</p>
    <div class="form-button d-flex">
      <button class="btn btn-success d-block mr-1">
        <i class="fa-solid fa-pen"></i>
      </button>
      <button class="btn btn-danger d-block" @click="deleteItem">
        <i class="fa-solid fa-trash"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: ['todoProps'],
  setup(props, context) {
    const changComplete = () => {
      // console.log(props.todoProps._id)
      context.emit('change-complete', props.todoProps._id)
    }
    const deleteItem = event => {
      event.preventDefault()
      context.emit('delete-item', props.todoProps._id)
    }
    return {
      changComplete,
      deleteItem
    }
  }
}
</script>

<style scoped>
.todo-item {
  padding: 15px 10px;
  margin: 10px 0px;
  background: #ccc;
  justify-content: space-between;
  align-content: center;
}

.is-completed {
  text-decoration: line-through;
}
</style>