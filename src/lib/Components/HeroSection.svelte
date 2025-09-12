<script lang="ts">
	import NeuralNetwork from './NeuralNetwork.svelte';
	import logo from '$lib/assets/logo.png';
</script>

<div class="hero-bg">
	<div class="bg-canvas" aria-hidden="true">
		<NeuralNetwork bg="transparent" />
	</div>

	<div class="hero">
		<div class="logo-container">
			<img src={logo} alt="ElectroPhoenix Logo" class="logo" />
		</div>
		<div class="hero-text">
			<h1 style="font-style: italic;">
				<span style="color: #0000ff;">Electro</span>Phoenix
			</h1>
			<p>Your Gateway to Cutting-Edge Electronics</p>
		</div>
	</div>
</div>

<style>
	.hero-bg {
		position: relative;
		width: 100vw;
		height: 100vh;
		overflow: hidden;
		background: transparent;
	}

	.bg-canvas {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		z-index: 0;
		pointer-events: none;
		display: block;
	}

	.hero {
		position: relative;
		z-index: 2;
		display: flex;
		align-items: center;
		gap: 0;
		width: 100vw;
		min-height: 40vh;
		box-sizing: border-box;
		padding: 3rem;
		background: transparent;
	}

	.logo-container {
		flex: 1 1 0;
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
		pointer-events: auto;
	}

	.logo {
		max-width: 80%;
		max-height: 60vh;
		width: 100%;
		height: auto;
		object-fit: contain;
	}

	.hero-text {
		flex: 1 1 0;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 2rem;
		box-sizing: border-box;
		pointer-events: auto;
		color: #111;
		text-shadow: 0 1px 0 rgba(255, 255, 255, 0.35);
	}

	.hero-text h1 {
		font-size: 4vw;
		margin: 0 0 1rem 0;
		color: #111 !important;
	}

	.hero-text p {
		font-size: 2vw;
		margin: 0;
		color: #111 !important;
	}

	@media (max-width: 900px) {
		.hero {
			flex-direction: column;
			padding: 2rem;
			gap: 1.2rem;
		}
		.hero-text h1 {
			font-size: 6.5vw;
		}
		.hero-text p {
			font-size: 3.2vw;
		}
	}
</style>
