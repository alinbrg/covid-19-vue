<template>
	<main v-if="!loading">
		<DataTitleComp :text="title" :dataDate="dataDate" />
		<DataBoxesComp :stats="stats" />

		<CountrySelectComp :countries="countries" @get-country="getCountryData" />

		<button
			v-if="stats.Country"
			@click="clearCountry"
			class="bg-red-600 text-white rounded p-3 focus:outline-none hover:bg-green-600 mb-10"
		>
			Clear Country
		</button>
	</main>
	<main class="flex flex-col align-center justify-center text-center" v-else>
		<div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
		<img :src="loadingImg" alt="loading image" class="w-40 m-auto" />
	</main>
</template>

<script>
// @ is an alias to /src
import DataTitleComp from "@/components/DataTitleComp";
import DataBoxesComp from "@/components/DataBoxesComp";
import CountrySelectComp from "@/components/CountrySelectComp";

export default {
	name: "MainComp",
	components: { DataTitleComp, DataBoxesComp, CountrySelectComp },
	data() {
		return {
			loading: true,
			title: "Global",
			dataDate: "",
			stats: {},
			countries: [],
			loadingImg: require("../assets/giphy.gif"),
		};
	},
	methods: {
		async fetchData() {
			const res = await fetch("https://api.covid19api.com/summary");
			const data = await res.json();
			return data;
		},
		getCountryData(country) {
			// console.log(country);
			this.stats = country;
			this.title = country.Country;
		},
		async clearCountry() {
			this.loading = true;
			this.title = "Global";
			const data = await this.fetchData();
			this.dataDate = data.Date;
			this.stats = data.Global;

			this.loading = false;
		},
	},
	async created() {
		const data = await this.fetchData();
		this.dataDate = data.Date;
		this.stats = data.Global;
		this.countries = data.Countries;
		this.loading = false;
	},
};
</script>
