<script lang="ts">
  import { onMount } from 'svelte';
  import logo1 from '$lib/images/logo1@2x.png';
  import logo2 from '$lib/images/logo2@2x.png';
  import logo3 from '$lib/images/strideUXLogo-mark@2x.png';
  import productImage from '$lib/images/prod-image@2x.png';
  import { readableColor } from 'polished';
  let feedback = '';

  // Survey theme palettes
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
      title: 'Lorem ipsum dolor',
    },
    {
      name: 'Example 3',
      primary: '#00F0FF',
      secondary: '#00ACB7',
      bg: '#000000',
      fgBg: '#2D2F35',
      text: '#FFFFFF',
      logo: logo3,
      title: 'Lorem ipsum dolor',
    },
  ];

  let selectedPaletteIdx = 0;

  // Helper: update CSS variables for palette
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

  // Set initial palette on mount
  onMount(() => {
    applyPalette(palettes[selectedPaletteIdx]);
  });

  // Reactively update palette on change
  $: if (typeof document !== 'undefined') {
    applyPalette(palettes[selectedPaletteIdx]);
  }

  // Compute accessible text color for the Next button
  $: nextButtonTextColor = readableColor(palettes[selectedPaletteIdx].primary);
</script>

<svelte:head>
  <title>Mountain Trek Mix Taste Test Survey</title>
</svelte:head>

<!-- Root container with theme background -->
<div id="palette-root" class="min-h-screen flex flex-col w-full bg-[var(--color-bg)]">
  <!-- Sticky header and progress bar -->
  <div class="sticky top-0 z-10 bg-[var(--color-fg-bg)]">
    <header class="w-full flex items-center justify-between px-6 py-3 shadow-sm bg-[var(--color-fg-bg)]">
      <div class="flex items-center gap-2 md:gap-3"> 
        <img src={palettes[selectedPaletteIdx].logo} alt="Logo" class="h-10 w-auto" />
        <h1 class="text-base font-medium leading-6 ml-2 font-roboto text-[16px] text-[var(--color-text)]">
          {palettes[selectedPaletteIdx].title}
        </h1>
      </div>
      <span class="text-base leading-6 font-roboto font-normal text-[14px] text-[var(--color-text)]">2 of 3</span>
    </header>
    <!-- Progress Bar -->
    <div class="w-full h-1 bg-[rgba(23,137,200,0.3)]">
      <div class="h-full" style="width:66.666vw; max-width:100vw; background-color: var(--color-primary);"></div>
    </div>
  </div>

  <!-- Main content card -->
  <div class="px-4 mt-4">
    <main class="shadow-lg rounded-xl p-4 sm:p-8 md:p-12 text-center bg-[var(--color-fg-bg)] box-border max-w-xl mx-auto">
      <h2 class="mb-6 font-roboto font-semibold text-2xl leading-8 text-[var(--color-text)]">
        We'd love your feedback
      </h2>

      <img
        src={productImage}
        alt="Product"
        class="mx-auto mb-6 rounded-md w-48 h-60 object-cover"
      />

      <label for="feedback" class="block font-semibold mb-2 text-base md:text-lg font-sans text-[var(--color-text)]">
        Anything you want to share with us?
      </label>
      <textarea
        id="feedback"
        bind:value={feedback}
        placeholder="I really liked..."
        class="w-full border border-gray-300 rounded-md px-4 py-3 text-base focus:outline-none focus:ring-2 min-h-[80px] md:min-h-[100px] font-sans text-[var(--color-text)] bg-transparent"
      ></textarea>
    </main>
  </div>

  <!-- Palette Switcher Dropdown -->
  <div class="mx-auto mt-8 mb-20 shadow rounded-lg p-4 w-full max-w-xs text-center bg-[var(--color-fg-bg)]">
    <label for="palette-select" class="mr-2 font-sans text-base text-[var(--color-text)]">Theme:</label>
    <select id="palette-select" bind:value={selectedPaletteIdx} class="border rounded px-2 py-1 font-sans text-[var(--color-text)] bg-[var(--color-fg-bg)]">
      {#each palettes as palette, idx}
        <option value={idx}>{palette.name}</option>
      {/each}
    </select>
  </div>

  <!-- Footer navigation -->
  <div class="bg-[var(--color-fg-bg)]">
    <div class="flex justify-between items-center w-full px-4">
      <button class="text-base hover:underline flex items-center gap-1 font-sans text-[var(--color-text)]">
        ← Previous
      </button>
      <button class="px-8 py-2 rounded-md transition flex items-center gap-1 shadow-sm font-sans text-base font-semibold next-btn" style="background: var(--color-primary); color: {nextButtonTextColor};">
        Next →
      </button>
    </div>
  </div>
</div>

<style>
  /* Next button hover uses palette secondary color */
  .next-btn:hover {
    background: var(--color-secondary) !important;
  }
</style>