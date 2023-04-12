<script>
  import { onMount } from 'svelte'
  import { pwaInfo } from 'virtual:pwa-info'

  let ReloadPrompt
  onMount(async () => {
    pwaInfo && (ReloadPrompt = (await import('$lib/ReloadPrompt.svelte')).default)
  })

  $: webManifest = pwaInfo ? pwaInfo.webManifest.linkTag : ''  
</script>

<svelte:head>
    {@html webManifest}
    <meta name="theme-color" content="#ffffff"/>
</svelte:head>

<main>
  <slot />
</main>

{#if ReloadPrompt}
  <svelte:component this={ReloadPrompt} />
{/if}
