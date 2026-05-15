<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  gsap.registerPlugin(ScrollTrigger);

  const files = [
    {
      name: 'about-me.js',
      icon: '📄',
      language: 'javascript',
      content: `// About Funmilayo Oba
const developer = {
  name: "Funmilayo Oba",
  title: "Frontend Developer",
  location: "Nigeria 🇳🇬",
  email: "funmilayooba@gmail.com",
  
  summary: \`
    Passionate frontend developer with experience
    building scalable, performant and beautiful
    web applications. I love turning ideas into
    smooth digital experiences.
  \`,

  education: {
    degree: "Computer Science",
    passion: "Self-taught & always learning"
  },

  interests: [
    "UI/UX Design",
    "Open Source",
    "Web Performance",
    "Creative Coding"
  ],

  currentlyLearning: [
    "SvelteKit",
    "Three.js",
    "Web Animations"
  ]
};

export default developer;`
    },
    {
      name: 'skills.json',
      icon: '🔧',
      language: 'json',
      content: `{
  "frontend": {
    "frameworks": ["Vue 3", "React", "Next.js", "SvelteKit"],
    "styling": ["TailwindCSS", "SCSS", "Framer Motion", "GSAP"],
    "languages": ["JavaScript", "TypeScript", "HTML5", "CSS3"]
  },

  "stateManagement": {
    "vue": ["Pinia", "Vuex"],
    "react": ["Context API", "Redux"]
  },

  "tools": {
    "versionControl": ["Git", "GitHub"],
    "deployment": ["Vercel", "Netlify"],
    "design": ["Figma"],
    "testing": ["Vitest", "Jest"],
    "bundlers": ["Vite", "Webpack"]
  },

  "apis": {
    "experience": ["REST APIs", "Web Crypto API", "Firebase"],
    "practices": ["Clean Code", "Component Architecture"]
  },

  "softSkills": [
    "Problem Solving",
    "Team Collaboration",
    "Attention to Detail",
    "Fast Learner"
  ]
}`
    },
    {
      name: 'projects.ts',
      icon: '🚀',
      language: 'typescript',
      content: `interface Project {
  name: string;
  description: string;
  stack: string[];
  live: string;
  github: string;
}

const projects: Project[] = [
  {
    name: "PulseBoard",
    description: "Real-time analytics dashboard with live data",
    stack: ["Vue 3", "TypeScript", "Pinia", "Tailwind"],
    live: "https://pulse-board-mu-virid.vercel.app",
    github: "https://github.com/Funmi-Oba/PulseBoard"
  },
  {
    name: "Cartify",
    description: "Full e-commerce app with REST API integration",
    stack: ["Vue 3", "Pinia", "Tailwind", "REST API"],
    live: "https://cartify2.vercel.app",
    github: "https://github.com/Funmi-Oba/Cartify"
  },
  {
    name: "ChatApp",
    description: "End-to-End encrypted messaging application",
    stack: ["React", "Vite", "Web Crypto API", "Tailwind"],
    live: "https://chat-app-one-teal-30.vercel.app",
    github: "https://github.com/Funmi-Oba/ChatApp"
  },
  {
    name: "GetChange",
    description: "Admin dashboard for staff & task management",
    stack: ["Vue", "Tailwind"],
    live: "https://get-change-one.vercel.app",
    github: "https://github.com/Funmi-Oba/GetChange"
  }
];

export default projects;`
    },
    {
      name: 'contact.md',
      icon: '📬',
      language: 'markdown',
      content: `# Let's Work Together

## Contact Information

- **Email:** funmilayooba@gmail.com
- **GitHub:** github.com/Funmi-Oba
- **LinkedIn:** linkedin.com/in/funmilayo-oba
- **Portfolio:** funmilayooba.vercel.app

## What I'm Looking For

I am open to:
- Full-time Frontend Developer roles
- Freelance & contract projects
- Open source collaborations
- Mentorship opportunities

## Response Time

I typically respond within **24 hours**.
Feel free to reach out — I'd love to connect!

## Currently Available

✅ Open to new opportunities
✅ Available for remote work
✅ Open to relocation discussions`
    }
  ];

  let activeFile = $state(files[0]);
  let lineNumbers = $derived(
    activeFile.content.split('\n').map((_, i) => i + 1)
  );

  function getTokenColor(line, language) {
    if (language === 'json') {
      line = line.replace(/"([^"]+)":/g, '<span style="color:#79b8ff;">\"$1\"</span>:');
      line = line.replace(/: "([^"]+)"/g, ': <span style="color:#9ecbff;">\"$1\"</span>');
      line = line.replace(/: (\d+)/g, ': <span style="color:#f8c555;">$1</span>');
      line = line.replace(/: (true|false|null)/g, ': <span style="color:#f97583;">$1</span>');
      return line;
    }
    if (language === 'markdown') {
      line = line.replace(/^(#{1,3} .+)/, '<span style="color:#79b8ff;">$1</span>');
      line = line.replace(/\*\*([^*]+)\*\*/g, '<span style="color:#f8c555;">**$1**</span>');
      line = line.replace(/^- (.+)/, '- <span style="color:#9ecbff;">$1</span>');
      line = line.replace(/✅/g, '<span style="color:#22c55e;">✅</span>');
      return line;
    }
    // JS/TS
    line = line.replace(
      /\b(const|let|var|function|return|export|default|import|from|interface|type|class|extends|implements|async|await|if|else|for|of|in|new)\b/g,
      '<span style="color:#f97583;">$1</span>'
    );
    line = line.replace(/"([^"]+)"/g, '<span style="color:#9ecbff;">"$1"</span>');
    line = line.replace(/`([^`]+)`/g, '<span style="color:#9ecbff;">`$1`</span>');
    line = line.replace(/\/\/.+/g, '<span style="color:#6a737d;">$&</span>');
    line = line.replace(/\b(\d+)\b/g, '<span style="color:#f8c555;">$1</span>');
    return line;
  }

  onMount(() => {
    gsap.from('.ide-title', {
      scrollTrigger: { trigger: '#ide', start: 'top 80%' },
      opacity: 0,
      y: 40,
      duration: 0.8
    });

    gsap.from('.ide-window', {
      scrollTrigger: { trigger: '#ide', start: 'top 70%' },
      opacity: 0,
      y: 60,
      duration: 1,
      clearProps: 'all'
    });
  });
</script>

<section id="ide" class="py-32 px-6 max-w-7xl mx-auto">

  <!-- Header -->
  <div class="ide-title text-center mb-16">
    <p class="text-indigo-400 font-mono text-sm tracking-widest uppercase mb-3">
      Explore My Code
    </p>
    <h2 class="text-4xl md:text-5xl font-black text-white mb-4">
      Open My Codebase
    </h2>
    <p class="text-slate-400 max-w-xl mx-auto">
      Browse through my portfolio like you would a codebase. Click any file to explore.
    </p>
  </div>

  <!-- IDE Window -->
  <div class="ide-window rounded-2xl overflow-hidden border border-[#2e2e45] bg-[#1e1e2e] shadow-2xl">

    <!-- Title Bar -->
    <div class="flex items-center gap-2 px-4 py-3 bg-[#13131f] border-b border-[#2e2e45]">
      <div class="w-3 h-3 rounded-full bg-red-500/80"></div>
      <div class="w-3 h-3 rounded-full bg-yellow-500/80"></div>
      <div class="w-3 h-3 rounded-full bg-green-500/80"></div>
      <span class="ml-4 text-slate-500 text-sm font-mono">funmilayo-portfolio — VS Code</span>
    </div>

    <div class="flex" style="height: 500px;">

      <!-- Sidebar -->
      <div class="w-56 bg-[#13131f] border-r border-[#2e2e45] flex flex-col">

        <!-- Explorer header -->
        <div class="px-4 py-3 border-b border-[#2e2e45]">
          <span class="text-slate-500 text-xs font-mono uppercase tracking-widest">Explorer</span>
        </div>

        <!-- Folder -->
        <div class="px-3 py-2">
          <div class="flex items-center gap-1 text-slate-400 text-xs font-mono mb-1 px-1">
            <span>▼</span>
            <span>FUNMILAYO-PORTFOLIO</span>
          </div>

          <!-- Files -->
          <div class="flex flex-col">
            {#each files as file}
              <button
                onclick={() => activeFile = file}
                class="flex items-center gap-2 px-3 py-1.5 rounded text-xs font-mono transition-all duration-150 text-left w-full {activeFile.name === file.name ? 'bg-[#2e2e45] text-white' : 'text-slate-400 hover:bg-[#2e2e45]/50 hover:text-slate-300'}"
              >
                <span>{file.icon}</span>
                <span>{file.name}</span>
              </button>
            {/each}
          </div>
        </div>
      </div>

      <!-- Editor Area -->
      <div class="flex-1 flex flex-col overflow-hidden">

        <!-- Tab bar -->
        <div class="flex bg-[#13131f] border-b border-[#2e2e45]">
          <div class="flex items-center gap-2 px-4 py-2 bg-[#1e1e2e] border-r border-[#2e2e45] border-t-2 border-t-indigo-500">
            <span class="text-xs">{activeFile.icon}</span>
            <span class="text-white text-xs font-mono">{activeFile.name}</span>
            <span class="text-slate-500 text-xs ml-1 hover:text-white cursor-pointer">×</span>
          </div>
        </div>

        <!-- Code -->
        <div class="flex-1 overflow-auto bg-[#1e1e2e]">
          <div class="flex min-h-full">

            <!-- Line numbers -->
            <div class="flex flex-col items-end pr-4 pl-4 py-4 bg-[#1e1e2e] select-none border-r border-[#2e2e45]">
              {#each lineNumbers as num}
                <span class="text-slate-600 text-xs font-mono leading-6">{num}</span>
              {/each}
            </div>

            <!-- Code content -->
            <div class="flex-1 py-4 px-4 overflow-x-auto">
              {#each activeFile.content.split('\n') as line}
                <div class="text-xs font-mono leading-6 whitespace-pre">
                  {@html getTokenColor(line, activeFile.language) || '&nbsp;'}
                </div>
              {/each}
            </div>
          </div>
        </div>

        <!-- Status bar -->
        <div class="flex items-center justify-between px-4 py-1 bg-indigo-600 text-white text-xs font-mono">
          <div class="flex items-center gap-4">
            <span>⎇ main</span>
            <span>Funmilayo Oba</span>
          </div>
          <div class="flex items-center gap-4">
            <span>{activeFile.language}</span>
            <span>UTF-8</span>
            <span>Ln {lineNumbers.length}</span>
          </div>
        </div>
      </div>
    </div>
  </div>

</section>