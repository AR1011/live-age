<script>
	import { onMount } from 'svelte';
	import AddDob from '$lib/components/AddDob.svelte';
	import { dobStore, page } from '../../stores.js';

	let dob = null;
	let year = '';
	let ms = '';

	function checkDob() {
		if (dob !== null) {
		} else {
			page.set('addDob');
		}
	}

	function calculateAgeInYearsMicrosecond(dateOfBirth) {
		if (!dateOfBirth) return null;
		const dob = new Date(dateOfBirth);
		const diff_ms = Date.now() - dob.getTime();
		let t = (diff_ms / 31557600000).toFixed(20);

		let s = t.split('.');
		year = s[0];
		ms = '.' + s[1];
	}

	function startLoop() {
		setInterval(() => {
			calculateAgeInYearsMicrosecond(dob);
		}, 10);
	}

	onMount(() => {
		checkDob();
		startLoop();
	});

	$: dob = $dobStore;
</script>

<main class="main">
	{#if $page === 'addDob'}
		<AddDob on:submit={checkDob} />
	{:else}
		<div class="counter">
			<p class="age-header">AGE</p>
			<p class="age">{year}<sup>{ms}</sup></p>
		</div>
	{/if}
</main>

<style>
	.main {
		cursor: crosshair;
	}

	.counter {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: calc(100vh - 100px);
		overflow: hidden;
		font-family: monospace;
		pointer-events: none;
		user-select: none;
	}

	.age-header {
		font-size: 30px;
		margin-bottom: 0;
		color: grey;
	}

	.age {
		font-size: 96px;
		margin-top: 0;
	}
	.age sup {
		font-size: 32px;
		margin-top: -20px;
		margin-bottom: 2rem;
	}
</style>
