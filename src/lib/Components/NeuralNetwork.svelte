<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	// Default values for desktop
	export let particleCount = 600;
	export let maxConnDist = 90;
	export let hoverRadius = 120;
	export let hoverStrength = 1.6;
	export let hoverDecay = 0.92;
	export let drift = 0.28;
	export let bg = '#efe7dd';
	export let baseColor = { r: 13, g: 183, b: 217 };
	export let layers = 3;

	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D | null = null;
	let DPR = Math.min(2, (typeof window !== 'undefined' && window.devicePixelRatio) || 1);
	let W = 800,
		H = 600;
	let raf = 0;

	const pointer = { x: -9999, y: -9999, active: false };

	class P {
		x: number;
		y: number;
		ox: number;
		oy: number;
		vx: number;
		vy: number;
		r: number;
		origR: number;
		alpha: number;
		cluster: number;
		constructor(x: number, y: number, r?: number) {
			this.x = this.ox = x;
			this.y = this.oy = y;
			this.vx = (Math.random() - 0.5) * 0.16;
			this.vy = (Math.random() - 0.5) * 0.16;
			this.r = r ?? 1 + Math.random() * 2.6;
			this.origR = this.r;
			this.alpha = 0.45 + Math.random() * 0.6;
			this.cluster = Math.random();
		}
		step() {
			this.vx += Math.sin((this.x + this.y) * 0.001) * 0.0006;
			this.vy += Math.cos((this.y - this.x) * 0.0012) * 0.0006;

			if (pointer.active) {
				const dx = this.x - pointer.x;
				const dy = this.y - pointer.y;
				const d2 = dx * dx + dy * dy;
				const r2 = hoverRadius * hoverRadius;
				if (d2 < r2 && d2 > 0.0001) {
					const d = Math.sqrt(d2);
					const nx = dx / d,
						ny = dy / d;
					const force = (1 - d / hoverRadius) * hoverStrength;
					this.vx += nx * force * 0.6;
					this.vy += ny * force * 0.6;
				}
			} else {
				// Restore to original position and radius at the same speed as drift
				this.x += (this.ox - this.x) * drift;
				this.y += (this.oy - this.y) * drift;
				this.r += (this.origR - this.r) * drift;
			}

			this.x += this.vx * drift;
			this.y += this.vy * drift;
			this.vx *= hoverDecay;
			this.vy *= hoverDecay;

			if (this.x < -80) this.x = W + 80;
			if (this.x > W + 80) this.x = -80;
			if (this.y < -80) this.y = H + 80;
			if (this.y > H + 80) this.y = -80;

			this.r =
				this.origR *
				(0.92 + 0.16 * Math.sin((this.x + performance.now() * 0.0009) * 0.6 + this.cluster * 5));
		}
	}

	let particles: P[] = [];

	function gaussian() {
		let u = 0,
			v = 0;
		while (u === 0) u = Math.random();
		while (v === 0) v = Math.random();
		return Math.sqrt(-2 * Math.log(u)) * Math.cos(2 * Math.PI * v);
	}

	function buildParticles() {
		particles = [];
		const clusters = 3 + Math.floor(Math.random() * 3);
		const centers: { x: number; y: number; spread: number }[] = [];
		for (let c = 0; c < clusters; c++) {
			centers.push({
				x: Math.random() * W,
				y: Math.random() * H,
				spread: 0.08 + Math.random() * 0.18
			});
		}
		for (let i = 0; i < particleCount; i++) {
			if (Math.random() > 0.86) {
				const c = centers[Math.floor(Math.random() * centers.length)];
				const rx = gaussian() * c.spread * W;
				const ry = gaussian() * c.spread * H;
				particles.push(
					new P(
						Math.max(0, Math.min(W, c.x + rx)),
						Math.max(0, Math.min(H, c.y + ry)),
						1 + Math.random() * 3.4
					)
				);
			} else {
				particles.push(new P(Math.random() * W, Math.random() * H, 0.6 + Math.random() * 2.2));
			}
		}
	}

	function setSize() {
		if (!canvas) return;
		W = Math.max(600, innerWidth);
		H = Math.max(400, innerHeight);
		canvas.width = Math.floor(W * DPR);
		canvas.height = Math.floor(H * DPR);
		canvas.style.width = `${W}px`;
		canvas.style.height = `${H}px`;
		ctx?.setTransform(DPR, 0, 0, DPR, 0, 0);
	}

	function rgbaStr(a: number, b: number, c: number, alpha: number) {
		return `rgba(${Math.round(a)},${Math.round(b)},${Math.round(c)},${alpha})`;
	}

	function attachEvents() {
		const onMouseMove = (e: MouseEvent) => {
			pointer.active = true;
			pointer.x = e.clientX;
			pointer.y = e.clientY;
		};
		const onMouseOut = () => {
			pointer.active = false;
			pointer.x = -9999;
			pointer.y = -9999;
		};
		const onTouchMove = (e: TouchEvent) => {
			if (e.touches && e.touches[0]) {
				pointer.active = true;
				pointer.x = e.touches[0].clientX;
				pointer.y = e.touches[0].clientY;
			}
		};
		const onTouchEnd = () => {
			pointer.active = false;
			pointer.x = -9999;
			pointer.y = -9999;
		};
		const onResize = () => {
			setSize();
			buildParticles();
		};

		window.addEventListener('mousemove', onMouseMove);
		window.addEventListener('mouseout', onMouseOut);
		window.addEventListener('mouseleave', onMouseOut);
		window.addEventListener('touchmove', onTouchMove, { passive: true });
		window.addEventListener('touchend', onTouchEnd);
		window.addEventListener('resize', onResize);

		return () => {
			window.removeEventListener('mousemove', onMouseMove);
			window.removeEventListener('mouseout', onMouseOut);
			window.removeEventListener('mouseleave', onMouseOut);
			window.removeEventListener('touchmove', onTouchMove);
			window.removeEventListener('touchend', onTouchEnd);
			window.removeEventListener('resize', onResize);
		};
	}

	function draw(now: number) {
		if (!ctx) return;
		ctx.clearRect(0, 0, W, H);
		ctx.fillStyle = bg;
		ctx.fillRect(0, 0, W, H);

		const vg = ctx.createRadialGradient(
			W * 0.5,
			H * 0.45,
			Math.min(W, H) * 0.2,
			W * 0.5,
			H * 0.5,
			Math.max(W, H)
		);
		vg.addColorStop(0, 'rgba(255,255,255,0)');
		vg.addColorStop(1, 'rgba(0,0,0,0.06)');
		ctx.fillStyle = vg;
		ctx.fillRect(0, 0, W, H);

		const cell = maxConnDist;
		const cols = Math.ceil(W / cell);
		const rows = Math.ceil(H / cell);
		const grid: { i: number; px: number; py: number }[][] = new Array(cols * rows);
		for (let i = 0; i < grid.length; i++) grid[i] = [];

		for (let i = 0; i < particles.length; i++) {
			const p = particles[i];
			p.step();
			const px = p.x + (pointer.active ? (pointer.x - W / 2) * 0.02 : 0);
			const py = p.y + (pointer.active ? (pointer.y - H / 2) * 0.02 : 0);
			const gx = Math.max(0, Math.min(cols - 1, Math.floor(px / cell)));
			const gy = Math.max(0, Math.min(rows - 1, Math.floor(py / cell)));
			grid[gx + gy * cols].push({ i, px, py });
		}

		for (let gx = 0; gx < cols; gx++) {
			for (let gy = 0; gy < rows; gy++) {
				const list = grid[gx + gy * cols];
				if (!list.length) continue;
				for (let k = 0; k < list.length; k++) {
					const A = list[k];
					for (let ox = -1; ox <= 1; ox++) {
						for (let oy = -1; oy <= 1; oy++) {
							const nx = gx + ox;
							const ny = gy + oy;
							if (nx < 0 || nx >= cols || ny < 0 || ny >= rows) continue;
							const neighbor = grid[nx + ny * cols];
							for (let m = 0; m < neighbor.length; m++) {
								const B = neighbor[m];
								if (A.i >= B.i) continue;
								const dx = A.px - B.px;
								const dy = A.py - B.py;
								const d2 = dx * dx + dy * dy;
								const maxD = maxConnDist;
								if (d2 > maxD * maxD) continue;
								const dist = Math.sqrt(d2);
								const alpha = Math.max(
									0,
									0.16 * (1 - dist / maxD) * (0.9 + particles[A.i].cluster * 0.7)
								);
								if (alpha < 0.01) continue;
								ctx.strokeStyle = rgbaStr(baseColor.r, baseColor.g, baseColor.b, alpha);
								ctx.lineWidth = 1 * (0.5 + (1 - dist / maxD));
								ctx.beginPath();
								const mx = (A.px + B.px) * 0.5 + Math.sin((A.px + B.px + now * 0.002) * 0.001) * 6;
								const my = (A.py + B.py) * 0.5 + Math.cos((A.py + B.py + now * 0.002) * 0.001) * 6;
								ctx.moveTo(A.px, A.py);
								ctx.quadraticCurveTo(mx, my, B.px, B.py);
								ctx.stroke();
							}
						}
					}
				}
			}
		}

		for (let i = 0; i < particles.length; i++) {
			const p = particles[i];
			const px = p.x + (pointer.active ? (pointer.x - W / 2) * 0.02 : 0);
			const py = p.y + (pointer.active ? (pointer.y - H / 2) * 0.02 : 0);
			ctx.save();
			ctx.globalCompositeOperation = 'lighter';
			ctx.shadowColor = `rgba(${baseColor.r}, ${baseColor.g}, ${baseColor.b}, ${0.08})`;
			ctx.shadowBlur = 8;
			ctx.fillStyle = rgbaStr(baseColor.r, baseColor.g, baseColor.b, Math.max(0.12, p.alpha));
			ctx.beginPath();
			ctx.arc(px, py, p.r, 0, Math.PI * 2);
			ctx.fill();
			ctx.restore();
		}

		raf = requestAnimationFrame(draw);
	}

	let cleanupEvents: (() => void) | null = null;

	// --- Responsive tuning for mobile ---
	function tuneForMobile() {
		if (typeof window === 'undefined') return; // SSR guard
		if (window.innerWidth <= 600) {
			particleCount = 220; // fewer particles
			maxConnDist = 60; // shorter lines
			drift = 0.45; // faster movement
		} else if (window.innerWidth <= 900) {
			particleCount = 350;
			maxConnDist = 75;
			drift = 0.34;
		} else {
			particleCount = 600;
			maxConnDist = 90;
			drift = 0.28;
		}
	}

	onMount(() => {
		tuneForMobile();
		if (typeof window !== 'undefined') {
			window.addEventListener('resize', tuneForMobile);
		}
		if (!canvas) return;
		ctx = canvas.getContext('2d', { alpha: true });
		setSize();
		buildParticles();
		cleanupEvents = attachEvents();
		raf = requestAnimationFrame(draw);
	});

	onDestroy(() => {
		if (raf) cancelAnimationFrame(raf);
		if (cleanupEvents) cleanupEvents();
		if (typeof window !== 'undefined') {
			window.removeEventListener('resize', tuneForMobile);
		}
	});
</script>

<div class="wrap">
	<canvas bind:this={canvas}></canvas>
</div>

<style>
	:global(html, body) {
		height: 100%;
		margin: 0;
	}
	:global(body) {
		background: var(--bg, #efe7dd);
	}
	.wrap {
		position: relative;
		width: 100vw;
		height: 100vh;
		overflow: hidden;
		touch-action: none;
	}
	canvas {
		display: block;
		width: 100vw;
		height: 100vh;
		max-width: 100vw;
		max-height: 100vh;
		-webkit-user-select: none;
		user-select: none;
	}
	@media (max-width: 900px) {
		.wrap,
		canvas {
			width: 100vw;
			height: 100vh;
		}
	}
	@media (max-width: 600px) {
		.wrap,
		canvas {
			width: 100vw;
			height: 100vh;
		}
	}
</style>
