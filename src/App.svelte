<script>
	let age, resting, hrr, aerobic, anaerobic, max_rate;
	let valid = false;

	const calculate = () => {
		try {
			max_rate = 205.8 - (0.685 * age);
			hrr = max_rate - resting;
			aerobic = `${Math.ceil(resting + hrr * .5)} - ${Math.ceil(resting + hrr * .75)}`;
			anaerobic = `${Math.ceil(resting + hrr * .8)} - ${Math.ceil(resting + hrr * .85)}`;
			valid = true;
		} catch (error) {
			valid = false;
		}
	}
	
</script>

<main>
	<div class="container">
		<section class="header">
			<h1>Beat-Range</h1>
			<h3>Find Your Healthy Working Heart Rate</h3>
		</section>
		<div class="box">
			<form>
				<div class="row">
					<div class="six columns offset-by-three">
						<label for="Age">Age</label>
						<input type="number" bind:value={age} class="u-full-width" placeholder="Enter your age" id="Age">
						<label for="RestingRate">Resting Heart Rate</label>
						<input type="number" bind:value={resting} class="u-full-width" placeholder="Enter your resting heart rate" id="RestingRate">
						<button type="button" class="button-primary u-full-width" on:click={calculate}>Calculate</button>
					</div>
				</div>
			</form>
		</div>
		{#if valid}
			<div class="results">
				<h4>Heart Range for a {age} year old with a resting heart rate of {resting}</h4>
				<div class="row">
					<div class="six columns offset-by-three">
						<table class="u-full-width">
							<thead>
								<tr>
									<th>Exercise</th>
									<th>Heart Rate Range</th>
								</tr>
							</thead>
							<tbody>
								<tr>
									<td>Aerobic</td>
									<td>{aerobic}</td>
								</tr>
								<tr>
									<td>Anaerobic</td>
									<td>{anaerobic}</td>
								</tr>
								<tr>
									<td>Max</td>
									<td>{Math.ceil(max_rate)}</td>
								</tr>
							</tbody>
						</table>
					</div>
				</div>
			</div>
		{/if}
	</div>
	
</main>

<style>
	.header {
		margin-top: 8rem;
		text-align: center;
	}
	.container {
		max-width: 800px;
	}
	/* .box {
		max-width: 300px;
		margin: auto;
	} */
	.results {
		padding-top: 2rem;
		text-align: center;
		/* max-width: 400px; */
		/* margin: auto; */
	}
</style>