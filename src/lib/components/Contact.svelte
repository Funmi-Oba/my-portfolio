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

    // Simulate sending (replace with real email service later)
    await new Promise(r => setTimeout(r, 1500));
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

<section id="contact" class="py-32 px-6 max-w-7xl mx-auto">

  <!-- Header -->
  <div class="contact-title text-center mb-16">
    <p class="text-indigo-400 font-mono text-sm tracking-widest uppercase mb-3">
      Get In Touch
    </p>
    <h2 class="text-4xl md:text-5xl font-black text-white mb-4">
      Let's Work Together
    </h2>
    <p class="text-slate-400 max-w-xl mx-auto">
      Have a project in mind or want to collaborate? I'd love to hear from you.
    </p>
  </div>

  <!-- Two columns -->
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">

    <!-- Left — Info -->
    <div class="contact-left flex flex-col gap-8">

      <!-- Availability badge -->
      <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full border border-green-500/30 bg-green-500/10 text-green-400 text-sm font-mono w-fit">
        <span class="w-2 h-2 rounded-full bg-green-400 animate-pulse"></span>
        Available for new opportunities
      </div>

      <p class="text-slate-300 text-lg leading-relaxed">
        I'm currently open to frontend developer roles, freelance projects,
        and exciting collaborations. Whether you have a question or just want
        to say hi, my inbox is always open!
      </p>

      <!-- Socials -->
      <div class="flex flex-col gap-4">
        {#each socials as social}
          <a
            href={social.href}
            target="_blank"
            class="flex items-center gap-4 p-4 rounded-xl border border-[#2e2e45] bg-[#1e1e2e] hover:border-indigo-500/50 transition-all duration-200 group"
          >
            <div class="w-2 h-2 rounded-full flex-shrink-0" style="background: {social.color};"></div>
            <div>
              <p class="text-slate-500 text-xs font-mono uppercase tracking-widest mb-0.5">
                {social.label}
              </p>
              <p class="text-slate-300 text-sm group-hover:text-white transition-colors duration-200">
                {social.value}
              </p>
            </div>
            <span class="ml-auto text-slate-600 group-hover:text-indigo-400 transition-colors duration-200">↗</span>
          </a>
        {/each}
      </div>
    </div>

    <!-- Right — Form -->
    <div class="contact-right">
      <div class="bg-[#1e1e2e] border border-[#2e2e45] rounded-2xl p-8">

        {#if sent}
          <!-- Success state -->
          <div class="flex flex-col items-center justify-center h-full py-12 text-center">
            <div class="w-16 h-16 rounded-full bg-green-500/20 border border-green-500/30 flex items-center justify-center text-3xl mb-4">
              ✅
            </div>
            <h3 class="text-white text-xl font-bold mb-2">Message Sent!</h3>
            <p class="text-slate-400 text-sm mb-6">
              Thanks for reaching out. I'll get back to you within 24 hours.
            </p>
            <button
              onclick={() => sent = false}
              class="px-6 py-2 border border-indigo-500 text-indigo-400 rounded-lg text-sm hover:bg-indigo-500 hover:text-white transition-all duration-200"
            >
              Send Another
            </button>
          </div>
        {:else}
          <!-- Form -->
          <div class="flex flex-col gap-5">
            <h3 class="text-white text-lg font-bold mb-2">Send a Message</h3>

            <!-- Name -->
          <div>
  <label for="name" class="text-slate-400 text-xs font-mono uppercase tracking-widest mb-2 block">
    Name
  </label>
  <input
    id="name"
    type="text"
    bind:value={name}
    placeholder="Your name"
    class="w-full px-4 py-3 rounded-lg bg-[#13131f] border border-[#2e2e45] text-white placeholder-slate-600 text-sm font-mono focus:outline-none focus:border-indigo-500 transition-colors duration-200"
  />
</div>

            <!-- Email -->
            <div>
  <label for="email" class="text-slate-400 text-xs font-mono uppercase tracking-widest mb-2 block">
    Email
  </label>
  <input
    id="email"
    type="email"
    bind:value={email}
    placeholder="your@email.com"
    class="w-full px-4 py-3 rounded-lg bg-[#13131f] border border-[#2e2e45] text-white placeholder-slate-600 text-sm font-mono focus:outline-none focus:border-indigo-500 transition-colors duration-200"
  />
</div>

            <!-- Message -->
            <div>
  <label for="message" class="text-slate-400 text-xs font-mono uppercase tracking-widest mb-2 block">
    Message
  </label>
  <textarea
    id="message"
    bind:value={message}
    placeholder="Tell me about your project..."
    rows="5"
    class="w-full px-4 py-3 rounded-lg bg-[#13131f] border border-[#2e2e45] text-white placeholder-slate-600 text-sm font-mono focus:outline-none focus:border-indigo-500 transition-colors duration-200 resize-none"
  ></textarea>
</div>

            <!-- Error -->
              </label>
              <textarea
                bind:value={message}
                placeholder="Tell me about your project..."
                rows="5"
                class="w-full px-4 py-3 rounded-lg bg-[#13131f] border border-[#2e2e45] text-white placeholder-slate-600 text-sm font-mono focus:outline-none focus:border-indigo-500 transition-colors duration-200 resize-none"
              ></textarea>
            </div>

            <!-- Error -->
            {#if error}
              <p class="text-red-400 text-xs font-mono">{error}</p>
            {/if}

            <!-- Submit -->
            <button
              onclick={handleSubmit}
              disabled={sending}
              class="w-full py-3 bg-indigo-600 hover:bg-indigo-500 disabled:opacity-50 disabled:cursor-not-allowed text-white rounded-lg font-semibold transition-all duration-200 hover:shadow-lg hover:shadow-indigo-500/25"
            >
              {sending ? 'Sending...' : 'Send Message ↗'}
            </button>
          </div>
        {/if}
      </div>
    </div>
  </div>

  <!-- Footer -->
  <div class="mt-24 pt-8 border-t border-[#2e2e45] flex flex-col md:flex-row items-center justify-between gap-4">
    <p class="text-slate-500 text-sm font-mono">
      © 2025 Funmilayo Oba. Built with SvelteKit & TailwindCSS.
    </p>
    <p class="text-slate-600 text-xs font-mono">
      Designed & Developed with ❤️
    </p>
  </div>

</section>