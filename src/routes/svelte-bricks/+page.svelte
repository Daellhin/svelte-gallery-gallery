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

	// -- Svelte-bricks
	import Masonry from "svelte-bricks"

	$: images = Array(numberOfImages)
		.fill(0)
		.map((e, i) => {
			const random1 = randomIntFromInterval(1, 5) * 100
			const random2 = randomIntFromInterval(1, 5) * 100
			return {
				id: i,
				src: `https://www.placebear.com/${random1}/${random2}`,
				width: random1,
				height: random2,
			}
		})

	// -- Bigger picture --
	import BiggerPictureThumbnails from "$lib/thumbnails.svelte"
	import { onMount } from "svelte"

	const minColWidth = 200
	const maxColWidth = 800
	const gap = 20

	let biggerPictureInstance: BiggerPictureThumbnails
	let imageAnchors: HTMLAnchorElement[]
	let innerWidth: number

	onMount(() => {
		biggerPictureInstance = new BiggerPictureThumbnails({
			target: document.body,
		})
		imageAnchors = Array.from(
			document.querySelectorAll<HTMLAnchorElement>(`.imageAnchor`)
		)
	})

	function openGallery(e: MouseEvent) {
		imageAnchors = Array.from(
			document.querySelectorAll<HTMLAnchorElement>(`.imageAnchor`)
		)
		e.preventDefault()
		biggerPictureInstance.open({
			items: imageAnchors,
			el: e.currentTarget!,
		})
	}
</script>
<svelte:window bind:innerWidth />


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
			<li>- Bottom row is all over the place</li>
			<li>- Can make pictures weird dimensions</li>
			<li>- Can crop images</li>
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
	<Masonry items={images} {minColWidth} {maxColWidth} {gap} let:item let:idx>
		<a
			class={`imageAnchor ID-${item.id}`}
			href={item.src}
			data-img={item.src}
			data-thumb={item.src}
			on:click={openGallery}
		>
			<img
				src={item.src}
				class="h-full w-full object-cover object-center rounded-lg"
				loading="lazy"
				title={idx.toString()}
			/>
		</a>
	</Masonry>
</div>
