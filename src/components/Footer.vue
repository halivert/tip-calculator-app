<template>
	<footer>
		<hr />
		<p>
			Challenge by
			<a
				:href="`https://www.frontendmentor.io/challenges/${challenge}`"
				target="_blank"
				rel="noopener noreferrer"
				>Frontend Mentor</a
			>.
			<br />
			Coded by <a href="https://halivert.dev">Halí</a>.
		</p>
	</footer>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
	name: "Footer",
	props: {
		challenge: {
			type: String,
			default: "",
		},
	},
});
</script>

<style scoped>
footer {
	font-family: var(--font-family);
	width: 100%;
	text-align: center;
	font-size: 16px;
	line-height: 1.5;
}

p {
	margin: 0.25em auto;
	padding: 0 0.5em;
	text-align: center;
}

a {
	text-decoration: none;
	color: var(--dark-cyan);
	position: relative;
	padding: 0 2px;
}

a:hover,
a:focus,
a:focus-visible {
	filter: brightness(200%);
	outline: none;
}

a:focus,
a:focus-visible {
	text-decoration: underline;
}

a:focus::before,
a:focus-visible::before {
	content: "";
	position: absolute;
	inset: 0;
	filter: brightness(55%);
	background: var(--background-100);
	z-index: -1;
	border-radius: 4px;
}
</style>
