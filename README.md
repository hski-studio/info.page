<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>hski.studio — Diseño para redes que se nota</title>
<style>
  :root{
    --paper:#d9dad5;
    --paper-2:#cfd0ca;
    --ink:#39383a;
    --violet:#5B5380;
    --lilac:#A09AC7;
    --yellow:#F9E19E;
    --gold:#DBBE75;

    --font-display: Impact, 'Arial Narrow Bold', 'Helvetica Neue', Arial, sans-serif;
    --font-body: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
    --font-mono: ui-monospace, 'SF Mono', 'Roboto Mono', Menlo, Consolas, monospace;

    --fs-hero: clamp(2.6rem, 10vw, 7.4rem);
    --fs-h2: clamp(1.9rem, 4.4vw, 3.2rem);
    --fs-lead: clamp(1.05rem, 2vw, 1.35rem);

    --pad: clamp(1.25rem, 5vw, 4rem);
    --radius: 2px;
  }

  *,*::before,*::after{ box-sizing:border-box; }
  html{ scroll-behavior:smooth; }
  body{
    margin:0;
    background:var(--paper);
    color:var(--ink);
    font-family:var(--font-body);
    -webkit-font-smoothing:antialiased;
    overflow-x:hidden;
  }

  ::selection{ background:var(--violet); color:var(--paper); }

  a{ color:inherit; }

  :focus-visible{
    outline:2px solid var(--violet);
    outline-offset:3px;
  }

  /* --- paper grain overlay --- */
  .grain{
    position:fixed; inset:0;
    pointer-events:none;
    z-index:999;
    opacity:0.05;
    mix-blend-mode:multiply;
  }

  /* --- dot-grid background pattern --- */
  .dotgrid{
    background-image: radial-gradient(var(--lilac) 1px, transparent 1px);
    background-size: 26px 26px;
    background-position: -6px -6px;
  }

  /* ============ HEADER ============ */
  header{
    position:fixed; top:0; left:0; right:0;
    z-index:100;
    display:flex; align-items:center; justify-content:space-between;
    padding: 1.1rem var(--pad);
    background:rgba(217,218,213,0.86);
    backdrop-filter: blur(6px);
    border-bottom:1px solid rgba(57,56,58,0.12);
  }
  .logo{
    font-family:var(--font-display);
    text-transform:uppercase;
    letter-spacing:-0.02em;
    font-size:1.15rem;
    font-weight:400;
    display:flex; align-items:baseline; gap:0.35rem;
  }
  .logo .dot{ color:var(--gold); }

  nav.desktop-nav{ display:flex; gap:2rem; }
  nav.desktop-nav a{
    font-family:var(--font-mono);
    font-size:0.78rem;
    text-transform:uppercase;
    letter-spacing:0.06em;
    text-decoration:none;
    position:relative;
    padding-bottom:3px;
  }
  nav.desktop-nav a::after{
    content:'';
    position:absolute; left:0; bottom:0;
    width:0; height:1.5px;
    background:var(--violet);
    transition:width .25s ease;
  }
  nav.desktop-nav a:hover::after{ width:100%; }

  .menu-btn{
    display:none;
    background:none; border:none;
    width:34px; height:26px;
    position:relative;
    cursor:pointer;
    padding:0;
  }
  .menu-btn span{
    position:absolute; left:0; right:0;
    height:2px; background:var(--ink);
    transition: transform .3s ease, opacity .3s ease, top .3s ease;
  }
  .menu-btn span:nth-child(1){ top:2px; }
  .menu-btn span:nth-child(2){ top:12px; }
  .menu-btn span:nth-child(3){ top:22px; }
  .menu-btn.open span:nth-child(1){ top:12px; transform:rotate(45deg); }
  .menu-btn.open span:nth-child(2){ opacity:0; }
  .menu-btn.open span:nth-child(3){ top:12px; transform:rotate(-45deg); }

  .mobile-nav{
    position:fixed; inset:0;
    background:var(--violet);
    color:var(--paper);
    z-index:90;
    display:flex; flex-direction:column;
    align-items:flex-start;
    justify-content:center;
    gap:1.6rem;
    padding: 2rem var(--pad);
    transform:translateY(-100%);
    transition:transform .45s cubic-bezier(.65,0,.35,1);
  }
  .mobile-nav.open{ transform:translateY(0); }
  .mobile-nav a{
    font-family:var(--font-display);
    text-transform:uppercase;
    font-size:clamp(1.8rem,8vw,3rem);
    text-decoration:none;
    letter-spacing:-0.01em;
  }

  /* ============ HERO ============ */
  .hero{
    min-height:100vh;
    display:flex; flex-direction:column;
    justify-content:center;
    padding: 6rem var(--pad) 3rem;
    position:relative;
    overflow:hidden;
  }
  .hero-eyebrow{
    font-family:var(--font-mono);
    font-size:0.78rem;
    letter-spacing:0.12em;
    text-transform:uppercase;
    color:var(--violet);
    margin-bottom:1.1rem;
    display:flex; align-items:center; gap:0.6rem;
  }
  .hero-eyebrow::before{
    content:'';
    width:8px; height:8px;
    background:var(--gold);
    border-radius:50%;
    display:inline-block;
  }
  h1.hero-title{
    font-family:var(--font-display);
    text-transform:uppercase;
    font-size:var(--fs-hero);
    line-height:0.92;
    letter-spacing:-0.02em;
    margin:0 0 1.4rem;
    color:var(--ink);
    max-width:16ch;
  }
  h1.hero-title .accent{ color:var(--violet); }

  .typed-line{
    font-family:var(--font-mono);
    font-size:var(--fs-lead);
    max-width:38ch;
    min-height:2.6em;
    color:var(--ink);
  }
  .typed-line .cursor{
    display:inline-block;
    width:0.55ch;
    background:var(--violet);
    margin-left:2px;
    animation: blink 1s step-end infinite;
  }
  @keyframes blink{ 50%{ opacity:0; } }

  .hero-sub{
    margin-top:1.6rem;
    font-size:1.05rem;
    max-width:46ch;
    color:rgba(57,56,58,0.82);
  }

  .hero-ctas{
    margin-top:2.4rem;
    display:flex; flex-wrap:wrap; gap:1rem;
  }

  .btn{
    font-family:var(--font-mono);
    font-size:0.85rem;
    text-transform:uppercase;
    letter-spacing:0.05em;
    text-decoration:none;
    padding:0.95rem 1.6rem;
    border-radius:var(--radius);
    display:inline-block;
    transition: transform .18s ease, box-shadow .18s ease;
    cursor:pointer;
    border:1.5px solid var(--ink);
    background:transparent;
    color:var(--ink);
  }
  .btn:hover{ transform:translate(-2px,-2px); box-shadow:3px 3px 0 var(--ink); }
  .btn-primary{
    background:var(--violet);
    border-color:var(--violet);
    color:var(--paper);
  }
  .btn-primary:hover{ box-shadow:3px 3px 0 var(--gold); }

  .btn-stamp.stamped{
    animation: stamp .32s ease;
  }
  @keyframes stamp{
    0%{ transform:scale(1) rotate(0); }
    35%{ transform:scale(0.9) rotate(-3deg); }
    100%{ transform:scale(1) rotate(0); }
  }

  .scanline{
    position:absolute; left:0; right:0; height:2px;
    background:linear-gradient(90deg, transparent, var(--lilac), transparent);
    opacity:0.5;
    top:20%;
    animation: scan 7s linear infinite;
    pointer-events:none;
  }
  @keyframes scan{
    0%{ top:10%; opacity:0; }
    10%{ opacity:0.5; }
    90%{ opacity:0.5; }
    100%{ top:92%; opacity:0; }
  }

  .scroll-cue{
    position:absolute; bottom:2rem; left:var(--pad);
    font-family:var(--font-mono);
    font-size:0.7rem;
    letter-spacing:0.08em;
    text-transform:uppercase;
    color:rgba(57,56,58,0.55);
    display:flex; align-items:center; gap:0.5rem;
  }
  .scroll-cue::after{
    content:'↓';
    animation: bob 1.6s ease-in-out infinite;
  }
  @keyframes bob{
    0%,100%{ transform:translateY(0); }
    50%{ transform:translateY(5px); }
  }

  /* ============ SECTION shared ============ */
  section{ padding: 5.5rem var(--pad); position:relative; scroll-margin-top:80px; }
  .section-head{ margin-bottom:2.8rem; max-width:60ch; }
  .section-tag{
    font-family:var(--font-mono);
    font-size:0.75rem;
    text-transform:uppercase;
    letter-spacing:0.1em;
    color:var(--violet);
    margin-bottom:0.7rem;
    display:block;
  }
  h2{
    font-family:var(--font-display);
    text-transform:uppercase;
    letter-spacing:-0.01em;
    font-size:var(--fs-h2);
    margin:0 0 0.8rem;
    line-height:1;
  }
  .section-desc{ font-size:1.02rem; color:rgba(57,56,58,0.78); }

  .reveal{
    opacity:0;
    transform:translateY(24px);
    transition: opacity .7s ease, transform .7s ease;
  }
  .reveal.is-visible{ opacity:1; transform:translateY(0); }

  /* ============ FICHERO (catalog carousel) ============ */
  .fichero-wrap{ position:relative; }
  .fichero-track{
    display:flex;
    gap:1.6rem;
    overflow-x:auto;
    scroll-snap-type:x proximity;
    padding: 1rem 0.2rem 2rem;
    cursor:grab;
    -ms-overflow-style:none;
    scrollbar-width:none;
    user-select:none;
  }
  .fichero-track::-webkit-scrollbar{ display:none; }
  .fichero-track.grabbing{ cursor:grabbing; }

  .ficha{
    scroll-snap-align:start;
    flex:0 0 auto;
    width:min(320px, 78vw);
    background: #eceee9;
    border:1.5px solid var(--ink);
    border-radius:var(--radius);
    padding:1.5rem 1.4rem 1.7rem;
    position:relative;
    transform-style:preserve-3d;
    transition: transform .25s ease, box-shadow .25s ease;
    will-change: transform;
  }
  .ficha:hover{ box-shadow:6px 6px 0 rgba(91,83,128,0.35); }
  .ficha::before{
    content:'';
    position:absolute; top:14px; left:14px;
    width:11px; height:11px;
    border-radius:50%;
    background:var(--paper);
    border:1.5px solid var(--ink);
  }
  .ficha-code{
    font-family:var(--font-mono);
    font-size:0.72rem;
    letter-spacing:0.05em;
    text-align:right;
    color:rgba(57,56,58,0.6);
    margin-bottom:1.6rem;
  }
  .ficha h3{
    font-family:var(--font-display);
    text-transform:uppercase;
    font-size:1.35rem;
    letter-spacing:-0.01em;
    margin:0 0 0.6rem;
  }
  .ficha p{ font-size:0.92rem; line-height:1.5; color:rgba(57,56,58,0.85); margin:0 0 1.2rem; }
  .sello{
    position:absolute; bottom:14px; right:14px;
    font-family:var(--font-mono);
    font-size:0.62rem;
    letter-spacing:0.08em;
    text-transform:uppercase;
    color:var(--gold);
    border:1.5px dashed var(--gold);
    border-radius:50%;
    width:56px; height:56px;
    display:flex; align-items:center; justify-content:center;
    text-align:center;
    transform:rotate(-14deg);
    line-height:1.05;
  }

  .fichero-hint{
    font-family:var(--font-mono);
    font-size:0.72rem;
    color:rgba(57,56,58,0.55);
    margin-top:0.6rem;
    display:flex; align-items:center; gap:0.5rem;
  }

  /* ============ PARA QUIÉN chips ============ */
  .chips{ display:flex; flex-wrap:wrap; gap:0.85rem; }
  .chip{
    font-family:var(--font-mono);
    font-size:0.85rem;
    padding:0.7rem 1.15rem;
    border-radius:999px;
    border:1.5px solid var(--ink);
    background:transparent;
    transition: background .2s ease, color .2s ease, transform .2s ease;
  }
  .chip:nth-child(4n+1){ background:var(--lilac); border-color:var(--lilac); }
  .chip:nth-child(4n+2){ background:var(--yellow); border-color:var(--yellow); }
  .chip:hover{ transform:rotate(-2deg) scale(1.03); }

  /* ============ PROCESO accordion ============ */
  .proceso-list{ border-top:1.5px solid var(--ink); }
  .proceso-item{ border-bottom:1.5px solid var(--ink); }
  .proceso-head{
    display:flex; align-items:center; gap:1.2rem;
    padding:1.3rem 0;
    cursor:pointer;
    background:none; border:none; width:100%;
    text-align:left;
    font-family:var(--font-body);
    color:var(--ink);
  }
  .proceso-code{
    font-family:var(--font-mono);
    font-size:0.85rem;
    color:var(--violet);
    flex:0 0 3.2rem;
  }
  .proceso-title{
    font-family:var(--font-display);
    text-transform:uppercase;
    font-size:clamp(1.15rem,2.6vw,1.6rem);
    letter-spacing:-0.01em;
    flex:1;
  }
  .proceso-icon{
    font-family:var(--font-mono);
    font-size:1.2rem;
    transition:transform .3s ease;
  }
  .proceso-item.open .proceso-icon{ transform:rotate(45deg); }
  .proceso-body{
    max-height:0;
    overflow:hidden;
    transition:max-height .35s ease;
  }
  .proceso-body p{
    padding: 0 0 1.4rem 4.4rem;
    max-width:60ch;
    font-size:0.95rem;
    color:rgba(57,56,58,0.8);
    margin:0;
  }

  /* ============ CTA / FOOTER ============ */
  .cta{
    background:var(--ink);
    color:var(--paper);
    text-align:left;
    padding-top:5rem;
    padding-bottom:2.5rem;
  }
  .cta h2{ color:var(--paper); max-width:14ch; }
  .cta .section-desc{ color:rgba(217,218,213,0.75); max-width:42ch; margin-bottom:2.2rem; }
  .cta .btn-primary{ background:var(--yellow); border-color:var(--yellow); color:var(--ink); }
  .cta .btn-primary:hover{ box-shadow:3px 3px 0 var(--lilac); }

  footer{
    margin-top:4rem;
    padding-top:1.6rem;
    border-top:1px solid rgba(217,218,213,0.25);
    display:flex; flex-wrap:wrap; gap:1.2rem;
    justify-content:space-between;
    align-items:center;
    font-family:var(--font-mono);
    font-size:0.78rem;
    color:rgba(217,218,213,0.6);
  }
  .social-links{ display:flex; gap:1.1rem; }
  .social-links a{ text-decoration:none; color:rgba(217,218,213,0.85); }
  .social-links a:hover{ color:var(--yellow); }

  @media (max-width: 760px){
    nav.desktop-nav{ display:none; }
    .menu-btn{ display:block; }
    .proceso-body p{ padding-left:0; }
    .proceso-code{ flex:0 0 2.4rem; }
  }

  @media (prefers-reduced-motion: reduce){
    *{ animation-duration:0.001ms !important; animation-iteration-count:1 !important; transition-duration:0.001ms !important; scroll-behavior:auto !important; }
  }
</style>
</head>
<body>

<svg class="grain" aria-hidden="true">
  <filter id="noise">
    <feTurbulence type="fractalNoise" baseFrequency="0.85" numOctaves="2" stitchTiles="stitch"></feTurbulence>
    <feColorMatrix type="saturate" values="0"></feColorMatrix>
  </filter>
  <rect width="100%" height="100%" filter="url(#noise)"></rect>
</svg>

<header>
  <div class="logo">hski<span class="dot">.</span>studio</div>
  <nav class="desktop-nav">
    <a href="#fichero">Fichero</a>
    <a href="#proceso">Proceso</a>
    <a href="#contacto">Contacto</a>
  </nav>
  <button class="menu-btn" id="menuBtn" aria-label="Abrir menú" aria-expanded="false">
    <span></span><span></span><span></span>
  </button>
</header>

<nav class="mobile-nav" id="mobileNav">
  <a href="#fichero">Fichero</a>
  <a href="#proceso">Proceso</a>
  <a href="#contacto">Contacto</a>
</nav>

<section class="hero dotgrid">
  <div class="scanline"></div>
  <span class="hero-eyebrow">Estudio de diseño — contenido para redes</span>
  <h1 class="hero-title">Tu marca,<br>bien <span class="accent">catalogada</span>.</h1>
  <p class="typed-line" id="typedLine"><span class="cursor">&nbsp;</span></p>
  <p class="hero-sub">Diseñamos piezas gráficas y gestionamos redes para negocios y emprendimientos que quieren dejar de improvisar el feed.</p>
  <div class="hero-ctas">
    <a href="#fichero" class="btn btn-primary">Ver el fichero</a>
    <a href="#contacto" class="btn">Escribinos</a>
  </div>
  <span class="scroll-cue">Desplegá el archivo</span>
</section>

<section id="fichero" class="reveal">
  <div class="section-head">
    <span class="section-tag">Archivo 01 — Servicios</span>
    <h2>El fichero</h2>
    <p class="section-desc">Cada servicio, catalogado como corresponde. Arrastrá para revisar el archivo completo.</p>
  </div>

  <div class="fichero-wrap">
    <div class="fichero-track" id="fichaTrack">
      <div class="ficha">
        <div class="ficha-code">FICHA N.º 01 / ARCHIVO: FEED</div>
        <h3>Piezas para redes</h3>
        <p>Posteos, carruseles e historias pensados para que tu feed deje de verse como relleno de último momento.</p>
        <div class="sello">HECHO<br>A MANO</div>
      </div>
      <div class="ficha">
        <div class="ficha-code">FICHA N.º 02 / ARCHIVO: GESTIÓN</div>
        <h3>Community management</h3>
        <p>Que alguien piense tu contenido con cabeza fría, no que lo improvise a las 23:50 del domingo.</p>
        <div class="sello">SIEMPRE<br>ACTIVO</div>
      </div>
      <div class="ficha">
        <div class="ficha-code">FICHA N.º 03 / ARCHIVO: IDENTIDAD</div>
        <h3>Identidad visual</h3>
        <p>Paletas, tipografías y un estilo propio que se reconozca aunque tapen el logo con el dedo.</p>
        <div class="sello">100%<br>ÚNICO</div>
      </div>
      <div class="ficha">
        <div class="ficha-code">FICHA N.º 04 / ARCHIVO: CALENDARIO</div>
        <h3>Estrategia de contenido</h3>
        <p>Calendarios y formatos claros: una excusa real para publicar seguido, y no cuando se acuerdan.</p>
        <div class="sello">ORDEN<br>REAL</div>
      </div>
    </div>
    <p class="fichero-hint">← desliza para ver el archivo completo →</p>
  </div>
</section>

<section class="dotgrid reveal">
  <div class="section-head">
    <span class="section-tag">Archivo 02 — Destinatarios</span>
    <h2>¿Para quién es esto?</h2>
    <p class="section-desc">Si tu feed te da un poco de vergüenza, seguí leyendo.</p>
  </div>
  <div class="chips">
    <span class="chip">Emprendedores primerizos</span>
    <span class="chip">Negocios de barrio</span>
    <span class="chip">Marcas que ya venden pero no se ven</span>
    <span class="chip">Community managers desbordados</span>
    <span class="chip">Empleadores que necesitan presencia</span>
    <span class="chip">Cualquiera cansado de Canva a las 2AM</span>
  </div>
</section>

<section id="proceso" class="reveal">
  <div class="section-head">
    <span class="section-tag">Archivo 03 — Método</span>
    <h2>Cómo se arma la ficha</h2>
    <p class="section-desc">Sin vueltas raras. Cuatro pasos, en orden, sin saltarse ninguno.</p>
  </div>
  <div class="proceso-list" id="procesoList">
    <div class="proceso-item open">
      <button class="proceso-head">
        <span class="proceso-code">A</span>
        <span class="proceso-title">Diagnóstico</span>
        <span class="proceso-icon">+</span>
      </button>
      <div class="proceso-body">
        <p>Miramos qué tenés, qué falta y qué está compitiendo contra vos sin que te des cuenta.</p>
      </div>
    </div>
    <div class="proceso-item">
      <button class="proceso-head">
        <span class="proceso-code">B</span>
        <span class="proceso-title">Boceto</span>
        <span class="proceso-icon">+</span>
      </button>
      <div class="proceso-body">
        <p>Proponemos una dirección visual concreta: paleta, tipografía y formatos, antes de producir nada.</p>
      </div>
    </div>
    <div class="proceso-item">
      <button class="proceso-head">
        <span class="proceso-code">C</span>
        <span class="proceso-title">Producción</span>
        <span class="proceso-icon">+</span>
      </button>
      <div class="proceso-body">
        <p>Se arman las piezas y el calendario. Vos revisás, ajustamos, y queda listo para publicar.</p>
      </div>
    </div>
    <div class="proceso-item">
      <button class="proceso-head">
        <span class="proceso-code">D</span>
        <span class="proceso-title">Entrega</span>
        <span class="proceso-icon">+</span>
      </button>
      <div class="proceso-body">
        <p>Te llega todo catalogado y listo para usar, con criterio para seguir solo si así lo preferís.</p>
      </div>
    </div>
  </div>
</section>

<section id="contacto" class="cta reveal">
  <span class="section-tag" style="color:var(--yellow)">Archivo 04 — Contacto</span>
  <h2>¿Hacemos que tu feed diga algo?</h2>
  <p class="section-desc">Contanos qué necesitás y armamos la primera ficha sin compromiso.</p>
  <a href="mailto:hola@hski.studio" class="btn btn-primary btn-stamp" id="stampBtn">Mandanos un mensaje</a>

  <footer>
    <span>hski.studio © 2026 — Todos los derechos catalogados</span>
    <div class="social-links">
      <a href="#" aria-label="Instagram">Instagram</a>
      <a href="#" aria-label="Behance">Behance</a>
      <a href="#" aria-label="WhatsApp">WhatsApp</a>
    </div>
  </footer>
</section>

<script>
(function(){
  var reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  /* ---- Typed tagline ---- */
  var typedEl = document.getElementById('typedLine');
  var text = "Diseñamos lo que tu marca todavía no sabe que necesita.";
  if(reduceMotion){
    typedEl.textContent = text;
  } else {
    var i = 0;
    var cursor = document.createElement('span');
    cursor.className = 'cursor';
    cursor.innerHTML = '&nbsp;';
    function typeNext(){
      if(i <= text.length){
        typedEl.textContent = text.slice(0, i);
        typedEl.appendChild(cursor);
        i++;
        setTimeout(typeNext, 32);
      }
    }
    typeNext();
  }

  /* ---- Mobile nav ---- */
  var menuBtn = document.getElementById('menuBtn');
  var mobileNav = document.getElementById('mobileNav');
  menuBtn.addEventListener('click', function(){
    var isOpen = mobileNav.classList.toggle('open');
    menuBtn.classList.toggle('open', isOpen);
    menuBtn.setAttribute('aria-expanded', isOpen);
  });
  mobileNav.querySelectorAll('a').forEach(function(a){
    a.addEventListener('click', function(){
      mobileNav.classList.remove('open');
      menuBtn.classList.remove('open');
      menuBtn.setAttribute('aria-expanded', 'false');
    });
  });

  /* ---- Scroll reveal ---- */
  var revealEls = document.querySelectorAll('.reveal');
  if('IntersectionObserver' in window){
    var io = new IntersectionObserver(function(entries){
      entries.forEach(function(entry){
        if(entry.isIntersecting){
          entry.target.classList.add('is-visible');
          io.unobserve(entry.target);
        }
      });
    }, { threshold: 0.15 });
    revealEls.forEach(function(el){ io.observe(el); });
  } else {
    revealEls.forEach(function(el){ el.classList.add('is-visible'); });
  }

  /* ---- Fichero: drag to scroll ---- */
  var track = document.getElementById('fichaTrack');
  var isDown = false, startX, scrollLeft;

  track.addEventListener('pointerdown', function(e){
    isDown = true;
    track.classList.add('grabbing');
    startX = e.pageX - track.offsetLeft;
    scrollLeft = track.scrollLeft;
  });
  window.addEventListener('pointerup', function(){
    isDown = false;
    track.classList.remove('grabbing');
  });
  track.addEventListener('pointermove', function(e){
    if(!isDown) return;
    e.preventDefault();
    var x = e.pageX - track.offsetLeft;
    var walk = (x - startX) * 1.2;
    track.scrollLeft = scrollLeft - walk;
  });

  /* ---- Fichero: tilt on hover ---- */
  if(!reduceMotion){
    track.querySelectorAll('.ficha').forEach(function(card){
      card.addEventListener('pointermove', function(e){
        var rect = card.getBoundingClientRect();
        var x = (e.clientX - rect.left) / rect.width - 0.5;
        var y = (e.clientY - rect.top) / rect.height - 0.5;
        card.style.transform = 'rotateY(' + (x * 8) + 'deg) rotateX(' + (y * -8) + 'deg) translateY(-2px)';
      });
      card.addEventListener('pointerleave', function(){
        card.style.transform = '';
      });
    });
  }

  /* ---- Proceso accordion ---- */
  var items = document.querySelectorAll('.proceso-item');
  function setBodyHeight(item, open){
    var body = item.querySelector('.proceso-body');
    body.style.maxHeight = open ? body.scrollHeight + 'px' : 0;
  }
  items.forEach(function(item){
    setBodyHeight(item, item.classList.contains('open'));
    item.querySelector('.proceso-head').addEventListener('click', function(){
      var willOpen = !item.classList.contains('open');
      items.forEach(function(other){
        other.classList.remove('open');
        setBodyHeight(other, false);
      });
      if(willOpen){
        item.classList.add('open');
        setBodyHeight(item, true);
      }
    });
  });
  window.addEventListener('resize', function(){
    items.forEach(function(item){
      if(item.classList.contains('open')) setBodyHeight(item, true);
    });
  });

  /* ---- Stamp button ---- */
  var stampBtn = document.getElementById('stampBtn');
  stampBtn.addEventListener('click', function(){
    stampBtn.classList.remove('stamped');
    void stampBtn.offsetWidth;
    stampBtn.classList.add('stamped');
  });
})();
</script>

</body>
</html>
