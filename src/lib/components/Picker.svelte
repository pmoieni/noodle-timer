<script lang="ts">
	const now = new Date();

	/*
	const monthstoidx: { [key: string]: number } = {
		jan: 0,
		feb: 1,
		mar: 2,
		apr: 3,
		may: 4,
		jun: 5,
		jul: 6,
		aug: 7,
		sep: 8,
		oct: 9,
		nov: 10,
		dec: 11
	};

	const idsToMonths: { [key: number]: string } = {
		0: 'jan',
		1: 'feb',
		2: 'mar',
		3: 'apr',
		4: 'may',
		5: 'jun',
		6: 'jul',
		7: 'aug',
		8: 'sep',
		9: 'oct',
		10: 'nov',
		11: 'dec'
	};
    */

	let title = '';
	let year = now.getFullYear();
	let month = now.getMonth();
	let day = now.getDate();
	let hour = now.getHours();
	let minute = now.getMinutes();

	function copyCode() {
		let code = window.location.href;

		const target = new Date(year, month, day, hour, minute).getTime();

		const now = new Date().getTime();

		code += `?title=${btoa(title)}&`;
		code += `target=${target}&`;
		code += `created_at=${now}`;

		navigator.clipboard.writeText(code);
	}
</script>

<form class="picker" method="dialog">
	<div class="inputs">
		<label for="title">Title</label>
		<input name="title" bind:value={title} type="text" />
		<label for="year">Year</label>
		<input name="year" bind:value={year} type="number" />
		<label for="month">Month</label>
		<select name="month" bind:value={month}>
			<option value={0}>January</option>
			<option value={1}>February</option>
			<option value={2}>March</option>
			<option value={3}>April</option>
			<option value={4}>May</option>
			<option value={5}>June</option>
			<option value={6}>July</option>
			<option value={7}>August</option>
			<option value={8}>September</option>
			<option value={9}>October</option>
			<option value={10}>November</option>
			<option value={11}>December</option>
		</select>
		<label for="day">Day</label>
		<input name="day" bind:value={day} type="number" />
		<label for="hour">Hour</label>
		<input name="hour" bind:value={hour} type="number" />
		<label for="minute">Minute</label>
		<input name="minute" bind:value={minute} type="number" />
	</div>
	<button onclick={copyCode}>Copy code</button>
</form>

<style>
	.picker {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: #fff;
		padding: 1rem;
		border-radius: 0.5rem;

		.inputs {
			display: flex;
			flex-direction: column;

			label {
				margin-bottom: 0.2rem;
			}

			input,
			select {
				outline: transparent;
				border: none;
				margin-bottom: 1rem;
				padding: 1rem;
				background-color: #ddd;
				border-radius: 0.5rem;
			}
		}

		button {
			width: 100%;
			background-color: #0f0;
			border: none;
			outline: transparent;
			padding: 1rem;
			border-radius: 0.5rem;
			font-weight: bold;
			color: #000;
		}
	}
</style>
