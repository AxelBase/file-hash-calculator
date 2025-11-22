<script lang="ts">
  import { base } from '$app/paths';

  const posts = [
    {
      href: '/blog/posts/post1',
      title: 'Introducing AxelBase File Hash Calculator',
      description: 'A 100% client-side, privacy-first web tool to compute SHA-256 and MD5 hashes instantly in your browser.'
    },
    {
      href: '/blog/posts/post2',
      title: 'Why Client-Side Hashing Matters',
      description: 'Learn why processing files locally in the browser is safer than uploading to servers — zero data transmission, full privacy.'
    },
    {
      href: '/blog/posts/post3',
      title: 'How to Verify File Integrity with SHA-256',
      description: 'Step-by-step guide on using SHA-256 hashes to confirm downloads, backups, and transfers haven’t been corrupted.'
    },
    {
      href: '/blog/posts/post4',
      title: 'MD5 vs SHA-256: When to Use Which',
      description: 'Understand the differences between MD5 and SHA-256, their use cases, and why SHA-256 is the modern standard.'
    },
    {
      href: '/blog/posts/post5',
      title: 'Hashing Large Files? No Problem.',
      description: 'See how our tool handles multi-gigabyte files with live progress bars — no freezes, no memory crashes.'
    },
    {
      href: '/blog/posts/post6',
      title: 'Works Offline — Forever',
      description: 'Once loaded, AxelBase File Hash Calculator runs completely offline. Bookmark it, use it anywhere, anytime.'
    },
    {
      href: '/blog/posts/post7',
      title: 'Deploy Your Own Version in 60 Seconds',
      description: 'Fork, deploy, and host your own branded version on GitHub Pages — fully static, free, and open source.'
    }
  ];
</script>

<svelte:head>
  <title>Blog | AxelBase File Hash Calculator</title>
  <meta name="description" content="Insights, tutorials, and best practices for using the AxelBase File Hash Calculator — the fastest, safest way to verify file integrity." />
</svelte:head>

<div class="container fade-in blog-index">
  <header class="blog-header">
    <h1>Blog: AxelBase Insights</h1>
    <p class="subtitle">
      Learn how to verify file integrity, understand cryptographic hashing, and get the most out of your 
      <strong>100% client-side File Hash Calculator</strong>. All tools are open source — 
      <a href="https://github.com/axelbase/file-hash-calculator" target="_blank" rel="noopener noreferrer">view on GitHub</a>.
    </p>
  </header>

  <div class="posts-grid">
    {#each posts as post}
      <a href="{base}{post.href}" class="card post-card">
        <div class="card-body">
          <h2 class="post-title">{post.title}</h2>
          <p class="post-description">{post.description}</p>
          <span class="read-more">Read Article &rarr;</span>
        </div>
      </a>
    {/each}
  </div>
</div>

<style>
  .blog-index {
    padding-top: 2rem;
    padding-bottom: 4rem;
  }

  .blog-header {
    text-align: center;
    margin-bottom: 3rem;
    border-bottom: 1px solid var(--bs-border-color);
    padding-bottom: 2rem;
  }

  .blog-header h1 {
    font-size: 2.8rem;
    margin-bottom: 1rem;
    color: var(--bs-emphasis-color);
  }

  .subtitle {
    font-size: 1.1rem;
    color: var(--bs-secondary-color);
    max-width: 700px;
    margin: 0 auto;
    line-height: 1.7;
  }

  .posts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 1.8rem;
  }

  .post-card {
    text-decoration: none;
    border: 1px solid var(--bs-border-color);
    border-radius: 0.75rem;
    overflow: hidden;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }

  .post-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 10px 25px rgba(0,0,0,0.1);
  }

  .post-card .card-body {
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  .post-title {
    font-size: 1.35rem;
    font-weight: 600;
    color: var(--bs-primary);
    margin-bottom: 0.75rem;
    line-height: 1.3;
  }

  .post-description {
    color: var(--bs-secondary-color);
    flex-grow: 1;
    margin-bottom: 1.2rem;
    line-height: 1.6;
  }

  .read-more {
    color: var(--bs-primary);
    font-weight: 600;
    font-size: 0.95rem;
    transition: transform 0.2s ease;
  }

  .post-card:hover .read-more {
    transform: translateX(6px);
  }

  @media (prefers-color-scheme: dark) {
    .post-card:hover {
      box-shadow: 0 10px 25px rgba(0,0,0,0.4);
    }
  }
</style>