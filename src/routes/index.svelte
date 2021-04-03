<script lang="ts" context="module">
	export async function load() {
		const image = 'successkid';

		/**
		 * This runs fine in dev but the production build fails with
		 * Error: Unknown variable dynamic import: ../static/successkid.jpg?width=500
		 *
		 * This works fine in production builds if you remove the query parameters,
		 * but that kind of defeats the purpose of vite imagetools
		 *
		 * https://github.com/rollup/plugins/tree/master/packages/dynamic-import-vars#limitations
		 */
		const { default: successkid } = await import(`../static/${image}.jpg?width=500`);

		return {
			props: {
				successkid
			}
		};
	}
</script>

<script lang="ts">
	import Counter from '$lib/Counter.svelte';

	export let successkid: string;
</script>

<main>
	<img src={successkid} />

	<h1>Hello world!</h1>

	<Counter />

	<p>Visit <a href="https://svelte.dev">svelte.dev</a> to learn how to build Svelte apps.</p>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 100;
		line-height: 1.1;
		margin: 4rem auto;
		max-width: 14rem;
	}

	p {
		max-width: 14rem;
		margin: 2rem auto;
		line-height: 1.35;
	}

	@media (min-width: 480px) {
		h1 {
			max-width: none;
		}

		p {
			max-width: none;
		}
	}
</style>
