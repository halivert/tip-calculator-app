<template>
	<div class="results">
		<div>
			<div class="result">
				<div>
					<strong>Tip Amount</strong>
					<small>/ person</small>
				</div>
				<span>${{ tipPerPerson.toFixed(2) }}</span>
			</div>
			<div class="result">
				<div>
					<strong>Total</strong>
					<small>/ person</small>
				</div>
				<span>${{ totalPerPerson.toFixed(2) }}</span>
			</div>
		</div>
		<button type="reset">Reset</button>
	</div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
	name: "Results",
	props: {
		tipPerPerson: {
			type: Number,
			default: 0,
		},
		totalPerPerson: {
			type: Number,
			default: 0,
		},
	},
});
</script>

<style scoped>
div.results {
	margin-top: 2em;
	background: var(--dark-cyan);
	color: var(--strong-cyan);
	display: flex;
	flex-direction: column;
	padding: 2em 1.25em;
	border-radius: 12px;
	gap: 1em;
	justify-content: space-around;
}

.results > div {
	display: flex;
	flex-direction: column;
	gap: 2em;
}

div.result {
	display: flex;
	flex-flow: row nowrap;
	justify-content: space-between;
	align-items: center;
}

.result > span {
	font-size: calc(var(--font-size) + 7px);
}

strong {
	display: block;
	font-weight: 700;
	color: var(--white);
}

small {
	color: var(--dark-grayish-cyan-200);
}

button[type="reset"] {
	margin-top: 1em;
	text-transform: uppercase;
	background: var(--strong-cyan);
	color: var(--dark-cyan);
	text-align: center;
	appearance: none;
	border: 0;
	border-radius: 4px;
	padding: 0.5em 0;
	font-family: var(--font-family);
	font-size: calc(var(--font-size) - 5px);
	font-weight: 700;
	cursor: pointer;
}

button[type="reset"]:hover,
button[type="reset"]:focus,
button[type="reset"]:focus-visible {
	background: var(--background-100);
}

@media screen and (min-width: 900px) {
	div.results {
		margin-top: 0;
		gap: 6em;
		width: 100%;
	}
}
</style>
