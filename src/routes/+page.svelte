<script>
	import { onMount } from 'svelte';

	let budget = '';
	let activeTag = '';

	const tags = ['COFFEE RUN', 'NIGHT OUT', 'WEEKLY GROCERIES'];

	function selectTag(tag) {
		activeTag = activeTag === tag ? '' : tag;
	}

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						entry.target.classList.add('animate-visible');
					}
				});
			},
			{ threshold: 0.1, rootMargin: '0px 0px -50px 0px' }
		);

		document.querySelectorAll('.animate-on-scroll').forEach((el) => {
			observer.observe(el);
		});

		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<title>Chooser — Smart choices, simplified.</title>
	<meta name="description" content="The ultimate decision companion for students." />
</svelte:head>

<!-- ======================== -->
<!-- SECTION 1: HERO          -->
<!-- ======================== -->
<section class="w-full bg-white">
	<div class="max-w-screen-xl mx-auto px-5 py-16 md:py-24">
		<div class="flex flex-col md:flex-row items-start gap-8 md:gap-12">
			<!-- Left: Text Content -->
			<div class="flex-1 flex flex-col justify-center">
				<p class="animate-on-scroll fade-up text-purple-600 text-xs font-semibold uppercase tracking-[0.2em] mb-4">
					Decide with intent
				</p>
				<h1 class="animate-on-scroll fade-up delay-1 text-5xl md:text-6xl lg:text-7xl font-black leading-[1.05] tracking-tight text-gray-900 mb-6">
					Smart<br />choices<br />
					<span class="text-purple-600">Simplified.</span>
				</h1>
				<p class="animate-on-scroll fade-up delay-2 text-gray-500 text-base md:text-lg leading-relaxed max-w-md mb-8">
					The ultimate decision companion for students. From tonight's dinner to next year's budget, Chooser makes your life easier.
				</p>
				<div class="animate-on-scroll fade-up delay-3 flex flex-wrap gap-3">
					<a href="/moods" class="bg-purple-600 hover:bg-purple-700 text-white text-sm font-semibold px-6 py-3 rounded-lg transition-colors inline-block">
						Get Started
					</a>
					<a href="/moods" class="border border-gray-300 hover:border-gray-400 text-gray-700 text-sm font-semibold px-6 py-3 rounded-lg transition-colors inline-block">
						Explore Moods
					</a>
				</div>
			</div>

			<!-- Right: Image + Testimonial Card -->
			<div class="animate-on-scroll fade-left delay-2 flex-1 relative w-full">
				<div class="rounded-2xl overflow-hidden bg-gray-200 aspect-[4/3] w-full">
					<img 
						src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=800&h=600&fit=crop" 
						alt="Laptop on desk" 
						class="w-full h-full object-cover"
					/>
				</div>
				<!-- Testimonial Card -->
				<div class="animate-on-scroll fade-up delay-4 absolute bottom-4 left-4 md:bottom-6 md:left-6 bg-white rounded-xl shadow-lg p-4 max-w-[280px]">
					<p class="text-purple-600 text-xs font-semibold mb-1">Editor's Pick</p>
					<p class="text-gray-800 text-sm font-semibold leading-snug">
						"How I cut my weekly spending by 40% using the Chooser Budget Dial."
					</p>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- ======================== -->
<!-- SECTION 2: HOW IT WORKS  -->
<!-- ======================== -->
<section class="w-full bg-gray-50">
	<div class="max-w-screen-xl mx-auto px-5 py-16 md:py-24">
		<!-- Section Header -->
		<div class="mb-12">
			<h2 class="animate-on-scroll fade-up text-2xl md:text-3xl font-bold text-gray-900 mb-3">
				How It Works
			</h2>
			<p class="animate-on-scroll fade-up delay-1 text-gray-500 text-base max-w-lg">
				Finding the right place shouldn't be a chore. Here is how we help you choose.
			</p>
		</div>

		<!-- 3 Cards -->
		<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
			<!-- Card 1 -->
			<div class="animate-on-scroll fade-up delay-1 bg-white border border-gray-200 rounded-2xl p-6 hover:shadow-md transition-shadow">
				<div class="w-10 h-10 bg-purple-100 rounded-lg flex items-center justify-center mb-5">
					<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-purple-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
						<path stroke-linecap="round" stroke-linejoin="round" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z" />
					</svg>
				</div>
				<h3 class="text-base font-bold text-gray-900 mb-2">Input Your Vibe</h3>
				<p class="text-gray-500 text-sm leading-relaxed">
					Tell us your mood, budget, or what you're craving. No complicated forms, just your honest intent.
				</p>
			</div>

			<!-- Card 2 -->
			<div class="animate-on-scroll fade-up delay-2 bg-white border border-gray-200 rounded-2xl p-6 hover:shadow-md transition-shadow">
				<div class="w-10 h-10 bg-purple-100 rounded-lg flex items-center justify-center mb-5">
					<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-purple-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
						<path stroke-linecap="round" stroke-linejoin="round" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z" />
					</svg>
				</div>
				<h3 class="text-base font-bold text-gray-900 mb-2">Smart Curation</h3>
				<p class="text-gray-500 text-sm leading-relaxed">
					We filter through local options and past favorites to give you a curated selection of choices.
				</p>
			</div>

			<!-- Card 3 -->
			<div class="animate-on-scroll fade-up delay-3 bg-white border border-gray-200 rounded-2xl p-6 hover:shadow-md transition-shadow">
				<div class="w-10 h-10 bg-purple-100 rounded-lg flex items-center justify-center mb-5">
					<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-purple-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
						<path stroke-linecap="round" stroke-linejoin="round" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
					</svg>
				</div>
				<h3 class="text-base font-bold text-gray-900 mb-2">Act & Savor</h3>
				<p class="text-gray-500 text-sm leading-relaxed">
					Make your decision with confidence. Chooser handles the details so you can enjoy the moment.
				</p>
			</div>
		</div>
	</div>
</section>

<!-- ================================ -->
<!-- SECTION 3: STUDENT DIAL + CTA    -->
<!-- ================================ -->
<section class="w-full bg-white">
	<div class="max-w-screen-xl mx-auto px-5 py-16 md:py-24">
		<!-- Student Dial -->
		<div class="flex flex-col items-center text-center mb-20">
			<!-- Icon -->
			<div class="animate-on-scroll scale-in w-12 h-12 bg-purple-100 rounded-xl flex items-center justify-center mb-5">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-purple-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
					<path stroke-linecap="round" stroke-linejoin="round" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
				</svg>
			</div>
			<h2 class="animate-on-scroll fade-up delay-1 text-3xl md:text-4xl font-bold text-gray-900 mb-3">
				The Student Dial
			</h2>
			<p class="animate-on-scroll fade-up delay-2 text-gray-500 text-base max-w-md mb-8">
				Type your available budget below to see options tailored to your pocket.
			</p>

			<!-- Budget Input -->
			<div class="animate-on-scroll fade-up delay-3 flex items-center bg-gray-100 rounded-xl overflow-hidden w-full max-w-sm mb-6">
				<span class="text-gray-400 text-lg font-semibold pl-4 pr-2">$</span>
				<input 
					type="text" 
					bind:value={budget}
					placeholder="0.00" 
					class="flex-1 bg-transparent py-3.5 text-lg font-medium text-gray-900 placeholder-gray-400 outline-none"
				/>
				<button class="bg-purple-600 hover:bg-purple-700 text-white m-1.5 px-4 py-2.5 rounded-lg transition-colors">
					<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
						<path stroke-linecap="round" stroke-linejoin="round" d="M14 5l7 7m0 0l-7 7m7-7H3" />
					</svg>
				</button>
			</div>

			<!-- Tags -->
			<div class="animate-on-scroll fade-up delay-4 flex flex-wrap justify-center gap-3">
				{#each tags as tag}
					<button 
						on:click={() => selectTag(tag)}
						class="text-xs font-semibold uppercase tracking-wider px-4 py-2 rounded-full border transition-colors
						{activeTag === tag 
							? 'bg-purple-600 text-white border-purple-600' 
							: 'bg-white text-gray-600 border-gray-300 hover:border-purple-400 hover:text-purple-600'}"
					>
						{tag}
					</button>
				{/each}
			</div>
		</div>

		<!-- CTA Banner -->
		<div class="animate-on-scroll fade-up rounded-3xl overflow-hidden relative" style="background: linear-gradient(135deg, #7c3aed 0%, #6d28d9 40%, #5b21b6 100%);">
			<!-- Decorative Elements -->
			<div class="absolute top-0 right-0 w-64 h-64 bg-white/[0.07] rounded-full -translate-y-1/2 translate-x-1/3"></div>
			<div class="absolute bottom-0 left-0 w-48 h-48 bg-white/[0.07] rounded-full translate-y-1/3 -translate-x-1/4"></div>
			<div class="absolute top-1/2 left-1/3 w-32 h-32 bg-white/[0.04] rounded-full"></div>
			
			<div class="relative flex flex-col md:flex-row items-center">
				<!-- Left: Text -->
				<div class="flex-1 p-8 md:p-12 lg:p-16">
					<span class="inline-block text-purple-200 text-xs font-semibold uppercase tracking-[0.2em] mb-4">Join the movement</span>
					<h2 class="text-2xl md:text-3xl lg:text-4xl font-bold text-white mb-4 leading-tight">
						Ready to curate<br />your choices?
					</h2>
					<p class="text-purple-200 text-base mb-8 max-w-sm leading-relaxed">
						Join over 10,000 students who have reclaimed their time and wallet with Chooser.
					</p>
					<div class="flex flex-wrap gap-3">
						<button class="bg-white hover:bg-gray-100 text-purple-700 text-sm font-semibold px-7 py-3.5 rounded-xl transition-all shadow-lg shadow-purple-900/20 hover:shadow-xl hover:shadow-purple-900/30 hover:-translate-y-0.5">
							Join the Beta
						</button>
						<button class="border border-white/30 hover:border-white/60 text-white text-sm font-semibold px-7 py-3.5 rounded-xl transition-all hover:-translate-y-0.5">
							Learn More →
						</button>
					</div>
				</div>

				<!-- Right: Images -->
				<div class="flex-1 flex gap-4 p-6 md:p-8 lg:p-10">
					<div class="flex-1 flex flex-col gap-4">
						<div class="animate-on-scroll scale-in delay-2 rounded-2xl overflow-hidden aspect-[4/5] ring-1 ring-white/20 shadow-2xl">
							<img 
								src="https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=400&h=500&fit=crop" 
								alt="Coffee latte art" 
								class="w-full h-full object-cover"
							/>
						</div>
					</div>
					<div class="flex-1 flex flex-col gap-4 pt-6">
						<div class="animate-on-scroll scale-in delay-3 rounded-2xl overflow-hidden aspect-[4/5] ring-1 ring-white/20 shadow-2xl">
							<img 
								src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=400&h=500&fit=crop" 
								alt="Workspace with laptop" 
								class="w-full h-full object-cover"
							/>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	/* ===== BASE STATES (hidden before scroll) ===== */
	:global(.animate-on-scroll.fade-up) {
		opacity: 0;
		transform: translateY(40px);
		transition: opacity 0.7s cubic-bezier(0.16, 1, 0.3, 1),
					transform 0.7s cubic-bezier(0.16, 1, 0.3, 1);
	}

	:global(.animate-on-scroll.fade-left) {
		opacity: 0;
		transform: translateX(60px);
		transition: opacity 0.7s cubic-bezier(0.16, 1, 0.3, 1),
					transform 0.7s cubic-bezier(0.16, 1, 0.3, 1);
	}

	:global(.animate-on-scroll.scale-in) {
		opacity: 0;
		transform: scale(0.85);
		transition: opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1),
					transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
	}

	/* ===== VISIBLE STATE (after scroll triggers) ===== */
	:global(.animate-on-scroll.animate-visible) {
		opacity: 1;
		transform: translateY(0) translateX(0) scale(1);
	}

	/* ===== STAGGERED DELAYS ===== */
	:global(.animate-on-scroll.delay-1) { transition-delay: 0.1s; }
	:global(.animate-on-scroll.delay-2) { transition-delay: 0.2s; }
	:global(.animate-on-scroll.delay-3) { transition-delay: 0.3s; }
	:global(.animate-on-scroll.delay-4) { transition-delay: 0.4s; }
	:global(.animate-on-scroll.delay-5) { transition-delay: 0.5s; }

	/* ===== Respect reduced motion preference ===== */
	@media (prefers-reduced-motion: reduce) {
		:global(.animate-on-scroll) {
			opacity: 1 !important;
			transform: none !important;
			transition: none !important;
		}
	}
</style>
