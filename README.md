<title>Silent Witness</title>
<style>
  :root {
    --color-primary: #1c5980;
    --color-secondary: #8fc1a1;
    --color-bg-light: #fefefe;
    --color-bg-dark: #121212;
    --color-text-light: #222222;
    --color-text-dark: #e0e0e0;
    --transition-speed: 0.35s;
    --border-radius: 12px;
    --box-shadow-light: 0 4px 15px rgba(28, 89, 128, 0.15);
    --box-shadow-dark: 0 4px 20px rgba(0, 0, 0, 0.6);
    --font-family: 'Poppins', sans-serif;
  }

  /* Reset & basics */
  *, *::before, *::after {
    box-sizing: border-box;
  }

  body {
    margin: 0; padding: 0;
    font-family: var(--font-family);
    background-color: var(--color-bg-light);
    color: var(--color-text-light);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    transition: background-color var(--transition-speed), color var(--transition-speed);
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body.dark-theme {
    background-color: var(--color-bg-dark);
    color: var(--color-text-dark);
  }

  /* Header */
  header {
    background: var(--color-primary);
    color: white;
    padding: 1.25rem 2.5rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: var(--box-shadow-light);
    border-bottom-left-radius: var(--border-radius);
    border-bottom-right-radius: var(--border-radius);
  }

  header .logo-container {
    display: flex;
    align-items: center;
    gap: 1.2rem;
  }

  header img.logo {
    height: 50px;
    border-radius: 8px;
    object-fit: contain;
    filter: drop-shadow(0 0 2px rgba(0,0,0,0.1));
  }

  header h1 {
    font-weight: 900;
    font-size: 2rem;
    margin: 0;
    letter-spacing: 1.2px;
  }

  header .controls {
    display: flex;
    align-items: center;
    gap: 1.2rem;
  }

  select#lang-select {
    padding: 0.4rem 0.75rem;
    font-size: 1rem;
    border-radius: var(--border-radius);
    border: none;
    cursor: pointer;
    background: white;
    color: var(--color-primary);
    box-shadow: 0 2px 8px rgba(28,89,128,0.15);
    transition: background-color 0.25s ease;
  }

  select#lang-select:hover, select#lang-select:focus {
    background-color: var(--color-secondary);
    color: white;
    outline: none;
  }

  button#theme-toggle {
    font-size: 1.6rem;
    background: transparent;
    border: none;
    color: white;
    cursor: pointer;
    transition: color 0.3s ease;
    padding: 0.2rem 0.5rem;
    border-radius: var(--border-radius);
  }

  button#theme-toggle:hover {
    color: var(--color-secondary);
    background-color: rgba(255 255 255 / 0.15);
  }

  /* Main Title + animated text */
  #main-title-section {
    max-width: 900px;
    margin: 3rem auto 4rem;
    text-align: center;
    padding: 0 1rem;
  }

  #main-title-section h1 {
    font-size: 3.4rem;
    font-weight: 900;
    margin-bottom: 0.25rem;
    color: var(--color-primary);
    user-select: none;
    letter-spacing: 1.4px;
    text-shadow: 0 2px 4px rgba(28,89,128,0.2);
  }

  #animated-text {
    font-size: 2.8rem;
    font-weight: 700;
    color: var(--color-secondary);
    user-select: none;
    animation: pulseText 2.5s infinite ease-in-out;
    letter-spacing: 0.8px;
  }

  @keyframes pulseText {
    0%, 100% {
      opacity: 1;
      transform: scale(1);
    }
    50% {
      opacity: 0.6;
      transform: scale(1.05);
    }
  }

  /* Donation Section */
  #donation-section {
    max-width: 400px;
    background: var(--color-primary);
    color: white;
    border-radius: var(--border-radius);
    padding: 2rem 2.5rem;
    margin: 2.5rem auto 5rem;
    box-shadow: 0 10px 25px rgba(28,89,128,0.3);
    text-align: center;
    user-select: none;
    font-weight: 600;
    letter-spacing: 0.8px;
  }

  #donation-section h2 {
    margin-bottom: 1.5rem;
    font-size: 1.9rem;
  }

  #paypal-button-container {
    margin-top: 1.5rem;
  }

  /* White Paper Section */
  #whitepaper-section {
    max-width: 900px;
    margin: 0 auto 4rem;
    padding: 0 2rem;
    text-align: center;
  }

  #whitepaper-section p {
    font-size: 1.2rem;
    margin-bottom: 1.25rem;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    line-height: 1.5;
    color: var(--color-text-light);
  }

  #whitepaper-btn {
    display: inline-block;
    background: var(--color-primary);
    color: white;
    padding: 1rem 2.2rem;
    font-weight: 700;
    border-radius: var(--border-radius);
    text-decoration: none;
    box-shadow: 0 6px 14px rgba(28,89,128,0.2);
    transition: background-color 0.35s ease, color 0.35s ease;
    user-select: none;
  }

  #whitepaper-btn:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
    box-shadow: 0 8px 22px rgba(143,193,161,0.5);
  }

  /* Carte interactive Section */
  #map-section {
    max-width: 1100px;
    margin: 3.5rem auto 5rem;
    padding: 0 1rem;
  }

  #map-section h2 {
    text-align: center;
    font-weight: 900;
    font-size: 2.2rem;
    margin-bottom: 1.25rem;
    user-select: none;
    letter-spacing: 1.2px;
    color: var(--color-primary);
    text-shadow: 0 1px 3px rgba(28,89,128,0.2);
  }

  #map {
    width: 100%;
    height: 550px;
    border-radius: 16px;
    box-shadow: var(--box-shadow-light);
    border: none;
  }

  /* Filter buttons */
  #filter-buttons {
    text-align: center;
    margin-bottom: 1.5rem;
  }

  #filter-buttons button {
    background: var(--color-primary);
    color: white;
    border: none;
    margin: 0 0.3rem;
    padding: 0.7rem 1.3rem;
    font-weight: 700;
    border-radius: var(--border-radius);
    cursor: pointer;
    transition: background-color 0.35s ease, color 0.35s ease;
    user-select: none;
    box-shadow: 0 3px 10px rgba(28,89,128,0.2);
  }

  #filter-buttons button.active,
  #filter-buttons button:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
    box-shadow: 0 5px 18px rgba(143,193,161,0.4);
  }

  /* Stats Section */
  #stats-section {
    max-width: 900px;
    margin: 0 auto 5rem;
    padding: 0 2rem;
  }

  #stats-section h2 {
    font-weight: 900;
    font-size: 2.2rem;
    margin-bottom: 1.5rem;
    user-select: none;
    text-align: center;
    color: var(--color-primary);
    letter-spacing: 1.2px;
  }

  #stats-section ul {
    list-style: none;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    font-size: 1.15rem;
    line-height: 1.7;
    padding-left: 0;
  }

  #stats-section ul li {
    position: relative;
    padding-left: 1.6rem;
    margin-bottom: 1rem;
    color: var(--color-text-light);
  }

  #stats-section ul li::before {
    content: '•';
    position: absolute;
    left: 0;
    top: 0;
    color: var(--color-secondary);
    font-size: 1.4rem;
    line-height: 1;
  }

  /* Detection Steps Section */
  #detection-steps {
    max-width: 900px;
    margin: 0 auto 5rem;
    padding: 0 2rem;
  }

  #detection-steps h2 {
    font-weight: 900;
    font-size: 2.2rem;
    margin-bottom: 1.5rem;
    text-align: center;
    user-select: none;
    color: var(--color-primary);
    letter-spacing: 1.2px;
  }

  #detection-steps ol {
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    font-size: 1.15rem;
    line-height: 1.7;
    padding-left: 0;
    counter-reset: step-counter;
  }

  #detection-steps ol li {
    margin-bottom: 1.3rem;
    position: relative;
    padding-left: 3rem;
    color: var(--color-text-light);
  }

  #detection-steps ol li::before {
    content: counter(step-counter);
    counter-increment: step-counter;
    position: absolute;
    left: 0;
    top: 0;
    background: var(--color-primary);
    color: white;
    width: 2.2rem;
    height: 2.2rem;
    border-radius: 50%;
    text-align: center;
    line-height: 2.2rem;
    font-weight: 900;
    box-shadow: 0 2px 8px rgba(28, 89, 128, 0.3);
    user-select: none;
    font-size: 1.2rem;
  }

  /* Contact Section */
  #contact-section {
    max-width: 600px;
    margin: 0 auto 4rem;
    padding: 0 1rem;
  }

  #contact-section h2 {
    font-weight: 900;
    font-size: 2.2rem;
    margin-bottom: 1.25rem;
    text-align: center;
    user-select: none;
    color: var(--color-primary);
    letter-spacing: 1.2px;
  }

  form#contact-form {
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
  }

  form#contact-form input,
  form#contact-form textarea {
    padding: 1rem;
    border-radius: var(--border-radius);
    border: 1.5px solid #ccc;
    font-size: 1rem;
    font-family: inherit;
    transition: border-color 0.3s ease;
  }

  form#contact-form input:focus,
  form#contact-form textarea:focus {
    border-color: var(--color-primary);
    outline: none;
    box-shadow: 0 0 8px rgba(28,89,128,0.3);
  }

  form#contact-form button {
    background: var(--color-primary);
    color: white;
    font-weight: 700;
    padding: 1rem;
    border: none;
    border-radius: var(--border-radius);
    cursor: pointer;
    transition: background-color 0.35s ease, color 0.35s ease;
    box-shadow: 0 4px 15px rgba(28,89,128,0.25);
  }

  form#contact-form button:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
    box-shadow: 0 6px 20px rgba(143,193,161,0.5);
  }

  /* Responsive */
  @media (max-width: 700px) {
    #main-title-section h1 {
      font-size: 2.4rem;
    }
    #animated-text {
      font-size: 2rem;
    }
    #map {
      height: 400px;
    }
    header {
      flex-direction: column;
      gap: 1.2rem;
      padding: 1rem 1.5rem;
      border-radius: 0 0 var(--border-radius) var(--border-radius);
    }
    header .controls {
      gap: 0.8rem;
    }
  }

  /* RTL Support for Arabic */
  html[lang="ar"] {
    direction: rtl;
  }

  html[lang="ar"] body {
    text-align: right;
  }

  html[lang="ar"] header {
    direction: rtl;
  }

  html[lang="ar"] #contact-section input,
  html[lang="ar"] #contact-section textarea {
    direction: rtl;
    text-align: right;
  }
</style>
