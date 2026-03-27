<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	// ---- State ----
	/** @type {Set<string>} */
	let selectedMoods = new Set();
	let budgetTier = 'mid';
	let manualBudget = '40';
	let soloFriendly = false;
	let outdoorOnly = true;

	/** @type {Record<string, number>} */
	const tierValues = { economic: 20, mid: 40, premium: 70 };

	const moods = [
		{
			id: 'chill',
			emoji: '🍷',
			label: 'Chill / Relax',
			image: 'https://images.unsplash.com/photo-1543007630-9710e4a00a20?w=400&h=300&fit=crop',
			color: 'from-purple-900/80 to-purple-600/30'
		},
		{
			id: 'party',
			emoji: '🎉',
			label: 'Fun / Party',
			image: 'https://images.unsplash.com/photo-1514525253161-7a46d19cd819?w=400&h=300&fit=crop',
			color: 'from-fuchsia-900/80 to-fuchsia-600/30'
		},
		{
			id: 'romantic',
			emoji: '❤️',
			label: 'Romantic',
			image: 'https://images.unsplash.com/photo-1596178065887-1198b6148b2b?w=400&h=300&fit=crop',
			color: 'from-rose-900/80 to-rose-600/30'
		},
		{
			id: 'family',
			emoji: '👨‍👩‍👧',
			label: 'Family',
			image: 'https://images.unsplash.com/photo-1555396273-367ea4eb4db5?w=400&h=300&fit=crop',
			color: 'from-amber-900/80 to-amber-600/30'
		},
		{
			id: 'work',
			emoji: '💻',
			label: 'Work / Study',
			image: 'https://images.unsplash.com/photo-1497366216548-37526070297c?w=400&h=300&fit=crop',
			color: 'from-slate-900/80 to-slate-600/30'
		},
		{
			id: 'foodie',
			emoji: '🍽️',
			label: 'Foodie / Trendy',
			image: 'https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=400&h=300&fit=crop',
			color: 'from-emerald-900/80 to-emerald-600/30'
		}
	];

	function toggleMood(/** @type {string} */ id) {
		if (selectedMoods.has(id)) {
			selectedMoods.delete(id);
		} else {
			selectedMoods.add(id);
		}
		selectedMoods = selectedMoods; // trigger reactivity
	}

	/** @param {string} tierId */
	function selectTier(tierId) {
		budgetTier = tierId;
		manualBudget = String(tierValues[tierId] || '');
	}

	function handleCurate() {
		const moodIds = Array.from(selectedMoods).join(',');
		const params = new URLSearchParams({
			moods: moodIds,
			budget: manualBudget,
			solo: String(soloFriendly),
			outdoor: String(outdoorOnly)
		});
		goto(`/results?${params.toString()}`);
	}

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) entry.target.classList.add('animate-visible');
				});
			},
			{ threshold: 0.08 }
		);
		document.querySelectorAll('.anim').forEach((el) => observer.observe(el));
		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<title>Moods — Chooser</title>
	<meta name="description" content="Pick your vibe and let Chooser find the perfect spot." />
</svelte:head>

<div class="moods-page">
	<div class="max-w-screen-xl mx-auto px-4 sm:px-6 h-full flex flex-col">

		<!-- Header text -->
		<div class="pt-5 pb-4 md:pt-6 md:pb-5 shrink-0">
			<p class="anim fade-up text-purple-600 text-[10px] font-semibold uppercase tracking-[0.2em] mb-1">
				Personalize your experience
			</p>
			<h1 class="anim fade-up d1 text-2xl md:text-3xl lg:text-4xl font-black leading-tight tracking-tight text-gray-900">
				Pick Your <span class="text-purple-600">Vibe</span>.
			</h1>
		</div>

		<!-- Content: Moods + Sidebar — fills remaining space -->
		<div class="flex flex-col lg:flex-row gap-4 lg:gap-6 flex-1 min-h-0 pb-4">

			<!-- Mood Cards Grid -->
			<div class="flex-[2.5] min-w-0 h-full">
				<div class="grid grid-cols-2 sm:grid-cols-3 gap-2.5 md:gap-3 h-full grid-rows-2">
					{#each moods as mood, i}
						<button
							on:click={() => toggleMood(mood.id)}
							class="anim fade-up group relative rounded-xl overflow-hidden cursor-pointer focus:outline-none mood-card"
							class:mood-selected={selectedMoods.has(mood.id)}
							style="animation-delay: {i * 60}ms"
						>
							<img
								src={mood.image}
								alt={mood.label}
								class="absolute inset-0 w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
								loading="lazy"
							/>
							<div class="absolute inset-0 bg-gradient-to-t {mood.color}"></div>

							<!-- Check badge -->
							<div class="check-badge" class:check-visible={selectedMoods.has(mood.id)}>
								<svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
									<path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
								</svg>
							</div>

							<!-- Selected border overlay -->
							<div class="select-border" class:select-border-visible={selectedMoods.has(mood.id)}></div>

							<!-- Centered label -->
							<div class="absolute bottom-0 left-0 right-0 p-3 flex flex-col items-center text-center">
								<span class="text-lg md:text-xl block drop-shadow-lg leading-none mb-1">{mood.emoji}</span>
								<span class="text-white font-bold text-xs md:text-sm drop-shadow-lg">{mood.label}</span>
							</div>
						</button>
					{/each}
				</div>
			</div>

			<!-- Sidebar — vertically centered, dominant -->
			<div class="lg:w-[300px] xl:w-[320px] shrink-0 lg:self-center">
				<div class="anim fade-up d3 sidebar-panel">

					<!-- Investment Level -->
					<div>
						<div class="flex items-center gap-2.5 mb-4">
							<div class="w-8 h-8 bg-purple-100 rounded-lg flex items-center justify-center">
								<svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-purple-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
									<path stroke-linecap="round" stroke-linejoin="round" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
								</svg>
							</div>
							<h3 class="font-bold text-gray-900 text-base">Investment Level</h3>
						</div>

						<div class="grid grid-cols-3 gap-2 mb-4">
							{#each [
								{ id: 'economic', label: 'Economic', val: '₾20' },
								{ id: 'mid', label: 'Mid-Tier', val: '₾40' },
								{ id: 'premium', label: 'Premium', val: '₾70' }
							] as tier}
								<button
									on:click={() => selectTier(tier.id)}
									class="text-xs font-semibold py-2.5 px-2 rounded-xl border-2 transition-all leading-tight
									{budgetTier === tier.id
										? 'bg-purple-600 text-white border-purple-600 shadow-md shadow-purple-200'
										: 'bg-white text-gray-600 border-gray-200 hover:border-purple-300'}"
								>
									{tier.label}<br/><span class="opacity-80 text-[10px]">{tier.val}</span>
								</button>
							{/each}
						</div>

						<div class="flex items-center bg-gray-50 border border-gray-200 rounded-xl overflow-hidden focus-within:border-purple-400 focus-within:ring-2 focus-within:ring-purple-100 transition-all">
							<span class="text-gray-400 text-base font-semibold pl-3 pr-1">₾</span>
							<input
								type="number"
								bind:value={manualBudget}
								on:focus={() => budgetTier = 'manual'}
								placeholder="40"
								class="flex-1 bg-transparent py-3 text-base font-medium text-gray-900 placeholder-gray-400 outline-none w-0"
							/>
							<span class="text-[10px] font-semibold text-gray-400 uppercase pr-3">GEL</span>
						</div>
					</div>

					<div class="border-t border-gray-100"></div>

					<!-- Fine-Tuning -->
					<div>
						<div class="flex items-center gap-2.5 mb-4">
							<div class="w-8 h-8 bg-purple-100 rounded-lg flex items-center justify-center">
								<svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-purple-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
									<path stroke-linecap="round" stroke-linejoin="round" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4" />
								</svg>
							</div>
							<h3 class="font-bold text-gray-900 text-base">Fine-Tuning</h3>
						</div>
						<div class="space-y-3">
							<div class="flex items-center justify-between">
								<span class="text-sm text-gray-700 font-medium">Solo Friendly</span>
								<label class="tog">
									<input type="checkbox" bind:checked={soloFriendly} />
									<span class="tog-s"></span>
								</label>
							</div>
							<div class="flex items-center justify-between">
								<span class="text-sm text-gray-700 font-medium">Outdoor Only</span>
								<label class="tog">
									<input type="checkbox" bind:checked={outdoorOnly} />
									<span class="tog-s"></span>
								</label>
							</div>
						</div>
					</div>

					<!-- CTA -->
					<button
						on:click={handleCurate}
						class="cta-btn"
						class:cta-active={selectedMoods.size > 0}
						disabled={selectedMoods.size === 0}
					>
						{selectedMoods.size > 0
							? `Curate My Experience (${selectedMoods.size})`
							: 'Select a Mood First'}
					</button>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	/* Page fills exactly the space between header and footer — no scroll */
	.moods-page {
		flex: 1;
		overflow: hidden;
		background: #f9fafb;
	}
	.moods-page > div {
		height: 100%;
	}

	/* ===== Mood Card States ===== */
	.mood-card {
		transition: transform 0.3s ease, box-shadow 0.3s ease;
	}
	.mood-card:hover {
		transform: scale(1.03);
		box-shadow: 0 4px 12px rgba(0,0,0,0.12);
	}
	.mood-card.mood-selected {
		outline: 3px solid #8b5cf6;
		outline-offset: 3px;
		box-shadow: 0 4px 20px rgba(139, 92, 246, 0.35);
	}
	.mood-card.mood-selected:hover {
		transform: none;
	}

	/* Check badge — always in DOM, hidden by default */
	.check-badge {
		position: absolute;
		top: 8px;
		right: 8px;
		width: 24px;
		height: 24px;
		background: #7c3aed;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 10;
		box-shadow: 0 2px 6px rgba(0,0,0,0.2);
		transform: scale(0);
		opacity: 0;
		transition: transform 0.25s cubic-bezier(0.16,1,0.3,1), opacity 0.25s ease;
	}
	.check-badge.check-visible {
		transform: scale(1);
		opacity: 1;
	}

	/* Selected inner border overlay — always in DOM */
	.select-border {
		position: absolute;
		inset: 0;
		border-radius: 0.75rem;
		pointer-events: none;
		border: 2px solid transparent;
		transition: border-color 0.3s ease;
	}
	.select-border.select-border-visible {
		border-color: rgba(167, 139, 250, 0.7);
	}

	/* ===== Sidebar Panel — dominant ===== */
	.sidebar-panel {
		background: white;
		border: 1px solid #e5e7eb;
		border-radius: 1.25rem;
		padding: 1.5rem;
		display: flex;
		flex-direction: column;
		gap: 1.25rem;
		box-shadow: 0 4px 24px rgba(0,0,0,0.06), 0 1px 4px rgba(0,0,0,0.04);
	}

	/* ===== CTA Button ===== */
	.cta-btn {
		width: 100%;
		padding: 0.875rem;
		border-radius: 0.875rem;
		font-weight: 700;
		font-size: 0.875rem;
		color: white;
		background: #d1d5db;
		border: none;
		cursor: not-allowed;
		transition: all 0.3s ease;
		box-shadow: none;
	}
	.cta-btn.cta-active {
		cursor: pointer;
		background: linear-gradient(135deg, #7c3aed, #a855f7);
		box-shadow: 0 6px 20px rgba(124, 58, 237, 0.35);
	}
	.cta-btn.cta-active:hover {
		background: linear-gradient(135deg, #6d28d9, #9333ea);
		box-shadow: 0 8px 24px rgba(124, 58, 237, 0.45);
		transform: translateY(-2px);
	}
	.cta-btn.cta-active:active {
		transform: translateY(0);
	}

	/* Toggle */
	.tog { position: relative; display: inline-block; width: 44px; height: 24px; flex-shrink: 0; }
	.tog input { opacity: 0; width: 0; height: 0; }
	.tog-s {
		position: absolute; cursor: pointer; inset: 0;
		background: #e5e7eb; border-radius: 24px;
		transition: .3s cubic-bezier(.4,0,.2,1);
	}
	.tog-s::before {
		content: ""; position: absolute;
		height: 18px; width: 18px; left: 3px; bottom: 3px;
		background: white; border-radius: 50%;
		transition: .3s cubic-bezier(.4,0,.2,1);
		box-shadow: 0 1px 3px rgba(0,0,0,.12);
	}
	.tog input:checked + .tog-s { background: linear-gradient(135deg, #7c3aed, #a855f7); }
	.tog input:checked + .tog-s::before { transform: translateX(20px); }

	/* Animations */
	:global(.anim.fade-up) {
		opacity: 0; transform: translateY(24px);
		transition: opacity .5s cubic-bezier(.16,1,.3,1), transform .5s cubic-bezier(.16,1,.3,1);
	}
	:global(.anim.animate-visible) {
		opacity: 1; transform: translateY(0) translateX(0) scale(1);
	}
	:global(.anim.d1) { transition-delay: .06s; }
	:global(.anim.d2) { transition-delay: .12s; }
	:global(.anim.d3) { transition-delay: .18s; }

	@media (prefers-reduced-motion: reduce) {
		:global(.anim) { opacity: 1 !important; transform: none !important; transition: none !important; }
		.check-badge { transition: none; }
		.mood-card { transition: none; }
	}
</style>
