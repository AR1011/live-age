<script>
	import { dobStore, page } from '../../stores.js';

	let dob = null;

	function submit() {
		if (dob) {
			dobStore.set(dob);
			page.set('dob');
		}
	}
</script>

<div class="add-dob">
	<form on:submit|preventDefault={submit} class="form">
		<input type="date" id="dob" name="dob" bind:value={dob} class="date-selector" />
		<button type="submit" class="submit-btn">Submit</button>
	</form>
</div>

<style>
	.add-dob {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: calc(100vh - 100px);
		overflow: hidden;
		font-family: monospace;
	}

	.form {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.date-selector {
		margin-bottom: 10px;
		font-family: monospace;
		padding: 5px;
		border-radius: 10px;
		border: 1px solid #ccc;
		width: 200px;
		height: 30px;
		font-size: 16px;
	}

	.submit-btn {
		background-color: black;
		color: white;
		padding: 8px 15px;
		border: none;
		border-radius: 10px;
		cursor: pointer;
		transition: 0.3s ease;
		font-family: monospace;
		font-size: 16px;
		width: 100px;
		height: 40px;
	}

	.submit-btn:hover {
		background-color: #555;
	}
</style>
