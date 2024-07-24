<script setup>
import { ref } from 'vue';

const showingList = ref(false);
const currentItem = ref({});

const props = defineProps({
    items: {
        type: Array,
        required: true,
    }
});

const emit = defineEmits(['select']);


currentItem.value = props.items[0];

function selectItem(item) {
    currentItem.value = item;
    emit('select', item);
    showingList.value = false;
}

</script>

<template>
    <label for="products-list" class="block text-lg font-medium leading-6 text-gray-700">Цукерка</label>
    <div class="relative mt-2">
        <button @click="showingList = !showingList" type="button" class="reltive w-full cursor-default rounded-md bg-white py-1.5 pl-3 pr-10 text-left to-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 sm:text-sm sm:leading-6">
            <span class="flex items-center">
                <img :src="currentItem.image" alt="" class="h-12 w-12 flex-shrink-0 rounded-sm">
                <span class="ml-3 block truncate">{{ currentItem.title }}</span>
            </span>
            <span class="pointer-events-none absolute right-0 inset-y-0 ring-0 ml-3 flex items-center pr-2">
                <svg class="h-10 w-10 text-gray-400" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                    <path fill-rule="evenodd" d="M10 3a.75.75 0 01.55.24l3.25 3.5a.75.75 0 11-1.1 1.02L10 4.852 7.3 7.76a.75.75 0 01-1.1-1.02l3.25-3.5A.75.75 0 0110 3zm-3.76 9.2a.75.75 0 011.06.04l2.7 2.908 2.7-2.908a.75.75 0 111.1 1.02l-3.25 3.5a.75.75 0 01-1.1 0l-3.25-3.5a.75.75 0 01.04-1.06z" clip-rule="evenodd" />
                </svg>
            </span>
        </button>

        <ul v-show="showingList" class="absolute z-10 mt-1 max-h-56 w-full overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm" tabindex="-1">
            <li v-for="(item, index) in items"  :key="index" @click="selectItem(item)" value="item" class="relative cursor-default select-none py-2 pl-3 pr-9 text-gray-900 hover:bg-blue-100" id="products-list-0">
                <div class="flex items-center">
                    <img :src="item.image" alt="" class="h-12 w-12 flex-shrink-0 rounded-sm">
                    <span class="ml-3 block truncate">{{ item.title }}</span>
                </div>
                <span v-if="item.title === currentItem.title" class="absolute right-0 inset-y-0 ring-0 flex items-center pr-4 text-indigo-400">
                    <svg class="h-7 w-7" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                        <path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd" />
                    </svg>
                </span>
            </li>
        </ul>
    </div>
</template>