<template>
	<div class="grid md:grid-cols-2 gap-4">
		<div class="shadow-md bg-purple-100 p-10 text-center rounded">
			<h3 class="text-3xl text-purple-600 font-bold mb-4">Cases</h3>
			<div class="text-2xl mb-4">
				<span class="font-bold">New:</span>
				{{ numWithCommas(stats.NewConfirmed) }}
			</div>
			<div class="text-2xl mb-4">
				<span class="font-bold">Total:</span>
				{{ numWithCommas(stats.TotalConfirmed) }}
			</div>
		</div>
		<div class="shadow-md bg-purple-200 p-10 text-center rounded">
			<h3 class="text-3xl text-purple-600 font-bold mb-4">Deaths</h3>
			<div class="text-2xl mb-4">
				<span class="font-bold">New:</span>
				{{ numWithCommas(stats.NewDeaths) }}
			</div>
			<div class="text-2xl mb-4">
				<span class="font-bold">Total:</span>
				{{ numWithCommas(stats.TotalDeaths) }}
			</div>
		</div>
	</div>
</template>
<script>
export default {
	name: "dataBoxesComp",
	props: ["stats"],
	methods: {
		numWithCommas(x) {
			return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
		},
	},
};
</script>
