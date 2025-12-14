<script lang="ts">
	import Window from '$lib/components/Window.svelte';

	let showEmail = false;
	const email = 'hi@weblu.ch';
</script>

<svelte:head>
	<title>Lukas Weber - Software Engineer</title>
</svelte:head>

<div class="flex min-h-screen items-center justify-center p-4">
	<Window title="About me">
		<div class="flex flex-col items-center gap-6 sm:flex-row sm:items-start">
			<div class="flex-shrink-0">
				<img
					src="https://avatars.githubusercontent.com/u/11683901"
					alt="Profile"
					class="h-24 w-24 rounded-full bg-gray-600/50 object-cover sm:h-32 sm:w-32"
				/>
			</div>
			<div class="flex-1 text-center sm:text-left">
				<h1 class="mb-4 text-2xl">Hi I'm Lukas!</h1>
				<p class="mb-4">
					I'm a software engineer based in Switzerland, most recently mainly working with Rust and
					having tons of fun with it. <br /><br />
					I love learning new technologies and coming up with simple and creative solutions to complex
					problems.<br /><br />
					Email me using
					{#if showEmail}
						<a class="text-blue-400 hover:text-blue-300" href={`mailto:${email}`}>{email}</a>
					{:else}
						<button
							type="button"
							class="text-blue-400 underline underline-offset-4 hover:text-blue-300"
							on:click={() => (showEmail = true)}
						>
							this address
						</button>
					{/if}.
				</p>
				<div class="flex justify-center gap-4 pt-4 sm:justify-start">
					<a
						href="https://github.com/lukasweber"
						target="_blank"
						rel="noopener noreferrer"
						class="text-blue-400 hover:text-blue-300">GitHub</a
					>
					<a
						href="https://gitlab.com/lukasweber"
						target="_blank"
						rel="noopener noreferrer"
						class="text-blue-400 hover:text-blue-300">GitLab</a
					>
					<a
						href="https://www.linkedin.com/in/lukas-weber-5a6a6a170/"
						target="_blank"
						rel="noopener noreferrer"
						class="text-blue-400 hover:text-blue-300">LinkedIn</a
					>
				</div>
			</div>
		</div>
	</Window>
</div>
