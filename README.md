  
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

+++
```html
<style type="text/css">
  /* What it does: Remove spaces around the email design added by some email clients. */
  /* Beware: It can remove the padding / margin and add a background color to the compose a reply window. */
  html,
  body {
    margin: 0 auto !important;
    padding: 0 !important;
    height: 100% !important;
    width: 100% !important;
    background-color: #EBEEF4 !important;
  }

  /* What it does: Stops Outlook from adding extra spacing to tables. */
  table,
  td {
    border-spacing: 0;
    padding: 0;
    mso-table-lspace: 0pt !important;
    mso-table-rspace: 0pt !important;
    mso-line-height-rule: exactly !important;
  }

  /* What it does: Replaces default bold style. */
  th {
    font-weight: normal;
  }

  /* What it does: Fixes webkit padding issue. */
  table {
    border-spacing: 0 !important;
    border-collapse: collapse !important;
    table-layout: fixed !important;
    margin: 0 auto !important;
  }

  /* What it does: Prevents Windows 10 Mail from underlining links despite inline CSS. Styles for underlined links should be inline. */
  a {
    text-decoration: none !important;
  }

  /* What it does: Uses a better rendering method when resizing images in IE. */
  img {
    border: 0;
    -ms-interpolation-mode: bicubic;
  }

  /* What it does: A work-around for email clients meddling in triggered links. */
  a[x-apple-data-detectors],
  /* iOS */
  .unstyle-auto-detected-links a,
  .aBn {
    border-bottom: 0 !important;
    cursor: default !important;
    color: inherit !important;
    text-decoration: none !important;
    font-size: inherit !important;
    font-family: inherit !important;
    font-weight: inherit !important;
    line-height: inherit !important;
  }

  .wrapper {
    width: 100% !important;
    table-layout: center !important;
    background-color: #EBEEF4 !important;
  }

  .main {
    background-color: #ffffff !important;
    margin: 0 auto !important;
    width: 100% !important;
    max-width: 550px !important;
    border-spacing: 0 !important;
    font-family: 'Inter', sans-serif !important;
  }

  .two-columns {
    text-align: center;
    font-size: 0;
    /* los elementos de las 2 columnas se estan comportando como un texto*/
  }

  .two-columns .column {
    width: 100% !important;
    max-width: 275px !important;
    display: inline-block !important;
    vertical-align: top !important;
    font-family: 'Inter', sans-serif !important;
    font-size: 16px !important;
  }

  /* What it does: Hover styles for buttons */
  .button-td,
  .button-a {
    transition: all 100ms ease-in;
  }

  .button-td-primary:hover,
  .button-a-primary:hover {
    background: #FF7900 !important;
    border-color: #FF7900 !important;
  }

  .button-td-secondary:hover,
  .button-a-secondary:hover {
    background: #ffffff !important;
    border-color: #1677D8 !important;
  }

  /* Extra small devices and tablet (phones, 600px and down)-(portrait tablets and large phones, 600px and up) */
  @media only screen and (max-width: 600px) {
    .two-columns .column {
      width: 100% !important;
      max-width: 100% !important;
    }

    .padding-mobile {
      margin-top: 0px !important;
      padding-top: 0px !important;
    }
  }

  /* Large devices (laptops/desktops, 992px and up) */
  @media only screen and (min-width: 601px) {
    .padding-mobile {
      padding-top: 0px !important;
    }
  }

  /* Extra large devices (large laptops and desktops, 1200px and up) */
  @media only screen and (min-width: 1200px) {
    .padding-mobile {
      padding-top: 0px !important;
    }
  }
</style>

<!-- FOOTER-->
<!-- Email Footer : BEGIN -->
<table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="margin: auto; background-color: #F7F9FC" class="main" width="100%">
  <tbody>
    <tr>
      <td style="background-color: #F7F9FC; padding: 5px 40px;text-align: left;">
        <br />
        <a href="https://www.bgeneral.com/?utm_source=Logo_footer&utm_medium=email&utm_campaign=correos_2020&lid=u1ms5fkex1ma" target="_blank">
          <img alt="Logo BG gris" src="https://us1-sharedresources-dashboardbeepluginuploads3buc-1uv5n1030xv7g.s3.amazonaws.com/images/W4R-R48-R95Z/BGfooter.png" style="display:block; color: #ffffff;width: 136px;max-width: 136px;" width="136" />
        </a>
      </td>
    </tr>

    <tr>
      <td style="background-color: #F7F9FC;padding:5px 40px; font-family: 'Inter', sans-serif; color: #6F7583; text-align: justify; line-height:18px;">
        <small>
          Este correo ha sido enviado por Banco General a la dirección electrónica que mantenemos en nuestra base de datos. Por ser un correo masivo, te agradecemos no contestes a esta dirección. Si deseas darnos tu opinión del contenido de este correo, puedes escribirnos a
          <a href="mailto:info@bgeneral.com" style="color: #0066CC;" target="_blank">info@bgeneral.com</a>.
          <br />
          <div style="line-height:16px; height:16px;">&nbsp;</div>
          Al entregar tu información, declaras que has leído, entiendes y aceptas el tratamiento de tus datos conforme al Aviso de Privacidad de Banco General y subsidiarias, el cual se encuentra disponible y actualizado en el
          <a href="https://www.bgeneral.com/personas/seguridad/?lid=kxqtksxmf6bd#tab-fede85291600681d96b" style="color: #0066CC;" target="_blank">sitio web</a>.
        </small>
        <br /><br />
      </td>
    </tr>

    <td style="background-color: #F7F9FC;padding:5px 40px; font-family: 'Inter', sans-serif; color: #6F7583;text-align: center; line-height:18px;">
      <small>
        <a href="#" style="color: #555555;text-decoration: none;">Cancelar suscripción</a>
      </small>
    </td>
  </tbody>
</table>
<!-- Email Footer : END -->
<!-- FOOTER : END-->
```
@@@@

<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>

.calculadora{
    position:absolute;
    top:220px;
    left:50%;
    transform:translateX(-50%);
    width:250px;
}

.fila{
    display:flex;
    align-items:center;
    justify-content:space-between;
    margin-bottom:15px;
    color:white;
    font-size:20px;
    font-weight:bold;
}

.btn-plus{
    width:35px;
    height:35px;
    cursor:pointer;
}

.resultado{
    min-width:40px;
    text-align:center;
}

.resultado-final{
    position:absolute;
    bottom:165px; /* ajustar según tu diseño */
    left:50%;
    transform:translateX(-50%);
    width:120px;
    height:50px;
    display:flex;
    justify-content:center;
    align-items:center;
    font-size:28px;
    font-weight:bold;
    color:#1677D8;
}

</style>
</head>

<body>

<div class="calculadora">

    <div class="fila">
        <span>1 pt</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn-plus"
            onclick="sumar(1)"
        >

        <span id="res1" class="resultado">0</span>
    </div>

    <div class="fila">
        <span>2 pts</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn-plus"
            onclick="sumar(2)"
        >

        <span id="res2" class="resultado">0</span>
    </div>

    <div class="fila">
        <span>3 pts</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn-plus"
            onclick="sumar(3)"
        >

        <span id="res3" class="resultado">0</span>
    </div>

</div>

<div id="resultadoFinal" class="resultado-final">
    0
</div>

<script>

let cantidad1 = 0;
let cantidad2 = 0;
let cantidad3 = 0;

function sumar(tipo){

    if(tipo === 1){
        cantidad1++;
        document.getElementById("res1").innerHTML = cantidad1 * 1;
    }

    if(tipo === 2){
        cantidad2++;
        document.getElementById("res2").innerHTML = cantidad2 * 2;
    }

    if(tipo === 3){
        cantidad3++;
        document.getElementById("res3").innerHTML = cantidad3 * 3;
    }

    actualizarTotal();
}

function actualizarTotal(){

    const total =
        (cantidad1 * 1) +
        (cantidad2 * 2) +
        (cantidad3 * 3);

    document.getElementById("resultadoFinal").innerHTML = total;
}

</script>

</body>
</html>

----

<style>
.calculadora{
    position:absolute;
    top:220px;
    left:50%;
    transform:translateX(-50%);
    width:250px;
}

.fila{
    display:flex;
    align-items:center;
    justify-content:space-between;
    margin-bottom:15px;
    color:white;
    font-size:20px;
    font-weight:bold;
}

.btn{
    width:35px;
    height:35px;
    cursor:pointer;
}

.resultado{
    min-width:40px;
    text-align:center;
}

.resultado-final{
    position:absolute;
    bottom:165px;
    left:50%;
    transform:translateX(-50%);
    width:120px;
    height:50px;
    display:flex;
    justify-content:center;
    align-items:center;
    font-size:28px;
    font-weight:bold;
    color:#1677D8;
}
</style>

<div class="calculadora">

    <div class="fila">
        <span>1 pt</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn"
            onclick="sumar(1)"
        >

        <img
            src="https://cdn-icons-png.flaticon.com/512/1828/1828899.png"
            class="btn"
            onclick="restar(1)"
        >

        <span id="res1" class="resultado">0</span>
    </div>

    <div class="fila">
        <span>2 pts</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn"
            onclick="sumar(2)"
        >

        <img
            src="https://cdn-icons-png.flaticon.com/512/1828/1828899.png"
            class="btn"
            onclick="restar(2)"
        >

        <span id="res2" class="resultado">0</span>
    </div>

    <div class="fila">
        <span>3 pts</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn"
            onclick="sumar(3)"
        >

        <img
            src="https://cdn-icons-png.flaticon.com/512/1828/1828899.png"
            class="btn"
            onclick="restar(3)"
        >

        <span id="res3" class="resultado">0</span>
    </div>

</div>

<div id="resultadoFinal" class="resultado-final">0</div>

<script>
let cantidad1 = 0;
let cantidad2 = 0;
let cantidad3 = 0;

function sumar(tipo){

    if(tipo === 1){
        cantidad1++;
        document.getElementById("res1").innerHTML = cantidad1 * 1;
    }

    if(tipo === 2){
        cantidad2++;
        document.getElementById("res2").innerHTML = cantidad2 * 2;
    }

    if(tipo === 3){
        cantidad3++;
        document.getElementById("res3").innerHTML = cantidad3 * 3;
    }

    actualizarTotal();
}

function restar(tipo){

    if(tipo === 1 && cantidad1 > 0){
        cantidad1--;
        document.getElementById("res1").innerHTML = cantidad1 * 1;
    }

    if(tipo === 2 && cantidad2 > 0){
        cantidad2--;
        document.getElementById("res2").innerHTML = cantidad2 * 2;
    }

    if(tipo === 3 && cantidad3 > 0){
        cantidad3--;
        document.getElementById("res3").innerHTML = cantidad3 * 3;
    }

    actualizarTotal();
}

function actualizarTotal(){

    const total =
        (cantidad1 * 1) +
        (cantidad2 * 2) +
        (cantidad3 * 3);

    document.getElementById("resultadoFinal").innerHTML = total;
}
</script>
$$$

<style>
.calculadora{
    position:absolute;
    top:220px;
    left:50%;
    transform:translateX(-50%);
    width:250px;
}

.fila{
    display:flex;
    align-items:center;
    justify-content:space-between;
    margin-bottom:15px;
    color:white;
    font-size:20px;
    font-weight:bold;
}

.btn{
    width:35px;
    height:35px;
    cursor:pointer;
}

.resultado{
    min-width:60px;
    text-align:center;
}

.resultado-final{
    position:absolute;
    bottom:165px;
    left:50%;
    transform:translateX(-50%);
    width:120px;
    height:50px;
    display:flex;
    justify-content:center;
    align-items:center;
    font-size:28px;
    font-weight:bold;
    color:#1677D8;
}
</style>

<div class="calculadora">

    <div class="fila">
        <span>1 pt</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn"
            onclick="sumar(1); brazeBridge.logClick('TU_EVENTO');"
        >

        <img
            src="https://cdn-icons-png.flaticon.com/512/1828/1828899.png"
            class="btn"
            onclick="restar(1); brazeBridge.logClick('TU_EVENTO');"
        >

        <span id="res1" class="resultado">0 pts</span>
    </div>

    <div class="fila">
        <span>2 pts</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn"
            onclick="sumar(2); brazeBridge.logClick('TU_EVENTO');"
        >

        <img
            src="https://cdn-icons-png.flaticon.com/512/1828/1828899.png"
            class="btn"
            onclick="restar(2); brazeBridge.logClick('TU_EVENTO');"
        >

        <span id="res2" class="resultado">0 pts</span>
    </div>

    <div class="fila">
        <span>3 pts</span>

        <img
            src="https://cdn-icons-png.flaticon.com/512/748/748113.png"
            class="btn"
            onclick="sumar(3); brazeBridge.logClick('TU_EVENTO');"
        >

        <img
            src="https://cdn-icons-png.flaticon.com/512/1828/1828899.png"
            class="btn"
            onclick="restar(3); brazeBridge.logClick('TU_EVENTO');"
        >

        <span id="res3" class="resultado">0 pts</span>
    </div>

</div>

<div id="resultadoFinal" class="resultado-final">0</div>

<script>
let cantidad1 = 0;
let cantidad2 = 0;
let cantidad3 = 0;

function sumar(tipo){

    if(tipo === 1){
        cantidad1++;
        document.getElementById("res1").innerHTML = (cantidad1 * 1) + " pts";
    }

    if(tipo === 2){
        cantidad2++;
        document.getElementById("res2").innerHTML = (cantidad2 * 2) + " pts";
    }

    if(tipo === 3){
        cantidad3++;
        document.getElementById("res3").innerHTML = (cantidad3 * 3) + " pts";
    }

    actualizarTotal();
}

function restar(tipo){

    if(tipo === 1 && cantidad1 > 0){
        cantidad1--;
        document.getElementById("res1").innerHTML = (cantidad1 * 1) + " pts";
    }

    if(tipo === 2 && cantidad2 > 0){
        cantidad2--;
        document.getElementById("res2").innerHTML = (cantidad2 * 2) + " pts";
    }

    if(tipo === 3 && cantidad3 > 0){
        cantidad3--;
        document.getElementById("res3").innerHTML = (cantidad3 * 3) + " pts";
    }

    actualizarTotal();
}

function actualizarTotal(){

    const total =
        (cantidad1 * 1) +
        (cantidad2 * 2) +
        (cantidad3 * 3);

    document.getElementById("resultadoFinal").innerHTML = total;
}
</script>

/////
<!-- ========================================= -->
<!-- 1. AGREGAR AL FINAL DEL <style> -->
<!-- ========================================= -->

.opcion {
  border: 3px solid transparent;
  border-radius: 12px;
  box-sizing: border-box;
  cursor: pointer;
}

.opcion.seleccionada {
  border: 3px solid #ffffff;
  box-shadow: 0 0 10px rgba(255,255,255,0.8);
}

.cta-deshabilitado {
  opacity: 0.5;
  pointer-events: none;
}


<!-- ========================================= -->
<!-- 2. REEMPLAZAR IMG_FLO -->
<!-- ========================================= -->

<img
  src="https://braze-images.com/appboy/communication/assets/image_assets/images/69c44d1c7c3b750063f7ba93/original.png?1774472476"
  alt="Ilustración"
  class="img_flo opcion"
  onclick="
    seleccionarOpcion(this);

    brazeBridge.logClick('body_clic_cta1');

    brazeBridge.logCustomEvent('Interaccion',{
      inapp_id:'TCACT-RENOSTCR-M-inapp_renosestrellas_202603_26',
      action:'body_clic_cta1'
    });
  "
>


<!-- ========================================= -->
<!-- 3. REEMPLAZAR IMG_FLO2 -->
<!-- ========================================= -->

<img
  src="https://braze-images.com/appboy/communication/assets/image_assets/images/69c45a4c01c0790063c9907c/original.png?1774475851"
  alt="Ilustración"
  class="img_flo2 anim1 opcion"
  onclick="
    seleccionarOpcion(this);

    brazeBridge.logClick('body_clic_cta2todo');

    brazeBridge.logCustomEvent('Interaccion',{
      inapp_id:'TCACT-RENOSTCR-M-inapp_renosestrellas_202603_26',
      action:'body_clic_cta2todo'
    });
  "
>


<!-- ========================================= -->
<!-- 4. MODIFICAR EL <a> DE IMG_FLOU -->
<!-- ========================================= -->

<a
  href="bgeneralprod://personal/credit-card/renewal-form"
  class="full-background cta-deshabilitado"
  id="ctaFinal"
>


<!-- ========================================= -->
<!-- 5. AGREGAR ANTES DE </body> -->
<!-- ========================================= -->

<script>

function seleccionarOpcion(elemento) {

  document.querySelectorAll('.opcion').forEach(op => {
    op.classList.remove('seleccionada');
  });

  elemento.classList.add('seleccionada');

  document.getElementById('ctaFinal')
          .classList.remove('cta-deshabilitado');
}

</script>

2828

<!-- CTA -->
<div class="cta-container">

  <button class="cta-btn" id="ctaBtn"
    onclick="brazeBridge.logClick('0');brazeBridge.logCustomEvent('Interaccion',{inapp_id:'TXN-panapass-M-mix_propension nba_no trx_promo_202604_17-30',action:'cta_principal'});handleClick();">
    Descubre tu sorpresa
  </button>

  <button class="cta-btn" id="ctaBtn2"
    style="display:none;"
    onclick="brazeBridge.logClick('1');brazeBridge.logCustomEvent('Interaccion',{inapp_id:'TXN-panapass-M-mix_propension nba_no trx_promo_202604_17-30',action:'cta_secundario'});window.location.href='https://tusitio.com';">
    Ver más detalles
  </button>

</div>

<style>
.cta-container {
  position: absolute;
  bottom: 58px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.show-btn {
  animation: fadeInUp .8s ease forwards;
}
</style>

<script>

let step = 1;

function handleClick() {

  const image = document.getElementById("mainImage");
  const button = document.getElementById("ctaBtn");

  if (step === 1) {

    if (window.brazeBridge) {

      brazeBridge.logCustomEvent('Interaccion',{
        inapp_id: 'TXN-panapass-M-mix_propension nba_no trx_promo_202604_17-30',
        action: 'body_clic1'
      });

    }

    setTimeout(() => {

      const contenedor = document.getElementById("contenedor");

      contenedor.innerHTML = `

<div>  
  <img
    src="https://braze-images.com/appboy/communication/assets/image_assets/images/69a70a907a9974006339836f/original.png?1772554895"
    alt="Ilustración"
    class="img_flo7 anim1">
</div>

<div>  
  <img
    src="https://braze-images.com/appboy/communication/assets/image_assets/images/69a70a907a9974006339836f/original.png?1772554895"
    alt="Ilustración"
    class="img_flo8 anim1">
</div>

<div>  
  <img
    src="https://braze-images.com/appboy/communication/assets/image_assets/images/69a70a907a9974006339836f/original.png?1772554895"
    alt="Ilustración"
    class="img_flo9 anim1">
</div>

<div>  
  <img
    src="https://braze-images.com/appboy/communication/assets/image_assets/images/69a70a907a9974006339836f/original.png?1772554895"
    alt="Ilustración"
    class="img_flo4 anim1">
</div>

<div>  
  <img
    src="https://braze-images.com/appboy/communication/assets/image_assets/images/69a70a907a9974006339836f/original.png?1772554895"
    alt="Ilustración"
    class="img_flo5 anim1">
</div>

<div>  
  <img
    src="https://braze-images.com/appboy/communication/assets/image_assets/images/69a70a907a9974006339836f/original.png?1772554895"
    alt="Ilustración"
    class="img_flo6 anim1">
</div>

      `;

    }, 2000);

    image.src = "https://braze-images.com/appboy/communication/assets/image_assets/images/69e0f34d25f02100ade007de/original.gif?1776350029";

    button.textContent = "¡Quiero recargar!";

    const secondBtn = document.getElementById("ctaBtn2");

    button.style.display = "none";
    secondBtn.style.display = "none";

    setTimeout(() => {
      button.style.display = "block";
      button.classList.add("show-btn");
    }, 2000);

    setTimeout(() => {
      secondBtn.style.display = "block";
      secondBtn.classList.add("show-btn");
    }, 3000);

    step = 2;

  } else {

    if (window.brazeBridge) {

      brazeBridge.logCustomEvent('Interaccion',{
        inapp_id: 'TXN-panapass-M-mix_propension nba_no trx_promo_202604_17-30',
        action: 'body_clic2'
      });

    }

    window.location.href = "bgeneralprod://personal/transactions/recharges";

  }

}

</script>

8282
// CAMBIA EL ONCLICK DEL CTA PRINCIPAL A:
onclick="brazeBridge.logClick('0');handleClick()"


// DENTRO DE handleClick(), BUSCA ESTA LÍNEA:
button.textContent = "¡Quiero recargar!";


// Y DEBAJO AGREGA ESTO:

setTimeout(() => {

  const contenedor = document.getElementById("contenedor");

  contenedor.innerHTML += `
    <div style="
      position:absolute;
      bottom:15px;
      width:100%;
      display:flex;
      justify-content:center;
    ">
      <button
        id="ctaBtn2"
        class="cta-btn"
        onclick="
          brazeBridge.logClick('1');
          brazeBridge.logCustomEvent('Interaccion',{
            inapp_id:'TXN-panapass-M-mix_propension nba_no trx_promo_202604_17-30',
            action:'cta_hazloahora'
          });
          window.location.href='bgeneralprod://personal/transactions/recharges';
        ">
        Hazlo ahora
      </button>
    </div>
  `;

}, 3000);


// Y REEMPLAZA EL ELSE COMPLETO POR ESTE:

} else {

  if (window.brazeBridge) {

    brazeBridge.logClick('2');

    brazeBridge.logCustomEvent('Interaccion', {
      inapp_id: 'TXN-panapass-M-mix_propension nba_no trx_promo_202604_17-30',
      action: 'cta_recargar'
    });

  }

  window.location.href = "bgeneralprod://personal/transactions/recharges";

}
99
setTimeout(() => {

  const contenedor = document.getElementById("contenedor");

  contenedor.innerHTML += `
    <div id="cta2Container" style="
      position:absolute;
      bottom:15px;
      width:100%;
      display:flex;
      justify-content:center;">
      <button id="ctaBtn2" class="cta-btn">
        Hazlo ahora
      </button>
    </div>
  `;

  document.getElementById("ctaBtn2").onclick = function() {

    if(window.brazeBridge){
      brazeBridge.logClick('1');
      brazeBridge.logCustomEvent('Interaccion',{
        inapp_id:'TXN-panapass-M-mix_propension nba_no trx_promo_202604_17-30',
        action:'cta_hazloahora'
      });
    }

    window.location.href = "bgeneralprod://personal/transactions/recharges";
  };

}, 3000);


2828


<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
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

/* CONTENEDOR PRINCIPAL */
.inapp-container {
    position: relative;
    width: 330px;
    height: 600px;

    background-image: url('https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b36df5371e80088e84731/original.png?1786459870');

    background-size: cover;
    background-position: center;

    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);

    overflow: hidden;
    color: #1677D8;
}


/* BOTÓN CERRAR */
.close-button {
    position: absolute;
    top: 12px;
    right: 12px;

    color: rgb(0, 0, 0);
    background: transparent;

    border: none;
    border-radius: 50%;

    width: 28px;
    height: 28px;

    font-size: 18px;
    font-weight: bold;

    cursor: pointer;
    z-index: 100;

    line-height: 28px;
    text-align: center;
}


/* =========================
   PESTAÑAS
   ========================= */

.tabs {
    position: absolute;

    top: 70px;
    left: 15px;

    width: 300px;

    display: flex;
    justify-content: center;
    gap: 5px;

    z-index: 50;
}


/* BOTONES DE LAS PESTAÑAS */

.tab-button {
    flex: 1;

    height: 38px;

    border: none;
    border-radius: 8px;

    background-color: rgba(255,255,255,0.75);

    color: #004c97;

    font-size: 11px;
    font-weight: bold;

    cursor: pointer;

    transition: all 0.2s ease;
}


/* PESTAÑA ACTIVA */

.tab-button.active {
    background-color: #004c97;
    color: white;
}


/* =========================
   CONTENEDOR DE SECCIONES
   ========================= */

.secciones {
    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;
}


/* TODAS LAS SECCIONES */

.seccion {
    display: none;

    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;
}


/* SECCIÓN ACTIVA */

.seccion.active {
    display: block;
}


/* =========================
   IMÁGENES
   ========================= */

.imagen-seccion {
    position: absolute;

    width: 85%;
    height: 55px;

    right: 25px;

    object-fit: contain;

    cursor: pointer;
}


/* POSICIONES */

.img-servicios {
    bottom: 340px;
}

.img-recargas {
    bottom: 270px;
}

.img-pagos {
    bottom: 202px;
}

.img-otros {
    bottom: 135px;
}


/* =========================
   TEXTO
   ========================= */

.Texto-abajo {
    position: absolute;

    bottom: 120px;

    width: 100%;

    text-align: center;

    font-size: 24px;
    font-weight: bold;

    color: #ffffff;

    font-family: 'Inter', sans-serif;
}


/* =========================
   ANIMACIÓN
   ========================= */

@keyframes money {

    0% {
        opacity: 0;
        transform: translateY(-380px);
    }

    7% {
        opacity: 1;
    }

    50% {
        opacity: 1;
    }

    100% {
        opacity: 1;
        transform: translateY(1000px);
    }
}


.anim1 {
    animation: money 20s ease-in forwards infinite;
}


/* =========================
   ANIMACIÓN BOTONES
   ========================= */

@keyframes bounceInOut {

    0% {
        transform: translate(0);
    }

    25% {
        transform: translateX(-2px);
    }

    50% {
        transform: translateX(2px);
    }

    75% {
        transform: translateX(-2px);
    }

    100% {
        transform: translateX(0px);
    }

}


.anim7 {
    animation: bounceInOut 1.0s infinite;
}

</style>
</head>


<body>


<div class="inapp-container">


    <!-- =========================
         BOTÓN CERRAR
         ========================= -->

    <button
        class="close-button"
        onclick='
            brazeBridge.logClick("Close Message");
            brazeBridge.closeMessage();
        '>
        X
    </button>



    <!-- =========================
         PESTAÑAS
         ========================= -->

    <div class="tabs">

        <button
            class="tab-button active"
            onclick="mostrarSeccion('servicios', this)">
            Servicios
        </button>

        <button
            class="tab-button"
            onclick="mostrarSeccion('recargas', this)">
            Recargas
        </button>

        <button
            class="tab-button"
            onclick="mostrarSeccion('pagos', this)">
            Pagos
        </button>

        <button
            class="tab-button"
            onclick="mostrarSeccion('otros', this)">
            Otros
        </button>

    </div>



    <!-- =========================
         SECCIONES
         ========================= -->

    <div class="secciones">



        <!-- =========================
             SERVICIOS
             ========================= -->

        <div
            id="servicios"
            class="seccion active">

            <a
                href="bgeneralprod://personal/transactions/payment">

                <img
                    src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b37d881f9f7008694f97e/original.png?1786460119"

                    alt="Servicios"

                    class="imagen-seccion img-servicios"

                    onclick="
                        brazeBridge.logClick('0');

                        brazeBridge.logCustomEvent(
                            'Interaccion',
                            {
                                inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                                action: 'body_clic_cta1'
                            }
                        );
                    "
                >

            </a>

        </div>



        <!-- =========================
             RECARGAS
             ========================= -->

        <div
            id="recargas"
            class="seccion">

            <a
                href="bgeneralprod://personal/transactions/recharges">

                <img
                    src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b383a4225d5008ac8a9d9/original.png?1786460217"

                    alt="Recargas"

                    class="imagen-seccion img-recargas"

                    onclick="
                        brazeBridge.logClick('1');

                        brazeBridge.logCustomEvent(
                            'Interaccion',
                            {
                                inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                                action: 'body_clic_cta2'
                            }
                        );
                    "
                >

            </a>

        </div>



        <!-- =========================
             PAGOS
             ========================= -->

        <div
            id="pagos"
            class="seccion">

            <a
                href="bgeneralprod://personal/transactions/recharges">

                <img
                    src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b38a8e1eaff008816b13e/original.png?1786460328"

                    alt="Pagos"

                    class="imagen-seccion img-pagos"

                    onclick="
                        brazeBridge.logClick('2');

                        brazeBridge.logCustomEvent(
                            'Interaccion',
                            {
                                inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                                action: 'body_clic_cta3'
                            }
                        );
                    "
                >

            </a>

        </div>



        <!-- =========================
             OTROS
             ========================= -->

        <div
            id="otros"
            class="seccion">

            <a
                href="bgeneralprod://authentication/ypmodule-access">

                <img
                    src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b38dea2e4b00088dc216b/original.png?1786460382"

                    alt="Otros"

                    class="imagen-seccion img-otros"

                    onclick="
                        brazeBridge.logClick('3');

                        brazeBridge.logCustomEvent(
                            'Interaccion',
                            {
                                inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                                action: 'body_clic_cta4'
                            }
                        );
                    "
                >

            </a>

        </div>


    </div>


</div>



<!-- =========================
     JAVASCRIPT
     ========================= -->

<script>

function mostrarSeccion(nombre, boton) {

    /*
     * Ocultar todas las secciones
     */

    var secciones = document.querySelectorAll('.seccion');

    secciones.forEach(function(seccion) {

        seccion.classList.remove('active');

    });



    /*
     * Quitar estado activo
     * de todos los botones
     */

    var botones = document.querySelectorAll('.tab-button');

    botones.forEach(function(btn) {

        btn.classList.remove('active');

    });



    /*
     * Mostrar la sección seleccionada
     */

    var seccionSeleccionada =
        document.getElementById(nombre);

    if (seccionSeleccionada) {

        seccionSeleccionada.classList.add('active');

    }



    /*
     * Activar el botón seleccionado
     */

    if (boton) {

        boton.classList.add('active');

    }

}

</script>


</body>
</html>

+++

ˢᵐ
℠

08 17
/* =========================
   PESTAÑAS COMO IMÁGENES
   ========================= */

.tabs {
    position: absolute;
    top: 70px;
    left: 15px;

    width: 300px;

    display: flex;
    justify-content: center;
    gap: 5px;

    z-index: 50;
}

/* BOTÓN DE CADA PESTAÑA */
.tab-button {
    position: relative;

    flex: 1;
    height: 38px;

    padding: 0;
    border: none;
    border-radius: 8px;

    background: transparent;

    cursor: pointer;

    overflow: hidden;

    transition: all 0.2s ease;
}

/* IMAGEN DE LA PESTAÑA */
.tab-button img {
    display: block;

    width: 100%;
    height: 100%;

    object-fit: cover;

    border-radius: 8px;
}

/* OVERLAY DE LA PESTAÑA */
.tab-button .tab-overlay {
    position: absolute;

    top: 0;
    left: 0;

    width: 100%;
    height: 100%;

    background-color: rgba(0, 76, 151, 0.55);

    border-radius: 8px;

    opacity: 0;

    pointer-events: none;

    transition: opacity 0.2s ease;
}

/* OVERLAY DE LA PESTAÑA ACTIVA */
.tab-button.active .tab-overlay {
    opacity: 1;
}

<div class="tabs">

    <!-- =========================
         EL MACHETAZO
         ========================= -->

    <button
        class="tab-button active"
        onclick="
            brazeBridge.logClick('0');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta1'
                }
            );

            mostrarSeccion('servicios', this);
        "
    >

        <img
            src="URL_IMAGEN_MACHETAZO"
            alt="El Machetazo"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         BARRIO PIZZA
         ========================= -->

    <button
        class="tab-button"
        onclick="
            brazeBridge.logClick('1');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta2'
                }
            );

            mostrarSeccion('recargas', this);
        "
    >

        <img
            src="URL_IMAGEN_BARRIO_PIZZA"
            alt="Barrio Pizza"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         DOIT CENTER
         ========================= -->

    <button
        class="tab-button"
        onclick="
            brazeBridge.logClick('2');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta3'
                }
            );

            mostrarSeccion('pagos', this);
        "
    >

        <img
            src="URL_IMAGEN_DOIT_CENTER"
            alt="Doit Center"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         OTROS
         ========================= -->

    <button
        class="tab-button"
        onclick="
            brazeBridge.logClick('3');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta4'
                }
            );

            mostrarSeccion('otros', this);
        "
    >

        <img
            src="URL_IMAGEN_OTROS"
            alt="Otros"
        >

        <span class="tab-overlay"></span>

    </button>

</div>

/* =========================
   IMÁGENES DE LAS SECCIONES
   ========================= */

.imagen-seccion,
.imagen-seccion2,
.imagen-seccion3,
.imagen-seccion4 {
    position: absolute;

    width: 85%;
    height: 80px;

    object-fit: contain;

    cursor: pointer;

    z-index: 10;
}

/* POSICIÓN DE LAS IMÁGENES */

.img-servicios {
    bottom: 340px;
    left: 7.5%;
}

.img-recargas {
    bottom: 270px;
    left: 7.5%;
}

.img-pagos {
    bottom: 202px;
    left: 7.5%;
}

.img-otros {
    bottom: 135px;
    left: 7.5%;
}


.secciones {
    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;

    z-index: 5;
}

.seccion {
    display: none;

    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;
}

.seccion.active {
    display: block;
}


17 08

<!DOCTYPE html>
<html lang="es">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Mensaje In-App</title>

<style>

/* =========================
   BODY
   ========================= */

body {
    margin: 0;
    background-color: rgba(0, 0, 0, 0.7);

    display: flex;
    justify-content: center;
    align-items: center;

    height: 100vh;

    font-family: 'Inter', sans-serif;
}


/* =========================
   CONTENEDOR PRINCIPAL
   ========================= */

.inapp-container {
    position: relative;

    width: 330px;
    height: 600px;

    background-image: url('https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b36df5371e80088e84731/original.png?1786459870');

    background-size: cover;
    background-position: center;

    border-radius: 8px;

    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);

    overflow: hidden;

    color: #1677D8;
}


/* =========================
   BOTÓN CERRAR
   ========================= */

.close-button {
    position: absolute;

    top: 12px;
    right: 12px;

    color: rgb(0, 0, 0);

    border: none;
    border-radius: 50%;

    width: 28px;
    height: 28px;

    font-size: 18px;
    font-weight: bold;

    cursor: pointer;

    line-height: 28px;
    text-align: center;

    text-decoration: none;

    z-index: 100;
}


/* =========================
   PESTAÑAS
   ========================= */

.tabs {
    position: absolute;

    top: 70px;
    left: 15px;

    width: 300px;

    display: flex;
    justify-content: center;

    gap: 5px;

    z-index: 50;
}


/* =========================
   BOTÓN DE CADA PESTAÑA
   ========================= */

.tab-button {
    position: relative;

    flex: 1;

    height: 38px;

    padding: 0;

    border: none;
    border-radius: 8px;

    background: transparent;

    cursor: pointer;

    overflow: hidden;

    transition: all 0.2s ease;
}


/* =========================
   IMAGEN DE LA PESTAÑA
   ========================= */

.tab-button img {
    display: block;

    width: 100%;
    height: 100%;

    object-fit: cover;

    border-radius: 8px;
}


/* =========================
   OVERLAY
   ========================= */

/* Las pestañas NO activas tienen overlay */

.tab-button .tab-overlay {
    position: absolute;

    top: 0;
    left: 0;

    width: 100%;
    height: 100%;

    background-color: rgba(0, 76, 151, 0.55);

    border-radius: 8px;

    opacity: 1;

    pointer-events: none;

    transition: opacity 0.2s ease;
}


/* =========================
   PESTAÑA ACTIVA
   ========================= */

/* La pestaña activa NO tiene overlay */

.tab-button.active .tab-overlay {
    opacity: 0;
}


/* =========================
   CONTENEDOR DE SECCIONES
   ========================= */

.secciones {
    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;

    z-index: 5;
}


/* =========================
   TODAS LAS SECCIONES
   ========================= */

.seccion {
    display: none;

    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;
}


/* =========================
   SECCIÓN ACTIVA
   ========================= */

.seccion.active {
    display: block;
}


/* =========================
   IMÁGENES DE LAS SECCIONES
   ========================= */

.imagen-seccion {
    position: absolute;

    width: 85%;
    height: 80px;

    object-fit: contain;

    cursor: pointer;

    z-index: 10;
}


/* =========================
   PRIMERA IMAGEN
   ========================= */

.imagen-1 {
    left: 7.5%;
    bottom: 340px;
}


/* =========================
   SEGUNDA IMAGEN
   ========================= */

.imagen-2 {
    left: 7.5%;
    bottom: 245px;
}


/* =========================
   TEXTO
   ========================= */

.Texto-abajo {
    position: absolute;

    bottom: 120px;

    width: 100%;

    text-align: center;

    font-size: 24px;
    font-weight: bold;

    color: #ffffff;

    font-family: 'Inter', sans-serif;
}


/* =========================
   ANIMACIÓN MONEY
   ========================= */

@keyframes money {

    0% {
        opacity: 0;
        transform: translateY(-380px);
    }

    7% {
        opacity: 1;
    }

    50% {
        opacity: 1;
    }

    100% {
        opacity: 1;
        transform: translateY(1000px);
    }
}


.anim1 {
    animation: money 20s ease-in forwards infinite;
}


/* =========================
   ANIMACIÓN BOTONES
   ========================= */

@keyframes bounceInOut {

    0% {
        transform: translate(0);
    }

    25% {
        transform: translateX(-2px);
    }

    50% {
        transform: translateX(2px);
    }

    75% {
        transform: translateX(-2px);
    }

    100% {
        transform: translateX(0px);
    }
}


.anim7 {
    animation: bounceInOut 1.0s infinite;
}

</style>

</head>


<body>


<div class="inapp-container">


<!-- =========================
     BOTÓN CERRAR
     ========================= -->

<button
    class="close-button"
    onclick='
        brazeBridge.logClick("Close Message");
        brazeBridge.closeMessage();
    '>
    X
</button>


<!-- =========================
     PESTAÑAS
     ========================= -->

<div class="tabs">


    <!-- =========================
         EL MACHETAZO
         ========================= -->

    <button
        class="tab-button active"

        onclick="
            brazeBridge.logClick('0');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta1'
                }
            );

            mostrarSeccion('servicios', this);
        "
    >

        <img
            src="URL_IMAGEN_MACHETAZO"
            alt="El Machetazo"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         BARRIO PIZZA
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('1');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta2'
                }
            );

            mostrarSeccion('recargas', this);
        "
    >

        <img
            src="URL_IMAGEN_BARRIO_PIZZA"
            alt="Barrio Pizza"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         DOIT CENTER
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('2');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta3'
                }
            );

            mostrarSeccion('pagos', this);
        "
    >

        <img
            src="URL_IMAGEN_DOIT_CENTER"
            alt="Doit Center"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         OTROS
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('3');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta4'
                }
            );

            mostrarSeccion('otros', this);
        "
    >

        <img
            src="URL_IMAGEN_OTROS"
            alt="Otros"
        >

        <span class="tab-overlay"></span>

    </button>


</div>


<!-- =========================
     SECCIONES
     ========================= -->

<div class="secciones">


    <!-- =========================
         SERVICIOS
         ========================= -->

    <div
        id="servicios"
        class="seccion active"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/payment"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c8f315d9faf00a3b8e27c/original.png?1786548017"

                alt="Servicios"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('0');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta1'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/payment"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c8f315d9faf00a3b8e27c/original.png?1786548017"

                alt="Servicios"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('0');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta1'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         RECARGAS
         ========================= -->

    <div
        id="recargas"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c91eaad10e300a37133e3/original.png?1786548713"

                alt="Recargas"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('1');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta2'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c91eaad10e300a37133e3/original.png?1786548713"

                alt="Recargas"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('1');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta2'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         PAGOS
         ========================= -->

    <div
        id="pagos"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c928d40e7cb00a15bb632/original.png?1786548877"

                alt="Pagos"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('2');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta3'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c928d40e7cb00a15bb632/original.png?1786548877"

                alt="Pagos"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('2');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta3'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         OTROS
         ========================= -->

    <div
        id="otros"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://authentication/ypmodule-access"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b38dea2e4b00088dc216b/original.png?1786460382"

                alt="Otros"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('3');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta4'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://authentication/ypmodule-access"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b38dea2e4b00088dc216b/original.png?1786460382"

                alt="Otros"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('3');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta4'
                        }
                    );
                "
            >

        </a>

    </div>


</div>


</div>


<!-- =========================
     JAVASCRIPT
     ========================= -->

<script>

function mostrarSeccion(nombre, boton) {

    /* =========================
       OCULTAR TODAS LAS SECCIONES
       ========================= */

    var secciones =
        document.querySelectorAll('.seccion');

    secciones.forEach(function(seccion) {

        seccion.classList.remove('active');

    });


    /* =========================
       QUITAR ACTIVE DE TODOS
       ========================= */

    var botones =
        document.querySelectorAll('.tab-button');

    botones.forEach(function(btn) {

        btn.classList.remove('active');

    });


    /* =========================
       MOSTRAR SECCIÓN
       ========================= */

    var seccionSeleccionada =
        document.getElementById(nombre);

    if (seccionSeleccionada) {

        seccionSeleccionada.classList.add('active');

    }


    /* =========================
       ACTIVAR PESTAÑA
       ========================= */

    if (boton) {

        boton.classList.add('active');

    }

}

</script>


</body>

</html>



<!DOCTYPE html>

<html lang="es">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Mensaje In-App</title>

<style>

/* =========================
   BODY
   ========================= */

body {
    margin: 0;
    background-color: rgba(0, 0, 0, 0.7);

    display: flex;
    justify-content: center;
    align-items: center;

    height: 100vh;

    font-family: 'Inter', sans-serif;
}


/* =========================
   CONTENEDOR PRINCIPAL
   ========================= */

.inapp-container {
    position: relative;

    width: 330px;
    height: 600px;

    background-image: url('https://braze-images.com/appboy/communication/assets/image_assets/images/6a833de868c06600863a4c85/original.png?1786985957');

    background-size: cover;
    background-position: center;

    border-radius: 8px;

    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);

    overflow: hidden;

    color: #1677D8;
}


/* =========================
   BOTÓN CERRAR
   ========================= */

.close-button {
    position: absolute;

    top: 12px;
    right: 12px;

    color: rgb(0, 0, 0);

    border: none;
    border-radius: 50%;

    width: 28px;
    height: 28px;

    font-size: 18px;
    font-weight: bold;

    cursor: pointer;

    line-height: 28px;
    text-align: center;

    text-decoration: none;

    z-index: 100;
}


/* =========================
   PESTAÑAS SUPERIORES
   ========================= */

.tabs {
    position: absolute;

    top: 70px;
    left: 15px;

    width: 300px;

    display: grid;

    /*
       6 columnas para poder
       centrar las 2 de abajo
    */
    grid-template-columns: repeat(6, 1fr);

    gap: 5px;

    z-index: 50;
}


/* =========================
   POSICIÓN DE LAS 5 PESTAÑAS
   ========================= */

/* 1 - ARRIBA */

.tabs .tab-button:nth-child(1) {
    grid-column: 1 / span 2;
}


/* 2 - ARRIBA */

.tabs .tab-button:nth-child(2) {
    grid-column: 3 / span 2;
}


/* 3 - ARRIBA */

.tabs .tab-button:nth-child(3) {
    grid-column: 5 / span 2;
}


/* 4 - ABAJO */

.tabs .tab-button:nth-child(4) {
    grid-column: 2 / span 2;
}


/* 5 - ABAJO */

.tabs .tab-button:nth-child(5) {
    grid-column: 4 / span 2;
}


/* =========================
   BOTÓN DE CADA PESTAÑA
   ========================= */

.tab-button {
    position: relative;

    width: 85px;
    height: 68px;

    padding: 0;

    border: none;

    background: transparent;

    cursor: pointer;

    overflow: hidden;

    transition: all 0.2s ease;
}


/* =========================
   IMAGEN DE LA PESTAÑA
   ========================= */

.tab-button img {
    display: block;

    width: 100%;
    height: 100%;

    object-fit: cover;

    border-radius: 8px;
}


/* =========================
   OVERLAY
   ========================= */

/* Las pestañas NO activas tienen overlay */

.tab-button .tab-overlay {
    position: absolute;

    top: 0;
    left: 0;

    width: 100%;
    height: 100%;

    background-color: rgba(0, 76, 151, 0.55);

    border-radius: 8px;

    opacity: 1;

    pointer-events: none;

    transition: opacity 0.2s ease;
}


/* =========================
   PESTAÑA ACTIVA
   ========================= */

/* La pestaña activa NO tiene overlay */

.tab-button.active .tab-overlay {
    opacity: 0;
}


/* =========================
   CONTENEDOR DE SECCIONES
   ========================= */

.secciones {
    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;

    z-index: 5;
}


/* =========================
   TODAS LAS SECCIONES
   ========================= */

.seccion {
    display: none;

    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;
}


/* =========================
   SECCIÓN ACTIVA
   ========================= */

.seccion.active {
    display: block;
}


/* =========================
   IMÁGENES DE LAS SECCIONES
   ========================= */

.imagen-seccion {
    position: absolute;

    width: 85%;
    height: 80px;

    object-fit: contain;

    cursor: pointer;

    z-index: 10;
}


/* =========================
   PRIMERA IMAGEN
   ========================= */

.imagen-1 {
    left: 7.5%;
    bottom: 140px;
}


/* =========================
   SEGUNDA IMAGEN
   ========================= */

.imagen-2 {
    left: 7.5%;
    bottom: 245px;
}


/* =========================
   TEXTO
   ========================= */

.Texto-abajo {
    position: absolute;

    bottom: 120px;

    width: 100%;

    text-align: center;

    font-size: 24px;
    font-weight: bold;

    color: #ffffff;

    font-family: 'Inter', sans-serif;
}


/* =========================
   ANIMACIÓN MONEY
   ========================= */

@keyframes money {

    0% {
        opacity: 0;
        transform: translateY(-380px);
    }

    7% {
        opacity: 1;
    }

    50% {
        opacity: 1;
    }

    100% {
        opacity: 1;
        transform: translateY(1000px);
    }
}


/* =========================
   ANIMACIÓN BOTONES
   ========================= */

@keyframes bounceInOut {

    0% {
        transform: translate(0);
    }

    25% {
        transform: translateX(-2px);
    }

    50% {
        transform: translateX(2px);
    }

    75% {
        transform: translateX(-2px);
    }

    100% {
        transform: translateX(0px);
    }

}


.anim7 {
    animation: bounceInOut 1.0s infinite;
}

</style>

</head>


<body>


<div class="inapp-container">


<!-- =========================
     BOTÓN CERRAR
     ========================= -->

<button
    class="close-button"

    onclick="
        brazeBridge.logClick('Close Message');
        brazeBridge.closeMessage();
    "
>
    X
</button>


<!-- =========================
     PESTAÑAS SUPERIORES
     ========================= -->

<div class="tabs">


    <!-- =========================
         PESTAÑA 1
         EL MACHETAZO
         ========================= -->

    <button
        class="tab-button active"

        onclick="
            brazeBridge.logClick('0');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta1'
                }
            );

            mostrarSeccion('servicios', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833e1ed430280086b7a09c/original.png?1786986013"

            alt="El Machetazo"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         PESTAÑA 2
         BARRIO PIZZA
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('1');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta2'
                }
            );

            mostrarSeccion('recargas', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833e5ae3320b0086e69f29/original.png?1786986074"

            alt="Barrio Pizza"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         PESTAÑA 3
         DOIT CENTER
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('2');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta3'
                }
            );

            mostrarSeccion('pagos', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833e8c367a6f008857f2b0/original.png?1786986123"

            alt="Doit Center"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         PESTAÑA 4
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('3');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta4'
                }
            );

            mostrarSeccion('otros', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833eb38f4996008ac8bbf8/original.png?1786986162"

            alt="Otros"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         PESTAÑA 5
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('3');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta4'
                }
            );

            mostrarSeccion('otros', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833f0d14d132008a624a36/original.png?1786986253"

            alt="Otros"
        >

        <span class="tab-overlay"></span>

    </button>


</div>


<!-- =========================
     SECCIONES
     ========================= -->

<div class="secciones">


    <!-- =========================
         SERVICIOS
         ========================= -->

    <div
        id="servicios"
        class="seccion active"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/payment"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c8f315d9faf00a3b8e27c/original.png?1786548017"

                alt="Servicios"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('0');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta1'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/payment"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c8f315d9faf00a3b8e27c/original.png?1786548017"

                alt="Servicios"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('0');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta1'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         RECARGAS
         ========================= -->

    <div
        id="recargas"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c91eaad10e300a37133e3/original.png?1786548713"

                alt="Recargas"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('1');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta2'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c91eaad10e300a37133e3/original.png?1786548713"

                alt="Recargas"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('1');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta2'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         PAGOS
         ========================= -->

    <div
        id="pagos"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c928d40e7cb00a15bb632/original.png?1786548877"

                alt="Pagos"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('2');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta3'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c928d40e7cb00a15bb632/original.png?1786548877"

                alt="Pagos"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('2');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta3'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         OTROS
         ========================= -->

    <div
        id="otros"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://authentication/ypmodule-access"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b38dea2e4b00088dc216b/original.png?1786460382"

                alt="Otros"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('3');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta4'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://authentication/ypmodule-access"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b38dea2e4b00088dc216b/original.png?1786460382"

                alt="Otros"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('3');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta4'
                        }
                    );
                "
            >

        </a>

    </div>


</div>


</div>


<!-- =========================
     JAVASCRIPT
     ========================= -->

<script>

function mostrarSeccion(nombre, boton) {


    /* =========================
       OCULTAR TODAS LAS SECCIONES
       ========================= */

    var secciones =
        document.querySelectorAll('.seccion');

    secciones.forEach(function(seccion) {

        seccion.classList.remove('active');

    });


    /* =========================
       QUITAR ACTIVE DE TODOS
       ========================= */

    var botones =
        document.querySelectorAll('.tab-button');

    botones.forEach(function(btn) {

        btn.classList.remove('active');

    });


    /* =========================
       MOSTRAR SECCIÓN
       ========================= */

    var seccionSeleccionada =
        document.getElementById(nombre);

    if (seccionSeleccionada) {

        seccionSeleccionada.classList.add('active');

    }


    /* =========================
       ACTIVAR PESTAÑA
       ========================= */

    if (boton) {

        boton.classList.add('active');

    }

}

</script>


</body>

</html>

2108
<!DOCTYPE html>

<html lang="es">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Mensaje In-App</title>

<style>

/* =========================
   BODY
   ========================= */

body {
    margin: 0;
    background-color: rgba(0, 0, 0, 0.7);

    display: flex;
    justify-content: center;
    align-items: center;

    height: 100vh;

    font-family: 'Inter', sans-serif;
}


/* =========================
   CONTENEDOR PRINCIPAL
   ========================= */

.inapp-container {
    position: relative;

    width: 330px;
    height: 600px;

    background-image: url('https://braze-images.com/appboy/communication/assets/image_assets/images/6a833de868c06600863a4c85/original.png?1786985957');

    background-size: cover;
    background-position: center;

    border-radius: 8px;

    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);

    overflow: hidden;

    color: #1677D8;
}


/* =========================
   BOTÓN CERRAR
   ========================= */

.close-button {
    position: absolute;

    top: 12px;
    right: 12px;

    color: rgb(0, 0, 0);

    border: none;
    border-radius: 50%;

    width: 28px;
    height: 28px;

    font-size: 18px;
    font-weight: bold;

    cursor: pointer;

    line-height: 28px;
    text-align: center;

    text-decoration: none;

    z-index: 100;
}


/* =========================
   PESTAÑAS
   ========================= */

.tabs {
    position: absolute;

    top: 70px;
    left: 15px;

    width: 300px;

    display: grid;

    grid-template-columns: repeat(6, 1fr);

    gap: 5px;

    z-index: 50;
}


/* =========================
   3 PESTAÑAS ARRIBA
   ========================= */

.tabs .tab-button:nth-child(1) {
    grid-column: 1 / span 2;
}

.tabs .tab-button:nth-child(2) {
    grid-column: 3 / span 2;
}

.tabs .tab-button:nth-child(3) {
    grid-column: 5 / span 2;
}


/* =========================
   2 PESTAÑAS ABAJO
   ========================= */

.tabs .tab-button:nth-child(4) {
    grid-column: 2 / span 2;
}

.tabs .tab-button:nth-child(5) {
    grid-column: 4 / span 2;
}


/* =========================
   BOTÓN DE CADA PESTAÑA
   ========================= */

.tab-button {
    position: relative;

    width: 85px;
    height: 68px;

    padding: 0;

    border: none;

    background: transparent;

    cursor: pointer;

    overflow: hidden;

    transition: all 0.2s ease;
}


/* =========================
   IMAGEN DE LA PESTAÑA
   ========================= */

.tab-button img {
    display: block;

    width: 100%;
    height: 100%;

    object-fit: cover;

    border-radius: 8px;
}


/* =========================
   OVERLAY
   ========================= */

/* Todas las pestañas comienzan
   con overlay */

.tab-button .tab-overlay {
    position: absolute;

    top: 0;
    left: 0;

    width: 100%;
    height: 100%;

    background-color: rgba(0, 76, 151, 0.55);

    border-radius: 8px;

    opacity: 1;

    pointer-events: none;

    transition: opacity 0.2s ease;
}


/* =========================
   PESTAÑA ACTIVA
   ========================= */

/* La pestaña activa no tiene overlay */

.tab-button.active .tab-overlay {
    opacity: 0;
}


/* =========================
   IMAGEN INICIAL
   ========================= */

.intro {
    position: absolute;

    top: 0;
    left: 0;

    width: 100%;
    height: 100%;

    display: flex;

    justify-content: center;
    align-items: center;

    z-index: 20;
}


/* =========================
   IMAGEN ILUSTRATIVA
   ========================= */

.imagen-intro {
    width: 90%;
    height: auto;

    object-fit: contain;
}


/* =========================
   CONTENEDOR DE SECCIONES
   ========================= */

.secciones {
    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;

    z-index: 5;
}


/* =========================
   TODAS LAS SECCIONES
   ========================= */

.seccion {
    display: none;

    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;
}


/* =========================
   SECCIÓN ACTIVA
   ========================= */

.seccion.active {
    display: block;
}


/* =========================
   IMÁGENES DE LAS SECCIONES
   ========================= */

.imagen-seccion {
    position: absolute;

    width: 85%;
    height: 80px;

    object-fit: contain;

    cursor: pointer;

    z-index: 10;
}


/* =========================
   PRIMERA IMAGEN
   ========================= */

.imagen-1 {
    left: 7.5%;
    bottom: 140px;
}


/* =========================
   SEGUNDA IMAGEN
   ========================= */

.imagen-2 {
    left: 7.5%;
    bottom: 245px;
}


/* =========================
   TEXTO
   ========================= */

.Texto-abajo {
    position: absolute;

    bottom: 120px;

    width: 100%;

    text-align: center;

    font-size: 24px;
    font-weight: bold;

    color: #ffffff;

    font-family: 'Inter', sans-serif;
}


/* =========================
   ANIMACIÓN MONEY
   ========================= */

@keyframes money {

    0% {
        opacity: 0;
        transform: translateY(-380px);
    }

    7% {
        opacity: 1;
    }

    50% {
        opacity: 1;
    }

    100% {
        opacity: 1;
        transform: translateY(1000px);
    }

}


/* =========================
   ANIMACIÓN BOTONES
   ========================= */

@keyframes bounceInOut {

    0% {
        transform: translate(0);
    }

    25% {
        transform: translateX(-2px);
    }

    50% {
        transform: translateX(2px);
    }

    75% {
        transform: translateX(-2px);
    }

    100% {
        transform: translateX(0px);
    }

}

.anim7 {
    animation: bounceInOut 1.0s infinite;
}

</style>

</head>


<body>


<div class="inapp-container">


<!-- =========================
     BOTÓN CERRAR
     ========================= -->

<button
    class="close-button"

    onclick="
        brazeBridge.logClick('Close Message');
        brazeBridge.closeMessage();
    "
>
    X
</button>


<!-- =========================
     PESTAÑAS
     ========================= -->

<div class="tabs">


    <!-- =========================
         PESTAÑA 1
         EL MACHETAZO
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('0');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta1'
                }
            );

            mostrarSeccion('servicios', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833e1ed430280086b7a09c/original.png?1786986013"

            alt="El Machetazo"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         PESTAÑA 2
         BARRIO PIZZA
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('1');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta2'
                }
            );

            mostrarSeccion('recargas', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833e5ae3320b0086e69f29/original.png?1786986074"

            alt="Barrio Pizza"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         PESTAÑA 3
         DOIT CENTER
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('2');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta3'
                }
            );

            mostrarSeccion('pagos', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833e8c367a6f008857f2b0/original.png?1786986123"

            alt="Doit Center"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         PESTAÑA 4
         OTROS
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('3');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta4'
                }
            );

            mostrarSeccion('otros', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833eb38f4996008ac8bbf8/original.png?1786986162"

            alt="Otros"
        >

        <span class="tab-overlay"></span>

    </button>


    <!-- =========================
         PESTAÑA 5
         ========================= -->

    <button
        class="tab-button"

        onclick="
            brazeBridge.logClick('3');

            brazeBridge.logCustomEvent(
                'Interaccion',
                {
                    inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                    action: 'body_clic_cta4'
                }
            );

            mostrarSeccion('otros', this);
        "
    >

        <img
            src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a833f0d14d132008a624a36/original.png?1786986253"

            alt="Otros"
        >

        <span class="tab-overlay"></span>

    </button>


</div>


<!-- =========================
     IMAGEN INICIAL
     ========================= -->

<div
    id="intro"
    class="intro"
>

    <img
        src=""
        alt="Imagen ilustrativa"
        class="imagen-intro"
    >

</div>


<!-- =========================
     SECCIONES
     ========================= -->

<div class="secciones">


    <!-- =========================
         SERVICIOS
         ========================= -->

    <div
        id="servicios"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/payment"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c8f315d9faf00a3b8e27c/original.png?1786548017"

                alt="Servicios"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('0');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta1'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/payment"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c8f315d9faf00a3b8e27c/original.png?1786548017"

                alt="Servicios"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('0');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta1'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         RECARGAS
         ========================= -->

    <div
        id="recargas"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c91eaad10e300a37133e3/original.png?1786548713"

                alt="Recargas"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('1');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta2'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c91eaad10e300a37133e3/original.png?1786548713"

                alt="Recargas"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('1');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta2'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         PAGOS
         ========================= -->

    <div
        id="pagos"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c928d40e7cb00a15bb632/original.png?1786548877"

                alt="Pagos"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('2');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta3'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://personal/transactions/recharges"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7c928d40e7cb00a15bb632/original.png?1786548877"

                alt="Pagos"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('2');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta3'
                        }
                    );
                "
            >

        </a>

    </div>


    <!-- =========================
         OTROS
         ========================= -->

    <div
        id="otros"
        class="seccion"
    >

        <!-- PRIMERA IMAGEN -->

        <a
            href="bgeneralprod://authentication/ypmodule-access"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b38dea2e4b00088dc216b/original.png?1786460382"

                alt="Otros"

                class="imagen-seccion imagen-1"

                onclick="
                    brazeBridge.logClick('3');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta4'
                        }
                    );
                "
            >

        </a>


        <!-- SEGUNDA IMAGEN -->

        <a
            href="bgeneralprod://authentication/ypmodule-access"
        >

            <img
                src="https://braze-images.com/appboy/communication/assets/image_assets/images/6a7b38dea2e4b00088dc216b/original.png?1786460382"

                alt="Otros"

                class="imagen-seccion imagen-2"

                onclick="
                    brazeBridge.logClick('3');

                    brazeBridge.logCustomEvent(
                        'Interaccion',
                        {
                            inapp_id: 'TXN-canal digital-A-mix_bienvenida_202608_12',
                            action: 'body_clic_cta4'
                        }
                    );
                "
            >

        </a>

    </div>


</div>


</div>


<!-- =========================
     JAVASCRIPT
     ========================= -->

<script>

function mostrarSeccion(nombre, boton) {


    /* =========================
       OCULTAR IMAGEN INICIAL
       ========================= */

    var intro =
        document.getElementById('intro');

    if (intro) {

        intro.style.display = 'none';

    }


    /* =========================
       OCULTAR TODAS LAS SECCIONES
       ========================= */

    var secciones =
        document.querySelectorAll('.seccion');

    secciones.forEach(function(seccion) {

        seccion.classList.remove('active');

    });


    /* =========================
       QUITAR ACTIVE DE TODOS
       ========================= */

    var botones =
        document.querySelectorAll('.tab-button');

    botones.forEach(function(btn) {

        btn.classList.remove('active');

    });


    /* =========================
       MOSTRAR SECCIÓN
       ========================= */

    var seccionSeleccionada =
        document.getElementById(nombre);

    if (seccionSeleccionada) {

        seccionSeleccionada.classList.add('active');

    }


    /* =========================
       ACTIVAR PESTAÑA
       ========================= */

    if (boton) {

        boton.classList.add('active');

    }

}

</script>


</body>

</html>

