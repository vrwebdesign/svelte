<script lang="ts">
	import { get_current_component } from 'svelte/internal'

	import { forwardEventsBuilder } from '$lib/directives'
	import { classname, condition } from '$lib/utils'

	/**
	 * TODO
	 */
	export let preview: boolean = false

	/**
	 * TODO
	 */
	export let value: string | undefined = undefined

	const forwardEvents = forwardEventsBuilder(get_current_component())

	$: classes = classname('textarea', { preview }, $$props.class)
</script>

{#if condition($$props)}
	{#if preview}
		<div use:forwardEvents {...$$restProps} class={classes}>
			{value}
		</div>
	{:else}
		<textarea bind:value use:forwardEvents {...$$restProps} class={classes} />
	{/if}
{/if}
