<template>
	<form @reset="resetForm" class="calculator">
		<Input name="Bill" v-model="bill" placeholder="0" type="number" />

		<TipSelector v-model="tip" />

		<Input
			name="Number of people"
			v-model="people"
			placeholder="0"
			type="number"
		/>

		<Results v-bind="results" />
	</form>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from "vue";
import Input from "./Input.vue";
import TipSelector from "./TipSelector.vue";
import Results from "./Results.vue";

export default defineComponent({
	components: {
		Input,
		TipSelector,
		Results,
	},
	setup() {
		const bill = ref("");
		const people = ref("");
		const tip = ref(0);

		const total = computed(() => {});

		const resetForm = () => {
			bill.value = "";
			people.value = "";
			tip.value = 0;
		};

		const results = computed(() => {
			const billNum: number = Math.trunc(parseFloat(bill.value) * 100) || 0;
			const peopleNum = parseInt(people.value);
			const tipNum: number = tip.value;

			const totalTip: number = billNum * tipNum;
			const tipPerPerson: number = totalTip / (peopleNum || 1) / 10000;
			const totalPerPerson: number =
				billNum / (peopleNum || 1) / 100 + tipPerPerson;

			return {
				tipPerPerson,
				totalPerPerson,
			};
		});

		return {
			bill,
			people,
			tip,
			total,
			resetForm,
			results,
		};
	},
});
</script>

<style scoped>
.calculator {
	margin: 0;
	box-sizing: border-box;
	background: var(--white);
	width: 100%;
	border-radius: 16px 16px 0 0;
	padding: 2em;
	font-family: var(--font-family);
	color: var(--dark-grayish-cyan-100);
	font-weight: 700;
}
</style>
