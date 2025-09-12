<script>
	import linkedin from '$lib/assets/linkedin.svg';
	import instagram from '$lib/assets/ig.svg';
	import logo from '$lib/assets/logo.png';
	import whatsapp from '$lib/assets/wp.svg';
</script>

<footer class="footer">
	<div class="footer-content">
		<div class="social-icons">
			<a
				href="https://www.linkedin.com/company/nehuelectrophoenix/"
				target="_blank"
				rel="noopener"
				aria-label="LinkedIn"
			>
				<img src={linkedin} alt="LinkedIn" />
			</a>
			<a
				href="https://www.instagram.com/electrophoenix.nehu/"
				target="_blank"
				rel="noopener"
				aria-label="Instagram"
			>
				<img src={instagram} alt="Instagram" />
			</a>
			<a
				href="https://chat.whatsapp.com/F11pAlckAvoJv0vDBhR9Ms"
				target="_blank"
				rel="noopener"
				aria-label="WhatsApp"
			>
				<img src={whatsapp} alt="WhatsApp" />
			</a>
		</div>

		<!-- Logo made small and inline with icons -->
		<img src={logo} alt="ElectroPhoenix Logo" class="logo" />
	</div>

	<div class="copyright">
		<p>
			© {new Date().getFullYear()}
			<span style="font-style: italic;"><span class="highlight">ELECTRO</span>PHOENIX.</span> All rights
			reserved.
		</p>
		<p>
			Website made by
			<a href="https://anuragsaud.com/" target="_blank" class="credit">Anurag Saud</a>
		</p>
	</div>
</footer>

<style>
	.footer {
		width: 100%;
		background: transparent; /* no black box */
		color: #000; /* all text black */
		padding: 2rem 1rem 1.5rem;
		text-align: center;
		border-top: 1px solid rgba(0, 0, 0, 0.1);
	}

	.footer-content {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1rem;
	}

	/* Logo smaller to match social icons */
	.logo {
		width: 40px;
		height: auto;
		opacity: 0.9;
	}

	.social-icons {
		display: flex;
		gap: 1.2rem;
		justify-content: center;
	}

	.social-icons img {
		width: 28px;
		height: 28px;
		transition: transform 0.3s ease;
	}

	.social-icons img:hover {
		transform: scale(1.2);
	}

	.copyright {
		margin-top: 1rem;
		font-size: 0.9rem;
		color: #000; /* ensure black */
		line-height: 1.5;
	}

	.highlight {
		color: #0000ff;
		font-style: italic;
		font-weight: 700;
	}

	.credit {
		color: #0000ff;
		text-decoration: none;
		font-style: italic;
		font-weight: 600;
	}

	.credit:hover {
		text-decoration: underline;
	}

	@media (max-width: 480px) {
		.logo {
			width: 34px;
		}

		.social-icons img {
			width: 24px;
			height: 24px;
		}

		.footer {
			padding: 1.5rem 1rem 1rem;
		}

		.copyright {
			font-size: 0.8rem;
		}
	}
</style>
