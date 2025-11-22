<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>Terms & Conditions | AxelBase File Hash Calculator</title>
  <meta name="description" content="Terms of use for the free, open-source, client-side File Hash Calculator by AxelBase." />
  <meta property="og:title" content="Terms & Conditions | AxelBase" />
  <meta property="og:description" content="Free to use, modify, and deploy. No warranty, no liability — pure open-source freedom." />
  <meta property="og:url" content="{base}/terms" />
  <meta property="og:type" content="website" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout">
  <div class="breadcrumbs">
    <a href="{base}/">Home</a> <span>/</span> <p>Terms & Conditions</p>
  </div>

  <article class="prose">
    <h1>Terms & Conditions</h1>
    <p class="post-meta">Last Updated: November 22, 2025</p>

    <p>By using <strong>AxelBase File Hash Calculator</strong> ("the Tool"), you agree to these Terms. The Tool is a free, open-source, client-side web application provided "as is" for computing cryptographic hashes.</p>

    <h2>1. Use of the Tool</h2>
    <p>You may use the Tool for any lawful purpose, including personal, educational, and commercial use. There are no rate limits, accounts, or paywalls.</p>

    <h2>2. No Warranty</h2>
    <p>The Tool is provided **with no warranty of any kind**, express or implied. While we strive for accuracy, we do not guarantee that hashes produced will always be correct or that the Tool will be error-free. Use at your own risk.</p>

    <h2>3. No Liability</h2>
    <p>In no event shall AxelBase, its creators, or contributors be liable for any damages arising from:</p>
    <ul>
      <li>Incorrect hash results</li>
      <li>Loss of data</li>
      <li>Security incidents</li>
      <li>Use in critical systems</li>
    </ul>
    <p><em>Cryptographic verification is your responsibility.</em></p>

    <h2>4. Open Source License</h2>
    <p>The source code is licensed under the **MIT License**. You are free to:</p>
    <ul>
      <li>Use it commercially</li>
      <li>Modify and redistribute</li>
      <li>Fork and deploy your own version</li>
      <li>Remove or replace branding</li>
    </ul>
    <p>See the GitHub repository for full license text.</p>

    <h2>5. Modifications & Forks</h2>
    <p>You may create and host modified versions. We encourage it! If you redistribute, please keep a link to the original project where reasonable.</p>

    <h2>6. Prohibited Use</h2>
    <p>You may not:</p>
    <ul>
      <li>Use the Tool for illegal purposes</li>
      <li>Misrepresent it as an official endorsement</li>
      <li>Imply that we collect user data (we don’t)</li>
    </ul>

    <h2>7. Changes to Terms</h2>
    <p>We may update these terms. Continued use after changes constitutes acceptance.</p>

    <p class="italic-note"><strong>Freedom, privacy, and open source.</strong> That’s what AxelBase stands for — now and always.</p>
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
  .italic-note { font-style: italic; text-align: center; margin-top: 3rem; color: var(--bs-secondary-color); font-size: 1.1rem; }
</style>