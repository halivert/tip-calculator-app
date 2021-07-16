<template>
	<form @reset.prevent="resetForm" class="calculator">
		<Input name="Bill" v-model="bill" />

		<TipSelector v-model="tip" />

		<Input name="Number of people" v-model="people" />

		<Results :total="total" />
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
		const bill = ref(0);
		const people = ref(0);
		const tip = ref("");

		const total = computed(() => {
			return 0;
		});

		const resetForm = () => {
			bill.value = 0;
			people.value = 0;
			tip.value = "";
		};

		return {
			bill,
			people,
			tip,
			total,
			resetForm
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
