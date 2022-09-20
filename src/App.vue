<template>
  <div class="container p-5">
    <div class="row justify-content-center">
      <div class="col-12 col-sm-12 col-md-6">
        <div class="bg-content-title text-center p-2">
          <h5 class="text-app-color">Website Todo</h5>
        </div>
        <div class="card mt-4 border-0 rounded-0 shadow-sm">
          <div class="card-body">
            <TodoItem v-for="todo in todoList" :key="todo.id" :content="todo.content" :itemId="todo.id"
              :done="todo.isDone" @deleteItem="deleteItemfromList" @toogleDone="toogleTodoStatus" />
          </div>
        </div>
        <div class="text-center mt-3">
          <button type="button" class="btn btn-primary rounded-4 shadow-lg py-2 px-4" @click="showModal = true">
            <div class="text-center">
              <strong class="text-app-color">
                <i class="bi bi-plus"></i>New Task
              </strong>
            </div>

          </button>
          <Modal :show="showModal" ref="modalRef" @closeModal="closeModal()" @sendTask="addTodoItem" />
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { reactive, ref } from 'vue';
import TodoItem from './components/TodoItem.vue';
import Modal from './components/Modal.vue';
const todoList = reactive([
  {
    id: 1,
    content: 'lorem ipsun',
    isDone: false
  },
  {
    id: 2,
    content: 'lorem ipsun',
    isDone: true
  }
])
const showModal = ref(false)
const modalRef = ref(null);
function deleteItemfromList(itemId) {
  var todo = todoList.find(x => x.id === itemId);
  const index = todoList.indexOf(todo);
  if (index > -1) {
    todoList.splice(index, 1);
  }
  return index;
}
function toogleTodoStatus(itemId) {
  var todo = todoList.find(x => x.id === itemId);
  const index = todoList.indexOf(todo);
  todoList[index].isDone = !todo.isDone
}
function closeModal() {
  showModal.value = false
}
function addTodoItem(value) {
  const todo = {
    id: new Date().getMilliseconds(),
    content: value,
    isDone: false
  }

  todoList.push(todo);
  closeModal();
  modalRef.value.cleanContent();
}
</script>