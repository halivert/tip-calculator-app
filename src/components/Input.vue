<template>
	<div class="field">
		<label :for="name">{{ name }}</label>
		<input
			:name="name"
			:value="modelValue"
			@input="emitBill"
			v-bind="$attrs"
		/>
	</div>
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
	props: {
		name: String,
		modelValue: [Number, String],
	},
	emits: ["update:modelValue"],
	setup(_, ctx) {
		const emitBill = (event) => {
			ctx.emit("update:modelValue", event.target.value);
		};

		return {
			emitBill,
		};
	},
});
</script>

<style scoped>
.field {
	display: flex;
	flex-flow: column;
	gap: 0.5em;
	box-sizing: border-box;
}

.field:not(:last-child) {
	margin-bottom: 1em;
}

input {
	color: var(--dark-cyan);
	box-sizing: border-box;
	outline: none;
	border: 2px solid transparent;
	background: var(--light-grayish-cyan-200);
	border-radius: 8px;
	text-align: right;
	appearance: textfield;
	padding: 0 0.5em;
}
</style>
