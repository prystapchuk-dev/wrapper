<script setup>
import { onMounted, ref, computed } from 'vue';
import SelectProduct from './components/SelectProduct.vue';
import RadioCountColor from './components/RadioCountColor.vue';
import RadioFormat from './components/RadioFormat.vue';
import RadioEdition from './components/RadioEdition.vue';
import ListDiscount from './components/ListDiscount.vue';


import * as data from '/test.json';


const selectProduct = ref({});
const countRadioColor = ref(3);
const percentDiscount = ref(5);
const wrapperEdition = ref(20000);
const wrapperFormats = [
  {
    "id": 1,
    "title": "Повноформатний",
    "size": "105*130",
    "candy_waight": "22-24",
    "default": true
  },
  {
    "id": 2,
    "title": "Спеціальний \"M\"",
    "size": "70*130",
    "candy_waight": "12-14",
    "default": false
  },
  {
    "id": 3,
    "title": "Спеціальний \"S\"",
    "size": "70*110",
    "candy_waight": "7-8",
    "default": false
  }
];

const wrapperEditions = [
  {
    "count": 5000,
    "default": false
  },
  {
    "count": 10000,
    "default": false
  },
  {
    "count": 20000,
    "default": true
  }
];

const wrapperFormat = ref({});


const dafaultWrapperFormat = wrapperFormats.filter((item) => {
  return item.default === true;
});


const dafaultWrapperEdition = wrapperEditions.filter((item) => {
  return item.default === true;
});

wrapperFormat.value = dafaultWrapperFormat[0];

wrapperEdition.value = dafaultWrapperEdition[0].count;


const handleSelect = (select) => {
  selectProduct.value = select;
}

const handleRadioColor = (countColor) => {
  countRadioColor.value = countColor;
}

const handleWrapperFormat = (format) => {
  wrapperFormat.value = format;
}

const handleWrapperEdition = (edition) => {
  wrapperEdition.value = edition;
}

const handlePercentDiscount = (percent) => {
  percentDiscount.value = percent;
}

const productList = [
  {
    "id": 1,
    "title": "Цукерки \"Фінік з волоським горiхом\"",
    "image": "https://gzpt.com.ua/content/images/50/600x600l80mc0/67267263088503.webp",
    "price": 350 
  },
  {
    "id": 1,
    "title": "Цукерки \"Банан\"",
    "image": "https://gzpt.com.ua/content/images/46/600x600l80mc0/80480006278786.webp",
    "price": 350 
  },
  {
    "id": 1,
    "title": "Цукерки \"Груша\"",
    "image": "https://gzpt.com.ua/content/images/1/600x600l80mc0/96422728717613.webp",
    "price": 350 
  },
];

const colorCountsList = [
  {
    "count": 3,
    "checked": false
  },
  {
    "count": 4,
    "checked": true
  },
  {
    "count": 5,
    "checked": false
  },
  {
    "count": 6,
    "checked": false
  },
];



const discountPercentList = [
  0,
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8,
  9,
  10,
  11,
  12,
  13,
  14,
  15,
];

const wrapperCost = 
  
  {
    1: {
      5000: {
        3: 8350,
        4: 8960,
        5: 10150,
        6: 11300,
      },
      10000: {
        3: 11660,
        4: 12370,
        5: 13860,
        6: 15360,
      },
      20000: {
        3: 14950,
        4: 15820,
        5: 17350,
        6: 18900,
      },
    },

    2: {
      5000: {
        3: 8350,
        4: 8700,
        5: 10500,
        6: 11000,
      },
      10000: {
        3: 9440,
        4: 10100,
        5: 11330,
        6: 12580,
      },
      20000: {
        3: 13240,
        4: 13990,
        5: 15620,
        6: 17260,
      },
    },
    3: {
      5000: {
        3: 8200,
        4: 8500,
        5: 9900,
        6: 10950,
      },
      10000: {
        3: 8900,
        4: 9600,
        5: 11000,
        6: 12100,
      },
      20000: {
        3: 12350,
        4: 13100,
        5: 14600,
        6: 16100,
      },
    },
  };


const forma = computed(() => {
  const edition = wrapperEdition.value;
  const format = wrapperFormat.value;
  console.log(format.id);

  const test1 = data["cost"][edition];

  const test2 = test1[format.id];

  return test2;
});



</script>

<template>
  <div class="container mx-auto pt-8 p-4">
    <h1 class="text-2xl">Калькулятор вартості брендування обгортки</h1>
    <div class="flex items-center justify-between space-x-4">
      <div class="basis-1/2">
        <SelectProduct @select="handleSelect" :items="productList" />
        <RadioCountColor @countColor="handleRadioColor" :colorCountsList="colorCountsList"/>
        <RadioFormat @wrapperFormat="handleWrapperFormat" :formatList="wrapperFormats"/>
        <RadioEdition @wrapperEdition="handleWrapperEdition" :editions="wrapperEditions" />
        <ListDiscount @percentDiscount="handlePercentDiscount" :percentList="discountPercentList"/>
      </div>
      <div class="basis-1/2">
        <div class="mt-12 border rounded-md border-indigo-600">
          <h1 class="text-3xl font-semibold text-green-600">Розрахунок</h1>
          <div class="w-36 h-240 rounded-lg border border-indigo-300 overflow-hidden">
            <img v-show="Object.keys(selectProduct).length" :src="selectProduct.image" alt="">
          </div>
          <h3 class="text-lg">{{ selectProduct.title }}</h3>
          <p>Кількість кольорів фантика: <span class="font-semibold">{{ countRadioColor }}</span></p>
          <p>Формат фантика: {{  wrapperFormat.title }}</p>
          <p>Тираж: {{ wrapperEdition }}</p>
          <p>Знижка: {{ percentDiscount }}</p>
          <p>Вартість фантика: {{ forma }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

