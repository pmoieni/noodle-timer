<script lang="ts">
	interface Props {
		progress: number;
	}

	let { progress }: Props = $props();
</script>

<div class="con">
	<div class="progress" style={`width: ${progress}%;`}>
		<img src="/glorp.png" alt="glorp" />
	</div>
</div>

<style>
	.con {
		height: 5rem;
		width: calc(100% - 10rem);
		max-width: 40rem;
		display: flex;
		align-items: center;
		justify-content: start;
		margin-top: 2rem;

		.progress {
			height: 100%;
			position: relative;
			background-image: url('/rainbow.png');
			background-position: center;
			background-repeat: repeat-x;
			background-size: contain;

			img {
				position: absolute;
				height: 5rem;
				width: auto;
				top: 50%;
				transform: translate(-50%, -50%);
				right: -5rem;
			}
		}
	}
</style>
