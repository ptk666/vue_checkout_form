<template>
  <main class="w-screen h-screen grid md:grid-cols-3 md:overflow-y-hidden">
    <PaymentCard
      class="md:col-span-2" 
      @sendCardNameToParent="cardName"
      @sendCardNumberToParent="cardNumber"
      @sendCardExpireMonthToParent="cardExpireMonth"
      @sendCardExpireYearToParent="cardExpireYear"
      @sendCardVerificationToParent="cardVerification"
    />
    <SummaryCard
      class="bg-slate-50"
      :card_name="card_name"
      :card_number="card_number"
      :card_expire_month="card_expire_month"
      :card_expire_year="card_expire_year"
      :card_verification="card_verification"
    />
    <FooterCard />
  </main>
</template>

<script setup>
import PaymentCard from '../components/PaymentCard.vue' 
import SummaryCard from '../components/SummaryCard.vue'
import FooterCard from '../components/FooterCard.vue'
import { ref } from 'vue';

// data
const card_name = ref('');
const card_number = ref('');
const card_expire_month = ref('');
const card_expire_year = ref('');
const card_verification = ref('');

// methods 
const cardName = (item) => {
  card_name.value = item;
}

const cardNumber = (item) => {
  card_number.value = item;
}

const cardExpireMonth = (item) => {
  card_expire_month.value = item;
}

const cardExpireYear = (item) => {
  card_expire_year.value = item;
}

const cardVerification = (item) => {
  card_verification.value = item;
}

</script>

<style>

</style>