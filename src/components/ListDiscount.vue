<script setup>
import { ref } from 'vue';

const showingList = ref(false);
const currentItem = ref({});

const props = defineProps({
    percentList: {
        type: Array,
        required: true,
    }
});

const emit = defineEmits(['percentDiscount']);


currentItem.value = props.percentList[0];

function selectItem(item) {
    currentItem.value = item;
    emit('percentDiscount', item);
    showingList.value = false;
}

</script>

<template>
    <legend class="text-sm font-semibold leading-6 text-gray-900">Кількість кольорів</legend>
    <p class="mt-1 text-sm leading text-gray-600">Кількість кольорів на фантику</p>
    <div class="mt-2 relative w-20 h-10" >
        <input v-model="currentItem" type="text" class="text-2xl font-medium w-full h-full p-3 cursor-default rounded-md bg-white text-left to-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 sm:text-sm sm:leading-6">
            <span class="absolute top-1/2 right-8 transform -translate-y-1/2">
                {{ '%' }}
            </span>
            <span @click="showingList = !showingList" class="h-8 w-12 absolute top-1/2 right-0 transform -translate-y-1/2 inset-y-0 ring-0 ml-3 block">
                <svg  class="ml-auto w-6 h-8 fill-indigo-600" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                    <path fill-rule="evenodd" d="M10 3a.75.75 0 01.55.24l3.25 3.5a.75.75 0 11-1.1 1.02L10 4.852 7.3 7.76a.75.75 0 01-1.1-1.02l3.25-3.5A.75.75 0 0110 3zm-3.76 9.2a.75.75 0 011.06.04l2.7 2.908 2.7-2.908a.75.75 0 111.1 1.02l-3.25 3.5a.75.75 0 01-1.1 0l-3.25-3.5a.75.75 0 01.04-1.06z" clip-rule="evenodd" />
                </svg>
            </span>
        </input>
        <ul v-show="showingList" class="absolute z-10 mt-1 max-h-56 overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm" tabindex="-1">
            <li v-for="(item, index) in percentList"  :key="index" @click="selectItem(item)" value="item" class="relative cursor-default select-none py-2 pl-3 pr-9 text-gray-900 hover:bg-blue-100" id="products-list-0">
                <div class="flex items-center w-4">
                   <span class="block truncate">{{ item }}</span>
                </div>
            </li>
        </ul>
    </div>
</template>