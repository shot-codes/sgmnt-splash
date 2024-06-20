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
	class="absolute top-1/2 left-1/2 mt-[250px] -translate-x-1/2 -translate-y-1/2 transform rounded border border-black px-6 py-2 transition duration-300 ease-in-out hover:bg-neutral-900 hover:text-neutral-100"
	>Curious?</a
>
