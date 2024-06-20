<script lang="ts">
	import { Canvas } from '@threlte/core';
	import LandingPageGraphic from '$lib/components/LandingPageGraphic.svelte';

	let fov = 24;
    let innerWidth: number;

    $: {
        if (innerWidth < 640) {
            fov = 50;
        } else if (innerWidth < 768){
            fov = 45;
        } else {
            fov = 24;
        }
    }
</script>

<svelte:window bind:innerWidth />
<img
	class="pointer-events-none absolute top-1/2 left-1/2 w-[250px] -translate-x-1/2 -translate-y-1/2 transform sm:w-[300px] md:w-[500px]"
	src="/img/sgmnt-2layer-solid-black.svg"
	alt="smgntlogo"
/>

<div
	class="absolute top-1/2 left-1/2 h-[500px] w-[600px] -translate-x-1/2 -translate-y-1/2 transform"
>
	<Canvas>
		<LandingPageGraphic {fov} />
	</Canvas>
</div>

<img
	class="pointer-events-none absolute top-1/2 left-1/2 w-[250px] -translate-x-1/2 -translate-y-1/2 transform sm:w-[300px] md:w-[500px]"
	src="/img/sgmnt-2layer-outline-black.svg"
	alt="smgntlogo"
/>

<a
	href="/about"
	class="absolute top-1/2 left-1/2 mt-[250px] -translate-x-1/2 -translate-y-1/2 transform rounded border border-black p-1 px-3 transition-all duration-500 hover:bg-black hover:text-white dark:border-white dark:hover:bg-white dark:hover:text-black"

	>Curious?</a
>
