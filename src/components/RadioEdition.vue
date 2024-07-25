<script setup>
import { ref, onMounted } from 'vue'
import { extractIdentifiers } from 'vue/compiler-sfc';



const emit = defineEmits(['wrapperEdition']);




const props = defineProps({
    editions: {
        type: Array,
        required: true
    }
});
const editionCount = ref();


const wrapperEdition = (edition) => {
    emit('wrapperEdition', edition);
}



function choiceClass(index) {
    if (index === 0) {
        return 'rounded-t-md';
    } if (index === (props.editions.length - 1)) {
        return 'rounded-b-md';
    }
}


</script>

<template>
   <fieldset>
        <legend class="text-sm font-semibold leading-6 text-gray-900">Кількість кольорів</legend>
        <p class="mt-1 text-sm leading text-gray-600">Кількість кольорів на фантику</p>
        <div class="flex flex-col items-start justify-start mt-4">
            <div v-for="(edition, index) in editions" :key="index" class="flex relative -mt-px">
                <input v-model="editionCount" class="absolute top-1/2 left-3 transform -translate-y-1/2 w-4 h-4 z-20" :id="edition.count" type="radio" :value="edition.count" name="edition" :checked="edition.default" @change="wrapperEdition(edition)" />
                <label :for="edition.count" :class="choiceClass(index)" class="flex justify-center items-start flex-col w-72 h-10 pl-10 border border-gray-300 cursor-pointer overflow-hidden hover:bg-gray-50/50">
                    <span class="text-sm font-medium">{{ edition.count.toLocaleString() }}</span>
                </label>
            </div>
        </div>
    </fieldset>
</template>

<style scoped>
input:checked + label {
    background-color: rgb(238 242 255); 
    border-color: rgb(79 70 229);
    z-index: 10;
}


</style>