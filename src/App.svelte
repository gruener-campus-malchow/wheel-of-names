<script>
	import Wheel from './lib/Wheel.svelte'
	const TAU = Math.PI * 2

	let name_input = 'alice\nbob\ncharlie'
	$: names = name_input.split('\n')
	let wheel_angle = 0

	$: fields = names.map((name, i) => ({
		label: name,
		start_angle: TAU * (i / names.length),
		label_angle: TAU * ((i + .5) / names.length),
		end_angle: TAU * ((i + 1) / names.length),
		color: ['fill-red-500', 'fill-amber-500', 'fill-green-600', 'fill-sky-600'][i % 4]
	}))

	function roll() {
		wheel_angle += TAU * (4 + Math.random())
	}
</script>

<main class="p-4 flex max-h-screen">
	<div class="flex flex-col gap-2 shrink-0">
		<h1 class="text-3xl font-extrabold">wheel-of-names</h1>
		<textarea class="input grow" bind:value={name_input}></textarea>
		<div class="flex justify-between">
			<div></div>
			<button class="btn" on:click={roll}>roll</button>
		</div>
	</div>
	<Wheel {fields} {wheel_angle} />
</main>
