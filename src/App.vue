<template>
	<div class="page">
		<main>
			<h1>Splitter</h1>
			<Calculator />
		</main>
		<Footer challenge="tip-calculator-app-ugJNGbJUX" />
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Footer from "./components/Footer.vue";
import Calculator from "./components/Calculator.vue";

export default defineComponent({
	components: {
		Footer,
		Calculator,
	},
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&display=swap");
@import './vars.css';

body {
	margin: 0;
	background: var(--background-100);
}

.page {
	box-sizing: border-box;
	min-height: 100vh;
	display: flex;
	flex-flow: column;
}

h1 {
	margin: 0;
	color: var(--dark-cyan);
	font-family: var(--font-family);
	text-transform: uppercase;
	font-size: 24px;
	word-break: break-all;
	letter-spacing: 0.4em;
	text-align: center;
	width: 5em;
}

main {
	display: flex;
	flex: 1;
	flex-flow: column;
	align-items: center;
	box-sizing: border-box;
	min-height: 100%;
	gap: 4em;
	padding-top: 4em;
}
</style>
