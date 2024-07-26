<script setup>
import { onMounted, ref, computed } from 'vue';
import SelectProduct from './components/SelectProduct.vue';
import RadioCountColor from './components/RadioCountColor.vue';
import RadioFormat from './components/RadioFormat.vue';
import RadioEdition from './components/RadioEdition.vue';
import ListDiscount from './components/ListDiscount.vue';


import * as data from '../test.json';


const selectProduct = ref({});
const countRadioColor = ref();
const percentDiscount = ref();
const wrapperEdition = ref();

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

const colorCountsList = [
  {
    "count": 3,
    "default": false
  },
  {
    "count": 4,
    "default": true
  },
  {
    "count": 5,
    "default": false
  },
  {
    "count": 6,
    "default": false
  },
];

const wrapperFormat = ref({});


const dafaultWrapperFormat = wrapperFormats.filter((item) => {
  return item.default === true;
});


const dafaultWrapperEdition = wrapperEditions.filter((item) => {
  return item.default === true;
});

const dafaultWrapperCountColor = colorCountsList.filter((item) => {
  return item.default === true;
});

wrapperFormat.value = dafaultWrapperFormat[0];

wrapperEdition.value = dafaultWrapperEdition[0];

countRadioColor.value = dafaultWrapperCountColor[0].count;

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
    "id": 2,
    "title": "Цукерки \"Банан\"",
    "image": "https://gzpt.com.ua/content/images/46/600x600l80mc0/80480006278786.webp",
    "price": 350 
  },
  {
    "id": 3,
    "title": "Цукерки \"Груша\"",
    "image": "https://gzpt.com.ua/content/images/1/600x600l80mc0/96422728717613.webp",
    "price": 350 
  },
  {
    "id": 4,
    "title": "Цукерки \"Полум'яні\"",
    "image": "https://gzpt.com.ua/content/images/40/1800x1800l80mc0/81712133041787.webp",
    "price": 250 
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

  return data.cost[wrapperFormat.value.id][wrapperEdition.value.count][countRadioColor.value];

});

const clishe = computed(() => {

return data.cost[wrapperFormat.value.id]["clishe"][countRadioColor.value];

});




const averageCandyWaight = computed(() => {
  const str = wrapperFormat.value.candy_waight + '';
  const arrs = str.split('-', 2);

  const sum = arrs.reduce((acc, arr) => acc + Number(arr), 0);
  const length = arrs.length;

  return sum / length;
});

const wellBePacked = computed(() => {
  return wrapperEdition.value.count / (1000 / averageCandyWaight.value);
});

const finalProductPrice = computed(() => {
  if (percentDiscount.value) {
    return selectProduct.value.price * (1 - (percentDiscount.value / 100));
  }

  return selectProduct.value.price;
});

const priceWrapperWithClishe = computed(() => {
  return forma.value + clishe.value;
});

const pricePerKilogram = computed(() => {
  return ((wellBePacked.value * finalProductPrice.value) + priceWrapperWithClishe.value) / wellBePacked.value;
});

const priceOneCandy = computed(() => {
  return pricePerKilogram.value / (1000 / averageCandyWaight.value);
});

const finalPrice = computed(() => {
  return wellBePacked.value * pricePerKilogram.value.toFixed();
});

const candiesForOneCilogram = computed(() => {
  return  1000 / averageCandyWaight.value;
});

</script>

<template>
  <div class="container mx-auto pt-8 p-4">
    <h1 class="text-2xl">Калькулятор вартості брендування обгортки</h1>
    <div class="flex justify-between space-x-4">
      <div class="basis-1/2">
        <SelectProduct @select="handleSelect" :items="productList" />
        <RadioCountColor @countColor="handleRadioColor" :colorCountsList="colorCountsList" :defaultValue="4"/>
        <RadioFormat @wrapperFormat="handleWrapperFormat" :formatList="wrapperFormats"/>
        <RadioEdition @wrapperEdition="handleWrapperEdition" :editions="wrapperEditions" />
        <ListDiscount @percentDiscount="handlePercentDiscount" :percentList="discountPercentList"/>
      </div>
      <div class="basis-1/2">
        <div class="border rounded-md border-indigo-600 p-4 space-y-2">
          <h1 class="text-3xl font-semibold text-green-600">Розрахунок</h1>
          <div class="w-36 h-240 rounded-lg border border-indigo-300 overflow-hidden">
            <img v-show="Object.keys(selectProduct).length" :src="selectProduct.image" alt="">
          </div>
          <h3 class="text-lg">{{ selectProduct.title }}</h3>
          <p>Кількість кольорів фантика: <span class="font-semibold">{{ countRadioColor }}</span></p>
          <p>Формат фантика: {{  wrapperFormat.title }}, розміри: ({{ wrapperFormat.size }}) мм</p>
          <p>Тираж: {{ wrapperEdition.count }}</p>
          <!--<p>Знижка: {{ percentDiscount }}</p>
          <p>{{ finalProductPrice }}</p>
          <p>Вартість фантика: {{ forma }}</p>
          <p>Вартість кліше: {{ clishe }}</p>
          <p>Всього за фантик: {{ priceWrapperWithClishe }}</p>-->
          <p>Вага цукерки*: {{ averageCandyWaight }}г</p>
          <p>Цукерок на 1кг: {{ candiesForOneCilogram.toFixed(1) }} шт</p>
          <p>Ціна 1 цукерки: {{ priceOneCandy.toFixed(2) }} грн</p>
          <p>Ціна за 1 кг: {{ pricePerKilogram.toFixed() }} грн</p>
          <p>Буде запаковано: {{ wellBePacked }} кг</p>
          <h1 class="text-2xl font-medium">Вартість всього проекту: {{ finalPrice.toFixed() }} грн</h1>
        </div>
      </div>
    </div>
  </div>
</template>

