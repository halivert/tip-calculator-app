<template>
	<div class="results">
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
		<button type="reset">Reset</button>
	</div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
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
}
</style>
