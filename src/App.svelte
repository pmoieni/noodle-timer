<script lang="ts">
	import { onMount } from 'svelte';
	import Progress from './lib/components/Progress.svelte';

	let isCorrupt = $state(false);

	const urlParams = new URLSearchParams(window.location.search);

	if (!urlParams.has('title') || !urlParams.has('target') || !urlParams.has('created_at')) {
		isCorrupt = true;
	}

	const title = atob(urlParams.get('title')!);
	const target = parseInt(urlParams.get('target')!);
	const createdAt = parseInt(urlParams.get('created_at')!);
	const totalTime = target - createdAt;
	const now = new Date().getTime();

	let timeLeft = $state(target - now);
	const timeLeftFormatted = $derived(new Date(timeLeft).toISOString().substring(11, 19));

	const getProgress = () => {
		const now = new Date().getTime();
		return Math.ceil(((now - createdAt) / totalTime) * 100);
	};

	let progress = $state(getProgress());
	// url: http://localhost:5173/?title=QUJJIEFieXNzIEZpbmFscw==&target=1763246124000&created_at=1763238924000

	onMount(() => {
		setInterval(() => {
			const now = new Date().getTime();
			timeLeft = target - now;
			progress = getProgress();
		}, 1000);
	});
</script>

<main>
	<h1>{isCorrupt ? '' : title}</h1>
	<div class="display">
		<img src="/glorpass.gif" alt="glorpass" />
		<h2>{isCorrupt ? 'corrupt link' : timeLeftFormatted}</h2>
		<img src="/glorpass.gif" alt="glorpass" />
	</div>
	<Progress {progress} />
</main>

<style>
	main {
		width: 100%;
		height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background-color: #000;

		& > h1 {
			color: #fff;
			font-weight: bold;
		}

		.display {
			display: flex;
			align-items: center;
			justify-content: center;

			h2 {
				color: #00ff00;
				font-weight: bold;
			}

			img {
				height: 5rem;
				width: auto;
			}
		}
	}
</style>
