<script lang="ts">
  import { base } from '$app/paths';
  import { fly } from 'svelte/transition';
  import "../app.css";

  const currentYear = new Date().getFullYear();

  let isDropdownOpen = false;

  function toggleDropdown() {
    isDropdownOpen = !isDropdownOpen;
  }

  function closeDropdown() {
    isDropdownOpen = false;
  }

  function clickOutside(node: HTMLElement) {
    const handleClick = (event: MouseEvent) => {
      if (node && !node.contains(event.target as Node)) {
        node.dispatchEvent(new CustomEvent('click_outside'));
      }
    };
    document.addEventListener('click', handleClick, true);
    return {
      destroy() {
        document.removeEventListener('click', handleClick, true);
      }
    };
  }
</script>

<header class="custom-navbar">
  <div class="navbar-content">
   
    <div style="display: flex; align-items: center; gap: 0.75rem;">
      <a href="{base}/" aria-label="Home">
        <img src="{base}/AxelLab-Logo.ico" alt="AxelBase Logo" class="navbar-brand-logo" />
      </a>
      <a class="navbar-brand-text" href="{base}/" style="text-decoration: none;">AxelBase</a>
    </div>

    <ul class="nav-list">
     
      <li class="nav-item bmac-nav-item" use:clickOutside on:click_outside={closeDropdown}>
        <button
          class="bmac-button d-flex align-items-center gap-2 text-white border-0 shadow-sm"
          on:click={toggleDropdown}
          aria-label="Support options"
        >
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
            <path d="M2,21V19H20V21H2M20,8V5H4V8H20M20,10H4V13C4,14.38 4.5,15.63 5.31,16.58L11.64,19H12.36L18.69,16.58C19.5,15.63 20,14.38 20,13V10M16,2H8V4H16V2Z" />
          </svg>
          <span class="d-none d-sm-inline fw-semibold">Buy me a Coffee</span>
        </button>

        {#if isDropdownOpen}
          <div class="bmac-dropdown mt-2" transition:fly={{ y: -10, duration: 250 }}>
            <a href="https://buymeacoffee.com/axelbase" target="_blank" rel="noopener" on:click={closeDropdown}>
              <span class="amount">$3</span> One Coffee
            </a>
            <a href="https://buymeacoffee.com/axelbase" target="_blank" rel="noopener" on:click={closeDropdown}>
              <span class="amount">$5</span> Two Coffees
            </a>
            <a href="https://buymeacoffee.com/axelbase" target="_blank" rel="noopener" on:click={closeDropdown}>
              <span class="amount">$10</span> Three Coffees
            </a>

            <a href="https://buymeacoffee.com/axelbase" target="_blank" rel="noopener" on:click={closeDropdown} class="custom-amount">
              Custom Amount
            </a>

            <a
              href="bitcoin:bc1q3p0e6vt492m4w4fpz5m2cl4zcfuqqkgaj6myc9?label=AxelBase&message=Buy%20me%20a%20coffee"
              on:click={closeDropdown}
              class="custom-amount"
            >
              Buy via Crypto (Bitcoin)
            </a>
          </div>
        {/if}
      </li>
     
      <li><a class="nav-link" href="{base}/">Home</a></li>
      <li><a class="nav-link" href="{base}/#about">About</a></li>
      <li><a class="nav-link" href="{base}/#how-to-use">How to use</a></li>
      <li><a class="nav-link" href="{base}/#faq">FAQ</a></li>
      <li><a class="nav-link" href="{base}/blog">Blog</a></li>
     
    </ul>
  </div>
</header>

<slot />

<footer class="custom-footer">
  <div class="container text-center">
    &copy; {currentYear} AxelBase File Hash Calculator
    <span class="text-muted">|</span>
    <a class="footer-link" href="{base}/privacy">Privacy</a>
    <span class="text-muted">|</span>
    <a class="footer-link" href="{base}/terms">Terms</a>
  </div>
</footer>

<style>
  /* Keep all existing File 2 styles – only override the BMAC section below */

  /* BMAC Button – Using File 1's exact style (pill, white text, no border, subtle shadow, hover lift) */
  .bmac-button {
    background: var(--primary-color);
    font-size: 0.95rem;
    padding: 0.65rem 1.5rem;
    border-radius: 999px; /* full pill shape */
    transition: all 0.3s ease;
    box-shadow: 0 4px 10px rgba(100, 28, 52, 0.3);
  }

  .bmac-button:hover {
    background: var(--primary-hover);
    transform: translateY(-2px);
    box-shadow: 0 6px 15px rgba(100, 28, 52, 0.4);
  }

  /* BMAC Dropdown – Directly from File 1, adapted to theme */
  .bmac-dropdown {
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translateX(-50%);
    margin-top: 8px;
    width: 240px;
    background: var(--card-bg);
    border-radius: 16px;
    box-shadow: 0 12px 32px rgba(100, 28, 52, 0.15);
    overflow: hidden;
    border: 1px solid var(--primary-light-tint);
    z-index: 1000;
  }

  .bmac-dropdown a {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 12px 20px;
    color: var(--text-main);
    text-decoration: none;
    font-size: 0.98rem;
    transition: all 0.2s ease;
  }

  .bmac-dropdown a:hover {
    background: var(--primary-light-tint);
    color: var(--primary-color);
    padding-left: 28px;
  }

  .bmac-dropdown .amount {
    font-weight: 700;
    color: var(--primary-color);
    font-size: 1.1rem;
  }

  .bmac-dropdown a:hover .amount {
    color: var(--primary-color);
  }

  .bmac-dropdown .custom-amount {
    font-weight: 600;
    color: var(--primary-color);
    border-top: 1px solid rgba(100, 28, 52, 0.1);
    justify-content: center !important;
  }

  .bmac-dropdown .custom-amount:hover {
    background: var(--primary-light-tint);
    color: var(--primary-color);
  }

  /* Responsive: hide text on small screens (as in File 1) */
  @media (max-width: 576px) {
    .bmac-button span {
      display: none;
    }
    .bmac-button {
      padding: 0.65rem 1rem;
    }
  }
</style>