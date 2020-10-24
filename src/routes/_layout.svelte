<script lang="ts">
	import GlobalStyle from '../components/GlobalStyle.svelte';

	import Nav from '../components/Nav.svelte';
</script>

<GlobalStyle />

<Nav />

<main>
	<slot></slot>
</main>