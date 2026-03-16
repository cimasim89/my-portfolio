<script lang="ts">
  import { onMount } from 'svelte'

  let scrolled = $state(false)

  onMount(() => {
    const handler = () => {
      scrolled = window.scrollY > 20
    }
    window.addEventListener('scroll', handler, { passive: true })
    return () => window.removeEventListener('scroll', handler)
  })

  const links = [
    { href: '#about', label: 'About' },
    { href: '#skills', label: 'Skills' },
    { href: '#projects', label: 'Projects' },
    { href: '#experience', label: 'Experience' },
    { href: '#education', label: 'Education' },
    { href: '#contact', label: 'Contact' },
  ]
</script>

<header
  class="fixed top-0 left-0 right-0 z-50 transition-all duration-300 {scrolled
    ? 'border-b border-white/8 bg-[#0a0a0a]/90 backdrop-blur-sm'
    : ''}"
>
  <div class="max-w-5xl mx-auto px-6 h-14 flex items-center justify-between">
    <a href="#hero" class="text-sm font-semibold tracking-tight text-white">SC</a>
    <nav class="hidden sm:flex items-center gap-7">
      {#each links as link}
        <a
          href={link.href}
          class="text-sm text-neutral-400 hover:text-white transition-colors duration-200"
        >{link.label}</a>
      {/each}
    </nav>
  </div>
</header>
