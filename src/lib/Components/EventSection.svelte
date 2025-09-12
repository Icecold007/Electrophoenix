<script lang="ts">
	import { onMount } from 'svelte';
	import SectionWrapper from './SectionWrapper.svelte';
	import art from '$lib/assets/art.jpg';
	import essay from '$lib/assets/essay.jpeg';
	import ideathon1 from '$lib/assets/ideathon1.jpeg';
	import ideathon2 from '$lib/assets/ideathon2.jpeg';
	import reconnect from '$lib/assets/reconnect.jpeg';

	let categories = [
		{
			title: 'Technical Essay Writing',
			image: essay,
			desc: 'Showcase your technical writing skills on trending topics in electronics and robotics.'
		},
		{
			title: 'Reconnect With Alumni',
			image: reconnect,
			desc: 'Network and learn from our accomplished alumni in a fun, interactive session.'
		},
		{
			title: 'Ideathon 1.0',
			image: ideathon1,
			desc: 'Pitch your innovative ideas and collaborate with fellow enthusiasts.'
		},
		{
			title: 'Art from e-waste',
			image: art,
			desc: 'Turn electronic waste into creative masterpieces and promote sustainability.'
		},
		{
			title: 'Ideathon 2.0',
			image: ideathon2,
			desc: 'A new round of brainstorming and prototyping for the next big thing.'
		}
	];

	let current = 0;
	let interval: ReturnType<typeof setInterval> | null = null;
	const SLIDE_DURATION = 5000;

	function next() {
		current = (current + 1) % categories.length;
	}
	function prev() {
		current = (current - 1 + categories.length) % categories.length;
	}
	function goTo(idx: number) {
		current = idx;
	}
	onMount(() => {
		interval = setInterval(next, SLIDE_DURATION);
		return () => interval && clearInterval(interval);
	});
	$: {
		if (interval) {
			clearInterval(interval);
			interval = setInterval(next, SLIDE_DURATION);
		}
	}
</script>

<SectionWrapper divId="events">
	<div class="event-slideshow-section">
		<h1 class="event-heading-slideshow animate-fade-in-alt">
			<span style="color:#0000ff;font-style:italic;">Electro</span>Phoenix Events
		</h1>
		<p class="event-subheading-slideshow animate-slide-down-alt">
			Where innovation meets excitement! Browse our signature events.
		</p>
		<div class="slideshow-container">
			<button class="nav-btn prev" on:click={prev} aria-label="Previous Event">&#8592;</button>
			{#each categories as event, i}
				<div
					class="slide {i === current ? 'active' : ''} {i < current ? 'left' : ''} {i > current
						? 'right'
						: ''}"
					aria-hidden={i !== current}
					style="z-index: {i === current ? 2 : 1};"
				>
					<div class="slide-content">
						<img src={event.image} alt={event.title} class="slide-img-square" />
						<div class="slide-info">
							<h2 class="slide-title">{event.title}</h2>
							<p class="slide-desc">{event.desc}</p>
						</div>
					</div>
				</div>
			{/each}
			<button class="nav-btn next" on:click={next} aria-label="Next Event">&#8594;</button>
			<div class="slide-dots">
				{#each categories as _, i}
					<span class="dot {i === current ? 'active' : ''}" on:click={() => goTo(i)}></span>
				{/each}
			</div>
		</div>
	</div>
</SectionWrapper>

<style>
	.event-slideshow-section {
		width: 100vw;
		padding: 5rem 5rem 5rem 5rem;
		background: transparent;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		overflow-x: hidden;
		position: relative;
	}

	.event-heading-slideshow {
		font-size: 2.8rem;
		font-weight: bold;
		text-align: center;
		margin-bottom: 0.5rem;
		font-style: italic;
		letter-spacing: 1px;
	}

	.event-subheading-slideshow {
		font-size: 1.2rem;
		text-align: center;
		margin-bottom: 2.5rem;
		color: #222;
	}

	.slideshow-container {
		position: relative;
		width: 100%;
		max-width: 540px;
		min-height: 420px;
		margin: 0 auto;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-top: 2.5rem; /* <-- Add this line for extra space */
	}

	.slide {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		opacity: 0;
		pointer-events: none;
		transform: scale(0.95) translateX(0);
		transition:
			opacity 0.7s cubic-bezier(0.4, 2, 0.6, 1),
			transform 0.7s cubic-bezier(0.4, 2, 0.6, 1);
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.slide.active {
		opacity: 1;
		pointer-events: auto;
		transform: scale(1) translateX(0);
		z-index: 2;
	}
	.slide.left {
		transform: scale(0.92) translateX(-60px);
		opacity: 0.2;
	}
	.slide.right {
		transform: scale(0.92) translateX(60px);
		opacity: 0.2;
	}
	.slide-content {
		background: #fff;
		border-radius: 2rem;
		box-shadow: 0 8px 32px 0 rgba(0, 0, 255, 0.13); /* blue shadow */
		padding: 3rem 2.5rem 2.5rem 2.5rem;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		max-width: 600px;
		min-height: 520px;
		animation: pop-in 0.7s cubic-bezier(0.4, 2, 0.6, 1) backwards;
	}
	@keyframes pop-in {
		0% {
			opacity: 0;
			transform: scale(0.8);
		}
		60% {
			opacity: 1;
			transform: scale(1.05);
		}
		100% {
			opacity: 1;
			transform: scale(1);
		}
	}
	.slide-img-square {
		width: 260px;
		height: 260px;
		object-fit: cover;
		border-radius: 1.2rem;
		box-shadow:
			0 0 32px 0 #0000ff99,
			0 2px 16px 0 rgba(0, 0, 255, 0.13);
		margin-bottom: 2rem;
		animation: pulse-glow 2.2s infinite cubic-bezier(0.4, 2, 0.6, 1);
		background: #f6f6f6;
	}
	@keyframes pulse-glow {
		0% {
			box-shadow:
				0 0 0 0 #0000ff33,
				0 2px 16px 0 rgba(0, 0, 255, 0.13);
		}
		70% {
			box-shadow:
				0 0 32px 8px #0000ff33,
				0 2px 16px 0 rgba(0, 0, 255, 0.13);
		}
		100% {
			box-shadow:
				0 0 0 0 #0000ff33,
				0 2px 16px 0 rgba(0, 0, 255, 0.13);
		}
	}
	.slide-info {
		text-align: center;
	}
	.slide-title {
		font-size: 1.3rem;
		font-weight: 700;
		font-style: italic;
		color: #0d183d;
		margin-bottom: 0.6rem;
		letter-spacing: 0.5px;
	}
	.slide-desc {
		font-size: 1rem;
		color: #222;
		line-height: 1.5;
	}

	.nav-btn {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		background: #fff;
		border: 2px solid #0000ff;
		color: #0000ff;
		font-size: 2rem;
		border-radius: 50%;
		width: 2.5rem;
		height: 2.5rem;
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		z-index: 3;
		transition:
			background 0.2s,
			color 0.2s,
			box-shadow 0.2s;
		box-shadow: 0 2px 8px 0 rgba(0, 0, 255, 0.1);
	}
	.nav-btn:hover {
		background: #0000ff;
		color: #fff;
	}
	.nav-btn.prev {
		left: -3.5rem;
	}
	.nav-btn.next {
		right: -3.5rem;
	}

	.slide-dots {
		position: absolute;
		bottom: -2.2rem;
		left: 50%;
		transform: translateX(-50%);
		display: flex;
		gap: 0.7rem;
		z-index: 4;
	}
	.dot {
		width: 0.9rem;
		height: 0.9rem;
		border-radius: 50%;
		background: #e0e0e0;
		cursor: pointer;
		transition:
			background 0.2s,
			box-shadow 0.2s;
		box-shadow: 0 2px 8px 0 rgba(0, 0, 255, 0.1);
	}
	.dot.active {
		background: #0000ff;
		box-shadow: 0 0 0 4px #0000ff33;
	}

	@media (max-width: 700px) {
		.slideshow-container {
			max-width: 98vw;
			min-height: 320px;
		}
		.slide-content {
			max-width: 98vw;
			min-height: 260px;
			padding: 1.2rem 0.5rem 1rem 0.5rem;
		}
		.slide-img-square {
			width: 90vw;
			max-width: 320px;
			height: 40vw;
			max-height: 320px;
		}
		.nav-btn.prev {
			left: 0.2rem;
		}
		.nav-btn.next {
			right: 0.2rem;
		}
	}
	.animate-fade-in-alt {
		animation: fade-in 1.2s cubic-bezier(0.4, 2, 0.6, 1) backwards;
	}
	.animate-slide-down-alt {
		animation: slide-down 1s cubic-bezier(0.4, 2, 0.6, 1) backwards;
	}
	@keyframes fade-in {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
	@keyframes slide-down {
		from {
			opacity: 0;
			transform: translateY(-40px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}
</style>
