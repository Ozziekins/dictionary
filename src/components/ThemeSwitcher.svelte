<script lang="ts">
  import IconMoon from '../icons/IconMoon.svelte'
  import IconSun from '../icons/IconSun.svelte'

  const THEME = 'theme'
  const DARK = 'dark'
  const LIGHT = 'light'

  let darkMode = !('theme' in localStorage)
    ? window.matchMedia('(prefers-color-scheme: dark)').matches
    : localStorage.getItem(THEME) === DARK

  function handleSwitchDarkMode() {
    darkMode = !darkMode
  }

  function handleKeydown(event: KeyboardEvent) {
    if (event.key === 'Enter' || event.key === ' ') {
      handleSwitchDarkMode()
    }
  }

  $: {
    darkMode
      ? document.documentElement.classList.add(DARK)
      : document.documentElement.classList.remove(DARK)

    localStorage.setItem(THEME, darkMode ? DARK : LIGHT)
  }
</script>

<label for="theme-switcher" class="flex gap-5">
  <div
    id="theme-switcher"
    aria-label="Theme switcher"
    class="cursor-pointer"
    on:click={handleSwitchDarkMode}
    on:keydown={handleKeydown}
  >
    {#if darkMode}
      <IconSun class="text-yellow-500" />
    {:else}
      <IconMoon class={`text-dark-grey dark:text-purple`} />
    {/if}
  </div>
</label>
