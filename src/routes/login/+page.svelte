<svelte:options runes={true} />

<script lang="ts">
	import LoginForm from '$lib/components/login-form.svelte';

	let loggedInUser = $state<string | null>(null);
	let loginMessage = $state('');

	// This function will be passed to the Login component as a callback
	function handleLoginSuccess(username: string, message: string) {
		loggedInUser = username;
		loginMessage = message;
		console.log(`Parent received: User - ${username}, Message - ${message}`);
	}

	function handleLogout() {
		loggedInUser = null;
		loginMessage = '';
	}
</script>

<div class="flex h-screen w-full items-center justify-center px-4">
	{#if loggedInUser}
		<h1>Welcome, {loggedInUser}!</h1>
		<p>{loginMessage}</p>
		<button onclick={handleLogout}>Logout</button>
	{:else}
		<LoginForm onLoginSuccess={handleLoginSuccess} />
	{/if}
</div>
