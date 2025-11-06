<script>
  import { onMount } from 'svelte';
  
  const logoUrl = "https://obj.miinet.cloud/branding/Wit.svg";
  const fallbackLogo = "data:image/svg+xml,%3Csvg width='400' height='120' xmlns='http://www.w3.org/2000/svg'%3E%3Ctext x='50%25' y='50%25' dominant-baseline='middle' text-anchor='middle' font-family='Helvetica,Arial,sans-serif' font-size='48' font-weight='700' fill='%23ffffff'%3EMIINETCLOUD%3C/text%3E%3C/svg%3E";
  
  let loaded = false;
  let logoError = false;
  
  onMount(() => {
    setTimeout(() => {
      loaded = true;
    }, 100);
  });
  
  function handleLogoError() {
    logoError = true;
  }
</script>

<main class:loaded>
  <div class="container">
    <div class="logo-section">
      <img 
        src={logoError ? fallbackLogo : logoUrl} 
        alt="MiinetCloud" 
        class="logo"
        on:error={handleLogoError}
      />
    </div>
    
    <nav class="nav-section">
      <a href="/login" class="btn btn-primary">
        <span class="btn-text">LOGIN</span>
        <span class="btn-overlay"></span>
      </a>
      <a href="https://github.com/miinetcloud" target="_blank" rel="noopener noreferrer" class="btn btn-secondary">
        <span class="btn-text">GITHUB</span>
        <span class="btn-overlay"></span>
      </a>
    </nav>
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    background-color: #1a1a1a;
    color: #ffffff;
  }

  main {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    opacity: 0;
    transform: scale(0.95);
    transition: opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1),
                transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
  }

  main.loaded {
    opacity: 1;
    transform: scale(1);
  }

  .container {
    width: 100%;
    max-width: 600px;
  }

  .logo-section {
    margin-bottom: 60px;
    padding: 40px;
    background-color: #000000;
    border: 6px solid #ffffff;
    transform: translateY(30px);
    opacity: 0;
    animation: slideInDown 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.2s forwards;
  }

  @keyframes slideInDown {
    to {
      transform: translateY(0);
      opacity: 1;
    }
  }

  .logo {
    width: 100%;
    height: auto;
    display: block;
    animation: pulse 2s ease-in-out 1s infinite;
  }

  @keyframes pulse {
    0%, 100% {
      transform: scale(1);
    }
    50% {
      transform: scale(1.02);
    }
  }

  .nav-section {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .btn {
    display: block;
    text-decoration: none;
    text-align: center;
    font-weight: 700;
    font-size: 24px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 24px 40px;
    border: 5px solid #000000;
    position: relative;
    overflow: hidden;
    transform: translateX(-50px);
    opacity: 0;
  }

  .btn:nth-child(1) {
    animation: slideInRight 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) 0.5s forwards;
  }

  .btn:nth-child(2) {
    animation: slideInRight 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) 0.7s forwards;
  }

  @keyframes slideInRight {
    to {
      transform: translateX(0);
      opacity: 1;
    }
  }

  .btn-text {
    position: relative;
    z-index: 2;
    display: inline-block;
    transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
  }

  .btn-overlay {
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    z-index: 1;
    transition: left 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  }

  .btn-primary {
    background-color: #003088;
    color: #ffffff;
    border-color: #ffffff;
  }

  .btn-primary .btn-overlay {
    background-color: #ffffff;
  }

  .btn-primary:hover {
    color: #003088;
    box-shadow: 8px 8px 0 rgba(255, 255, 255, 0.3);
    transform: translate(-4px, -4px);
    transition: all 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
  }

  .btn-primary:hover .btn-overlay {
    left: 0;
  }

  .btn-primary:hover .btn-text {
    transform: scale(1.05);
  }

  .btn-primary:active {
    transform: translate(0, 0);
    box-shadow: 2px 2px 0 rgba(255, 255, 255, 0.3);
    transition: all 0.1s ease;
  }

  .btn-secondary {
    background-color: #000000;
    color: #ffffff;
    border-color: #ffffff;
  }

  .btn-secondary .btn-overlay {
    background-color: #003088;
  }

  .btn-secondary:hover {
    color: #ffffff;
    box-shadow: 8px 8px 0 rgba(0, 48, 136, 0.5);
    transform: translate(-4px, -4px);
    transition: all 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
  }

  .btn-secondary:hover .btn-overlay {
    left: 0;
  }

  .btn-secondary:hover .btn-text {
    transform: scale(1.05);
  }

  .btn-secondary:active {
    transform: translate(0, 0);
    box-shadow: 2px 2px 0 rgba(0, 48, 136, 0.5);
    transition: all 0.1s ease;
  }

  @media (max-width: 600px) {
    .logo-section {
      margin-bottom: 40px;
      padding: 20px;
      border-width: 4px;
    }

    .btn {
      font-size: 20px;
      padding: 20px 30px;
      letter-spacing: 1.5px;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    * {
      animation-duration: 0.01ms !important;
      animation-iteration-count: 1 !important;
      transition-duration: 0.01ms !important;
    }

    main {
      opacity: 1;
      transform: scale(1);
    }

    .logo-section {
      transform: translateY(0);
      opacity: 1;
    }

    .btn {
      transform: translateX(0);
      opacity: 1;
    }

    .logo {
      animation: none;
    }
  }
</style>
