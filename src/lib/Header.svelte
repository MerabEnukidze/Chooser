<script>
	import { page } from '$app/stores';
</script>

<header class="w-full bg-white/80 backdrop-blur-lg border-b border-gray-100/80 sticky top-0 z-50">
	<nav class="max-w-screen-xl w-full mx-auto flex items-center justify-between py-4 px-5">
		<!-- Logo -->
		<a href="/" class="text-purple-700 font-bold text-xl italic tracking-tight">
			Chooser
		</a>

		<!-- Nav Links -->
		<ul class="flex items-center gap-6">
			<li>
				<a 
					href="/" 
					class="text-sm font-medium transition-colors {$page.url.pathname === '/' ? 'text-purple-700 underline underline-offset-4 decoration-2' : 'text-gray-600 hover:text-gray-900'}"
				>
					Home
				</a>
			</li>
			<li>
				<a 
					href="/moods" 
					class="text-sm font-medium transition-colors {$page.url.pathname === '/moods' ? 'text-purple-700 underline underline-offset-4 decoration-2' : 'text-gray-600 hover:text-gray-900'}"
				>
					Moods
				</a>
			</li>
			<li>
				<a 
					href="/trending" 
					class="text-sm font-medium transition-colors {$page.url.pathname === '/trending' ? 'text-purple-700 underline underline-offset-4 decoration-2' : 'text-gray-600 hover:text-gray-900'}"
				>
					Trending
				</a>
			</li>
		</ul>

		<!-- Profile Icon -->
		<button class="w-8 h-8 rounded-full border-2 border-purple-600 flex items-center justify-center text-purple-600 hover:bg-purple-50 transition-colors">
			<svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
				<path stroke-linecap="round" stroke-linejoin="round" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
			</svg>
		</button>
	</nav>
</header>
