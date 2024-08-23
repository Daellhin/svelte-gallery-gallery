<script lang="ts">
	import Gallery from "svelte-gallery"

	function randomIntFromInterval(min: number, max: number) {
		// min and max included
		return Math.floor(Math.random() * (max - min + 1) + min)
	}

	let numberOfImages = 20

	$: images = Array(numberOfImages)
		.fill(0)
		.map((e) => {
			const random1 = randomIntFromInterval(1, 5) * 100
			const random2 = randomIntFromInterval(1, 5) * 100
			return {
				src: `https://www.placebear.com/${random1}/${random2}`,
				width: random1,
				height: random2,
			}
		})
	$: console.log(images)
</script>

<h1 class="text-4xl font-semibold">Svelte-Gallery</h1>
<div class="breadcrumbs text-sm">
	<ul>
		<li><a href="/">Home</a></li>
		<li><a href="/svelte-gallery">Svelte-Gallery</a></li>
	</ul>
</div>

<div role="alert" class="alert">
	<svg
		xmlns="http://www.w3.org/2000/svg"
		fill="none"
		viewBox="0 0 24 24"
		class="stroke-info h-6 w-6 shrink-0"
	>
		<path
			stroke-linecap="round"
			stroke-linejoin="round"
			stroke-width="2"
			d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
		></path>
	</svg>
	<span>
		Source:
		<a class="link" href="https://github.com/madeleineostoja/svelte-gallery">
			https://github.com/madeleineostoja/svelte-gallery
		</a>
		<ul class="menu">
			<li>- Uses grid</li>
			<li>- Crops images</li>
		</ul>
	</span>
</div>

<div class="mt-4">
	<input
		type="range"
		min="0"
		max="100"
		bind:value={numberOfImages}
		class="range"
		title={numberOfImages.toString()}
	/>
	<Gallery {images} />
</div>
