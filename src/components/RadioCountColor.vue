<script setup>
import { onMounted } from 'vue';
const emit = defineEmits(['countColor'])

const props = defineProps({
    colorCountsList: {
        type: Array,
        required: true
    },
    defaultValue: {
        type: Number,
        required: false
    }
});

const countColor = (e) => {
    emit('countColor', e.target.value);
}
    
   

</script>

<template>
    
   <fieldset class="mt-8">
    <legend class="text-sm font-semibold leading-6 text-gray-900">Кількість кольорів</legend>
    <hr class="w-[30%]">
    <p class="mt-1 text-sm leading text-gray-600">Кількість кольорів на фантику</p>
    <div class="flex items-center justify-start mt-4 space-x-4">
        <div v-for="(item, index) in colorCountsList" :key="index">
            <input class="hidden" :id="item.count" type="radio" :value="item.count" :checked="item.default"  name="radio" @change="countColor">
            <label :for="item.count" class="flex flex-col items-center justify-center w-16 h-10 p-4 rounded-md border border-gray-300 cursor-pointer hover:bg-gray-50/50">
                <span class="text-sm font-medium uppercase">{{ item.count }}</span>
            </label>
        </div>
    </div>
</fieldset>
  
</template>

<style scoped>
    input:checked + label {
        color: white;
        border-color: rgb(79 70 229);
        background-color: rgb(79 70 229);
        box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    }

    input:checked + label:hover {
        background-color: rgb(99 102 241);
    }
</style>