<script>
import { ref, onMounted } from 'vue';
import { useAxios } from '@vueblocks/vue-use-axios';
// import { useDateFormat, useNow } from '@vueuse/core';
</script>
<script setup>
// const completeDate = useDateFormat(useNow(), 'YYYY-MM-DD HH:mm:ss')
const arrData = ref([]);

const getPrice = () => {
	const { refetch, data } = useAxios('https://min-api.cryptocompare.com/data/price?fsym=BTC&tsyms=EUR');
	const fetchBitcoinRate = () => {
		setInterval(() => {
      if (arrData.value.length>59)
        arrData.value.pop()
      arrData.value.unshift(`${data.value.EUR}€ ${new Date().toLocaleString()}`)
			refetch();
		}, 1000);
	};
	onMounted(() => {
		fetchBitcoinRate();
	});
};
getPrice();
</script>

<template>
	<p>{{}}</p>
	<p v-for="(item, index) in arrData" :key="index">
		Bitcoin price {{ item }}
	</p>
</template>

<style scoped></style>
