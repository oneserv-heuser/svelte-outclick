# Svelte Click Outside
A SvelteJS component that allows you to listen for clicks outside of an element.

## Install
```
pnpm add -D babakfp/svelte-click-outside
```

Install it in 'devDependencies'.
[Pnpm](https://pnpm.io) is a package manager like npm. You can use any other package manager instead.

## How to use
```HTML
<script>
	// The component
	import ClickOutside from './ClickOutside.svelte'

	let open = false
	let excludeHandle
</script>

<button
	bind:this={excludeHandle}
	on:click={_=> open = !open}
>
	Toggle Content
</button>

<!-- You need this wrapper to be able to style the components wrapper globally. -->
<div class="my-div">
	{#if open}
		<ClickOutside
			class="component-wrapper-element"
			on:clickOutside={_=> open = false}
			exclude={[excludeHandle]}
		>
			Click outside of the box to close it.
		</ClickOutside>
	{/if}
</div>

<style>
	/* We are styling the components wrapper */
	.my-div :global(.component-wrapper-element) {
		background: #FF3E00;
	}
</style>
```

See the [Demo file](src/App.svelte) for more.

It works same as the Javascripts Click Event. An click event attached to the entire window and checks whether the target is contained within the element.

element/elements inside the component tags going to be wrapped inside a div element. You can style it by a `class` prop.
```HTML
<ClickOutside class="my-class my-class-two" />
```

Also you need to have a parent element to wrap the component inside it, to be able to add your custom styles for the component wrapper element.
```HTML
<div class="my-div">
	<ClickOutside class="my-class my-class-two" />
</div>

<style>
	div :global(.my-class) {
		/*  */
	}
</style>
```

### Exclusions
By default, clicking on any element outside of the wrapped element will cause the event to trigger. You can specify excluded elements that will not trigger the event. For example, a button that triggers a popup must be excluded. Otherwise, it will immediately close the popup when it is opened. The component has an `exclude` prop that expects an array of DOM nodes. Clicks on those nodes (and their children) will be ignored.

## Install demo
```
git clone https://github.com/babakfp/svelte-click-outside.git
cd svelte-click-outside
pnpm i
pnpm dev
```
