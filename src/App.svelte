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
		color: ['fill-red-500', 'fill-amber-500', 'fill-green-600', 'fill-sky-600'][i % 4],
		is_winner: false,
	}))

	function shuffle() {
		name_input = names
			.map(n => ({n, sort: Math.random()}))
			.sort((a, b) => a.sort - b.sort)
			.map(n => n.n)
			.join('\n')
	}

	function roll() {
		wheel_angle += TAU * (4 + Math.random())
		fields.forEach((_, i) => fields[i].is_winner = false)
		setTimeout(() => fields[Math.floor(((-wheel_angle / TAU) % 1 + 1) * fields.length)].is_winner = true, 4000)
	}
</script>

<main class="p-4 flex max-sm:flex-col max-h-screen">
	<div class="flex flex-col gap-2 shrink-0">
		<h1 class="text-3xl font-extrabold">wheel-of-names</h1>
		<textarea class="input grow" bind:value={name_input}></textarea>
		<div class="flex justify-between">
			<button class="btn" on:click={shuffle}>shuffle</button>
			<button class="btn" on:click={roll}>roll</button>
		</div>
	</div>
	<Wheel {fields} {wheel_angle} />
</main>
