<script lang="ts">
  import Aurora from '$lib/components/Aurora.svelte'
  import BlurText from '$lib/components/BlurText.svelte'
  import RotatingText from '$lib/components/RotatingText.svelte'
</script>

<svelte:head>
  <title>Simone is a dev</title>
  <meta name="description" content="Welcome to my personal website" />
</svelte:head>

<div class="min-h-screen flex flex-col justify-between pb-20">
  <Aurora
    colorStops={['#2a8e10', '#ffffff', '#FF3232']}
    blend={0.8}
    amplitude={1.0}
    speed={0.5}
  />
  <div
    class="items-center justify-items-center p-8 gap-16 sm:p-20 font-[family-name:var(--font-geist-sans)]"
  >
    <main class="flex flex-col gap-8 row-start-2 items-center">
      <BlurText
        text="Simone is a dev"
        delay={150}
        animateBy="words"
        direction="top"
        className="text-7xl mb-8"
      />
      <div class="flex flex-row gap-2 items-center text-3xl">
        <span>Programming is</span>
        <RotatingText
          texts={['Fun', 'Passion', 'Life', 'Love', 'Art']}
          mainClassName="px-2 sm:px-2 md:px-3 bg-cyan-300 text-black overflow-hidden py-0.5 sm:py-1 md:py-2 justify-center rounded-lg"
          staggerFrom="last"
          staggerDuration={0.025}
          splitLevelClassName="overflow-hidden pb-0.5 sm:pb-1 md:pb-1"
          rotationInterval={2000}
        />
      </div>
    </main>
  </div>
  <footer class="row-start-3 flex gap-6 flex-wrap items-center justify-center">
    <a
      class="flex items-center gap-2 hover:underline hover:underline-offset-4"
      href="https://spaziocodice.com/"
      target="_blank"
      rel="noopener noreferrer"
    >
      Spazio Codice
    </a>
    <a
      class="flex items-center gap-2 hover:underline hover:underline-offset-4"
      href="https://github.com/cimasim89"
      target="_blank"
      rel="noopener noreferrer"
    >
      Go to my Github →
    </a>
  </footer>
</div>
