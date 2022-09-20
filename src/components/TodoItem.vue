<template>
    <div class="card border-0">
        <div class="card-body">
            <div class="row">
                <div class="col-1">
                    <input class="form-check-input rounded-5" type="checkbox" name="IsDone" :checked="props.done"
                        @click="$emit('toogleDone',props.itemId)">
                </div>
                <div class="col-10">
                    <p 
                    class="text-list-color"
                    :class="{'text-decoration-line-through':props.done}">{{ props.content }}</p>
                </div>
                <div class="col-1">
                    <button class="btn" @click="$emit('deleteItem',props.itemId)">
                        <i class="bi bi-trash text-list-color"></i>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
const props = defineProps({
    itemId: {
        type: Number,
        required: true
    },
    content: {
        type: String,
        required: true
    },
    done: {
        type: Boolean,
        required: true
    }
})

defineEmits(['deleteItem', 'toogleDone'])
</script>