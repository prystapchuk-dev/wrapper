<script setup>
import { ArrowsPointingOutIcon } from '@heroicons/vue/20/solid'
import { TagIcon } from '@heroicons/vue/20/solid'

const emit = defineEmits(['wrapperFormat']);

const wrapperFormat = (format) => {
    emit('wrapperFormat', format);
}

const props = defineProps({
    formatList: {
        type: Array,
        required: true
    }
});
</script>

<template>
    <fieldset class="mt-8">
        <legend class="text-sm font-semibold leading-6 text-gray-900">Формат</legend>
        <hr class="w-[30%]">
        <p class="mt-1 text-sm leading text-gray-600">Оберіть розмір обгортки</p>
        <div class="flex items-center justify-start mt-4 space-x-4">
            <div v-for="(format, index) in formatList" :key="index">
                <input class="hidden" :id="index" type="radio" :value="format" name="format" :checked="format.default" @change="wrapperFormat(format)">
                <label :for="index" class="flex flex-col w-40 h-22 p-2 rounded-md border border-gray-300 cursor-pointer hover:bg-gray-50/50">
                    <span class="text-sm font-medium">{{ format.title }}</span>
                    <ul class="mt-2">
                        <li class="text-sm"><span>{{ format.size }} мм</span></li>
                        <li class="text-sm">Вага цукерки: <span class="font-medium">{{ format.candy_waight }} г</span></li>
                    </ul>
                </label>
            </div>
        </div>
    </fieldset>
</template>

<style scoped>
input:checked + label {
        border-color: rgb(79 70 229);
        box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        background-image: url('src/components/icons/icon.svg');
        background-size: 18px 18px;
        background-repeat: no-repeat;
        background-position: top 8px right 5px;   
    }
</style>