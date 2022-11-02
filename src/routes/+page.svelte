<script lang="ts">
	import { slide } from 'svelte/transition';

	enum ServiceType {
		Hourly,
		Monthly
	}

	let days = 1;
	let hours = 1;
	const hourPriceMonthly = 15;
	const hourPriceHourly = 35;
	const weeks = 4;
	$: costHourly = hours * hourPriceHourly;
	$: costMonthly = days * hours * hourPriceMonthly * weeks;
	let type = ServiceType.Monthly;

	function changeType(serviceType: ServiceType) {
		type = serviceType;
	}
</script>

<svelte:head>
	<title>اسعار خدمة خالة العيال</title>
</svelte:head>

<div class="w-4/5 lg:w-1/2 m-auto gap-5 grid">
	<h1>اسعار خدمة خالة العيال</h1>
	<!-- Montly Hourly Tab Select -->
	<div class="tabs tabs-boxed flex justify-center items-center w-fit">
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<div
			class:tab-active={type == ServiceType.Monthly}
			on:click={() => changeType(ServiceType.Monthly)}
			class="tab transition"
		>
			شهري
		</div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<div
			class:tab-active={type == ServiceType.Hourly}
			on:click={() => changeType(ServiceType.Hourly)}
			class="tab transition"
		>
			بالساعات
		</div>
	</div>
	<!-- Monthly / Hourly -->
	<div class="min-h-16">
		{#if type == ServiceType.Monthly}
			<!-- Monthly -->
			<div transition:slide>
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
				<div class="text-lg mt-5">الاشتراك الشهري = {costMonthly} جنيه</div>
			</div>
		{:else}
			<!-- Hourly -->
			<div transition:slide class="grid gap-2">
				<!--  عدد الساعات -->
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
				<div class="text-lg mt-5">الحساب بالساعة = {costHourly} جنيه</div>
			</div>
		{/if}
	</div>
</div>

<style>
	h1 {
		@apply text-2xl font-bold;
	}

	label {
		@apply text-lg;
	}
</style>
