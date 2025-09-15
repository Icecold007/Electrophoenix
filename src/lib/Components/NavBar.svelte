<script>
	import logo from '$lib/assets/logo.png';
	let isOpen = false;

	function toggleMenu() {
		isOpen = !isOpen;
	}
</script>

<nav class="navbar">
	<div class="container">
		<a href="/" class="logo">
			<img src={logo} alt="logo" />
		</a>

		<button class="hamburger" on:click={toggleMenu} aria-label="Toggle Menu" aria-expanded={isOpen}>
			<div class="bar"></div>
			<div class="bar"></div>
			<div class="bar"></div>
		</button>

		<!-- Overlay background -->
		<div class:overlay={isOpen} on:click={() => (isOpen = false)}></div>

		<ul class:open={isOpen}>
			<li><a href="#about" on:click={() => (isOpen = false)}>About</a></li>
			<li><a href="#events" on:click={() => (isOpen = false)}>Events</a></li>
			<li><a href="#team" on:click={() => (isOpen = false)}>Team</a></li>
			<li><a href="#contact" on:click={() => (isOpen = false)}>Contact</a></li>
		</ul>
	</div>
</nav>

<style>
	.navbar {
		position: fixed;
		top: 1.5rem;
		left: 50%;
		transform: translateX(-50%);
		/* background: rgba(255, 255, 255, 0.92); */
		box-shadow:
			0 8px 32px 0 #0000ff33,
			0 2px 16px 0 rgba(0, 0, 255, 0.13);
		border-radius: 2rem;
		padding: 0.5rem 2.5rem;
		z-index: 200;
		backdrop-filter: blur(8px);
		min-width: 220px;
		max-width: 90vw;
		width: fit-content;
		transition: box-shadow 0.2s;
	}
	.container {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 2rem;
		position: relative;
	}
	.logo img {
		height: 2.2rem;
		width: auto;
		border-radius: 0.7rem;
		box-shadow: 0 2px 12px 0 #0000ff22;
	}
	ul {
		display: flex;
		align-items: center;
		gap: 2.2rem;
		list-style: none;
		margin: 0;
		padding: 0;
		transition: max-height 0.3s;
	}
	ul li a {
		font-size: 1.08rem;
		font-weight: 600;
		color: #0000ff;
		text-decoration: none;
		padding: 0.4rem 1.1rem;
		border-radius: 1.2rem;
		transition:
			background 0.18s,
			color 0.18s,
			box-shadow 0.18s;
		position: relative;
	}
	ul li a:hover,
	ul li a:focus {
		background: #0000ff;
		color: #fff;
		box-shadow: 0 2px 12px 0 #0000ff33;
	}
	.hamburger {
		display: none;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 2.2rem;
		height: 2.2rem;
		background: none;
		border: none;
		cursor: pointer;
		padding: 0;
		margin-left: 1.2rem;
		position: relative;
		z-index: 210; /* keep above overlay */
	}
	.bar {
		width: 1.7rem;
		height: 3px;
		background: #0000ff;
		margin: 2.5px 0;
		border-radius: 2px;
		transition: all 0.3s;
	}

	/* Overlay when menu open */
	.overlay {
		display: none;
	}
	.overlay.overlay {
		display: block;
		position: fixed;
		inset: 0;
		background: rgba(0, 0, 0, 0.4);
		backdrop-filter: blur(4px);
		z-index: 150;
	}

	@media (max-width: 800px) {
		.container {
			gap: 0.8rem;
		}

		ul {
			position: absolute;
			top: 110%;
			left: 0;
			right: 0;
			/* background: rgba(255, 255, 255, 0.96); */
			backdrop-filter: blur(12px);
			box-shadow: 0 8px 32px rgba(0, 0, 255, 0.15);
			border-radius: 0 0 1.5rem 1.5rem;
			flex-direction: column;
			align-items: center;
			gap: 1rem;
			padding: 1.5rem 0;
			max-height: 0;
			overflow: hidden;
			opacity: 0;
			transform: translateY(-10px);
			transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
			display: flex;
			z-index: 200;
		}

		ul.open {
			max-height: 500px;
			opacity: 1;
			transform: translateY(0);
		}

		ul li a {
			font-size: 1.2rem;
			width: 100%;
			text-align: center;
			padding: 0.8rem 0;
			border-radius: 0.8rem;
		}

		.hamburger {
			display: flex;
			width: 2rem;
			height: 2rem;
		}

		.bar {
			width: 1.5rem;
			height: 3px;
		}

		/* Hamburger → X animation */
		.hamburger[aria-expanded='true'] .bar:nth-child(1) {
			transform: rotate(45deg) translate(5px, 5px);
		}
		.hamburger[aria-expanded='true'] .bar:nth-child(2) {
			opacity: 0;
		}
		.hamburger[aria-expanded='true'] .bar:nth-child(3) {
			transform: rotate(-45deg) translate(5px, -5px);
		}
	}

	@media (max-width: 600px) {
		.navbar {
			top: 0.7rem;
			padding: 0.4rem 0.8rem;
			max-width: 95vw;
			border-radius: 1.2rem;
		}
		.logo img {
			height: 1.6rem;
		}
		ul li a {
			font-size: 1.05rem;
		}
	}
</style>
