<script lang="ts">
	// -- Setup --
	import Fa from "svelte-fa"
	import { faInfoCircle } from "@fortawesome/free-solid-svg-icons"

	const packageName = "svelte-gallery"
	const source = "https://github.com/janosh/svelte-bricks"

	let numberOfImages = 20

	function randomIntFromInterval(min: number, max: number) {
		// min and max included
		return Math.floor(Math.random() * (max - min + 1) + min)
	}

	// -- Svelte-gallery --
	import Gallery from "svelte-gallery"

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
</script>

<h1 class="text-4xl font-semibold capitalize">{packageName}</h1>
<div class="breadcrumbs text-sm">
	<ul>
		<li><a href="/">Home</a></li>
		<li><a class="capitalize" href={"/" + packageName}>{packageName}</a></li>
	</ul>
</div>

<div role="alert" class="alert">
	<Fa icon={faInfoCircle} class="" />
	<span>
		Source:
		<a class="link" href={source}>{source}</a>
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
	<!-- Gallery code -->
	<Gallery {images} />
</div>
