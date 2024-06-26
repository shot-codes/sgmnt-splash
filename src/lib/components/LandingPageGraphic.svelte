<script lang="ts">
	import { T, useFrame } from '@threlte/core';
	import { interactivity, OrbitControls } from '@threlte/extras';
	import { Color } from 'three';
	import { spring } from 'svelte/motion';

	import { LayerMaterial, Fresnel, Displace } from 'lamina/vanilla';

	export let fov = 24;

	const displace = new Displace({
		strength: 2,
		scale: 0.5,
		type: 'perlin',
		offset: [0, 0, 0],
		mode: 'normal',
		visible: true
	});

	const material = new LayerMaterial({
		color: '#9fcfff',
		lighting: 'physical',
		layers: [
			displace,
			new Fresnel({
				color: new Color('#ffa080'),
				alpha: 1,
				power: 0.75,
				intensity: 1,
				bias: 0,
				mode: 'screen',
				visible: true
			})
		]
	});

	const scale = spring(1.0, { stiffness: 0.1 });

	useFrame(() => {
		// @ts-expect-error - this property is present when running, not sure why ts doesn't pick up on it.
		displace.offset[0] += 0.005 * (1 + ($scale - 1) * 5);
	});

	interactivity();
</script>

<T.PerspectiveCamera makeDefault position={[10, 10, 10]} {fov}>
	<OrbitControls enablePan={false} enableRotate={false} enableZoom={false} target={[0, 0, 0]} />
</T.PerspectiveCamera>

<T.DirectionalLight castShadow position={[3, 10, 10]} />
<T.DirectionalLight position={[-3, 10, -10]} intensity={0.9} />
<T.AmbientLight intensity={0.9} />

<T.Mesh
	{material}
	on:pointerenter={() => {
		$scale = 1.5;
	}}
	on:pointerleave={() => {
		$scale = 1.0;
	}}
>
	<T.SphereGeometry args={[1, 64, 64]} />
</T.Mesh>
