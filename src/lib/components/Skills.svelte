<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  gsap.registerPlugin(ScrollTrigger);

  const skillCategories = [
    {
      category: 'Frontend',
      icon: '🎨',
      color: '#6366f1',
      skills: [
        { name: 'Vue 3', level: 90 },
        { name: 'React', level: 80 },
        { name: 'Next.js', level: 75 },
        { name: 'SvelteKit', level: 70 },
        { name: 'TypeScript', level: 78 }
      ]
    },
    {
      category: 'Styling',
      icon: '✨',
      color: '#a855f7',
      skills: [
        { name: 'TailwindCSS', level: 92 },
        { name: 'CSS / SCSS', level: 88 },
        { name: 'Framer Motion', level: 75 },
        { name: 'GSAP', level: 70 }
      ]
    },
    {
      category: 'State & Tools',
      icon: '⚙️',
      color: '#14b8a6',
      skills: [
        { name: 'Pinia', level: 85 },
        { name: 'Vuex', level: 80 },
        { name: 'Git & GitHub', level: 88 },
        { name: 'Vite', level: 82 }
      ]
    },
    {
      category: 'Backend & APIs',
      icon: '🔧',
      color: '#f59e0b',
      skills: [
        { name: 'REST APIs', level: 85 },
        { name: 'Node.js', level: 65 },
        { name: 'Web Crypto API', level: 70 },
        { name: 'Firebase', level: 68 }
      ]
    }
  ];

  const tools = [
    'VS Code', 'Figma', 'Git', 'GitHub', 'Vercel',
    'Netlify', 'Postman', 'Chrome DevTools', 'npm', 'Vite'
  ];

  onMount(() => {
    gsap.from('.skills-title', {
      scrollTrigger: { trigger: '#skills', start: 'top 80%' },
      opacity: 0,
      y: 40,
      duration: 0.8
    });

    gsap.from('.skill-category', {
      scrollTrigger: { trigger: '#skills', start: 'top 70%' },
      opacity: 0,
      y: 60,
      duration: 0.8,
      stagger: 0.2,
      clearProps: 'all'
    });

    ScrollTrigger.create({
      trigger: '#skills',
      start: 'top 60%',
      once: true,
      onEnter: () => {
        document.querySelectorAll('.skill-bar-fill').forEach((bar) => {
          const width = bar.getAttribute('data-width');
          gsap.to(bar, {
            width: width + '%',
            duration: 1.2,
            ease: 'power2.out'
          });
        });
      }
    });
  });
</script>

<section id="skills" class="py-32 px-6 max-w-7xl mx-auto">

  <!-- Header -->
  <div class="skills-title text-center mb-16">
    <p class="text-indigo-400 font-mono text-sm tracking-widest uppercase mb-3">
      What I Know
    </p>
    <h2 class="text-4xl md:text-5xl font-black text-white mb-4">
      Skills & Technologies
    </h2>
    <p class="text-slate-400 max-w-xl mx-auto">
      Technologies I've worked with and the confidence level I've built in each.
    </p>
  </div>

  <!-- Skills Grid -->
  <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-16">
    {#each skillCategories as category}
      <div class="skill-category border border-[#2e2e45] bg-[#1e1e2e] rounded-2xl p-6 hover:border-indigo-500/50 transition-all duration-300">

        <!-- Category Header -->
        <div class="flex items-center gap-3 mb-6">
          <span class="text-2xl">{category.icon}</span>
          <h3 class="text-lg font-bold text-white">{category.category}</h3>
          <div class="ml-auto w-2 h-2 rounded-full" style="background: {category.color};"></div>
        </div>

        <!-- Skills -->
        <div class="flex flex-col gap-4">
          {#each category.skills as skill}
            <div>
              <div class="flex justify-between items-center mb-1.5">
                <span class="text-slate-300 text-sm font-medium">{skill.name}</span>
                <span class="text-slate-500 text-xs font-mono">{skill.level}%</span>
              </div>
              <div class="w-full h-1.5 bg-[#2e2e45] rounded-full overflow-hidden">
                <div
                  class="skill-bar-fill h-full rounded-full"
                  style="width: 0%; background: linear-gradient(to right, {category.color}, {category.color}88);"
                  data-width={skill.level}
                ></div>
              </div>
            </div>
          {/each}
        </div>
      </div>
    {/each}
  </div>

  <!-- Tools -->
  <div class="text-center">
    <p class="text-slate-500 font-mono text-sm uppercase tracking-widest mb-6">
      Tools & Software
    </p>
    <div class="flex flex-wrap gap-3 justify-center">
      {#each tools as tool}
        <span class="px-4 py-2 rounded-full border border-[#2e2e45] bg-[#1e1e2e] text-slate-400 text-sm font-mono hover:border-indigo-500/50 hover:text-indigo-400 transition-all duration-200 cursor-default">
          {tool}
        </span>
      {/each}
    </div>
  </div>

</section>