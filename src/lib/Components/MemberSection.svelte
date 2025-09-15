<script lang="ts">
	import ayaan from '$lib/assets/ayaan.jpg';
	import anurag from '$lib/assets/moi.jpg';
	import ayushi from '$lib/assets/ayushi.jpg';
	import biku from '$lib/assets/biku2.png';
	import citti from '$lib/assets/citti.jpg';
	import mahi from '$lib/assets/mahi.jpg';
	import neelu from '$lib/assets/neelu.jpg';
	import ritu from '$lib/assets/ritu.jpg';
	import rohit from '$lib/assets/rohit.jpg';
	import ruksana from '$lib/assets/ruksana.jpg';
	import tsuki from '$lib/assets/tsuki.jpg';
	import bada from '$lib/assets/bada.jpg';
	import ribok from '$lib/assets/ribokk.jpg';
	import anjali from '$lib/assets/anjali.jpg';
	import SectionWrapper from './SectionWrapper.svelte';

	export let members = [
		{
			name: 'Ayaan Hafiz',
			role: 'President',
			description: 'Btech ECE 4th Year',
			image: ayaan,
			linkedin: 'https://www.linkedin.com/in/ayaan-hafiz-9612bb249/'
		},
		{
			name: 'Ayushi',
			role: 'Vice-President',
			description: 'Btech ECE 4th Year',
			image: ayushi,
			linkedin:
				'https://www.linkedin.com/in/aayushi-a5578a250/?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app'
		},
		{
			name: 'Bandeep Bhatta',
			role: 'General Secretary',
			description: 'Btech ECE 3rd Year',
			image: biku,
			linkedin: 'https://www.linkedin.com/in/bandeep-bhatta/'
		},
		{
			name: 'Rukhshana Yasmin',
			role: 'Asst. General Secretary',
			description: 'Btech ECE 4th Year',
			image: ruksana,
			linkedin:
				'https://www.linkedin.com/in/rukhshana-yasmin-52944030a?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app'
		},
		{
			name: 'Shiva Sai Naluvala',
			role: 'Technical Lead',
			description: 'Btech ECE 3rd Year',
			image: citti,
			linkedin: 'https://www.linkedin.com/in/shivasainaluvala/'
		},
		{
			name: 'Anurag Saud',
			role: 'Asst. Technical Lead',
			description: 'Btech ECE 2nd Year',
			image: anurag,
			linkedin: 'https://www.linkedin.com/in/anuragsaud/'
		},
		{
			name: 'Rohit K. Shaw',
			role: 'Event Coordinator',
			description: 'Btech ECE 4th Year',
			image: rohit,
			linkedin: 'https://www.linkedin.com/in/shawrhit/'
		},
		{
			name: 'Ritu Kumari Kisku',
			role: 'Asst. Event Coordinator',
			description: 'Btech ECE 2nd Year',
			image: ritu,
			linkedin: ''
		},
		{
			name: 'Anjali Chaurasia',
			role: 'Media Head',
			description: 'Btech ECE 3rd Year',
			image: anjali,
			linkedin: 'https://www.linkedin.com/in/anjalichaurasia28/'
		},
		{
			name: 'Subhojit Baidya',
			role: 'HR Head',
			description: 'Btech ECE 2nd Year',
			image: bada,
			linkedin: 'https://www.linkedin.com/in/subhojit-baidya-96a603209/'
		},
		{
			name: 'Mohit Kumar',
			role: 'Public Relation Head',
			description: 'Btech ECE 2nd Year',
			image: mahi,
			linkedin: 'https://www.linkedin.com/in/mohit-kumar-4a459635b/'
		},
		{
			name: 'Indraneel Chowdhury',
			role: 'Asst. Public Relation Head',
			description: 'Btech ECE 2nd Year',
			image: neelu,
			linkedin: 'https://www.linkedin.com/in/indraneel-chowdhury-a02432345/'
		},
		{
			name: 'Chandrasmita Gayan',
			role: 'Finance Secretary',
			description: 'Btech ECE 2nd Year',
			image: tsuki,
			linkedin:
				'https://www.linkedin.com/in/chandrasmita-gayan-944999367?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app'
		},
		{
			name: 'Riboklang Khongbeh',
			role: 'Asst. Finance Secretary',
			description: 'Btech ECE 4th Year',
			image: ribok,
			linkedin: 'https://www.linkedin.com/in/ribok-khongbeh-35b73a27a/'
		}
	];
</script>

<SectionWrapper divId="team">
	<div class="members">
		<h2 class="members-heading animate-fade-in">
			Our <span style="color: #0000ff">Executive </span> Members
		</h2>
		<div class="grid">
			{#each members as member, i}
				<div class="member-card animate-pop-in" style="animation-delay: {i * 80}ms;">
					<div class="member-img-wrap">
						<img src={member.image} alt={member.name} class="member-img" />
					</div>
					<h3 class="member-name">{member.name}</h3>
					<p class="role">{member.role}</p>
					<p class="description">{member.description}</p>
					{#if member.linkedin}
						<div class="links">
							<a
								href={member.linkedin}
								target="_blank"
								rel="noopener"
								aria-label="LinkedIn"
								class="linkedin-link"
							>
								<svg width="22" height="22" fill="#0db7d9" viewBox="0 0 24 24"
									><path
										d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-10h3v10zm-1.5-11.268c-.966 0-1.75-.784-1.75-1.75s.784-1.75 1.75-1.75 1.75.784 1.75 1.75-.784 1.75-1.75 1.75zm15.5 11.268h-3v-5.604c0-1.337-.025-3.063-1.868-3.063-1.868 0-2.154 1.459-2.154 2.967v5.7h-3v-10h2.881v1.367h.041c.401-.761 1.379-1.563 2.841-1.563 3.041 0 3.603 2.003 3.603 4.605v5.591z"
									/></svg
								>
							</a>
						</div>
					{/if}
				</div>
			{/each}
		</div>
	</div>
</SectionWrapper>

<style>
	.members {
		width: 100vw;
		padding: 3rem 1rem 4rem 1rem;
		background: transparent;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		overflow-x: hidden;
	}

	.members-heading {
		font-size: 2.3rem;
		font-weight: bold;
		text-align: center;
		margin-bottom: 2.5rem;
		font-style: italic;
		letter-spacing: 1px;
		color: #111;
	}

	.grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
		gap: 2.2rem;
		width: 100%;
		max-width: 1200px;
		justify-items: center;
	}

	.member-card {
		/* background: #fff; */
		border-radius: 1.5rem;
		box-shadow: 0 4px 24px 0 rgba(13, 183, 217, 0.1);
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 2.2rem 1.2rem 1.5rem 1.2rem;
		transition:
			transform 0.22s cubic-bezier(0.4, 2, 0.6, 1),
			box-shadow 0.22s cubic-bezier(0.4, 2, 0.6, 1);
		position: relative;
		cursor: pointer;
		border: 2px solid #e0e0e0;
		animation: pop-in 0.7s cubic-bezier(0.4, 2, 0.6, 1) backwards;
	}
	.member-card:hover {
		transform: translateY(-10px) scale(1.04) rotate(-1deg);
		box-shadow:
			0 8px 32px 0 #0000ffbb,
			0 2px 16px 0 rgba(0, 0, 255, 0.13);
		border-color: #3636df;
	}

	.member-img-wrap {
		width: 110px;
		height: 110px;
		border-radius: 1.2rem;
		overflow: hidden;
		margin-bottom: 1.2rem;
		box-shadow: 0 0 0 0 #0000ff;
		animation: pulse-glow 2.2s infinite cubic-bezier(0.4, 2, 0.6, 1);
		background: #f6f6f6;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.member-img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 1.2rem;
		transition: transform 0.3s;
	}
	.member-card:hover .member-img {
		transform: scale(1.09) rotate(2deg);
	}

	@keyframes pulse-glow {
		0% {
			box-shadow: 0 0 0 0 #0000ff33;
		}
		70% {
			box-shadow: 0 0 24px 8px #0000ff33;
		}
		100% {
			box-shadow: 0 0 0 0 #0000ff33;
		}
	}

	.member-name {
		font-size: 1.18rem;
		font-weight: 700;
		font-style: italic;
		color: #0d183d;
		margin-bottom: 0.2rem;
		letter-spacing: 0.5px;
		text-align: center;
	}

	.role {
		font-size: 1rem;
		font-weight: 600;
		color: #0000ff;
		margin-bottom: 0.2rem;
		text-align: center;
	}

	.description {
		font-size: 0.98rem;
		color: #222;
		margin-bottom: 0.7rem;
		text-align: center;
	}

	.links {
		margin-top: 0.5rem;
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.7rem;
	}
	.linkedin-link {
		display: flex;
		align-items: center;
		justify-content: center;
		background: #e6f0ff;
		border-radius: 50%;
		width: 38px;
		height: 38px;
		transition: background 0.2s;
	}
	.linkedin-link:hover {
		background: #0db7d9;
	}
	.linkedin-link:hover svg {
		fill: #fff;
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
	.animate-fade-in {
		animation: fade-in 1.2s cubic-bezier(0.4, 2, 0.6, 1) backwards;
	}
	@keyframes fade-in {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	@media (max-width: 700px) {
		.grid {
			grid-template-columns: 1fr;
			gap: 1.2rem;
		}
		.member-card {
			padding: 1.2rem 0.5rem 1rem 0.5rem;
		}
		.member-img-wrap {
			width: 80px;
			height: 80px;
		}
	}
</style>
