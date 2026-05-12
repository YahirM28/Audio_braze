  
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


++++


<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Mensaje In-App</title>

  <style>
    body {
      margin: 0;
      background-color: rgba(0,0,0,0.7);
      display:flex;
      justify-content:center;
      align-items:center;
      height:100vh;
      font-family:sans-serif;
    }

    .inapp-container {
      position: relative;
      width: 345px;
      height: 630px;
      background-image: url('https://braze-images.com/appboy/communication/assets/image_assets/images/69f8ab128b6e41008075c577/original.png?1777904398');
      background-size: cover;
      border-radius: 12px;
      overflow: hidden;
    }

    .close-button {
      position:absolute;
      top:5px;
      right:5px;
      border:none;
      background:transparent;
      font-size:22px;
      cursor:pointer;
      z-index:1000;
    }

    .trigger {
      position:absolute;
      width:120px;
      cursor:pointer;
    }

    .trigger-1 { top:220px; left:20px; }
    .trigger-2 { top:220px; right:20px; }
    .trigger-3 { top:330px; left:20px; }
    .trigger-4 { top:330px; right:20px; }
    .trigger-5 { top:440px; left:110px; }

    .overlay {
      display:none;
      position:fixed;
      inset:0;
      background:rgba(0,0,0,0.5);
      z-index:999;
    }

    .overlay.open { display:block; }

    .modal {
      width:80%;
      max-width:350px;
      margin:150px auto;
      position:relative;
    }

    .close-btn {
      position:absolute;
      top:10px;
      right:10px;
      width:30px;
      cursor:pointer;
    }

    .boton-descubre {
      position:absolute;
      bottom:20px;
      left:50%;
      transform:translateX(-50%);
      width:220px;
      height:50px;
      background:#1677D8;
      color:#fff;
      border:none;
      border-radius:10px;
      display:flex;
      align-items:center;
      justify-content:center;
      font-weight:bold;
      text-decoration:none;
    }
  </style>
</head>

<body>

<div class="inapp-container">

<!-- X -->
<button class="close-button"
onclick="
(function(){
  var brazeBridge = window.brazeBridge || window.appboyBridge;
  var INAPP_ID='inapp_prueba_martech';

  brazeBridge?.logClick && brazeBridge.logClick('Close Message');

  window.braze?.logCustomEvent && window.braze.logCustomEvent('Interaccion',{
    inapp_id: INAPP_ID,
    action:'dismiss-' + INAPP_ID
  });

  brazeBridge?.closeMessage && brazeBridge.closeMessage();
})();
">×</button>

<!-- TRIGGERS -->
<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8bf4526206c00b50d1569/original.png?1777909573" class="trigger trigger-1"
onclick="(function(){var b=window.brazeBridge||window.appboyBridge;var id='inapp_prueba_martech';b?.logClick&&b.logClick('1');window.braze?.logCustomEvent&&window.braze.logCustomEvent('Interaccion',{inapp_id:id,action:'open_modal1-'+id});document.getElementById('popupOverlay1').classList.add('open');})();"/>

<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8bf195720f5007de16280/original.png?1777909529" class="trigger trigger-2"
onclick="(function(){var b=window.brazeBridge||window.appboyBridge;var id='inapp_prueba_martech';b?.logClick&&b.logClick('2');window.braze?.logCustomEvent&&window.braze.logCustomEvent('Interaccion',{inapp_id:id,action:'open_modal2-'+id});document.getElementById('popupOverlay2').classList.add('open');})();"/>

<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8be7d21565d007d2d3ad3/original.png?1777909373" class="trigger trigger-3"
onclick="(function(){var b=window.brazeBridge||window.appboyBridge;var id='inapp_prueba_martech';b?.logClick&&b.logClick('3');window.braze?.logCustomEvent&&window.braze.logCustomEvent('Interaccion',{inapp_id:id,action:'open_modal3-'+id});document.getElementById('popupOverlay3').classList.add('open');})();"/>

<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8bee1a1cacf007f407996/original.png?1777909472" class="trigger trigger-4"
onclick="(function(){var b=window.brazeBridge||window.appboyBridge;var id='inapp_prueba_martech';b?.logClick&&b.logClick('4');window.braze?.logCustomEvent&&window.braze.logCustomEvent('Interaccion',{inapp_id:id,action:'open_modal4-'+id});document.getElementById('popupOverlay4').classList.add('open');})();"/>

<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8be42577aa1007dc03e99/original.png?1777909313" class="trigger trigger-5"
onclick="(function(){var b=window.brazeBridge||window.appboyBridge;var id='inapp_prueba_martech';b?.logClick&&b.logClick('5');window.braze?.logCustomEvent&&window.braze.logCustomEvent('Interaccion',{inapp_id:id,action:'open_modal5-'+id});document.getElementById('popupOverlay5').classList.add('open');})();"/>

<!-- MODALES -->
<!-- Modal 1 -->
<div class="overlay" id="popupOverlay1" onclick="if(event.target===this){this.classList.remove('open');}">
<div class="modal" onclick="event.stopPropagation()">
<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8b81bb41a31007dd6eed3/original.png?1777907735" style="width:100%">
<img class="close-btn" src="https://braze-images.com/appboy/communication/assets/image_assets/images/6942de097bf958006374cb93/original.png?1765989897"
onclick="document.getElementById('popupOverlay1').classList.remove('open')">
</div>
</div>

<!-- Modal 2 -->
<div class="overlay" id="popupOverlay2" onclick="if(event.target===this){this.classList.remove('open');}">
<div class="modal" onclick="event.stopPropagation()">
<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8b978e1a30a009856e6f5/original.png?1777908084" style="width:100%">
<img class="close-btn" src="https://braze-images.com/appboy/communication/assets/image_assets/images/6942de097bf958006374cb93/original.png?1765989897"
onclick="document.getElementById('popupOverlay2').classList.remove('open')">
</div>
</div>

<!-- Modal 3 -->
<div class="overlay" id="popupOverlay3" onclick="if(event.target===this){this.classList.remove('open');}">
<div class="modal" onclick="event.stopPropagation()">
<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8b9c53f47d0007ff901f0/original.png?1777908162" style="width:100%">
<img class="close-btn" src="https://braze-images.com/appboy/communication/assets/image_assets/images/6942de097bf958006374cb93/original.png?1765989897"
onclick="document.getElementById('popupOverlay3').classList.remove('open')">
</div>
</div>

<!-- Modal 4 -->
<div class="overlay" id="popupOverlay4" onclick="if(event.target===this){this.classList.remove('open');}">
<div class="modal" onclick="event.stopPropagation()">
<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8ba7fe852bd007ff291a4/original.png?1777908348" style="width:100%">
<img class="close-btn" src="https://braze-images.com/appboy/communication/assets/image_assets/images/6942de097bf958006374cb93/original.png?1765989897"
onclick="document.getElementById('popupOverlay4').classList.remove('open')">
</div>
</div>

<!-- Modal 5 -->
<div class="overlay" id="popupOverlay5" onclick="if(event.target===this){this.classList.remove('open');}">
<div class="modal" onclick="event.stopPropagation()">
<img src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8bfc1a7922b0081367536/original.png?1777909693" style="width:100%">
<img class="close-btn" src="https://braze-images.com/appboy/communication/assets/image_assets/images/6942de097bf958006374cb93/original.png?1765989897"
onclick="document.getElementById('popupOverlay5').classList.remove('open')">
</div>
</div>

<!-- CTA -->
<a href="bgeneralprod://personal/transactions/recharges" class="boton-descubre"
onclick="
(function(){
  var b = window.brazeBridge || window.appboyBridge;
  var id='inapp_prueba_martech';

  b?.logClick && b.logClick('0');

  window.braze?.logCustomEvent && window.braze.logCustomEvent('Interaccion',{
    inapp_id:id,
    action:'cta_click-'+id
  });

  b?.closeMessage && b.closeMessage();
})();
">
Recarga ya
</a>

</div>

</body>
</html>

!!!!

<!-- ====== TRIGGER 1 ====== -->
<img
  src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8bf4526206c00b50d1569/original.png?1777909573"
  class="trigger trigger-1"
  alt="Abrir Modal 1"
  onclick="
    window.brazeBridge = window.brazeBridge || window.appboyBridge || window.brazeBridge;

    /* Click analytics */
    if (window.brazeBridge && typeof brazeBridge.logClick === 'function') {
      brazeBridge.logClick('1');
    }

    /* Custom event */
    if (window.braze && typeof braze.logCustomEvent === 'function') {
      braze.logCustomEvent('Interaccion', {
        inapp_id: 'inapp_prueba_martech',
        action: 'body_click-inapp_prueba_martech'
      });
    }

    /* Open modal */
    var ov = document.getElementById('popupOverlay1');

    if (ov) {
      ov.classList.add('open');
    }
  "
/>

<!-- ================== MODAL 1 ================== -->
<div
  class="overlay"
  id="popupOverlay1"
  onclick="
    if (event.target === this) {

      if (window.braze && typeof braze.logCustomEvent === 'function') {
        braze.logCustomEvent('Interaccion', {
          inapp_id: 'inapp_prueba_martech',
          action: 'modal1_dismiss-inapp_prueba_martech',
          reason: 'overlay_click'
        });
      }

      this.classList.remove('open');
    }
  "
>
  <div class="modal" onclick="event.stopPropagation()">

    <img
      src="https://braze-images.com/appboy/communication/assets/image_assets/images/69f8b81bb41a31007dd6eed3/original.png?1777907735"
      alt="Contenido Modal 1"
      style="width:100%; height:60%; padding-left:10px; padding-bottom:10px;"
    />

    <!-- CLOSE BUTTON TEXTO -->
    <button
      class="close-btn"
      onclick="
        if (window.braze && typeof braze.logCustomEvent === 'function') {
          braze.logCustomEvent('Interaccion', {
            inapp_id: 'inapp_prueba_martech',
            action: 'modal1_close-inapp_prueba_martech'
          });
        }

        var ov = document.getElementById('popupOverlay1');

        if (ov) {
          ov.classList.remove('open');
        }
      "
    >
      X
    </button>

  </div>
</div>

###
<a
  href="bgeneralprod://personal/transactions/recharges"
  class="boton-descubre"
  onclick="
    brazeBridge.logClick('Recarga ya');

    if(window.brazeBridge && typeof brazeBridge.logCustomEvent === 'function')
    {
      brazeBridge.logCustomEvent('Interaccion',
      {
        inapp_id: 'inapp_prueba_martech',
        action: 'cta_recarga_click-inapp_prueba_martech'
      });
    }

    brazeBridge.closeMessage();
  "
>
  Recarga ya
</a>


@@@@
<style type="text/css">
  body, table, td, p, a {
    font-family: Arial, sans-serif !important;
  }

  table {
    border-collapse: collapse !important;
    border-spacing: 0 !important;
  }

  td {
    mso-line-height-rule: exactly;
  }
</style>

<table
  role="presentation"
  width="100%"
  border="0"
  cellspacing="0"
  cellpadding="0"
  align="center"
  bgcolor="#F7F9FC"
  style="background-color:#F7F9FC;"
>
  <tr>
    <td align="center">

      <table
        role="presentation"
        width="550"
        border="0"
        cellspacing="0"
        cellpadding="0"
        style="width:550px; max-width:550px; background:#F7F9FC;"
      >

        <!-- LOGO -->
        <tr>
          <td
            style="padding:24px 40px 16px 40px;"
          >
            <img
              src="https://us1-sharedresources-dashboardbeepluginuploads3buc-1uv5n1030xv7g.s3.amazonaws.com/images/W4R-R48-R95Z/BGfooter.png"
              width="136"
              alt="Banco General"
              style="display:block; border:0;"
            >
          </td>
        </tr>

        <!-- TEXT -->
        <tr>
          <td
            style="
              padding:0 40px;
              font-size:12px;
              line-height:18px;
              color:#6F7583;
              text-align:justify;
            "
          >
            Este correo ha sido enviado por Banco General...
          </td>
        </tr>

        <!-- SPACER -->
        <tr>
          <td height="24" style="line-height:24px; font-size:24px;">
            &nbsp;
          </td>
        </tr>

        <!-- UNSUBSCRIBE -->
        <tr>
          <td
            align="center"
            style="
              padding:0 40px 24px 40px;
              font-size:12px;
              line-height:18px;
              color:#6F7583;
            "
          >
            <a
              href="#"
              style="color:#555555; text-decoration:none;"
            >
              Cancelar suscripción
            </a>
          </td>
        </tr>

      </table>

    </td>
  </tr>
</table>
