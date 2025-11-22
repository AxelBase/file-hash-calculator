<script>
  import { base } from '$app/paths';
  import { fly } from 'svelte/transition';
  import "../app.css";
  
  // Buy Me A Coffee Logic
  const paypalUsername = 'AxelLab427'; // **REMEMBER TO REPLACE THIS**
  const donationAmounts = [1, 3, 5, 10];
  let isDropdownOpen = false;
  
  function toggleDropdown() {
    isDropdownOpen = !isDropdownOpen;
  }
  function closeDropdown() {
    isDropdownOpen = false;
  }
  
  // Custom action to handle click outside for the dropdown
  function clickOutside(node) {
    const handleClick = (event) => {
      if (node && !node.contains(event.target) && isDropdownOpen) {
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

  // Get current year for footer
  const currentYear = new Date().getFullYear();
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
        <button class="bmac-button" on:click={toggleDropdown}>
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12.35,22.2L12,22A10,10,0,0,1,2,12V10A2,2,0,0,1,4,8H7.2A5.13,5.13,0,0,1,12,3A5.13,5.13,0,0,1,16.8,8H20A2,2,0,0,1,22,10V12A10,10,0,0,1,12.35,22.2M4,10V12A8,8,0,0,0,12,20A8,8,0,0,0,20,12V10H16.8A5.11,5.11,0,0,1,12.5,5.12A5.15,5.15,0,0,1,7.2,10H4Z" />
          </svg>
          Buy me a coffee
        </button>

        {#if isDropdownOpen}
          <div class="bmac-dropdown" transition:fly={{ y: -10, duration: 300, easing: 'cubic-bezier(0.25, 0.46, 0.45, 0.94)' }}>
            {#each donationAmounts as amount}
              <a
                href={`https://paypal.me/${paypalUsername}/${amount}`}
                target="_blank"
                rel="noopener noreferrer"
                on:click={closeDropdown}
              >
                ${amount}
              </a>
            {/each}
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