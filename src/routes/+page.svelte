<script lang="ts">
  import { onMount } from 'svelte';

  let prompt = '';
  let isGenerating = false;

  let brandName = 'No brand yet';
  let tagline = 'Describe your idea to forge your first brand.';
  let palette = ['#020617', '#0b1220', '#38bdf8', '#e5e7eb', '#f97316'];

  function handleMouseMove(event: MouseEvent) {
    const x = (event.clientX / window.innerWidth) * 100;
    const y = (event.clientY / window.innerHeight) * 100;
    document.documentElement.style.setProperty('--spot-x', `${x}%`);
    document.documentElement.style.setProperty('--spot-y', `${y}%`);
  }

  async function handleGenerate() {
    if (!prompt.trim()) return;
    isGenerating = true;

    await new Promise((r) => setTimeout(r, 1200));

    brandName = 'Obsidian Current';
    tagline = 'High-signal cloud identity, carved in glass and steel.';
    palette = ['#020617', '#020617', '#0ea5e9', '#e2e8f0', '#eab308'];

    isGenerating = false;
  }

  onMount(() => {
    document.addEventListener('mousemove', handleMouseMove);
    return () => document.removeEventListener('mousemove', handleMouseMove);
  });
</script>

<div class="bf-bg-noise">
  <div class="spotlight-layer"></div>

  <main
    class="relative flex min-h-screen flex-col items-center justify-center overflow-hidden bg-slate-950 text-slate-100 px-6 py-10"
  >
    <!-- Molten, floating background glows -->
    <div class="pointer-events-none absolute inset-0 -z-10">
      <div
        class="absolute -left-24 -top-32 h-80 w-80 rounded-full bg-sky-500/18 blur-3xl animate-float-slow"
      ></div>
      <div
        class="absolute -right-10 bottom-0 h-96 w-96 rounded-full bg-slate-300/10 blur-3xl animate-float-slower"
      ></div>
    </div>

    <section class="mx-auto flex w-full max-w-6xl flex-col gap-10 lg:flex-row lg:items-stretch">
      <!-- Left: Hero / prompt -->
      <div
        class="flex flex-1 flex-col justify-between gap-8 rounded-3xl border border-slate-700/60 bg-slate-950/80 p-8 shadow-[0_42px_120px_rgba(2,6,23,0.95)] backdrop-blur-2xl transition-transform duration-500 hover:-translate-y-1"
      >
        <div class="space-y-6">
          <div
            class="inline-flex items-center gap-2 rounded-full border border-slate-600/80 bg-slate-900/80 px-3 py-1 text-[11px] uppercase tracking-[0.16em] text-slate-300"
          >
            <span class="h-1.5 w-1.5 animate-pulse rounded-full bg-emerald-400 shadow-[0_0_12px_rgba(52,211,153,0.9)]"></span>
            <span>Live · BrandForge by SkyCloud</span>
          </div>

          <div class="space-y-3">
            <h1 class="text-4xl font-semibold tracking-tight sm:text-5xl">
              Forge a
              <span class="bg-gradient-to-r from-slate-50 via-sky-200 to-slate-200 bg-clip-text text-transparent">
                cinematic brand
              </span>
              <br />
              from a single prompt.
            </h1>
            <p class="max-w-xl text-sm text-slate-400 sm:text-base">
              Type what you&apos;re building. BrandForge sculpts a full identity — name, tagline, palette and a live
              micro-site — in seconds. No templates. No noise. Just premium signal.
            </p>
          </div>

          <div class="space-y-4">
            <label class="text-[11px] font-semibold uppercase tracking-[0.22em] text-slate-500">
              Your idea
            </label>

            <!-- Molten, frosted prompt card -->
            <div
              class="group relative overflow-hidden rounded-2xl border border-slate-600/80 bg-gradient-to-br from-slate-950/95 via-slate-950/80 to-slate-900/80 shadow-[0_28px_80px_rgba(2,6,23,1)]"
            >
              <div
                class="pointer-events-none absolute inset-px rounded-[1.05rem] border border-white/5 bg-gradient-to-b from-white/8 via-transparent to-transparent opacity-70"
              ></div>

              <div class="relative flex flex-col gap-3 p-4 sm:p-5">
                <textarea
                  bind:value={prompt}
                  rows="3"
                  placeholder="Example: A minimalist cloud consultancy helping small businesses modernize without the enterprise drama."
                  class="w-full resize-none border-0 bg-transparent text-sm text-slate-100 placeholder:text-slate-500 focus:outline-none focus:ring-0"
                ></textarea>

                <div class="flex flex-col gap-3 sm:flex-row sm:items-center sm:justify-between">
                  <p class="max-w-xs text-[11px] text-slate-500">
                    Tip: include your audience, vibe, and what you&apos;re selling. BrandForge handles the rest.
                  </p>

                  <button
                    class="inline-flex items-center justify-center gap-2 rounded-xl border border-sky-400/60 bg-gradient-to-r from-slate-50 via-slate-100 to-slate-300 px-4 py-2 text-sm font-medium text-slate-900 shadow-[0_0_36px_rgba(148,163,184,0.7)] transition-transform duration-150 hover:-translate-y-[1px] hover:shadow-[0_0_48px_rgba(148,163,184,0.9)] disabled:cursor-not-allowed disabled:border-slate-700 disabled:bg-slate-700 disabled:text-slate-300 disabled:shadow-none"
                    on:click|preventDefault={handleGenerate}
                    disabled={isGenerating}
                  >
                    {#if isGenerating}
                      <span
                        class="h-3 w-3 animate-spin rounded-full border-[2px] border-slate-900 border-b-transparent"
                      ></span>
                      Forging…
                    {:else}
                      <span>Forge my brand</span>
                    {/if}
                  </button>
                </div>
              </div>
            </div>
          </div>

          <div class="flex flex-wrap gap-3 text-xs text-slate-400">
            <span class="rounded-full border border-slate-600 bg-slate-900/80 px-3 py-1">Instant brand kit</span>
            <span class="rounded-full border border-slate-600 bg-slate-900/80 px-3 py-1">AI-crafted micro-site</span>
            <span class="rounded-full border border-slate-600 bg-slate-900/80 px-3 py-1">Dark embossed aesthetic</span>
          </div>
        </div>

        <div class="flex items-center justify-between text-[11px] text-slate-500">
          <span>Modern cloud infrastructure, without the noise.</span>
          <span class="text-slate-400">Powered by SkyCloud Solutions</span>
        </div>
      </div>

      <!-- Right: Preview card -->
      <div
        class="flex flex-1 flex-col gap-5 rounded-3xl border border-slate-700/70 bg-slate-950/80 p-6 shadow-[0_42px_120px_rgba(2,6,23,1)] backdrop-blur-2xl transition-transform duration-500 hover:-translate-y-1"
      >
        <header class="flex items-center justify-between gap-3">
          <div class="flex items-center gap-3">
            <div
              class="flex h-10 w-10 items-center justify-center rounded-xl border border-slate-600 bg-gradient-to-br from-slate-950 to-slate-800 shadow-inner"
            >
              <span class="text-lg font-semibold tracking-tight text-slate-100">BF</span>
            </div>
            <div>
              <p class="text-[11px] uppercase tracking-[0.24em] text-slate-500">Preview</p>
              <p class="text-sm font-medium text-slate-100">BrandForge Output</p>
            </div>
          </div>

          <div
            class="inline-flex items-center gap-2 rounded-full border border-emerald-500/40 bg-emerald-500/10 px-3 py-1 text-[11px] text-emerald-200"
          >
            <span class="h-1.5 w-1.5 rounded-full bg-emerald-400"></span>
            <span>Instant · Not yet saved</span>
          </div>
        </header>

        <div
          class="relative flex flex-1 flex-col gap-4 overflow-hidden rounded-2xl border border-slate-700/80 bg-gradient-to-b from-slate-900/95 via-slate-950/95 to-black/95 p-5"
        >
          <div
            class="pointer-events-none absolute inset-x-10 -top-10 h-40 rounded-full bg-gradient-to-b from-white/10 via-transparent to-transparent blur-3xl opacity-70"
          ></div>

          <div class="relative space-y-2">
            <h2 class="text-xl font-semibold tracking-tight text-slate-50">
              {brandName}
            </h2>
            <p class="text-xs text-slate-400">
              {tagline}
            </p>
          </div>

          <div class="relative mt-4 grid gap-3 md:grid-cols-[2fr,3fr]">
            <div class="space-y-3">
              <p class="text-[11px] font-semibold uppercase tracking-[0.22em] text-slate-500">
                Palette
              </p>
              <div class="flex gap-2">
                {#each palette as color}
                  <div class="flex flex-1 flex-col items-center gap-1">
                    <div
                      class="h-10 w-full rounded-lg border border-slate-700/80"
                      style={`background: ${color};`}
                    ></div>
                    <span class="text-[10px] text-slate-500">{color}</span>
                  </div>
                {/each}
              </div>
            </div>

            <div class="space-y-3">
              <p class="text-[11px] font-semibold uppercase tracking-[0.22em] text-slate-500">
                Hero snapshot
              </p>
              <div
                class="relative h-28 overflow-hidden rounded-xl border border-slate-700/80 bg-gradient-to-br from-slate-950 via-slate-900 to-slate-950"
              >
                <div class="absolute inset-0 opacity-70">
                  <div class="absolute -left-10 top-4 h-32 w-32 rounded-full bg-sky-500/30 blur-3xl"></div>
                  <div class="absolute -right-8 bottom-2 h-28 w-28 rounded-full bg-slate-200/15 blur-3xl"></div>
                </div>
                <div class="relative flex h-full flex-col justify-between p-3 text-[11px] text-slate-100">
                  <div>
                    <div
                      class="inline-flex items-center gap-1 rounded-full bg-black/60 px-2 py-0.5 text-[9px] text-slate-200"
                    >
                      • Live micro-site
                    </div>
                    <p class="mt-2 text-[11px] font-medium text-slate-100">
                      Obsidian-dark hero, glassy CTAs, ready to deploy.
                    </p>
                  </div>
                  <div class="flex items-center justify-between text-[10px] text-slate-400">
                    <span>CTA: Get started</span>
                    <span>Layout: Focused, minimal</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="relative mt-2 flex flex-wrap items-center justify-between gap-3 text-[11px]">
            <div class="flex flex-wrap gap-2">
              <span class="rounded-full border border-slate-700 bg-black/70 px-2.5 py-1 text-slate-400">
                Generated kit · v0
              </span>
              <span class="rounded-full border border-slate-700 bg-black/70 px-2.5 py-1 text-slate-400">
                Downloadable assets · Coming soon
              </span>
            </div>
            <button
              class="rounded-full border border-slate-700 bg-black/70 px-3 py-1 text-[11px] text-slate-300 hover:border-sky-400 hover:text-sky-200 transition-colors"
              disabled
            >
              Publish micro-site · Soon
            </button>
          </div>
        </div>
      </div>
    </section>
  </main>
</div>
