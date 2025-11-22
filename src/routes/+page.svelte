<script>
  import { calculateHash } from '$lib/hash.js';
  import { formatBytes, normalizeHash } from '$lib/utils.js';
  import { base } from '$app/paths';
  import "../app.css"; /* Import CSS here is crucial if it was missing */
  // ... rest of the script is unchanged ...
  let file = null;
  let text = '';
  let algorithm = 'SHA-256';
  let hash = '';
  let expected = '';
  let status = '';
  let fileInfo = '';
  let progress = 0;
  let isProcessing = false;

  // This reactive statement triggers compute() whenever anything changes
  $: file, text, algorithm, compute();

  async function compute() {
    const input = file || text;

    // Reset if nothing to hash
    if (!input || (typeof input === 'string' && input.trim() === '')) {
      hash = '';
      status = '';
      fileInfo = '';
      progress = 0;
      return;
    }

    isProcessing = true;
    hash = '';
    status = 'Computing...';
    progress = 0;

    try {
      const result = await calculateHash(
        input,
        algorithm,
        file
          ? (done, total) => {
              progress = Math.round((done / total) * 100);
            }
          : null
      );

      hash = result;
      fileInfo = file ? `${file.name} • ${formatBytes(file.size)}` : '';
      status = '';
    } catch (err) {
      console.error(err);
      hash = 'Error';
      status = 'Failed to compute hash';
    } finally {
      isProcessing = false;
    }
  }

  function clearFile() {
    file = null;
  }

  function clearText() {
    text = '';
  }

  function handleDrop(e) {
    e.preventDefault();
    const droppedFile = e.dataTransfer?.files[0];
    if (droppedFile) {
      file = droppedFile;
      text = ''; // clear text when file is dropped
    }
  }

  function copyHash() {
    navigator.clipboard.writeText(hash);
    status = 'Copied!';
    setTimeout(() => (status = ''), 1500);
  }

  $: matchStatus =
    expected && hash && normalizeHash(expected) === hash
      ? 'match'
      : expected && hash
      ? 'mismatch'
      : '';
</script>

<svelte:head>
  <title>AxelBase – File Hash Calculator</title>
  <link rel="icon" href="{base}/AxelLab-Logo.ico" />
</svelte:head>

<main class="container py-5">
  <div class="row justify-content-center">
    <div class="col-lg-8">
      <h1 class="text-center mb-5 fw-bold" style="color: var(--primary-color);">AxelBase – File Hash Calculator</h1>

      <div class="card shadow">
        <div class="card-body p-4 p-md-5">

          <div class="mb-4">
            <label for="file-input" class="form-label fw-bold">1. Select File (Drag & Drop Supported)</label>
            <div
              role="button"
              tabindex="0"
              aria-labelledby="dropzone-label"
              class="border border-2 border-dashed rounded-3 p-5 text-center user-select-none position-relative"
              class:border-primary={!!file}
              on:click={() => document.getElementById('file-input')?.click()}
              on:drop|preventDefault={handleDrop}
              on:dragover|preventDefault
              on:dragleave|preventDefault
              on:keydown={(e) => (e.key === 'Enter' || e.key === ' ') && (e.preventDefault(), document.getElementById('file-input')?.click())}
            >
              <input
                id="file-input"
                type="file"
                class="d-none"
                on:change={(e) => (file = e.target.files[0] || null)}
              />

              {#if file}
                <div class="text-success fw-bold mb-2">
                  <span class="badge bg-success-subtle text-success p-2 rounded-pill">{file.name} • {formatBytes(file.size)}</span>
                  <button
                    type="button"
                    class="btn btn-sm btn-outline-danger ms-3"
                    on:click|stopPropagation={clearFile}
                    aria-label="Remove file"
                  >Remove</button>
                </div>
              {:else}
                <p id="dropzone-label" class="mb-2 fw-medium">
                  Click to select a file<br>or **drag and drop** here
                </p>
                <p class="text-muted small">Any file size • 100% client-side</p>
              {/if}
            </div>
          </div>

          <div class="mb-4">
            <label for="text-input" class="form-label fw-bold">2. Or enter text to hash:</label>
            <div class="position-relative">
              <textarea
                id="text-input"
                class="form-control pe-5"
                rows="4"
                bind:value={text}
                placeholder="Paste text here..."
                on:input={() => file = null}
              ></textarea>
              {#if text}
                <button
                  type="button"
                  class="btn btn-sm btn-outline-secondary position-absolute top-0 end-0 mt-2 me-2"
                  style="z-index:10"
                  on:click={clearText}
                  aria-label="Clear text"
                >Clear</button>
              {/if}
            </div>
          </div>

          <fieldset class="mb-4">
            <legend class="form-label fw-bold">3. Select Algorithm:</legend>
            <div class="d-flex gap-4 flex-wrap">
              <div class="form-check form-check-inline">
                <input class="form-check-input" type="radio" id="sha256" value="SHA-256" bind:group={algorithm} />
                <label class="form-check-label fw-medium" for="sha256">SHA-256 (recommended)</label>
              </div>
              <div class="form-check form-check-inline">
                <input class="form-check-input" type="radio" id="md5" value="MD5" bind:group={algorithm} />
                <label class="form-check-label fw-medium" for="md5">MD5</label>
              </div>
            </div>
          </fieldset>

          {#if isProcessing && file}
            <div class="progress mb-3" role="progressbar" aria-valuenow={progress} aria-valuemin="0" aria-valuemax="100">
              <div class="progress-bar progress-bar-striped progress-bar-animated" style="width:{progress}%">
                {progress}%
              </div>
            </div>
          {/if}

          {#if hash}
            <div class="mb-3">
              <label for="hash-output" class="form-label fw-bold">4. Result Hash ({algorithm}):</label>
              <div class="input-group">
                <input id="hash-output" type="text" class="form-control" value={hash} readonly />
                <button class="btn btn-outline-secondary" type="button" on:click={copyHash}>Copy</button>
              </div>
            </div>

            <div class="mb-3">
              <label for="expected-hash" class="form-label fw-bold">5. Expected Hash (Verification):</label>
              <input
                id="expected-hash"
                type="text"
                class="form-control {matchStatus === 'match' ? 'hash-match' : matchStatus === 'mismatch' ? 'hash-mismatch' : ''}"
                placeholder="Paste expected hash to compare..."
                bind:value={expected}
                aria-describedby={matchStatus ? 'match-feedback' : null}
              />
              {#if matchStatus}
                <div id="match-feedback" class="mt-2 fw-bold {matchStatus === 'match' ? 'text-success' : 'text-danger'}">
                  {matchStatus === 'match' ? 'Match!' : 'No match'}
                </div>
              {/if}
            </div>
          {/if}

          {#if status && status !== 'Copied!'}
            <div class="text-center text-muted mt-3 fw-medium">{status}</div>
          {/if}

        </div>
      </div>
      
      <div class="text-center mt-5 text-muted small">
        AxelBase – 100% client-side • No data sent • Works offline
      </div>
      
      <section id="about" class="py-5 mt-5 bg-light rounded-4">
        <div class="container">
          <h2 class="text-center mb-4 display-5 fw-bold" style="color: var(--primary-color);">About AxelBase File Hash Calculator</h2>
          <p class="lead text-center mb-5">The fastest, most private way to verify file integrity — 100% in your browser, zero data ever leaves your device.</p>

          <div class="row g-5">
            <div class="col-lg-10 mx-auto">
              <p>AxelBase File Hash Calculator was born from a simple but critical need: **verify downloaded files, backups, and software without compromising privacy**. Most online hash tools require you to upload your file — even if it’s a confidential document, private key backup, or multi-gigabyte ISO. That’s unacceptable.</p>

              <p>That’s why AxelBase runs **entirely client-side** using the native Web Crypto API — the same secure technology used by password managers and cryptocurrency wallets. From the moment you load the page, every byte is processed locally. No servers. No logs. No uploads. No tracking. Nothing.</p>

              <p>Whether you're a developer verifying a Linux ISO, a security professional checking firmware, or a regular user confirming a backup hasn’t been corrupted, AxelBase gives you instant, trustworthy results with **absolute privacy**.</p>

              <h3 class="h4 mt-5">Why This Matters</h3>
              <p>In 2025, data breaches and tracking are everywhere. Traditional hash checkers — even from reputable sites — often log IP addresses, store files temporarily, or use third-party analytics. AxelBase rejects that model completely. We believe *your files should stay yours*.</p>

              <p>Built with SvelteKit and deployed as a fully static site, AxelBase works offline after the first visit, supports files of any size with live progress, and produces accurate SHA-256 and MD5 hashes instantly. It’s open source (MIT licensed), fully auditable, and can be self-hosted in seconds.</p>

              <p>From privacy advocates to enterprise teams, thousands already trust AxelBase because it delivers what others only promise: **true zero-knowledge file verification**.</p>

              <p class="text-center mt-5">
                <strong>No data collected. No trust required. Just pure, fast, secure hashing.</strong>
              </p>
            </div>
          </div>
        </div>
      </section>

      <section id="how-to-use" class="py-5 mt-5">
        <div class="container">
          <h2 class="text-center mb-5 display-5 fw-bold" style="color: var(--primary-color);">How to Use AxelBase</h2>

          <div class="row justify-content-center">
            <div class="col-lg-8">
              <ol class="list-group list-group-numbered fs-5 shadow" style="border-radius: 15px;">
                <li class="list-group-item py-4">
                  <strong>Drag & Drop or Select a File</strong><br>
                  Simply drag any file onto the dashed zone or click to browse. You can also paste text directly if you’re verifying a string (e.g., a GPG signature or API token).
                </li>
                <li class="list-group-item py-4">
                  <strong>Choose Your Algorithm</strong><br>
                  Select **SHA-256** (recommended — modern, secure) or **MD5** (only for legacy compatibility). The hash updates instantly when you switch.
                </li>
                <li class="list-group-item py-4">
                  <strong>Watch the Magic Happen</strong><br>
                  For small files: instant result. For large files (even 20+ GB): a smooth progress bar shows real-time status. No freezing. No crashes.
                </li>
                <li class="list-group-item py-4">
                  <strong>Verify with Confidence</strong><br>
                  paste the official expected hash into the “Expected hash” field. Get instant visual feedback: <span class="text-success fw-bold">Match!</span> or <span class="text-danger fw-bold">No match</span>.
                </li>
                <li class="list-group-item py-4">
                  <strong>Copy & Go</strong><br>
                  Click “Copy” to grab the hash. Done. Your file was never uploaded, never logged, never seen by anyone.
                </li>
              </ol>

              <div class="text-center mt-5">
                <p class="fs-4 text-muted">Works offline • No installation • Supports multi-gigabyte files • 100% private</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section id="faq" class="py-5 mt-5 bg-light rounded-4">
        <div class="container">
          <h2 class="text-center mb-5 display-5 fw-bold" style="color: var(--primary-color);">Frequently Asked Questions</h2>

          <div class="accordion mx-auto" id="faqAccordion" style="max-width: 800px;">
            <div class="accordion-item">
              <h2 class="accordion-header">
                <button class="accordion-button collapsed fs-5 fw-semibold" type="button" data-bs-toggle="collapse" data-bs-target="#q1">
                  Is my file really never uploaded?
                </button>
              </h2>
              <div id="q1" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
                <div class="accordion-body">
                  **Yes — 100% guaranteed.** Open DevTools → Network tab → select a 5 GB file. You’ll see zero outgoing requests. All processing uses the browser’s built-in Web Crypto API. Your file never leaves your computer.
                </div>
              </div>
            </div>

            <div class="accordion-item">
              <h2 class="accordion-header">
                <button class="accordion-button collapsed fs-5 fw-semibold" type="button" data-bs-toggle="collapse" data-bs-target="#q2">
                  Why should I use SHA-256 instead of MD5?
                </button>
              </h2>
              <div id="q2" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
                <div class="accordion-body">
                  MD5 is cryptographically broken (collisions possible since 2004). SHA-256 is the current industry standard used by Linux distros, Microsoft, GitHub, Bitcoin, and TLS certificates. **Always prefer SHA-256 unless matching a legacy MD5 checksum.**
                </div>
              </div>
            </div>

            <div class="accordion-item">
              <h2 class="accordion-header">
                <button class="accordion-button collapsed fs-5 fw-semibold" type="button" data-bs-toggle="collapse" data-bs-target="#q3">
                  Can it handle really large files?
                </button>
              </h2>
              <div id="q3" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
                <div class="accordion-body">
                  Yes — even 50+ GB files. We use streaming chunked reading (10–50 MB at a time), so memory usage stays low and progress is smooth. Tested successfully with Windows ISOs, Linux distros, and full disk backups.
                </div>
              </div>
            </div>

            <div class="accordion-item">
              <h2 class="accordion-header">
                <button class="accordion-button collapsed fs-5 fw-semibold" type="button" data-bs-toggle="collapse" data-bs-target="#q4">
                  Does it work offline?
                </button>
              </h2>
              <div id="q4" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
                <div class="accordion-body">
                  Absolutely. After the first visit, your browser caches everything. Bookmark it, disconnect from the internet — it still works perfectly. Ideal for air-gapped systems or travel.
                </div>
              </div>
            </div>

            <div class="accordion-item">
              <h2 class="accordion-header">
                <button class="accordion-button collapsed fs-5 fw-semibold" type="button" data-bs-toggle="collapse" data-bs-target="#q5">
                  Is it open source? Can I host my own version?
                </button>
              </h2>
              <div id="q5" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
                <div class="accordion-body">
                  Yes! Licensed under MIT. Fork it, brand it, deploy on your domain in under 60 seconds via GitHub Pages, Vercel, Netlify, or Cloudflare Pages. Perfect for companies wanting an internal tool.
                </div>
              </div>
            </div>

            <div class="accordion-item">
              <h2 class="accordion-header">
                <button class="accordion-button collapsed fs-5 fw-semibold" type="button" data-bs-toggle="collapse" data-bs-target="#q6">
                  Is there any tracking or analytics?
                </button>
              </h2>
              <div id="q6" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
                <div class="accordion-body">
                  **None whatsoever.** No Google Analytics, no Plausible, no cookies, no fingerprinting. We don’t want your data — because we believe privacy is a right, not a feature.
                </div>
              </div>
            </div>
          </div>
        </div>
      </section> 	
    </div>
  </div>
</main>

<style>
  /* Removed redundant styles, relying on app.css now
*/
</style>