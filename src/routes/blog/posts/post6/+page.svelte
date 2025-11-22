<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>Works Offline — Forever | AxelBase Blog</title>
  <meta name="description" content="Once loaded, AxelBase File Hash Calculator works completely offline. No internet needed — ever." />
  <meta property="og:title" content="Works Offline — Forever" />
  <meta property="og:description" content="Bookmark it, save it, use it on planes, ships, or air-gapped systems. True offline capability." />
  <meta property="og:url" content="{base}/blog/posts/post6" />
  <meta property="og:type" content="article" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout">
  <div class="breadcrumbs">
    <a href="{base}/blog">Blog</a> <span>/</span> <p>Works Offline — Forever</p>
  </div>

  <article class="prose">
    <h1>Works Offline — Forever</h1>
    <p class="post-meta">Published: November 27, 2025</p>

    <p>One of the most powerful features of AxelBase is simple: <strong>once you’ve opened it once, it works forever — with or without internet</strong>.</p>

    <h2>How True Offline Mode Works</h2>
    <p>AxelBase is a 100% static SvelteKit app. After the first visit:</p>
    <ul>
      <li>All JavaScript, CSS, and HTML are cached</li>
      <li>Your browser can serve the entire tool from disk</li>
      <li>No network requests are made on reload</li>
    </ul>

    <h2>Real Offline Use Cases</h2>
    <ul>
      <li>Verify files on an air-gapped workstation</li>
      <li>Check hashes during travel (plane, train, ship)</li>
      <li>Audit files in secure facilities</li>
      <li>Use in areas with poor connectivity</li>
    </ul>

    <h2>How to Make It Permanent</h2>
    <p>Click “Add to Home Screen” (mobile) or “Install” (desktop Chrome/Edge) → it becomes a standalone app with its own window and icon.</p>

    <p>Or simply bookmark it and disable internet — it will still work perfectly.</p>

    <p class="italic-note">Your tools should work anywhere. AxelBase does.</p>
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