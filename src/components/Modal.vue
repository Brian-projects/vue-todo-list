<template>
  <div
    class="modal fade"
    :class="{ show: props.show, 'display-modal': props.show }"
    tabindex="-1"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content" ref="modalContentRef">
        <div class="modal-header">
          <h5 class="modal-title" style="color: #9aa3c1">Modal title</h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
            @click="$emit('closeModal')"
          ></button>
        </div>
        <div class="modal-body">
          <div class="mb-3">
            <div class="text-start">
              <label for="task" class="form-label">Task</label>
            </div>
            <input
              type="text"
              class="form-control"
              placeholder="Write something..."
              name="task"
              v-model="content"
            />
          </div>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal"
            @click="$emit('closeModal')"
          >
            Close
          </button>
          <button
            type="button"
            class="btn btn-primary"
            @click="$emit('sendTask', content)"
            :disabled="!content"
          >
            Save changes
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
import { onClickOutside } from "@vueuse/core";

const content = ref(null);
const modalContentRef = ref(null);

const props = defineProps({
  show: {
    type: Boolean,
    required: true,
  },
});
const emits = defineEmits(["closeModal", "sendTask"]);
function cleanContent() {
  content.value = "";
}
defineExpose({
  cleanContent,
});
onClickOutside(modalContentRef, function (event) {
  emits("closeModal");
});
</script>
