<script>
  import { onMount } from 'svelte';
  import * as THREE from 'three';
  import { gsap } from 'gsap';

  let canvas;
  let scene, camera, renderer;
  let particles;
  let geometries = [];

  onMount(() => {
    initThree();
    animateText();

    window.addEventListener('resize', onResize);
    return () => {
      window.removeEventListener('resize', onResize);
      renderer.dispose();
    };
  });

  function initThree() {
    scene = new THREE.Scene();
    camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.z = 5;

    renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(window.devicePixelRatio);

    // Particles
    const particleGeometry = new THREE.BufferGeometry();
    const count = 1500;
    const positions = new Float32Array(count * 3);
    for (let i = 0; i < count * 3; i++) {
      positions[i] = (Math.random() - 0.5) * 20;
    }
    particleGeometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
    const particleMaterial = new THREE.PointsMaterial({
      size: 0.02,
      color: '#6366f1',
      transparent: true,
      opacity: 0.8
    });
    particles = new THREE.Points(particleGeometry, particleMaterial);
    scene.add(particles);

    // Floating shapes
    const shapes = [
      new THREE.TorusGeometry(0.8, 0.2, 16, 100),
      new THREE.OctahedronGeometry(0.6),
      new THREE.TetrahedronGeometry(0.5),
      new THREE.IcosahedronGeometry(0.5)
    ];

    const materials = [
      new THREE.MeshBasicMaterial({ color: '#6366f1', wireframe: true }),
      new THREE.MeshBasicMaterial({ color: '#a855f7', wireframe: true }),
      new THREE.MeshBasicMaterial({ color: '#6366f1', wireframe: true }),
      new THREE.MeshBasicMaterial({ color: '#a855f7', wireframe: true })
    ];

    const pos = [[-3, 1, -2], [3, -1, -3], [-2, -2, -1], [2, 2, -2]];

    shapes.forEach((geo, i) => {
      const mesh = new THREE.Mesh(geo, materials[i]);
      mesh.position.set(pos[i][0], pos[i][1], pos[i][2]);
      scene.add(mesh);
      geometries.push(mesh);
    });

    // Mouse interaction
    window.addEventListener('mousemove', (e) => {
      const x = (e.clientX / window.innerWidth - 0.5) * 2;
      const y = -(e.clientY / window.innerHeight - 0.5) * 2;
      gsap.to(camera.position, { x: x * 0.3, y: y * 0.3, duration: 1 });
    });

    animate();
  }

  function animate() {
    requestAnimationFrame(animate);
    particles.rotation.y += 0.0003;
    particles.rotation.x += 0.0001;
    geometries.forEach((mesh, i) => {
      mesh.rotation.x += 0.003 * (i % 2 === 0 ? 1 : -1);
      mesh.rotation.y += 0.005 * (i % 2 === 0 ? 1 : -1);
    });
    renderer.render(scene, camera);
  }

  function animateText() {
    gsap.from('.hero-badge', { opacity: 0, y: 30, duration: 0.8, delay: 0.2 });
    gsap.from('.hero-title', { opacity: 0, y: 60, duration: 1, delay: 0.4 });
    gsap.from('.hero-desc', { opacity: 0, y: 40, duration: 1, delay: 0.7 });
    gsap.from('.hero-btns', { opacity: 0, y: 40, duration: 1, delay: 1.0 });
    gsap.from('.hero-links', { opacity: 0, y: 40, duration: 1, delay: 1.3 });
  }

  function onResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
  }
</script>

<section id="home" class="relative w-full h-screen flex items-center justify-center overflow-hidden">

  <!-- Three.js Canvas -->
  <canvas bind:this={canvas} class="absolute inset-0 w-full h-full"></canvas>

  <!-- Gradient overlay -->
  <div class="absolute inset-0 bg-gradient-to-b from-transparent via-[#161622]/40 to-[#161622]"></div>

  <!-- Content -->
  <div class="relative z-10 text-center px-6 max-w-4xl mx-auto">

    <!-- Badge -->
    <div class="hero-badge inline-flex items-center gap-2 px-4 py-2 rounded-full border border-indigo-500/30 bg-indigo-500/10 text-indigo-400 text-sm font-mono mb-6">
      <span class="w-2 h-2 rounded-full bg-indigo-400 animate-pulse"></span>
      Available for work
    </div>

    <!-- Name -->
    <h1 class="hero-title text-5xl md:text-7xl lg:text-8xl font-black mb-6 leading-tight">
      <span class="bg-gradient-to-r from-indigo-400 via-purple-400 to-pink-400 bg-clip-text text-transparent">
        Funmilayo Oba
      </span>
    </h1>

    <!-- Description -->
    <p class="hero-desc text-slate-300 text-lg md:text-xl max-w-2xl mx-auto mb-10 leading-relaxed">
      A passionate <span class="text-indigo-400 font-semibold">Frontend Developer</span> who builds
      immersive, performant, and beautiful web experiences with Vue, React and SvelteKit.
    </p>

    <!-- Buttons -->
    <div class="hero-btns flex flex-wrap gap-4 justify-center mb-12">
      <a href="#projects" class="px-8 py-3 bg-indigo-600 hover:bg-indigo-500 text-white rounded-lg font-semibold transition-all duration-200 hover:scale-105 hover:shadow-lg hover:shadow-indigo-500/25">
        View My Work
      </a>
      <a href="#contact" class="px-8 py-3 border border-slate-600 hover:border-indigo-400 text-slate-300 hover:text-indigo-400 rounded-lg font-semibold transition-all duration-200 hover:scale-105">
        Get In Touch
      </a>
    </div>

    <!-- Social Links -->
    <div class="hero-links flex gap-6 justify-center">
      <a href="https://github.com/Funmi-Oba" target="_blank" class="text-slate-400 hover:text-white transition-colors duration-200 font-mono text-sm">
        GitHub ↗
      </a>
      <a href="https://linkedin.com/in/funmilayo-oba" target="_blank" class="text-slate-400 hover:text-white transition-colors duration-200 font-mono text-sm">
        LinkedIn ↗
      </a>
      <a href="https://funmilayooba.vercel.app/" target="_blank" class="text-slate-400 hover:text-white transition-colors duration-200 font-mono text-sm">
        Portfolio ↗
      </a>
    </div>
  </div>

  <!-- Scroll indicator -->
  <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 text-slate-500">
    <span class="text-xs font-mono tracking-widest uppercase">Scroll</span>
    <div class="w-px h-12 bg-gradient-to-b from-slate-500 to-transparent animate-bounce"></div>
  </div>

</section>