<script lang="ts">
	// -- Setup --
	import Fa from "svelte-fa"
	import { faInfoCircle } from "@fortawesome/free-solid-svg-icons"

	const packageName = "lightgallery"
	const source = "https://github.com/janosh/svelte-bricks"

	let numberOfImages = 20

	function randomIntFromInterval(min: number, max: number) {
		// min and max included
		return Math.floor(Math.random() * (max - min + 1) + min)
	}

	import lightGallery from "lightgallery"
	import { onMount } from "svelte"
	import lgThumbnail from "lightgallery/plugins/thumbnail"
	import lgZoom from "lightgallery/plugins/zoom"

	onMount(() => {
		lightGallery(document.getElementById("lightgallery")!, {
			plugins: [lgZoom, lgThumbnail],
			speed: 500,
		})
	})
</script>

<h1 class="text-4xl font-semibold capitalize">{packageName}</h1>
<div class="breadcrumbs text-sm">
	<ul>
		<li><a href="/">Home</a></li>
		<li><a class="capitalize" href={"/" + packageName}>{packageName}</a></li>
	</ul>
</div>

<div class="header d-flex flex-column align-items-center">
	<h1 class="display-6 mt-3 mb-0">lightGallery</h1>
	<p class="lead mt-2 mb-4">
	  lightGallery is a feature-rich, modular JavaScript gallery plugin for building beautiful image and video galleries for the web and the mobile
	</p>
	<a class="btn mb-5 btn-outline-primary" href="https://github.com/sachinchoolur/lightGallery" target="_blank">View on GitHub</a>
  </div>
  <div class="gallery-container d-flex align-items-center justify-content-center" id="gallery-container">
  
	<a data-lg-size="1400-1400" class="gallery-item" data-src="https://images.unsplash.com/photo-1588093413519-17cec3f64e40?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1400&q=80" data-sub-html="<h4>Photo by - <a href='https://unsplash.com/@entrycube' >Diego Guzmán </a></h4> <p> Location - <a href='https://unsplash.com/s/photos/fushimi-inari-taisha-shrine-senbontorii%2C-68%E7%95%AA%E5%9C%B0-fukakusa-yabunouchicho%2C-fushimi-ward%2C-kyoto%2C-japan'>Fushimi Ward, Kyoto, Japan</a></p>">
	  <img class="img-fluid" src="https://images.unsplash.com/photo-1588093413519-17cec3f64e40?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=240&q=80" />
	</a>
	<a data-lg-size="1443-1329" class="gallery-item" data-src="https://images.unsplash.com/photo-1563502310703-1ffe473ad66d?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1443&q=80" data-sub-html="<h4>Photo by - <a href='https://unsplash.com/@asoshiation' >Shah </a></h4><p> Location - <a href='https://unsplash.com/s/photos/shinimamiya%2C-osaka%2C-japan'>Shinimamiya, Osaka, Japan</a></p>">
	  <img class="img-fluid" src="https://images.unsplash.com/photo-1563502310703-1ffe473ad66d?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=240&q=80" />
	</a>
	<a data-lg-size="1400-1402" class="gallery-item" data-src="https://images.unsplash.com/photo-1613541444699-39429d990353?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1400&q=80" data-sub-html="<h4>Photo by - <a href='https://unsplash.com/@katherine_xx11' >Katherine Gu </a></h4><p> For all those years we were alone and helpless.</p>">
	  <img class="img-fluid" src="https://images.unsplash.com/photo-1613541444699-39429d990353?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=240&q=80" />
	</a>
  </div>