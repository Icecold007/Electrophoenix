<script lang="ts">
	import SectionWrapper from './SectionWrapper.svelte';

	let name = '';
	let email = '';
	let message = '';
	let submitted = false;

	function handleSubmit() {
		submitted = true;
	}
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" />
	<link
		href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap"
		rel="stylesheet"
	/>
</svelte:head>
<SectionWrapper divId="contact">
	<div class="contact-section">
		<h2 class="contact-heading">
			<span style="color:#0000ff;font-style:italic;">Contact</span> Us
		</h2>

		<form class="contact-form" on:submit|preventDefault={handleSubmit}>
			<div class="form-group">
				<label for="name">Name</label>
				<input id="name" type="text" bind:value={name} required placeholder="Your Name" />
			</div>
			<div class="form-group">
				<label for="email">Email</label>
				<input id="email" type="email" bind:value={email} required placeholder="you@email.com" />
			</div>
			<div class="form-group">
				<label for="message">Message</label>
				<textarea
					id="message"
					rows="5"
					bind:value={message}
					required
					placeholder="Type your message..."
				></textarea>
			</div>
			<button class="submit-btn" type="submit">Send Message</button>
			{#if submitted}
				<p class="thankyou">Thank you for reaching out! We'll get back to you soon.</p>
			{/if}
		</form>
	</div>
</SectionWrapper>

<style>
	:global(body) {
		font-family: 'Inter', sans-serif;
		background-color: #f0f4f8;
		margin: 0;
		display: grid;
		place-items: center;
		min-height: 100vh;
		color: #333;
	}

	.contact-section {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 3rem 1rem;
		box-sizing: border-box;
	}

	@keyframes slide-in-up {
		from {
			opacity: 0;
			transform: translateY(40px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.contact-heading {
		font-size: 2.5rem;
		font-weight: bold;
		text-align: center;
		margin-bottom: 2.5rem;
		font-style: italic;
		letter-spacing: 1px;
		color: #111;

		animation: slide-in-up 0.6s 0.1s cubic-bezier(0.25, 1, 0.5, 1) backwards;
	}

	.contact-form {
		background: #fff;
		border-radius: 1.5rem;
		box-shadow:
			0 10px 40px rgba(0, 0, 255, 0.1),
			0 4px 15px rgba(0, 0, 255, 0.08);
		padding: 2.5rem;
		max-width: 450px;
		width: 100%;
		display: flex;
		flex-direction: column;
		gap: 1.5rem;
		box-sizing: border-box;
	}

	.form-group {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
		opacity: 0;

		animation: slide-in-up 0.5s cubic-bezier(0.25, 1, 0.5, 1) forwards;
	}

	.form-group:nth-of-type(1) {
		animation-delay: 0.3s;
	}
	.form-group:nth-of-type(2) {
		animation-delay: 0.4s;
	}
	.form-group:nth-of-type(3) {
		animation-delay: 0.5s;
	}

	label {
		font-weight: 600;
		color: #0000ff;
		font-size: 1rem;
		font-style: italic;
	}

	input,
	textarea {
		border: 2px solid #e0e0e0;
		border-radius: 0.75rem;
		padding: 0.8rem 1.1rem;
		font-size: 1rem;
		font-family: inherit;
		background: #f7f7f7;

		transition:
			border 0.2s,
			box-shadow 0.2s,
			transform 0.2s ease-out,
			background 0.2s;
		outline: none;
		resize: none;
	}

	input:focus,
	textarea:focus {
		border-color: #0000ff;
		box-shadow: 0 0 0 3px #0000ff33;
		background: #fff;
		transform: scale(1.02);
	}

	.submit-btn {
		background: #0000ff;
		color: #fff;
		font-size: 1.1rem;
		font-weight: 700;
		border: 2px solid transparent;
		border-radius: 0.75rem;
		padding: 0.9rem 2.2rem;
		cursor: pointer;
		margin-top: 0.5rem;
		box-shadow: 0 2px 12px 0 #0000ff33;
		transition: all 0.2s ease-out;
		font-style: italic;
		letter-spacing: 0.5px;
		opacity: 0;
		animation: slide-in-up 0.5s 0.6s cubic-bezier(0.25, 1, 0.5, 1) forwards;
	}

	.submit-btn:hover,
	.submit-btn:focus {
		background: #fff;
		color: #0000ff;
		border-color: #0000ff;
		box-shadow: 0 4px 24px 0 #0000ff33;
		transform: translateY(-3px) scale(1.03);
	}

	.thankyou {
		margin-top: 1rem;
		color: #0000ff;
		font-weight: 600;
		text-align: center;
		font-style: italic;
		animation: fade-in 0.7s;
	}

	@keyframes fade-in {
		from {
			opacity: 0;
			transform: translateY(10px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	@media (max-width: 600px) {
		.contact-section {
			padding: 2rem 1rem;
		}

		.contact-heading {
			font-size: 2rem;
			margin-bottom: 2rem;
		}

		.contact-form {
			padding: 2rem 1.5rem;
			max-width: 100%;
		}

		.submit-btn {
			padding: 1rem 1.5rem;
			font-size: 1.05rem;
		}
	}
</style>
