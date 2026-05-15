<script>
  import { onMount } from 'svelte';

  let scrolled = $state(false);
  let menuOpen = $state(false);
  let isDark = $state(true);

  const navLinks = [
    { label: 'Home', href: '#home' },
    { label: 'Projects', href: '#projects' },
    { label: 'Skills', href: '#skills' },
    { label: 'IDE', href: '#ide' },
    { label: 'Contact', href: '#contact' }
  ];

  onMount(() => {
    const saved = localStorage.getItem('theme');
    isDark = saved ? saved === 'dark' : true;
    applyTheme(isDark);

    window.addEventListener('scroll', () => {
      scrolled = window.scrollY > 50;
    });
  });

  function toggleTheme() {
    isDark = !isDark;
    applyTheme(isDark);
    localStorage.setItem('theme', isDark ? 'dark' : 'light');
  }

  function applyTheme(dark) {
    const app = document.getElementById('app');
    const body = document.body;
    if (dark) {
      body.style.backgroundColor = '#161622';
      body.style.color = '#e2e8f0';
      if (app) app.style.backgroundColor = '#161622';
    } else {
      body.style.backgroundColor = '#f8fafc';
      body.style.color = '#0f172a';
      if (app) app.style.backgroundColor = '#f8fafc';
    }
  }

  let navBg = $derived(
    scrolled
      ? isDark ? 'rgba(22,22,34,0.95)' : 'rgba(248,250,252,0.95)'
      : 'transparent'
  );

  let linkColor = $derived(isDark ? '#94a3b8' : '#475569');
  let toggleBg = $derived(isDark ? 'rgba(255,255,255,0.05)' : 'rgba(0,0,0,0.05)');
  let toggleBorder = $derived(isDark ? 'rgba(255,255,255,0.1)' : 'rgba(0,0,0,0.1)');
  let mobileBg = $derived(isDark ? '#1e1e2e' : '#ffffff');
</script>

<nav
  class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
  style="background-color: {navBg}; backdrop-filter: {scrolled ? 'blur(12px)' : 'none'}; border-bottom: {scrolled ? '1px solid rgba(255,255,255,0.08)' : 'none'};"
>
  <div class="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">

    <!-- Logo -->
    <a href="#home" class="text-xl font-bold bg-gradient-to-r from-indigo-400 to-purple-400 bg-clip-text text-transparent">
      &lt;Funmilayo /&gt;
    </a>

    <!-- Desktop Links -->
    <ul class="hidden md:flex items-center gap-8">
      {#each navLinks as link}
        <li>
          <a href={link.href} class="text-sm font-medium transition-colors duration-200 hover:text-indigo-400" style="color: {linkColor};">
            {link.label}
          </a>
        </li>
      {/each}
    </ul>

    <!-- Right Side Desktop -->
    <div class="hidden md:flex items-center gap-3">
      <button
        onclick={toggleTheme}
        aria-label="Toggle theme"
        class="w-9 h-9 rounded-lg flex items-center justify-center transition-all duration-200 text-base"
        style="border: 1px solid {toggleBorder}; background-color: {toggleBg};"
      >
        {isDark ? '☀️' : '🌙'}
      </button>
      <a href="/resume.pdf" target="_blank" class="px-4 py-2 border border-indigo-500 text-indigo-400 rounded-lg text-sm font-medium hover:bg-indigo-500 hover:text-white transition-all duration-200">
        Resume ↗
      </a>
    </div>

    <!-- Mobile Right Side -->
    <div class="md:hidden flex items-center gap-3">
      <button
        onclick={toggleTheme}
        aria-label="Toggle theme"
        class="w-9 h-9 rounded-lg flex items-center justify-center text-base"
        style="border: 1px solid {toggleBorder};"
      >
        {isDark ? '☀️' : '🌙'}
      </button>
      <button
        onclick={() => menuOpen = !menuOpen}
        aria-label="Toggle menu"
        class="text-slate-400 hover:text-white text-xl"
      >
        {menuOpen ? '✕' : '☰'}
      </button>
    </div>
  </div>

  <!-- Mobile Menu -->
  {#if menuOpen}
    <div class="md:hidden border-t px-6 py-4" style="background-color: {mobileBg}; border-color: rgba(255,255,255,0.08);">
      <ul class="flex flex-col gap-4 mb-4">
        {#each navLinks as link}
          <li>
            <a href={link.href} onclick={() => menuOpen = false} class="hover:text-indigo-400 transition-colors duration-200 text-sm font-medium" style="color: {linkColor};">
              {link.label}
            </a>
          </li>
        {/each}
      </ul>
      <a href="/resume.pdf" target="_blank" class="block text-center px-4 py-2 border border-indigo-500 text-indigo-400 rounded-lg text-sm font-medium hover:bg-indigo-500 hover:text-white transition-all duration-200">
        Resume ↗
      </a>
    </div>
  {/if}
</nav>