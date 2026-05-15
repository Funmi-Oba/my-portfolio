<script>
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let name = $state('');
	let email = $state('');
	let message = $state('');
	let sending = $state(false);
	let sent = $state(false);
	let error = $state('');

	async function handleSubmit() {
		if (!name || !email || !message) {
			error = 'Please fill in all fields.';
			return;
		}
		error = '';
		sending = true;
		await new Promise((r) => setTimeout(r, 1500));
		sending = false;
		sent = true;
		name = '';
		email = '';
		message = '';
	}

	const socials = [
		{
			label: 'GitHub',
			value: 'github.com/Funmi-Oba',
			href: 'https://github.com/Funmi-Oba',
			color: '#6366f1'
		},
		{
			label: 'LinkedIn',
			value: 'linkedin.com/in/funmilayo-oba',
			href: 'https://linkedin.com/in/funmilayo-oba',
			color: '#a855f7'
		},
		{
			label: 'Email',
			value: 'funmilayooba@gmail.com',
			href: 'mailto:funmilayooba@gmail.com',
			color: '#14b8a6'
		},
		{
			label: 'Portfolio',
			value: 'funmilayooba.vercel.app',
			href: 'https://funmilayooba.vercel.app',
			color: '#ec4899'
		}
	];

	onMount(() => {
		gsap.from('.contact-title', {
			scrollTrigger: { trigger: '#contact', start: 'top 80%' },
			opacity: 0,
			y: 40,
			duration: 0.8
		});
		gsap.from('.contact-left', {
			scrollTrigger: { trigger: '#contact', start: 'top 70%' },
			opacity: 0,
			x: -60,
			duration: 0.8,
			clearProps: 'all'
		});
		gsap.from('.contact-right', {
			scrollTrigger: { trigger: '#contact', start: 'top 70%' },
			opacity: 0,
			x: 60,
			duration: 0.8,
			clearProps: 'all'
		});
	});
</script>

<section id="contact" class="mx-auto max-w-7xl px-6 py-32">
	<div class="contact-title mb-16 text-center">
		<p class="mb-3 font-mono text-sm tracking-widest text-indigo-400 uppercase">Get In Touch</p>
		<h2 class="mb-4 text-4xl font-black text-white md:text-5xl">Let's Work Together</h2>
		<p class="mx-auto max-w-xl text-slate-400">
			Have a project in mind or want to collaborate? I'd love to hear from you.
		</p>
	</div>

	<div class="grid grid-cols-1 gap-12 lg:grid-cols-2">
		<!-- Left -->
		<div class="contact-left flex flex-col gap-8">
			<div
				class="inline-flex w-fit items-center gap-2 rounded-full border border-green-500/30 bg-green-500/10 px-4 py-2 font-mono text-sm text-green-400"
			>
				<span class="h-2 w-2 animate-pulse rounded-full bg-green-400"></span>
				Available for new opportunities
			</div>
			<p class="text-lg leading-relaxed text-slate-300">
				I'm currently open to frontend developer roles, freelance projects, and exciting
				collaborations. Whether you have a question or just want to say hi, my inbox is always open!
			</p>
			<div class="flex flex-col gap-4">
				{#each socials as social}
					<a
						href={social.href}
						target="_blank"
						class="group flex items-center gap-4 rounded-xl border border-[#2e2e45] bg-[#1e1e2e] p-4 transition-all duration-200 hover:border-indigo-500/50"
					>
						<div
							class="h-2 w-2 flex-shrink-0 rounded-full"
							style="background: {social.color};"
						></div>
						<div>
							<p class="mb-0.5 font-mono text-xs tracking-widest text-slate-500 uppercase">
								{social.label}
							</p>
							<p
								class="text-sm text-slate-300 transition-colors duration-200 group-hover:text-white"
							>
								{social.value}
							</p>
						</div>
						<span
							class="ml-auto text-slate-600 transition-colors duration-200 group-hover:text-indigo-400"
							>↗</span
						>
					</a>
				{/each}
			</div>
		</div>

		<!-- Right -->
		<div class="contact-right">
			<div class="rounded-2xl border border-[#2e2e45] bg-[#1e1e2e] p-8">
				{#if sent}
					<div class="flex flex-col items-center justify-center py-12 text-center">
						<div
							class="mb-4 flex h-16 w-16 items-center justify-center rounded-full border border-green-500/30 bg-green-500/20 text-3xl"
						>
							✅
						</div>
						<h3 class="mb-2 text-xl font-bold text-white">Message Sent!</h3>
						<p class="mb-6 text-sm text-slate-400">
							Thanks for reaching out. I'll get back to you within 24 hours.
						</p>
						<button
							onclick={() => (sent = false)}
							class="rounded-lg border border-indigo-500 px-6 py-2 text-sm text-indigo-400 transition-all duration-200 hover:bg-indigo-500 hover:text-white"
						>
							Send Another
						</button>
					</div>
				{:else}
					<div class="flex flex-col gap-5">
						<h3 class="mb-2 text-lg font-bold text-white">Send a Message</h3>

						<div>
							<label
								for="name"
								class="mb-2 block font-mono text-xs tracking-widest text-slate-400 uppercase"
								>Name</label
							>
							<input
								id="name"
								type="text"
								bind:value={name}
								placeholder="Your name"
								class="w-full rounded-lg border border-[#2e2e45] bg-[#13131f] px-4 py-3 font-mono text-sm text-white placeholder-slate-600 transition-colors duration-200 focus:border-indigo-500 focus:outline-none"
							/>
						</div>

						<div>
							<label
								for="email"
								class="mb-2 block font-mono text-xs tracking-widest text-slate-400 uppercase"
								>Email</label
							>
							<input
								id="email"
								type="email"
								bind:value={email}
								placeholder="your@email.com"
								class="w-full rounded-lg border border-[#2e2e45] bg-[#13131f] px-4 py-3 font-mono text-sm text-white placeholder-slate-600 transition-colors duration-200 focus:border-indigo-500 focus:outline-none"
							/>
						</div>

						<div>
							<label
								for="message"
								class="mb-2 block font-mono text-xs tracking-widest text-slate-400 uppercase"
								>Message</label
							>
							<textarea
								id="message"
								bind:value={message}
								placeholder="Tell me about your project..."
								rows="5"
								class="w-full resize-none rounded-lg border border-[#2e2e45] bg-[#13131f] px-4 py-3 font-mono text-sm text-white placeholder-slate-600 transition-colors duration-200 focus:border-indigo-500 focus:outline-none"
							></textarea>
						</div>

						{#if error}
							<p class="font-mono text-xs text-red-400">{error}</p>
						{/if}

						<button
							onclick={handleSubmit}
							disabled={sending}
							class="w-full rounded-lg bg-indigo-600 py-3 font-semibold text-white transition-all duration-200 hover:bg-indigo-500 hover:shadow-lg hover:shadow-indigo-500/25 disabled:cursor-not-allowed disabled:opacity-50"
						>
							{sending ? 'Sending...' : 'Send Message ↗'}
						</button>
					</div>
				{/if}
			</div>
		</div>
	</div>

	<div
		class="mt-24 flex flex-col items-center justify-between gap-4 border-t border-[#2e2e45] pt-8 md:flex-row"
	>
		<p class="font-mono text-sm text-slate-500">
			© 2026 Funmilayo Oba. Built with SvelteKit & TailwindCSS.
		</p>
		<p class="font-mono text-xs text-slate-600">Designed & Developed with ❤️</p>
	</div>
</section>
