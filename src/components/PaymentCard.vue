<template>
  <div class="p-10 w-full h-full">
    <div class="my-10">
        <p class="text-left text-xl font-bold">Payment Information</p>
        <div class="card mt-3 md:bg-slate-50 text-slate-800 md:border rounded">
            <div class="md:p-5">
                <div class="flex md:justify-end mb-2 md:mb-0">
                    <div class="card-type md:text-end bg-slate-50 rounded">
                        <img v-if="card_type == '../assets/images/1.png' " src="../assets/images/1.png" class="p-2" height="50" width="50" alt="Card Type">
                        <img v-if="card_type == '../assets/images/3.png'" src="../assets/images/3.png" class="p-2" height="50" width="50" alt="Card Type">
                        <img v-if="card_type == '../assets/images/2.png'" src="../assets/images/2.png" class="p-2" height="50" width="50" alt="Card Type">
                    </div>
                </div>
                <form id="form" class="grid grid-cols-3">
                    <div class="block mb-2 col-span-3">
                        <label for="card-name" class="text-xs text-slate-50 md:text-gray-500">Cardholder's Name</label>
                        <input v-model="card_name" @change="cardName" id="card-name" type="text" class="border rounded mt-1 w-full h-7 p-3 text-xs border-gray-300" placeholder="Juan Dela Cruz">
                    </div>
                    <div class="block mb-5 col-span-3">
                        <label for="card-name" class="text-xs text-slate-50 md:text-gray-500">Card Number</label>
                        <input v-model="card_number" @input="handleInput" @change="cardNumberType(); cardNumber()" id="card-name" type="text" class="border rounded mt-1 w-full h-7 p-3 text-xs border-gray-300" placeholder="4345 6789 3323 5556" maxlength="19">
                    </div>
                    <div class="block col-span-1 mr-2 flex flex-col justify-end">
                        <label for="card-name" class="text-xs text-slate-50 md:text-gray-500 leading-snug">Expiration Date (Month)</label>
                        <input v-model="card_month" id="card-name" type="text" @input="monthInputHandle" @change="cardExpireMonth" class="border rounded mt-1 w-full h-7 p-3 text-xs border-gray-300" placeholder="09" maxlength="2">
                    </div>
                    <div class="block col-span-1 mr-2 flex flex-col justify-end">
                        <label for="card-name" class="text-xs text-slate-50 md:text-gray-500">Expiration Date (Year)</label>
                        <input v-model="card_year" @change="yearInputHandle(); cardExpireYear()" id="card-name" type="text" class="border rounded mt-1 w-full h-7 p-3 text-xs border-gray-300" placeholder="2027" maxlength="4">
                    </div>
                    <div class="block col-span-1 flex flex-col justify-end">
                        <label for="card-name" class="text-xs text-slate-50 md:text-gray-500">CVV / CVC</label>
                        <input v-model="card_verification" @change="cardVerification" id="card-name" type="text" class="border rounded mt-1 w-full h-7 p-3 text-xs border-gray-300" placeholder="265" maxlength="3">
                    </div>              
                </form>
            </div>
        </div>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

// datas
/* eslint-disable */
const card_name = ref('');
const card_number = ref(null);
const card_type = ref('');
const card_month = ref('');
const card_year = ref('');
const card_verification = ref('');

// computed


// methods
const emit = defineEmits(['sendCardNameToParent', 'sendCardNumberToParent', 'sendCardExpireMonthToParent', 'sendCardExpireYearToParent', 'sendCardVerificationToParent']);

const cardName = () => {
    emit('sendCardNameToParent', card_name.value);
}

const handleInput = (e) => {
    card_number.value = e.target.value

    // remove spaces from previous value
    .replace(/\s/g, '')
    // add space after every set of 4 digits
    .replace(/(.{4})/g, '$1 ')
    // remove space after last set of digits
    .trim();
}

const cardNumberType = () => {
    let card_identifier = card_number.value[0];

    switch(card_identifier) {
        // amex
        case '3':
            card_identifier = '../assets/images/1.png';
            break;
        // visa
        case '4':
            card_identifier = '../assets/images/3.png';
            break;
        case '5':
            card_identifier = '../assets/images/2.png';
            break;
        default:
            alert('Sorry, the card number type is not supported. Only Amex, Visa, and Mastercard are supported.');
    }

    card_type.value = card_identifier;
}

const cardNumber = () => {
    emit('sendCardNumberToParent', card_number.value);
}

const cardExpireMonth = () => {
    emit('sendCardExpireMonthToParent', card_month.value);
}

const cardExpireYear = () => {
    emit('sendCardExpireYearToParent', card_year.value);
}

const cardVerification = () => {
    emit('sendCardVerificationToParent', card_verification.value);
}

const monthInputHandle = (e) => {
    if(card_month.value.length == 2) {
        e.preventDefault();
    }

    if(card_month.value >= 13) {
        alert('Please enter a valid month number');
        e.preventDefault();
    }
}

const yearInputHandle = (e) => {
    const now = new Date();
    const year = now.getFullYear();

    if(card_year.value < year) {
        alert(`Cannot be in the past of the year. The payment card expiration year must be between ${year} and ${year + 20}`);
    }
}

</script>

<style>

</style>