<script lang="ts">
	// -- Setup --
	import Fa from "svelte-fa"
	import { faInfoCircle, faImage } from "@fortawesome/free-solid-svg-icons"

	const packageName = "tailwind-image-gallery"
	const source = "https://tailwindflex.com/@alok/tailwind-image-gallery"

	interface ImageType {
		src: string
		width: number | undefined
		height: number | undefined
	}

	let numberOfImages = 50

	function randomIntFromInterval(min: number, max: number) {
		// min and max included
		return Math.floor(Math.random() * (max - min + 1) + min)
	}

	// -- tailwind-image-gallery --
	let innerWidth = 0

	$: gridCols = getGridCols(innerWidth)
	$: images = Array(numberOfImages)
		.fill(0)
		.map((e) => {
			const random1 = randomIntFromInterval(200, 600)
			const random2 = randomIntFromInterval(200, 600)
			return {
				src: `https://www.placebear.com/${random1}/${random2}`,
				width: undefined,
				height: undefined,
			}
		}) as ImageType[]
	$: gridSpan2 = calculateGridSpans(images, gridCols)

	function getGridCols(screenWidth: number) {
		switch (true) {
			case screenWidth < 640: // Below 'sm'
				return 2
			case screenWidth >= 640 && screenWidth < 768: // 'sm'
				return 3
			case screenWidth >= 768 && screenWidth < 1024: // 'md'
				return 4
			case screenWidth >= 1024 && screenWidth < 1280: // 'lg'
				return 5
			case screenWidth >= 1280 && screenWidth < 1536: // 'xl'
				return 6
			case screenWidth >= 1536: // '2xl'
				return 7
			default:
				return 0
		}
	}

	function calculateGridSpans(images: ImageType[], gridCols: number) {
		if (innerWidth < 0) return Array(images.length).fill(false)

		let currentRowFill = 0

		return images.map((image, index) => {
			const isWide =
				image.width && image.height ? image.width > 1.2 * image.height : false
			const span2 = isWide && currentRowFill + 2 <= gridCols

			currentRowFill = (currentRowFill + (span2 ? 2 : 1)) % gridCols
			return span2
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
			<li>- Uses grid</li>
			<li>- Supports lazy loading</li>
			<li>- Very nice</li>
		</ul>
	</span>
</div>

<div class="mt-4">
	<div>
		Grid-cols: {gridCols}
	</div>
	<div>
		Images: {images.length}
	</div>
	<input
		type="range"
		min="0"
		max="100"
		bind:value={numberOfImages}
		class="range"
		title={numberOfImages.toString()}
	/>

	<!-- Gallery code -->
	<div class="mx-auto">
		<div
			class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 2xl:grid-cols-7 gap-2 sm:gap-4"
		>
			{#each images as image, index}
				<div
					class="group relative flex h-48 items-end overflow-hidden rounded-lg md:h-80"
					class:md:col-span-2={gridSpan2[index]}
				>
					<img
						loading="lazy"
						src={image.src}
						class="absolute inset-0 h-full w-full object-cover object-center"
						title={`${image.width}x${image.height}=${gridSpan2[index]}`}
						bind:naturalWidth={image.width}
						bind:naturalHeight={image.height}
					/>
					<div
						class="flex items-center justify-center w-full h-full bg-base-300 rounded-t-lg"
					>
						<Fa icon={faImage} size="lg" />
					</div>
				</div>
			{/each}
		</div>
	</div>
</div>
