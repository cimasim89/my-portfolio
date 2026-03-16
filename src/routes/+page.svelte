<script lang="ts">
  import Aurora from '$lib/components/Aurora.svelte'
  import Navbar from '$lib/components/Navbar.svelte'

  const skills = {
    frontend: ['React.js', 'Next.js', 'TypeScript', 'Tailwind CSS'],
    backend: ['Java', 'Spring Framework', 'Axon Framework', 'REST APIs'],
    other: ['Rust', 'Git', 'Event-Driven Architecture'],
    approach: ['Domain-Driven Design', 'Design Patterns', 'Functional Programming'],
  }

  const projects = [
    {
      name: 'GitHub',
      description:
        'Open source projects, experiments and personal repositories.',
      tags: ['React', 'Rust', 'TypeScript'],
      link: 'https://github.com/cimasim89',
      comingSoon: false,
    },
    {
      name: 'Trillium',
      description: 'Digital platform for Casalini Libri. Book discovery and management for libraries and publishers.',
      tags: ['Next.js', 'TypeScript'],
      link: 'https://trillium.casalinilibri.com/it',
      comingSoon: false,
    },
  ]

  const experience = [
    {
      company: 'Spazio Codice',
      role: 'Software Engineer',
      period: 'Current',
      note: 'Main freelance association',
      link: 'https://spaziocodice.com',
    },
    {
      company: 'Asystel SRL',
      role: 'Software Engineer',
      period: 'Past',
      note: 'Trevi (PG)',
      link: null,
    },
    {
      company: 'Fabrick',
      role: 'Freelance Collaboration',
      period: 'Freelance',
      note: null,
      link: null,
    },
    {
      company: 'MTU Academy',
      role: 'Freelance Collaboration',
      period: 'Freelance',
      note: null,
      link: null,
    },
  ]
</script>

<svelte:head>
  <title>Simone Cimarelli — Software Engineer</title>
  <meta
    name="description"
    content="Freelance Software Engineer specialising in React, Next.js, TypeScript and Java. Mainly associated with Spazio Codice."
  />
</svelte:head>

<Navbar />

<!-- ── HERO ─────────────────────────────────────────────── -->
<section id="hero" class="relative min-h-screen flex items-center">
  <div class="absolute inset-0 pointer-events-none">
    <Aurora
      colorStops={['#1a5c08', '#0a0a0a', '#0a0a0a']}
      blend={0.6}
      amplitude={1.2}
      speed={0.4}
    />
  </div>

  <div class="relative z-10 max-w-5xl mx-auto px-6 pt-14 pb-24">
    <p class="text-xs uppercase tracking-widest text-neutral-500 mb-6">
      Available for freelance
    </p>
    <h1 class="text-5xl sm:text-7xl font-bold tracking-tight leading-none mb-5">
      Simone<br />Cimarelli
    </h1>
    <p class="text-lg text-neutral-400 mb-6">Software Engineer</p>
    <p class="text-neutral-500 max-w-sm leading-relaxed mb-10">
      Building scalable web applications and distributed systems. Freelance
      engineer, mainly associated with
      <a
        href="https://spaziocodice.com"
        target="_blank"
        rel="noopener noreferrer"
        class="text-neutral-300 hover:text-white transition-colors">Spazio Codice</a
      >.
    </p>
    <div class="flex flex-wrap gap-3">
      <a
        href="#projects"
        class="px-5 py-2.5 bg-white text-black text-sm font-medium rounded-md hover:bg-neutral-100 transition-colors"
      >
        View Work
      </a>
      <a
        href="https://github.com/cimasim89"
        target="_blank"
        rel="noopener noreferrer"
        class="px-5 py-2.5 border border-white/15 text-neutral-300 text-sm rounded-md hover:border-white/30 hover:text-white transition-all"
      >
        GitHub ↗
      </a>
    </div>
  </div>

  <!-- scroll hint -->
  <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2">
    <span class="text-xs text-neutral-700 tracking-widest uppercase">Scroll</span>
    <div class="w-px h-8 bg-gradient-to-b from-neutral-700 to-transparent"></div>
  </div>
</section>

<!-- ── ABOUT ─────────────────────────────────────────────── -->
<section id="about" class="py-24 border-t border-white/5">
  <div class="max-w-5xl mx-auto px-6">
    <p class="text-xs uppercase tracking-widest text-neutral-600 mb-10">About</p>
    <div class="max-w-2xl">
      <p class="text-2xl sm:text-3xl font-light leading-relaxed text-neutral-200">
        Freelance software engineer focused on
        <span class="text-white font-normal">frontend development</span>
        and
        <span class="text-white font-normal">distributed systems</span>. Mainly
        working with
        <a
          href="https://spaziocodice.com"
          target="_blank"
          rel="noopener noreferrer"
          class="text-white underline underline-offset-4 decoration-white/20 hover:decoration-white/60 transition-all"
          >Spazio Codice</a
        >, building modern web applications and event-driven backends.
      </p>
      <p class="text-neutral-500 mt-6 leading-relaxed">
        Outside of client work I explore systems programming with Rust, and enjoy
        working on side projects that push the boundaries of what I know.
      </p>
      <p class="text-neutral-500 mt-4 leading-relaxed">
        When I'm not coding, you'll find me running tabletop RPG campaigns as both
        player and GM, playing saxophone in a band, or slowly learning guitar.
      </p>
    </div>
  </div>
</section>

<!-- ── SKILLS ─────────────────────────────────────────────── -->
<section id="skills" class="py-24 border-t border-white/5">
  <div class="max-w-5xl mx-auto px-6">
    <p class="text-xs uppercase tracking-widest text-neutral-600 mb-10">Skills</p>
    <div class="grid grid-cols-2 sm:grid-cols-4 gap-10 sm:gap-6">
      <div>
        <h3 class="text-sm font-medium text-white mb-5">Frontend</h3>
        <ul class="space-y-3">
          {#each skills.frontend as skill}
            <li class="text-sm text-neutral-400">{skill}</li>
          {/each}
        </ul>
      </div>
      <div>
        <h3 class="text-sm font-medium text-white mb-5">Backend</h3>
        <ul class="space-y-3">
          {#each skills.backend as skill}
            <li class="text-sm text-neutral-400">{skill}</li>
          {/each}
        </ul>
      </div>
      <div>
        <h3 class="text-sm font-medium text-white mb-5">Other</h3>
        <ul class="space-y-3">
          {#each skills.other as skill}
            <li class="text-sm text-neutral-400">{skill}</li>
          {/each}
        </ul>
      </div>
      <div>
        <h3 class="text-sm font-medium text-white mb-5">Approach</h3>
        <ul class="space-y-3">
          {#each skills.approach as skill}
            <li class="text-sm text-neutral-400">{skill}</li>
          {/each}
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- ── PROJECTS ─────────────────────────────────────────────── -->
<section id="projects" class="py-24 border-t border-white/5">
  <div class="max-w-5xl mx-auto px-6">
    <p class="text-xs uppercase tracking-widest text-neutral-600 mb-10">Projects</p>
    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
      {#each projects as project}
        {#if !project.comingSoon && project.link}
          <a
            href={project.link}
            target="_blank"
            rel="noopener noreferrer"
            class="group p-6 border border-white/8 rounded-lg hover:border-white/20 hover:bg-white/2 transition-all duration-200"
          >
            <div class="flex items-start justify-between mb-5">
              <div
                class="w-9 h-9 rounded-md border border-white/10 bg-white/5 flex items-center justify-center text-xs font-medium text-neutral-300"
              >
                GH
              </div>
              <span
                class="text-neutral-600 group-hover:text-neutral-300 transition-colors text-sm"
                >↗</span
              >
            </div>
            <h3 class="font-medium text-white mb-2">{project.name}</h3>
            <p class="text-sm text-neutral-500 leading-relaxed">{project.description}</p>
            {#if project.tags.length > 0}
              <div class="mt-5 flex flex-wrap gap-2">
                {#each project.tags as tag}
                  <span
                    class="text-xs px-2 py-0.5 rounded bg-white/5 text-neutral-500 border border-white/8"
                    >{tag}</span
                  >
                {/each}
              </div>
            {/if}
          </a>
        {:else}
          <div class="p-6 border border-white/8 rounded-lg">
            <div class="flex items-start justify-between mb-5">
              <div
                class="w-9 h-9 rounded-md border border-white/10 bg-white/5 flex items-center justify-center text-xs font-medium text-neutral-300"
              >
                T
              </div>
              <span
                class="text-xs px-2 py-0.5 rounded-full bg-amber-500/10 text-amber-400 border border-amber-500/20"
                >Coming Soon</span
              >
            </div>
            <h3 class="font-medium text-white mb-2">{project.name}</h3>
            <p class="text-sm text-neutral-500 leading-relaxed">{project.description}</p>
          </div>
        {/if}
      {/each}
    </div>
  </div>
</section>

<!-- ── EXPERIENCE ─────────────────────────────────────────────── -->
<section id="experience" class="py-24 border-t border-white/5">
  <div class="max-w-5xl mx-auto px-6">
    <p class="text-xs uppercase tracking-widest text-neutral-600 mb-10">Experience</p>
    <div class="max-w-2xl space-y-0">
      {#each experience as exp, i}
        <div class="grid grid-cols-[90px_1fr] gap-6 py-7 {i > 0 ? 'border-t border-white/5' : ''}">
          <div class="text-xs text-neutral-600 pt-0.5 uppercase tracking-wide">{exp.period}</div>
          <div>
            {#if exp.link}
              <a
                href={exp.link}
                target="_blank"
                rel="noopener noreferrer"
                class="font-medium text-white hover:text-neutral-300 transition-colors mb-1 inline-flex items-center gap-1"
              >
                {exp.company}
                <span class="text-neutral-600 text-xs">↗</span>
              </a>
            {:else}
              <div class="font-medium text-white mb-1">{exp.company}</div>
            {/if}
            <div class="text-sm text-neutral-400">
              {exp.role}{exp.note ? ` · ${exp.note}` : ''}
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- ── EDUCATION ─────────────────────────────────────────────── -->
<section id="education" class="py-24 border-t border-white/5">
  <div class="max-w-5xl mx-auto px-6">
    <p class="text-xs uppercase tracking-widest text-neutral-600 mb-10">Education</p>
    <div class="max-w-2xl">
      <div class="grid grid-cols-[90px_1fr] gap-6">
        <div class="text-xs text-neutral-600 pt-0.5 uppercase tracking-wide">Degree</div>
        <div>
          <div class="font-medium text-white mb-1">Università degli Studi di Perugia</div>
          <div class="text-sm text-neutral-400 mb-1">
            Laurea Magistrale in Informatica
          </div>
          <div class="text-sm text-neutral-600">Perugia, Italia</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ── CONTACT ─────────────────────────────────────────────── -->
<section id="contact" class="py-24 border-t border-white/5">
  <div class="max-w-5xl mx-auto px-6">
    <p class="text-xs uppercase tracking-widest text-neutral-600 mb-10">Contact</p>
    <div class="max-w-xl">
      <h2 class="text-3xl sm:text-4xl font-light leading-tight mb-4">
        Let's work<br />together.
      </h2>
      <p class="text-neutral-500 mb-10">
        Available for freelance projects and collaborations.
      </p>
      <div class="flex flex-col sm:flex-row gap-3">
        <a
          href="https://github.com/cimasim89"
          target="_blank"
          rel="noopener noreferrer"
          class="px-5 py-3 border border-white/10 text-neutral-300 text-sm rounded-md hover:border-white/25 hover:text-white transition-all text-center"
        >
          GitHub ↗
        </a>
        <a
          href="https://spaziocodice.com"
          target="_blank"
          rel="noopener noreferrer"
          class="px-5 py-3 border border-white/10 text-neutral-300 text-sm rounded-md hover:border-white/25 hover:text-white transition-all text-center"
        >
          Spazio Codice ↗
        </a>
        <a
          href="https://spaziocodice.com/thoughts-on-coding/"
          target="_blank"
          rel="noopener noreferrer"
          class="px-5 py-3 border border-white/10 text-neutral-300 text-sm rounded-md hover:border-white/25 hover:text-white transition-all text-center"
        >
          Blog ↗
        </a>
      </div>
    </div>
  </div>
</section>

<!-- ── FOOTER ─────────────────────────────────────────────── -->
<footer class="border-t border-white/5 py-8">
  <div class="max-w-5xl mx-auto px-6 flex items-center justify-between">
    <span class="text-xs text-neutral-700">Simone Cimarelli</span>
    <span class="text-xs text-neutral-700">© {new Date().getFullYear()}</span>
  </div>
</footer>
