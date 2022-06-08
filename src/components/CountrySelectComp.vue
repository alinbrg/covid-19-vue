<template>
	<select
		@change="onChange()"
		v-model="selected"
		class="form-select block w-full border p-3 rounded mt-10 focus:outline-none mb-10"
	>
		<option value="0" selected>Select Country</option>
		<option
			v-for="(country, index) in countries"
			:key="index"
			:value="country.ID"
		>
			{{ country.Country }}
		</option>
	</select>
</template>

<script>
export default {
	name: "CountrySelectComp",
	props: ["countries"],
	data() {
		return {
			selected: 0,
		};
	},
	methods: {
		onChange() {
			const country = this.countries.find((item) => item.ID === this.selected);
			// console.log(country);
			this.$emit("get-country", country);
		},
	},
};
</script>
