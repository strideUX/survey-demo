<script lang="ts">
  import { onMount } from 'svelte';
  import logo1 from '$lib/images/logo1@2x.png';
  import logo2 from '$lib/images/logo2@2x.png';
  import logo3 from '$lib/images/logo3@2x.png';
  import productImage from '$lib/images/prod-image@2x.png';
  import { readableColor } from 'polished';
  let feedback = '';

  // Define the three palettes, each with a logo and title
  const palettes = [
    {
      name: 'Example 1',
      primary: '#0067A0',
      secondary: '#1789C8',
      bg: '#F1F2ED',
      fgBg: '#FFFFFF',
      text: '#424242',
      logo: logo1,
      title: 'Mountain Trek Mix Taste Test Survey',
    },
    {
      name: 'Example 2',
      primary: '#FCB154',
      secondary: '#FF9E9E',
      bg: '#9942FF',
      fgBg: '#FFFFFF',
      text: '#512889',
      logo: logo2,
      title: 'Lorem ipsum dolor sit amet',
    },
    {
      name: 'Example 3',
      primary: '#00F0FF',
      secondary: '#00ACB7',
      bg: '#000000',
      fgBg: '#2D2F35',
      text: '#FFFFFF',
      logo: logo3,
      title: 'Lorem ipsum dolor sit amet',
    },
  ];

  let selectedPaletteIdx = 0;

  // Helper to update CSS variables on the root container
  function applyPalette(palette: typeof palettes[0]) {
    const root = document.getElementById('palette-root');
    if (root) {
      root.style.setProperty('--color-primary', palette.primary);
      root.style.setProperty('--color-secondary', palette.secondary);
      root.style.setProperty('--color-bg', palette.bg);
      root.style.setProperty('--color-fg-bg', palette.fgBg);
      root.style.setProperty('--color-text', palette.text);
    }
  }

  // Set initial palette in browser
  onMount(() => {
    applyPalette(palettes[selectedPaletteIdx]);
  });

  // Reactively update palette on change (browser only)
  $: if (typeof document !== 'undefined') {
    applyPalette(palettes[selectedPaletteIdx]);
  }

  // Compute accessible text color for the Next button
  $: nextButtonTextColor = readableColor(palettes[selectedPaletteIdx].primary);
</script>

<svelte:head>
  <title>Mountain Trek Mix Taste Test Survey</title>
</svelte:head>

<!-- Page background -->
<div id="palette-root" class="min-h-screen flex flex-col w-full" style="background: var(--color-bg);">
  <!-- Sticky wrapper for header and progress bar -->
  <div class="sticky-header-bar" style="position: sticky; top: 0; z-index: 10; background: var(--color-fg-bg);">
    <header class="w-full flex items-center justify-between px-8 py-3 shadow-sm" style="background: var(--color-fg-bg);">
      <div class="flex items-center gap-2 md:gap-3"> 
        <img src={palettes[selectedPaletteIdx].logo} alt="Logo" style="height: 40px; width: auto;" />
        <h1 class="text-base font-medium leading-6 ml-2" style="font-family: 'Roboto', sans-serif; font-weight: 500; font-size: 16px; line-height: 24px; color: var(--color-text);">{palettes[selectedPaletteIdx].title}</h1>
      </div>
      <span class="text-base leading-6" style="font-family: 'Roboto', sans-serif; font-weight: 500; font-size: 16px; line-height: 24px; color: var(--color-text);">2 of 3</span>
    </header>
    <!-- Progress Bar below header, full width -->
    <div class="w-full h-1" style="background-color: rgba(23, 137, 200, 0.3);">
      <div class="h-full" style="width:66.666vw; max-width:100vw; background-color: var(--color-primary);"></div>
    </div>
  </div>

  <!-- Main content card with outer container for horizontal padding -->
  <div style="padding-left: 16px; padding-right: 16px; margin-top: 16px;">
    <main class="shadow-lg rounded-xl p-4 sm:p-8 md:p-12 text-center" style="background: var(--color-fg-bg); box-sizing: border-box; max-width: 600px; margin: 0 auto;">
      <h2 class="mb-6" style="font-family: 'Roboto', sans-serif; font-weight: 600; font-size: 24px; line-height: 32px; color: var(--color-text);">
        We'd love your feedback
      </h2>

      <img
        src={productImage}
        alt="Product"
        class="mx-auto mb-6 rounded-md w-48 h-60 object-cover"
      />

      <label for="feedback" class="block font-semibold mb-2 text-base md:text-lg font-sans" style="color: var(--color-text);">
        Anything you want to share with us?
      </label>
      <textarea
        id="feedback"
        bind:value={feedback}
        placeholder="I really liked..."
        class="w-full border border-gray-300 rounded-md px-4 py-3 text-base focus:outline-none focus:ring-2 min-h-[80px] md:min-h-[100px] font-sans"
        style="color: var(--color-text);"
      ></textarea>
    </main>
  </div>

  <!-- Palette Switcher Dropdown as a floating card below the main card -->
  <div class="mx-auto mt-8 mb-8 shadow rounded-lg p-4 w-full max-w-xs text-center" style="background: var(--color-fg-bg);">
    <label for="palette-select" class="mr-2 font-sans text-base" style="color: var(--color-text);">Theme:</label>
    <select id="palette-select" bind:value={selectedPaletteIdx} class="border rounded px-2 py-1 font-sans" style="color: var(--color-text); background: var(--color-fg-bg);">
      {#each palettes as palette, idx}
        <option value={idx}>{palette.name}</option>
      {/each}
    </select>
  </div>

  <!-- Footer navigation -->
  <div class="footer-bar" style="background: var(--color-fg-bg);">
    <div class="flex justify-between items-center w-full px-8">
      <button class="text-base hover:underline flex items-center gap-1 font-sans" style="color: var(--color-text);">
        ← Previous
      </button>
      <button class="px-8 py-2 rounded-md transition flex items-center gap-1 shadow-sm font-sans text-base font-semibold next-btn" style="background: var(--color-primary); color: {nextButtonTextColor};">
        Next →
      </button>
    </div>
  </div>
</div>

<style>
  .next-btn:hover {
    background: var(--color-secondary) !important;
  }
</style>