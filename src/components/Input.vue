<template>
	<div class="field">
		<label :for="name">
			<span>{{ name }}</span>
			<span class="errors">{{ errors }}</span>
		</label>
		<i class="icon">
			<slot name="icon"></slot>
		</i>
		<input
			:class="{ 'has-error': errors }"
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
		errors: String,
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
	position: relative;
	display: flex;
	flex-flow: column;
	gap: 0.5em;
	box-sizing: border-box;
}

.field:not(:last-child) {
	margin-bottom: 2em;
}

label {
	display: flex;
	justify-content: space-between;
}

.errors {
	color: var(--error);
}

.icon {
	font-size: calc(var(--font-size) - 5px);
	color: var(--dark-grayish-cyan-200);
	position: absolute;
	display: flex;
	flex-flow: column;
	height: 3rem;
	aspect-ratio: 1 / 1;
	bottom: 0;
	justify-content: center;
	align-items: center;
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
	height: 3rem;
}

input:hover,
input:focus,
input:focus-visible {
	border: 2px solid var(--strong-cyan);
}

input.has-error {
	border: 2px solid var(--error);
}
</style>
