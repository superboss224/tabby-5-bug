<script>
	import { fade, fly } from 'svelte/transition';
	import Tabs from './Tabs.svelte';
	import Slide from "./Slide.svelte";

	let name = 'Tabby';

	let tabItems = [
		{ id: 1, label: 'Tab1', back: 'red' },
		{ id: 2, label: 'Tab2', back: 'blue' },
		{ id: 3, label: 'Tab3', back: 'green' },
	];
	let activeTab = 0, state = 0;

	let slideWrapper, anim = {};

	function animController() {
		if(activeTab == state) return;
	
		const nodeWidth = slideWrapper.offsetWidth; 
		const currentMultiplier = activeTab > state ? 1 : -1;

		console.log(`activeTab ${activeTab > state ? ">" : "<"} state`);

		anim = {
			in: nodeWidth * currentMultiplier,
			out: nodeWidth * -currentMultiplier,
		};
	}

	$: if (slideWrapper) {
		animController();
		state = activeTab;
	}
	$: currentTab = tabItems[activeTab];
	$: slideWrapper && console.log(slideWrapper.offsetWidth);
</script>

<h1>Hello {name}!</h1>

<main>
	{#if currentTab.id=== 1}
		<div
				 style="--back: {currentTab.back}"

				 bind:this={slideWrapper}
				 in:fly={{ x: anim.in, duration: 500, opacity: 1 }}
				 out:fly={{ x: anim.out, duration: 500, opacity: 1 }}
		>
			<Slide text={currentTab.label} />
		</div>
	{:else if currentTab.id === 2}
		<div
				 style="--back: {currentTab.back}"

				 bind:this={slideWrapper}
				 in:fly={{ x: anim.in, duration: 500, opacity: 1 }}
				 out:fly={{ x: anim.out, duration: 500, opacity: 1 }}
		>
			<Slide text={currentTab.label} />
		</div>
	{:else if currentTab.id === 3}
		<div
				 style="--back: {currentTab.back}"

				 bind:this={slideWrapper}
				 in:fly={{ x: anim.in, duration: 500, opacity: 1 }}
				 out:fly={{ x: anim.out, duration: 500, opacity: 1 }}
		>
			<Slide text={currentTab.label} />
		</div>
	{/if}

	<Tabs bind:activeTab items={tabItems} />
</main>

<style>
	main {overflow: hidden; position: relative}
	div {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		background: var(--back);
		overflow: hidden;
		color: white;
		text-align: center;
	}
</style>
