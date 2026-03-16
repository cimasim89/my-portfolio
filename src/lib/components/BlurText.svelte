<script lang="ts">
  import { onMount } from 'svelte'

  interface Props {
    text?: string
    delay?: number
    className?: string
    animateBy?: 'words' | 'letters'
    direction?: 'top' | 'bottom'
    threshold?: number
    rootMargin?: string
    onAnimationComplete?: () => void
  }

  let {
    text = '',
    delay = 200,
    className = '',
    animateBy = 'words',
    direction = 'top',
    threshold = 0.1,
    rootMargin = '0px',
    onAnimationComplete,
  }: Props = $props()

  let elements = $derived(animateBy === 'words' ? text.split(' ') : text.split(''))
  let inView = $state(false)
  let ref: HTMLParagraphElement

  onMount(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          inView = true
          observer.unobserve(ref)
          if (onAnimationComplete) {
            const maxDelay = (elements.length - 1) * delay + 700
            setTimeout(onAnimationComplete, maxDelay)
          }
        }
      },
      { threshold, rootMargin },
    )
    observer.observe(ref)
    return () => observer.disconnect()
  })
</script>

<p bind:this={ref} class="blur-text {className} flex flex-wrap">
  {#each elements as element, i}
    <span
      class="inline-block will-change-[transform,filter,opacity]"
      style="
        transition-property: filter, opacity, transform;
        transition-duration: 700ms;
        transition-timing-function: cubic-bezier(0.22, 1, 0.36, 1);
        transition-delay: {i * delay}ms;
        filter: {inView ? 'blur(0px)' : 'blur(10px)'};
        opacity: {inView ? 1 : 0};
        transform: {inView
        ? 'translate3d(0,0,0)'
        : `translate3d(0,${direction === 'top' ? '-50px' : '50px'},0)`};
      "
    >{element === ' ' ? '\u00A0' : element}{animateBy === 'words' &&
      i < elements.length - 1
      ? '\u00A0'
      : ''}</span>
  {/each}
</p>
