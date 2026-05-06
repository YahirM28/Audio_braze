  
    <script>
document.addEventListener("click", function () {
  const audio = document.getElementById("bgAudio");
  audio.play();
}, { once: true });
</script>


<audio id="bgAudio" loop>
  <source src="images/audio.mp3" type="audio/mpeg">
</audio>



<!DOCTYPE html>
<html lang="es">
<head>
<title></title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>

body {
  margin: 0;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: 'Inter', sans-serif;
}

.slideshow-container {
  position: relative;
  width: 330px;
  height: 600px;
  overflow: hidden;
  border-radius: 8px;
}

.carousel-images {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-images img,
.slide-with-hotspots {
  width: 100%;
  flex-shrink: 0;
}

/* ===== HOTSPOTS ===== */

.slide-with-hotspots {
  position: relative;
}

.slide-with-hotspots img {
  width: 100%;
  display: block;
}

.hotspot {
  position: absolute;
  width: 80%;
  height: 60px;
  left: 10%;
  cursor: pointer;
}

/* SOLO PARA VISUALIZAR (puedes quitarlo) */
.hotspot {
  background: rgba(255, 0, 0, 0.2);
}

/* ===== BOTONES ===== */

.button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: transparent;
  border: none;
  cursor: pointer;
}

.prev { left: 0; }
.next { right: 0; }

.close-button {
  position: absolute;
  top: 12px;
  right: 12px;
  background: #fff;
  border-radius: 50%;
  width: 28px;
  height: 28px;
  cursor: pointer;
  text-align: center;
  line-height: 28px;
}

/* ===== MODAL ===== */

.modal {
  display: none;
  position: fixed;
  z-index: 999;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.8);
}

.modal-content {
  background: #fff;
  margin: 40% auto;
  padding: 20px;
  width: 80%;
  border-radius: 10px;
  text-align: center;
}

.close {
  float: right;
  cursor: pointer;
  font-weight: bold;
}

</style>
</head>

<body>

<div class="slideshow-container">

  <div class="carousel-images">

    <!-- SLIDE 1 -->
    <img src="https://braze-images.com/appboy/communication/assets/svg_assets/files/68e81b2311c934006319256f/original.svg?1760041762">

    <!-- SLIDE 2 (CON HOTSPOTS) -->
    <div class="slide-with-hotspots">
      <img src="https://braze-images.com/appboy/communication/assets/svg_assets/files/68e81b575049ed007455d44d/original.svg?1760041815">

      <div class="hotspot" style="top: 20%;" onclick="openModal(1)"></div>
      <div class="hotspot" style="top: 45%;" onclick="openModal(2)"></div>
      <div class="hotspot" style="top: 70%;" onclick="openModal(3)"></div>
    </div>

    <!-- SLIDE 3 -->
    <img src="https://braze-images.com/appboy/communication/assets/svg_assets/files/68e81b78bbc24d0065fa3097/original.svg?1760041848">

  </div>

  <!-- BOTÓN CERRAR -->
  <button class="close-button" onclick='brazeBridge.logClick("Close Message"); brazeBridge.closeMessage()'>X</button>

  <!-- NAV -->
  <button class="button prev" onclick="prevSlide()">◀</button>
  <button class="button next" onclick="nextSlide()">▶</button>

</div>

<!-- MODAL -->
<div id="modal" class="modal">
  <div class="modal-content">
    <span class="close" onclick="closeModal()">X</span>
    <div id="modal-body"></div>
  </div>
</div>

<script>

const carouselImages = document.querySelector('.carousel-images');
const slides = document.querySelectorAll('.carousel-images > *');

let currentIndex = 0;
let slideInterval;

function showSlide(index) {
  const total = slides.length;

  if (index >= total) currentIndex = 0;
  else if (index < 0) currentIndex = total - 1;
  else currentIndex = index;

  const offset = -currentIndex * 100;
  carouselImages.style.transform = `translateX(${offset}%)`;
}

function nextSlide() {
  showSlide(currentIndex + 1);
}

function prevSlide() {
  showSlide(currentIndex - 1);
}

function stop() {
  clearInterval(slideInterval);
}

slideInterval = setInterval(nextSlide, 10000);

// detener autoplay si interactúa
document.querySelectorAll('.button, .hotspot').forEach(el => {
  el.addEventListener('click', stop);
});

/* ===== MODAL ===== */

function openModal(type) {
  const modal = document.getElementById("modal");
  const body = document.getElementById("modal-body");

  if (type === 1) {
    body.innerHTML = "<h2>Opción 1</h2><p>Contenido del modal 1</p>";
  } else if (type === 2) {
    body.innerHTML = "<h2>Opción 2</h2><p>Contenido del modal 2</p>";
  } else if (type === 3) {
    body.innerHTML = "<h2>Opción 3</h2><p>Contenido del modal 3</p>";
  }

  modal.style.display = "block";
}

function closeModal() {
  document.getElementById("modal").style.display = "none";
}

</script>

</body>
</html>
----
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Mensaje In-App</title>
  <style>
    body {
      margin: 0;
      background-color: rgba(0, 0, 0, 0.7);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      font-family: 'Inter', sans-serif;
    }
    .inapp-container {
      position: relative;
      width: 345px;
      height: 630px;
      background-image: url('https://braze-images.com/appboy/communication/assets/image_assets/images/69f8ab128b6e41008075c577/original.png?1777904398');
      background-size: cover;
      background-position: center;
      border-radius: 12px;
      overflow: hidden;
      color: white;
    }

    .boton-descubre {
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      bottom: 20px;
      width: 220px;
      height: 50px;
      background-color: #1677D8;
      color: #fff;
      border-radius: 10px;
      font-size: 18px;
      font-weight: bold;
      display: flex;
      align-items: center;
      justify-content: center;
      text-decoration: none;
    }

    .close-button {
      position: absolute;
      top: 2px;
      right: 2px;
      background: transparent;
      border: none;
      font-size: 20px;
      cursor: pointer;
      z-index: 10001;
    }

    .overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.5);
    }
    .overlay.open { display: block; }

    .modal {
      width: 80%;
      max-width: 350px;
      margin: 170px auto;
      position: relative;
    }

    .close-btn {
      position: absolute;
      top: 5px;
      right: 18px;
      width: 30px;
      height: 30px;
      cursor: pointer;
    }
  </style>
</head>

<body>

<div class="inapp-container">

  <!-- Cerrar in-app -->
  <button class="close-button"
    onclick="
      window.brazeBridge = window.brazeBridge || window.appboyBridge;

      if (brazeBridge?.logClick) brazeBridge.logClick('Close Message');
      if (window.braze?.logCustomEvent) {
        braze.logCustomEvent('Interaccion', { action: 'dismiss' });
      }
      if (brazeBridge?.closeMessage) brazeBridge.closeMessage();
    "
  >X</button>

  <!-- ================= CTA PRINCIPAL (FIX ANDROID) ================= -->
  <a
    href="bgeneralprod://personal/transactions/recharges"
    class="boton-descubre"
    onclick="
      (function(anchor, e){
        e.preventDefault();

        window.brazeBridge = window.brazeBridge || window.appboyBridge;

        var href = anchor.getAttribute('href');
        var INAPP_ID='inapp_prueba_martech';

        // ✅ tracking primero
        if (brazeBridge?.logClick) {
          brazeBridge.logClick('0');
        }

        if (window.braze?.logCustomEvent) {
          braze.logCustomEvent('Interaccion', {
            inapp_id: INAPP_ID,
            action: 'cta_boton_base_click-' + INAPP_ID
          });
        }

        // 🟡 delay corto para asegurar tracking
        setTimeout(function(){
          window.location.href = href;
        }, 120);

        // 🔵 cierre después
        setTimeout(function(){
          if (brazeBridge?.closeMessage) {
            brazeBridge.closeMessage();
          }
        }, 400);

      })(this, event);
    "
  >
    Recarga ya
  </a>

</div>

</body>
</html>

