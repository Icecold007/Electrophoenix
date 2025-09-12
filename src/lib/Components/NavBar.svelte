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

		<ul class:open={isOpen}>
			<li><a href="#about">About</a></li>
			<li><a href="#events">Events</a></li>
			<li><a href="#team">Team</a></li>

			<li><a href="#contact">Contact</a></li>
		</ul>
	</div>
</nav>

<style>
	.navbar {
		position: fixed;
		top: 1.5rem;
		left: 50%;
		transform: translateX(-50%);
		background: rgba(255, 255, 255, 0.92);
		box-shadow:
			0 8px 32px 0 #0000ff33,
			0 2px 16px 0 rgba(0, 0, 255, 0.13);
		border-radius: 2rem;
		padding: 0.5rem 2.5rem;
		z-index: 100;
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
		font-style: italic;
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
	}
	.bar {
		width: 1.7rem;
		height: 3px;
		background: #0000ff;
		margin: 2.5px 0;
		border-radius: 2px;
		transition: all 0.3s;
	}
	@media (max-width: 800px) {
		.navbar {
			padding: 0.5rem 1rem;
		}
		.container {
			gap: 1rem;
		}
		ul {
			position: absolute;
			top: 100%;
			left: 0;
			right: 0;
			background: rgba(255, 255, 255, 0.98);
			box-shadow: 0 8px 32px 0 #0000ff33;
			border-radius: 0 0 1.5rem 1.5rem;
			flex-direction: column;
			align-items: stretch;
			gap: 0.5rem;
			padding: 1.2rem 0 1rem 0;
			max-height: 0;
			overflow: hidden;
			transition: max-height 0.35s cubic-bezier(0.4, 2, 0.6, 1);
			display: none;
		}
		ul.open {
			max-height: 400px;
			display: flex;
		}
		.hamburger {
			display: flex;
		}
	}
	@media (max-width: 600px) {
		.navbar {
			top: 0.7rem;
			padding: 0.3rem 0.3rem;
			min-width: unset;
			max-width: 98vw;
			border-radius: 1.2rem;
		}
		.logo img {
			height: 1.5rem;
		}
		ul {
			padding: 0.7rem 0 0.5rem 0;
		}
		.hamburger {
			width: 1.7rem;
			height: 1.7rem;
			margin-left: 0.5rem;
		}
		.bar {
			width: 1.2rem;
			height: 2.5px;
		}
	}
</style>
