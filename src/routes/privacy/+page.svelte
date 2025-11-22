<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>Privacy Policy | AxelBase File Hash Calculator</title>
  <meta name="description" content="We collect zero data. Your files never leave your device. 100% client-side hashing with full privacy guaranteed." />
  <meta property="og:title" content="Privacy Policy | AxelBase File Hash Calculator" />
  <meta property="og:description" content="No logs, no tracking, no uploads. Your files and hashes stay on your device — always." />
  <meta property="og:url" content="{base}/privacy" />
  <meta property="og:type" content="website" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout">
  <div class="breadcrumbs">
    <a href="{base}/">Home</a> <span>/</span> <p>Privacy Policy</p>
  </div>

  <article class="prose">
    <h1>Privacy Policy</h1>
    <p class="post-meta">Effective Date: November 22, 2025</p>

    <p>Welcome to <strong>AxelBase File Hash Calculator</strong> — a completely client-side web tool that computes SHA-256 and MD5 hashes directly in your browser. We take your privacy extremely seriously, which is why we designed this tool with one core principle: <strong>your files never leave your device</strong>.</p>

    <h2>We Collect Absolutely Nothing</h2>
    <p>Because all hashing happens locally using the Web Crypto API:</p>
    <ul>
      <li><strong>No files are uploaded</strong> — ever</li>
      <li><strong>No IP addresses are logged</strong></li>
      <li><strong>No usage analytics</strong> — we don’t use Google Analytics, Plausible, or any tracking</li>
      <li><strong>No cookies, localStorage, or fingerprints</strong></li>
      <li><strong>No server-side processing</strong> at all</li>
    </ul>

    <p>When you close the tab, everything disappears. We have no way — and no desire — to see what files you hash.</p>

    <h2>How It Actually Works</h2>
    <p>Your browser reads your file in secure chunks, feeds them directly into the built-in cryptographic engine, and displays the result. Nothing is sent over the internet. Even if you're completely offline after the first load, the tool works perfectly.</p>

    <h2>Third-Party Services</h2>
    <p>We do not use any external analytics, advertising, or CDN-tracked scripts. The only external resource is an optional favicon. All code runs from your device or trusted static hosting (GitHub Pages, Vercel, etc.) with no telemetry.</p>

    <h2>Your Responsibility</h2>
    <p>While we guarantee no data leaves your browser, you remain responsible for:</p>
    <ul>
      <li>Using the tool on a secure, updated device and browser</li>
      <li>Not sharing screenshots containing sensitive hashes</li>
      <li>Verifying you're on the official domain</li>
    </ul>

    <h2>Children’s Privacy</h2>
    <p>This tool is safe for all ages and collects no data from anyone, including children under 13.</p>

    <h2>Changes to This Policy</h2>
    <p>We may update this policy if we add new features. You’ll always find the latest version here.</p>

    <p class="italic-note"><strong>Your privacy is not a feature — it’s the entire product.</strong> Thank you for trusting AxelBase.</p>
  </article>
</div>

<style>
  .post-layout { max-width: 800px; padding: 2rem 0 4rem; }
  .breadcrumbs { display: flex; align-items: center; gap: .5rem; margin-bottom: 1.5rem; font-size: .9rem; color: var(--bs-secondary-color); }
  .breadcrumbs a { color: var(--bs-primary); text-decoration: none; }
  .breadcrumbs a:hover { text-decoration: underline; }
  .prose { line-height: 1.8; }
  .post-meta { color: var(--bs-secondary-color); font-size: .9rem; margin-bottom: 2rem; padding-bottom: 1rem; border-bottom: 1px solid var(--bs-border-color); }
  .prose h1 { font-size: 2.5rem; color: var(--bs-emphasis-color); margin-bottom: .5rem; }
  .prose h2 { margin-top: 2.5rem; color: var(--bs-primary); }
  .prose ul { padding-left: 1.5rem; }
  .prose ul li { margin-bottom: .5rem; }
  .prose ul li::marker { color: var(--bs-primary); }
  .italic-note { font-style: italic; text-align: center; margin-top: 3rem; color: var(--bs-secondary-color); font-size: 1.1rem; }
</style>