<template>
  <div class="text-slate-800 py-10 md:px-5 px-10">
    <div class="mt-10 md:mt-0">
        <div class="title items-center md:block lg:flex lg:justify-between mb-10 md:mb-5 lg:mb-10">
            <p class="text-left text-xl font-bold mb-1">Order Summary</p>
            <span class="text-xs py-2 px-3 border rounded-full bg-slate-800 text-slate-50">{{ items.length }} Item(s)</span>
        </div>

        <div class="flex flex-col mb-5 md:mb-2">
            <div v-for="item in items" :key="item.id" class="mb-2 items-center border border-t-transparent border-x-transparent pb-2 border-b-slate-800">
                <div class="flex">
                    <img src="../assets/images/Placeholder_view_vector.svg.png" height="30" width="50" class="rounded-md" alt="Placeholder Image">
                    <div class="ml-3 md:h-5">
                        <span class="block text-xs">{{ item.name }}</span>
                        <span class="text-xs text-gray-400">{{ item.details }}</span>
                    </div>
                </div>
                <span class="float-right font-bold">${{ item.price }}</span>
            </div>
        </div>

        <div class="block mb-5 md:mb-0">
            <div class="subtotal flex justify-end items-center mb-3">
                <label class="mr-5 text-xs text-gray-400">Subtotal:</label>
                <span class="font-bold">${{ subtotal }}</span>
            </div>
            <div class="subtotal flex justify-end items-center mb-3">
                <label class="mr-5 text-xs text-gray-400">Shipping Fee:</label>
                <span class="font-bold">${{ shipping_fee }}</span>
            </div>
            <div class="subtotal flex justify-end items-center mb-3">
                <label class="mr-5 text-xs text-gray-400">Tax:</label>
                <span class="font-bold">${{ tax }}</span>
            </div>
            <div class="subtotal flex justify-end items-center mb-3">
                <label class="mr-5 text-xs text-gray-400">Total:</label>
                <span class="font-bold">${{ total }}</span>
            </div>
        </div>

        <button @click="verifyCard" :disabled="btn_checker" class="text-sm font-bold p-2 bg-amber-500 text-slate-50 border rounded w-full">Pay Now: ${{ total }}</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, defineProps } from 'vue';

// data
const items = ref([
    { 
        id: 1,
        name: 'The Standard Sweatshirt',
        details: 'Charcoal Gray, M',
        price: 50
    },
    {
        id: 2,
        name: 'The Premium Sweatshirt',
        details: 'Olive, L',
        price: 80
    },
    {
        id: 3,
        name: 'The Luxurious Sweatshirt',
        details: 'White, XL',
        price: 150
    },
    {
        id: 4,
        name: 'The Diamond Sweatshirt',
        details: 'Gray, XXL',
        price: 200
    }
]);
const shipping_fee = ref(10);

// props
const props = defineProps({
    card_name: String,
    card_number: String,
    card_expire_month: String,
    card_expire_year: String,
    card_verification: String
});


// computed
const subtotal = computed(() => {
    const item = items.value.reduce((a, b) => (a + b.price), 0);

    return item;
});

const tax = computed(() => {
    return subtotal.value / 50;
});

const total = computed(() => {
    return subtotal.value + shipping_fee.value + tax.value;
})

const getCardName = computed(() => {
    return props.card_name;
})

const getCardNumber = computed(() => {
    return props.card_number;
})

const getCardExpireMonth = computed(() => {
    return props.card_expire_month;
})

const getCardExpireYear = computed(() => {
    return props.card_expire_year;
})

const getCardVerification = computed(() => {
    return props.card_verification;
})

const btn_checker = computed(() => {
    return getCardName.value != ''
    && getCardNumber.value != ''
    && getCardExpireMonth.value != ''
    && getCardExpireYear.value != ''
    && getCardVerification.value != ''
    ? false : true;
})

// methods

const verifyCard = () => {
    alert('Success!');
}

</script>

<style>

</style>