<script lang="ts">
	import ayaan from '$lib/assets/ayaan.jpg';
	import SectionWrapper from './SectionWrapper.svelte';
</script>

<SectionWrapper divId="about">
	<div class="About-club">
		<div class="About">
			<h1 class="Heading" style="font-style: italic; font-weight: bold;">
				About <span style="color:#0000ff;">Electro</span>Phoenix
			</h1>
			<p class="Content" style="font-size: 18px; margin-top: 20px;">
				We are the Electronics and Communication Engineering club of NEHU, focused on innovation
				across electronics, communication, AI/ML and robotics. We learn by building projects, blogs,
				workshops and mentorship.
			</p>
		</div>
		<div class="President">
			<h2 class="text-bold Heading" style="font-weight: bold; font-style: italic;">
				Letter From Our <span style="color:#0000ff">President</span>
			</h2>
			<div class="container">
				<div class="image">
					<img src={ayaan} alt="" />
				</div>
				<div class="letter">
					<p class="text-center">Hello everyone,</p>
					<p class=" text-center">
						Myself Ayaan Hafiz, final year Btech ECE student and the president of
						electrophoenix,NEHU. I believe that everyone can achieve what they want if they have the
						dedication to put in the work. Doesn’t matter who you are and where you come from, if
						you are serious about your work no one can stop you from achieving it. That is what i
						expect from everyone in this club, a dedication to achieve heights no one has ever
						crossed. I encourage everyone to come and join us and be a part of this great club where
						we discuss, collaborate and join hands to take our professional career to the next
						level.
					</p>
				</div>
			</div>
		</div>
	</div>
</SectionWrapper>

<style>
	.About-club {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
		width: 100vw;
		text-align: center;
		padding: 20rem;
		overflow-x: hidden;
		box-sizing: border-box;
	}

	.About {
		text-align: center;
		padding: 20px;
		width: 100%;
	}

	.Heading {
		text-align: center;
		padding: 2rem 1rem;
		font-size: 3.5rem;
	}

	@media (max-width: 768px) {
		.Heading {
			font-size: 2rem;
			padding: 1rem;
		}
	}

	.Content {
		text-align: center;
		padding: 1rem;
		font-size: 1rem;
		line-height: 1.6;
	}

	.About,
	.President {
		max-width: 1200px;
		margin: 0 auto;
		padding: 2rem 1rem;
	}

	.container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 2rem;
	}

	.letter {
		max-width: 500px;
		font-size: 1rem;
		text-align: left;
		line-height: 1.6;
	}

	.image {
		width: 300px;
		max-width: 90%;
		height: auto;
		border-radius: var(--radius-xl);
		overflow: hidden;
	}

	@media (max-width: 768px) {
		.letter {
			text-align: center;
		}
	}
</style>
