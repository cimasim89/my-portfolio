<script lang="ts">
  import { onMount } from 'svelte'

  interface Props {
    texts: string[]
    mainClassName?: string
    splitLevelClassName?: string
    elementLevelClassName?: string
    rotationInterval?: number
    staggerDuration?: number
    staggerFrom?: 'first' | 'last' | 'center' | 'random' | number
    loop?: boolean
    auto?: boolean
  }

  let {
    texts,
    mainClassName = '',
    splitLevelClassName = '',
    elementLevelClassName = '',
    rotationInterval = 2000,
    staggerDuration = 0,
    staggerFrom = 'first' as 'first' | 'last' | 'center' | 'random' | number,
    loop = true,
    auto = true,
  }: Props = $props()

  type CharItem = { char: string; isSpace: boolean; delay: number }

  let currentIndex = $state(0)
  let phase = $state<'entering' | 'exiting' | 'idle'>('entering')
  let busy = false

  function splitChars(text: string): string[] {
    if (typeof Intl !== 'undefined' && Intl.Segmenter) {
      const seg = new Intl.Segmenter('en', { granularity: 'grapheme' })
      return Array.from(seg.segment(text), s => s.segment)
    }
    return Array.from(text)
  }

  function buildChars(index: number): CharItem[] {
    const words = texts[index].split(' ')
    const items: CharItem[] = []

    words.forEach((word, wi) => {
      splitChars(word).forEach(char => items.push({ char, isSpace: false, delay: 0 }))
      if (wi < words.length - 1) items.push({ char: ' ', isSpace: true, delay: 0 })
    })

    const nonSpace = items.filter(c => !c.isSpace)
    const total = nonSpace.length
    const d = staggerDuration * 1000 // seconds → milliseconds
    let nonSpaceIdx = 0

    items.forEach(c => {
      if (c.isSpace) return
      const i = nonSpaceIdx++
      if (staggerFrom === 'first') c.delay = i * d
      else if (staggerFrom === 'last') c.delay = (total - 1 - i) * d
      else if (staggerFrom === 'center')
        c.delay = Math.abs(Math.floor(total / 2) - i) * d
      else if (staggerFrom === 'random')
        c.delay = Math.abs(Math.floor(Math.random() * total) - i) * d
      else c.delay = Math.abs((staggerFrom as number) - i) * d
    })

    return items
  }

  function maxDelay(charItems: CharItem[]): number {
    const delays = charItems.filter(c => !c.isSpace).map(c => c.delay)
    return delays.length > 0 ? Math.max(...delays) : 0
  }

  let chars = $derived(buildChars(currentIndex))

  const EXIT_DURATION = 300
  const ENTER_DURATION = 350

  async function rotate() {
    if (busy) return
    busy = true

    const nextIndex = loop
      ? (currentIndex + 1) % texts.length
      : Math.min(currentIndex + 1, texts.length - 1)

    if (nextIndex === currentIndex) {
      busy = false
      return
    }

    const exitMax = maxDelay(chars)
    phase = 'exiting'
    await new Promise<void>(r => setTimeout(r, exitMax + EXIT_DURATION + 20))

    // Both state updates are batched by Svelte into a single render:
    // new chars (from new currentIndex) get the entering class from the start.
    currentIndex = nextIndex
    phase = 'entering'

    const enterMax = maxDelay(chars)
    await new Promise<void>(r => setTimeout(r, enterMax + ENTER_DURATION + 20))

    phase = 'idle'
    busy = false
  }

  onMount(() => {
    if (!auto) return
    const id = setInterval(rotate, rotationInterval)
    return () => clearInterval(id)
  })
</script>

<span class="flex flex-wrap whitespace-pre-wrap relative {mainClassName}">
  <span class="sr-only">{texts[currentIndex]}</span>
  <span class="flex flex-wrap whitespace-pre-wrap relative" aria-hidden="true">
    {#each chars as item}
      {#if item.isSpace}
        <span class="whitespace-pre"> </span>
      {:else}
        <span class="inline-flex {splitLevelClassName}">
          <span
            class="inline-block {elementLevelClassName}"
            class:char-entering={phase === 'entering'}
            class:char-exiting={phase === 'exiting'}
            style="animation-delay: {item.delay}ms"
          >{item.char}</span>
        </span>
      {/if}
    {/each}
  </span>
</span>

<style>
  .char-entering {
    animation: charEnter 350ms cubic-bezier(0.22, 1, 0.36, 1) both;
  }

  .char-exiting {
    animation: charExit 300ms cubic-bezier(0.22, 1, 0.36, 1) both;
  }

  @keyframes charEnter {
    from {
      transform: translateY(100%);
    }
    to {
      transform: translateY(0);
    }
  }

  @keyframes charExit {
    from {
      transform: translateY(0);
    }
    to {
      transform: translateY(-120%);
    }
  }
</style>
