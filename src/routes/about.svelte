<script>
	let isToggled = false

	function toggle() {
		isToggled = !isToggled
	}
</script>

<style>
	* {
		font-family: 'Gilroy'
	}
	
	.custom-btn {
		@apply bg-red-500 px-4 py-3 shadow rounded;
	}

	.secret-text {
		@apply opacity-0 pointer-events-none;

		&.is-shown {
			@apply opacity-100 pointer-events-auto;
		}
	}

	dl {
		& dt {
			@apply text-xl;
		}

		& dd {
			@apply font-normal text-2xl;

			@screen lg {
				@apply font-bold;
			}

			&:hover {
				@apply text-blue-700;
			}
		}
	}
</style>

<div class="space-y-16">
	<div class="text-3xl text-purple-800 italic">
		I’m a purple-colored italic text
	</div>

	<div>
		<button class="custom-btn" on:click="{toggle}">
			I’m a red button. Click me
		</button>

		<div class="secret-text" class:is-shown="{isToggled}">
			You found a secret text
		</div>
	</div>

	<!-- If you enable nesting -->
	<dl>
		<dt>What am I</dt>
		<dd>
			I’m a text that should turn bold at large viewport. And blue when hovered.
		</dd>
	</dl>
</div>
