<template>
	<div>
		<label>Select Tip %</label>

		<div class="tips">
			<label v-for="tip in tips" :key="tip" :for="tip">
				<input
					name="tip"
					:id="tip"
					type="radio"
					:value="tip"
					v-model="selectedTip"
				/>
				<span>{{ tip }}%</span>
			</label>
			<input
				type="text"
				v-model="customTip"
				placeholder="Custom"
				@focus="rememberLastCustomTip"
				@input="emitCustomTip($event.target.value)"
				@blur="restoreLastTip"
			/>
		</div>
	</div>
</template>

<script>
import { defineComponent, ref, toRefs, watch } from "vue";

export default defineComponent({
	name: "TipSelector",
	props: {
		modelValue: Number,
	},
	emits: ["update:modelValue"],
	setup(props, ctx) {
		const lastCustomTip = ref("");
		const selectedTip = ref("");
		const customTip = ref("");
		const { modelValue: lastTip } = toRefs(props);

		watch(selectedTip, (selectedTip) => {
			if (selectedTip) {
				if (customTip.value) lastCustomTip.value = customTip.value;
				customTip.value = "";
				ctx.emit("update:modelValue", selectedTip);
			}
		});

		const rememberLastCustomTip = () => {
			selectedTip.value = "";
			if (!customTip.value && lastCustomTip.value) {
				customTip.value = lastCustomTip.value;
			}
		};

		const restoreLastTip = ({ target }) => {
			if (parseInt(target.value) !== lastTip.value) {
				selectedTip.value = lastTip.value;
			}
		};

		const emitCustomTip = (value) => {
			lastCustomTip.value = value;
			ctx.emit("update:modelValue", parseInt(value) || 0);
		};

		return {
			tips: [5, 10, 15, 25, 50],
			selectedTip,
			customTip,
			rememberLastCustomTip,
			emitCustomTip,
			restoreLastTip,
			lastTip,
		};
	},
});
</script>

<style scoped>
div:not(:last-child) {
	margin-bottom: 2em;
}

.tips {
	display: flex;
	flex-flow: row wrap;
	margin-top: 0.5em;
	gap: 1em;
}

.tips > :is(label, input) {
	box-sizing: border-box;
	flex: 1 1 30%;
	margin: 0;
	min-width: 0;
	cursor: pointer;
}

input[type="radio"] {
	position: absolute;
	opacity: 0;
}

input[type="radio"] + span {
	display: block;
	text-align: center;
	background: var(--dark-cyan);
	color: var(--white);
	font-size: var(--font-size);
	padding: 0.2em;
	border-radius: 8px;
	text-transform: capitalize;
	border: 2px solid transparent;
}

input[type="radio"]:checked + span,
input[type="radio"]:checked:focus + span,
input[type="radio"]:checked:focus-visible + span {
	background: var(--strong-cyan);
	color: var(--dark-cyan);
}

input[type="radio"]:checked:hover + span {
	background: var(--strong-cyan);
	color: var(--dark-cyan);
	border-color: hsl(0, 0%, 0%, 0.2);
}

input[type="radio"]:hover + span,
input[type="radio"]:focus + span,
input[type="radio"]:focus-visible + span {
	background: var(--background-100);
	color: var(--dark-cyan);
}

input[type="text"] {
	box-sizing: border-box;
	outline: none;
	border: 2px solid transparent;
	background: var(--light-grayish-cyan-200);
	border-radius: 8px;
	text-align: right;
	appearance: textfield;
	padding: 0 0.5em;
}

input[type="text"]:active,
input[type="text"]:focus,
input[type="text"]:focus-visible {
	border-color: var(--strong-cyan);
}
</style>
