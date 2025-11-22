<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>Deploy Your Own Version in 60 Seconds | AxelBase</title>
  <meta name="description" content="Fork and deploy your own branded version of AxelBase File Hash Calculator on GitHub Pages — completely free and in under a minute." />
  <meta property="og:title" content="Deploy Your Own Version in 60 Seconds" />
  <meta property="og:description" content="Make it yours: custom name, logo, colors, domain — all with zero cost or setup." />
  <meta property="og:url" content="{base}/blog/posts/post7" />
  <meta property="og:type" content="article" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout">
  <div class="breadcrumbs">
    <a href="{base}/blog">Blog</a> <span>/</span> <p>Deploy Your Own Version in 60 Seconds</p>
  </div>

  <article class="prose">
    <h1>Deploy Your Own Version in 60 Seconds</h1>
    <p class="post-meta">Published: November 28, 2025</p>

    <p>Want your own branded file hash tool? With your name, logo, and domain? You can have it live in under a minute — completely free.</p>

    <h2>One-Click Deploy Options</h2>
    <ul>
      <li><strong>GitHub Pages</strong> → Click “Use this template” → Enable Pages → Done</li>
      <li><strong>Vercel / Netlify / Cloudflare Pages</strong> → Connect repo → Auto-deploy</li>
    </ul>

    <h2>Make It Yours</h2>
    <ul>
      <li>Change the title in <code>+page.svelte</code></li>
      <li>Replace <code>AxelLab-Logo.ico</code> with your favicon</li>
      <li>Update colors in CSS variables</li>
      <li>Host on your own domain (e.g. hash.yourcompany.com)</li>
    </ul>

    <h2>Perfect For</h2>
    <ul>
      <li>Companies providing internal tools</li>
      <li>Security teams</li>
      <li>Open-source projects</li>
      <li>Personal branding</li>
    </ul>

    <p>Repository: <a href="https://github.com/axelbase/file-hash-calculator" target="_blank">github.com/axelbase/file-hash-calculator</a></p>

    <p class="italic-note">Your tool. Your brand. Zero cost. Live in 60 seconds.</p>
  </article>
</div>

<style>
  .post-layout { max-width: 800px; padding: 2rem 0 4rem; }
  .breadcrumbs { display: flex; align-items: center; gap: .5rem; margin-bottom: 1.5rem; font-size: .9rem; color: var(--bs-secondary-color); }
  .breadcrumbs a { color: var(--bs-primary); text-decoration: none; }
  .breadcrumbs a:hover { text-decoration: underline; }
  .prose { line-height: 1.8; }
  .post-meta { color: var(--bs-secondary-color); font-size: .9rem; margin-bottom: 2rem; padding-bottom: 1rem; border-bottom: 1px solid var(--bs-border-color); }
  .prose h1 { font-size: 2.5rem; color: var(--bs-emphasis-color); }
  .prose h2 { margin-top: 2.5rem; color: var(--bs-primary); }
  .italic-note { font-style: italic; text-align: center; margin-top: 3rem; color: var(--bs-secondary-color); }
</style>