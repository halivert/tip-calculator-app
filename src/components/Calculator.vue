<template>
	<form @submit.prevent="getErrors" @reset="resetForm" class="calculator">
		<input type="submit" style="display: none" />
		<div class="column">
			<Input name="Bill" v-model="bill" placeholder="0" type="number">
				<template #icon>
					<Icon icon="dollar-sign" />
				</template>
			</Input>

			<TipSelector v-model="tip" />

			<Input
				name="Number of people"
				v-model="people"
				placeholder="0"
				type="number"
				:errors="peopleErrors"
			>
				<template #icon>
					<Icon icon="user" />
				</template>
			</Input>
		</div>

		<Results v-bind="results" />
	</form>
</template>

<script lang="ts">
import { library } from "@fortawesome/fontawesome-svg-core";
import { faUser, faDollarSign } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

import { computed, defineComponent, ref, watch } from "vue";
import Input from "./Input.vue";
import TipSelector from "./TipSelector.vue";
import Results from "./Results.vue";

library.add(faUser, faDollarSign);

export default defineComponent({
	name: "Calculator",
	components: {
		Input,
		TipSelector,
		Results,
		Icon: FontAwesomeIcon,
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
			const peopleNum = parseInt(people.value) || 0;
			let tipPerPerson: number = 0;
			let totalPerPerson: number = 0;

			if (peopleNum) {
				const billNum: number = Math.trunc(parseFloat(bill.value) * 100) || 0;
				const tipNum: number = tip.value;

				const totalTip: number = billNum * tipNum;
				tipPerPerson = totalTip / (peopleNum || 1) / 10000;
				totalPerPerson = billNum / (peopleNum || 1) / 100 + tipPerPerson;
			}

			return {
				tipPerPerson,
				totalPerPerson,
			};
		});

		const peopleErrors = ref("");
		const getErrors = () => {
			peopleErrors.value = !people.value ? "Can't be zero" : "";
		};

		watch(people, (value) => {
			if (value) peopleErrors.value = "";
		});

		return {
			bill,
			people,
			tip,
			total,
			results,
			peopleErrors,
			resetForm,
			getErrors,
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

@media screen and (min-width: 900px) {
	.calculator {
		display: flex;
		width: 100%;
		gap: 2em;
		border-radius: 16px;
	}

	.calculator > * {
		flex: 1 0 0%;
	}
}
</style>
