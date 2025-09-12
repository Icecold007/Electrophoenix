<script lang="ts">
	import ayaan from '$lib/assets/ayaan.jpg';
</script>

<div class="About-club">
	<div class="About">
		<h1 class="Heading" style="font-style: italic; font-weight: bold;">
			About <span style="color:#0000ff;">Electro</span>Phoenix
		</h1>
		<p class="Content" style="font-size: 18px; margin-top: 20px;">
			ElectroPhoenix is a student-run organization dedicated to fostering innovation and creativity
			in the field of electronics and robotics. Our mission is to provide a collaborative
			environment where students can learn, experiment, and develop their skills in these exciting
			areas.
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
				<p class="text-center">Dear ElectroPhoenix Members,</p>
				<p class=" text-center">
					I am honored to serve as the President of ElectroPhoenix. Our organization is committed to
					providing you with the resources and support you need to excel in your projects and
					initiatives. Together, we can push the boundaries of innovation and creativity in
					electronics and robotics.
				</p>
				<p class="text-center">Sincerely,</p>
				<p class="text-center">Ayaan</p>
			</div>
		</div>
	</div>
</div>

<style>
	.About-club {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
		width: 100vw;
		text-align: center;
		padding: 2rem;
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
