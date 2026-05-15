<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  gsap.registerPlugin(ScrollTrigger);

  const projects = [
    {
      title: 'PulseBoard',
      description: 'A real-time analytics dashboard featuring live-streaming data simulation, interactive charts, metric cards and activity feed.',
      tags: ['Vue 3', 'TypeScript', 'Tailwind', 'Pinia'],
      github: 'https://github.com/Funmi-Oba/PulseBoard',
      live: 'https://pulse-board-mu-virid.vercel.app/',
      image: '/images/projects/pulseboard.png',
      color: '#6366f1'
    },
    {
      title: 'Cartify',
      description: 'A fully functional e-commerce web app with scalable architecture, RESTful API integration, and responsive UI design.',
      tags: ['Vue 3', 'Tailwind', 'REST API', 'Pinia'],
      github: 'https://github.com/Funmi-Oba/Cartify',
      live: 'https://cartify2.vercel.app/',
      image: '/images/projects/cartify.png',
      color: '#14b8a6'
    },
    {
      title: 'Exclusive',
      description: 'A full featured e-commerce web application with product listings, cart, wishlist and a complete checkout interface.',
      tags: ['Vue', 'Tailwind', 'Vuex'],
      github: 'https://github.com/Funmi-Oba/Exclusive-ECommerce',
      live: 'https://exclusive-ecommerce-nu.vercel.app/login',
      image: '/images/projects/exclusive.png',
      color: '#f43f5e'
    },
    {
      title: 'ChatApp',
      description: 'An End-to-End Encrypted messaging application. Your private key never leaves your device.',
      tags: ['React', 'Vite', 'Tailwind', 'Web Crypto API'],
      github: 'https://github.com/Funmi-Oba/ChatApp',
      live: 'https://chat-app-one-teal-30.vercel.app/login',
      image: '/images/projects/chatapp.png',
      color: '#22c55e'
    },
    {
      title: 'GetChange',
      description: 'An admin dashboard to monitor and manage staff activities, task status, wallet transactions and disbursements.',
      tags: ['Vue', 'Tailwind'],
      github: 'https://github.com/Funmi-Oba/GetChange',
      live: 'https://get-change-one.vercel.app/',
      image: '/images/projects/getchange.png',
      color: '#f59e0b'
    },
    {
      title: 'Portfolio Website',
      description: 'A personal portfolio website with smooth animations, responsive design and a clean modern interface.',
      tags: ['Next.js', 'Tailwind', 'Framer Motion'],
      github: 'https://github.com/Funmi-Oba/FunmiObaPortfolio',
      live: 'https://funmilayooba.vercel.app/',
      image: '/images/projects/portfolio.png',
      color: '#ec4899'
    }
  ];

  const allTags = ['All', 'Vue 3', 'React', 'Next.js', 'TypeScript'];
  let activeFilter = $state('All');

  let filteredProjects = $derived(
    activeFilter === 'All'
      ? projects
      : projects.filter(p => p.tags.includes(activeFilter))
  );

  onMount(() => {
    gsap.from('.projects-title', {
      scrollTrigger: { trigger: '#projects', start: 'top 80%' },
      opacity: 0,
      y: 40,
      duration: 0.8
    });

    gsap.from('.project-card', {
      scrollTrigger: { trigger: '#projects', start: 'top 70%' },
      opacity: 0,
      y: 60,
      duration: 0.8,
      stagger: 0.15
    });
  });
</script>

<section id="projects" class="py-32 px-6 max-w-7xl mx-auto">

  <!-- Header -->
  <div class="projects-title text-center mb-16">
    <p class="text-indigo-400 font-mono text-sm tracking-widest uppercase mb-3">
      My Work
    </p>
    <h2 class="text-4xl md:text-5xl font-black text-white mb-4">
      Featured Projects
    </h2>
    <p class="text-slate-400 max-w-xl mx-auto">
      A collection of projects that showcase my skills across dashboards, e-commerce, and real-time applications.
    </p>
  </div>

  <!-- Filter Tabs -->
  <div class="flex flex-wrap gap-3 justify-center mb-12">
    {#each allTags as filter}
      <button
        onclick={() => activeFilter = filter}
        class="px-4 py-2 rounded-full text-sm font-medium transition-all duration-200 {activeFilter === filter ? 'bg-indigo-600 text-white shadow-lg shadow-indigo-500/25' : 'border border-[#2e2e45] text-slate-400 hover:border-indigo-500 hover:text-indigo-400'}"
      >
        {filter}
      </button>
    {/each}
  </div>

  <!-- Projects Grid -->
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
    {#each filteredProjects as project, i}
      <div class="project-card group relative rounded-2xl overflow-hidden transition-all duration-300 hover:-translate-y-3 hover:shadow-2xl border border-[#2e2e45] bg-[#1e1e2e] hover:border-indigo-500/50">

        <!-- Laptop Mockup -->
        <div class="p-4 pb-0">
          <div class="rounded-t-xl overflow-hidden bg-[#13131f] border border-[#2e2e45]">

            <!-- Browser bar -->
            <div class="flex items-center gap-1.5 px-3 py-2 bg-[#0d0d1a] border-b border-[#2e2e45]">
              <div class="w-2.5 h-2.5 rounded-full bg-red-500/80"></div>
              <div class="w-2.5 h-2.5 rounded-full bg-yellow-500/80"></div>
              <div class="w-2.5 h-2.5 rounded-full bg-green-500/80"></div>
              <div class="flex-1 mx-2 bg-[#2e2e45] rounded px-2 py-0.5">
                <span class="text-slate-500 text-xs font-mono truncate block">{project.live}</span>
              </div>
            </div>

            <!-- Screenshot -->
            <div class="overflow-hidden" style="height: 180px;">
              <img
                src={project.image}
                alt={project.title}
                class="w-full h-full object-cover object-top transition-transform duration-700 group-hover:scale-105"
              />
            </div>
          </div>

          <!-- Laptop stand -->
          <div class="h-2 bg-[#0d0d1a] border-x border-[#2e2e45] mx-4"></div>
          <div class="h-1 bg-[#161622] border border-[#2e2e45] rounded-b-sm mx-2"></div>
        </div>

        <!-- Card Content -->
        <div class="p-5">

          <!-- Number + accent -->
          <div class="flex items-center justify-between mb-3">
            <div class="w-8 h-0.5 rounded-full" style="background: {project.color};"></div>
            <span class="font-mono text-xs text-slate-600">{String(i + 1).padStart(2, '0')}</span>
          </div>

          <!-- Title -->
          <h3 class="text-lg font-bold text-white mb-2 group-hover:text-indigo-400 transition-colors duration-200">
            {project.title}
          </h3>

          <!-- Description -->
          <p class="text-slate-400 text-sm leading-relaxed mb-4">
            {project.description}
          </p>

          <!-- Tags -->
          <div class="flex flex-wrap gap-1.5 mb-4">
            {#each project.tags as tag}
              <span class="px-2 py-0.5 rounded-md text-xs font-mono border border-[#2e2e45] text-slate-400 bg-[#13131f]">
                {tag}
              </span>
            {/each}
          </div>

          <!-- Divider -->
          <div class="w-full h-px bg-[#2e2e45] mb-4"></div>

          <!-- Links -->
          <div class="flex gap-4">
            <a href={project.github} target="_blank" class="text-slate-400 hover:text-white text-sm font-medium transition-colors duration-200">
              GitHub ↗
            </a>
            <a href={project.live} target="_blank" class="text-sm font-medium transition-colors duration-200" style="color: {project.color};">
              Live Demo ↗
            </a>
          </div>
        </div>

        <!-- Hover glow -->
        <div class="absolute inset-0 opacity-0 group-hover:opacity-5 transition-opacity duration-300 pointer-events-none rounded-2xl" style="background: {project.color};"></div>
      </div>
    {/each}
  </div>

</section>