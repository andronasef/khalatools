<script>
	let days = 1;
	let hours = 1;
	const hourPrice = 15;
	const weeks = 4;
	$: cost = days * hours * hourPrice * weeks;
</script>

<div class="w-4/5 lg:w-1/2 m-auto gap-5 grid">
	<h1>اسعار خالة العيال</h1>
	<!--  عدد الايام -->
	<div class="grid gap-2">
		<label class="label" for="days">عدد الايام</label>
		<input
			name="days"
			type="range"
			min="1"
			max="7"
			bind:value={days}
			class="range range-primary"
			step="1"
		/>
		<div class="w-full flex justify-between text-xs px-2">
			<span>1</span>
			<span>2</span>
			<span>3</span>
			<span>4</span>
			<span>5</span>
			<span>6</span>
			<span>7</span>
		</div>
	</div>
	<!--  عدد الساعات -->
	<div class="grid gap-2">
		<label class="label" for="hours">عدد الساعات</label>
		<input
			name="hours"
			type="range"
			min="1"
			max="8"
			bind:value={hours}
			class="range range-primary"
			step="1"
		/>
		<div class="w-full flex justify-between text-xs px-2">
			<span>1</span>
			<span>2</span>
			<span>3</span>
			<span>4</span>
			<span>5</span>
			<span>6</span>
			<span>7</span>
			<span>8</span>
		</div>
	</div>
	<div class="text-lg mt-5">الاشتراك الشهري = {cost} جنيه</div>
</div>

<style>
	h1 {
		@apply text-2xl font-bold;
	}

	label {
		@apply text-lg;
	}
</style>
