<template>
	<HeaderComp />
	<div class="container">
		<MainComp />
	</div>
</template>

<script>
import HeaderComp from "@/components/HeaderComp";
import MainComp from "@/components/MainComp";

export default {
	name: "App",
	components: { HeaderComp, MainComp },
};
</script>
