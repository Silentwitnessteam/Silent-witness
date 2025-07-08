<section id="visuals" tabindex="0" aria-label="Galerie images humain et technologie">
  <h2>Humain & Technologie</h2>
  <div class="carousel" aria-live="polite" aria-roledescription="carousel">
    <button class="carousel-button prev" aria-label="Image précédente" aria-controls="carousel-track" aria-disabled="false">&#10094;</button>
    <div class="carousel-track" id="carousel-track">
      <div class="carousel-slide" role="group" aria-roledescription="slide" aria-label="Image 1 sur 3">
        <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=800&q=80" alt="Homme avec un casque de réalité augmentée" />
      </div>
      <div class="carousel-slide" role="group" aria-roledescription="slide" aria-label="Image 2 sur 3">
        <img src="https://images.unsplash.com/photo-1497493292307-31c376b6e479?auto=format&fit=crop&w=800&q=80" alt="Femme et robot collaborant ensemble" />
      </div>
      <div class="carousel-slide" role="group" aria-roledescription="slide" aria-label="Image 3 sur 3">
        <img src="https://images.unsplash.com/photo-1518770660439-4636190af475?auto=format&fit=crop&w=800&q=80" alt="Visage humain et visage robot en transparence" />
      </div>
    </div>
    <button class="carousel-button next" aria-label="Image suivante" aria-controls="carousel-track" aria-disabled="false">&#10095;</button>

    <div class="carousel-indicators" role="tablist" aria-label="Indicateurs de position">
      <button role="tab" aria-selected="true" aria-controls="slide1" id="indicator1" tabindex="0"></button>
      <button role="tab" aria-selected="false" aria-controls="slide2" id="indicator2" tabindex="-1"></button>
      <button role="tab" aria-selected="false" aria-controls="slide3" id="indicator3" tabindex="-1"></button>
    </div>
  </div>
</section>

<style>
  /* Carousel styles améliorés */
  .carousel {
    max-width: 900px;
    margin: 3rem auto;
    overflow: hidden;
    border-radius: 12px;
    box-shadow: 0 5px 15px rgba(28,89,128,0.3);
    background: white;
    position: relative;
    user-select: none;
  }
  .carousel-track {
    display: flex;
    transition: transform 0.5s ease;
    will-change: transform;
  }
  .carousel-slide {
    min-width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .carousel-slide img {
    width: 100%;
    max-height: 400px;
    object-fit: cover;
    border-radius: 12px;
    pointer-events: none;
  }
  .carousel-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: #1c5980cc;
    border: none;
    color: white;
    font-size: 2.5rem;
    padding: 0.3rem 1rem;
    cursor: pointer;
    border-radius: 50%;
    transition: background-color 0.3s ease;
    user-select: none;
    z-index: 10;
  }
  .carousel-button:hover,
  .carousel-button:focus {
    background: #8fc1a1cc;
    color: #1c5980;
    outline: none;
  }
  .carousel-button.prev {
    left: 15px;
  }
  .carousel-button.next {
    right: 15px;
  }
  .carousel-indicators {
    position: absolute;
    bottom: 15px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 10px;
  }
  .carousel-indicators button {
    width: 14px;
    height: 14px;
    background: #ccc;
    border-radius: 50%;
    border: none;
    cursor: pointer;
  }
  .carousel-indicators button[aria-selected="true"] {
    background: #1c5980;
  }
</style>

<script>
  const track = document.querySelector('.carousel-track');
  const slides = Array.from(track.children);
  const prevButton = document.querySelector('.carousel-button.prev');
  const nextButton = document.querySelector('.carousel-button.next');
  const indicators = document.querySelectorAll('.carousel-indicators button');
  let currentIndex = 0;
  let autoplayInterval;

  function updateCarousel() {
    const slideWidth = slides[0].getBoundingClientRect().width;
    track.style.transform = `translateX(-${currentIndex * slideWidth}px)`;
    indicators.forEach((btn, i) => {
      btn.setAttribute('aria-selected', i === currentIndex ? 'true' : 'false');
      btn.tabIndex = i === currentIndex ? 0 : -1;
    });
  }

  function goToSlide(index) {
    if (index < 0) index = slides.length - 1;
    else if (index >= slides.length) index = 0;
    currentIndex = index;
    updateCarousel();
  }

  prevButton.addEventListener('click', () => {
    goToSlide(currentIndex - 1);
    resetAutoplay();
  });

  nextButton.addEventListener('click', () => {
    goToSlide(currentIndex + 1);
    resetAutoplay();
  });

  indicators.forEach((btn, i) => {
    btn.addEventListener('click', () => {
      goToSlide(i);
      resetAutoplay();
    });
  });

  function startAutoplay() {
    autoplayInterval = setInterval(() => {
      goToSlide(currentIndex + 1);
    }, 5000);
  }

  function resetAutoplay() {
    clearInterval(autoplayInterval);
    startAutoplay();
  }

  // Start autoplay on load
  startAutoplay();

  // Pause autoplay on hover/focus
  const carousel = document.querySelector('.carousel');
  carousel.addEventListener('mouseenter', () => clearInterval(autoplayInterval));
  carousel.addEventListener('mouseleave', startAutoplay);
  carousel.addEventListener('focusin', () => clearInterval(autoplayInterval));
  carousel.addEventListener('focusout', startAutoplay);

  // Responsive fix on resize
  window.addEventListener('resize', updateCarousel);

  // Initialize carousel position
  updateCarousel();
</script>

