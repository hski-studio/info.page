<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>hski.studio — Diseño, redes y multimedia</title>
<style>
  :root{
    /* --- brand --- */
    --paper:#d9dad5;
    --ink:#39383a;
    --violet:#5B5380;
    --lilac:#A09AC7;
    --yellow:#F9E19E;
    --gold:#DBBE75;

    /* --- derived, for the collage skin --- */
    --bg-collage:#726d8c;          /* violeta aclarado, telón de fondo tipo escritorio */
    --bg-collage-2:#655f7d;
    --cream:#f3f1e8;               /* papel de las notas */
    --cream-2:#e9e6d8;
    --folder:var(--gold);
    --folder-dark:#c2a25f;
    --tape:#f6ecc9;

    --font-display: 'Segoe UI', Verdana, Arial, sans-serif;
    --font-script: Georgia, 'Times New Roman', 'Iowan Old Style', serif;
    --font-mono: ui-monospace, 'SF Mono', 'Roboto Mono', Menlo, Consolas, monospace;
    --font-body: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;

    --fs-hero: clamp(2.3rem, 7.5vw, 4.6rem);
    --fs-h2: clamp(1.7rem, 4vw, 2.6rem);
    --fs-lead: clamp(1rem, 1.8vw, 1.2rem);

    --pad: clamp(1.1rem, 5vw, 4rem);
    --radius: 3px;
  }

  *,*::before,*::after{ box-sizing:border-box; }
  html{ scroll-behavior:smooth; }
  body{
    margin:0;
    background:var(--bg-collage);
    background-image:
      radial-gradient(circle at 20% 15%, rgba(255,255,255,0.05), transparent 40%),
      radial-gradient(circle at 80% 60%, rgba(0,0,0,0.06), transparent 45%),
      url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120'%3E%3Cg fill='none' stroke='%23ffffff' stroke-opacity='0.045' stroke-width='1'%3E%3Ccircle cx='20' cy='20' r='10'/%3E%3Ccircle cx='90' cy='40' r='6'/%3E%3Ccircle cx='55' cy='90' r='14'/%3E%3Cpath d='M0 60 Q30 40 60 60 T120 60'/%3E%3C/g%3E%3C/svg%3E");
    background-blend-mode:normal;
    color:var(--ink);
    font-family:var(--font-body);
    -webkit-font-smoothing:antialiased;
    overflow-x:hidden;
  }

  ::selection{ background:var(--violet); color:var(--cream); }
  a{ color:inherit; }
  :focus-visible{ outline:2px solid var(--cream); outline-offset:3px; }

  .grain{ position:fixed; inset:0; pointer-events:none; z-index:999; opacity:0.045; mix-blend-mode:multiply; }

  /* ============ decorative bits ============ */
  .sparkle{
    position:absolute; width:20px; height:20px;
    color:var(--yellow);
    animation: twinkle 2.6s ease-in-out infinite;
    pointer-events:none;
  }
  .sparkle svg{ width:100%; height:100%; display:block; }
  .sparkle.s2{ animation-delay:.6s; color:var(--cream); }
  .sparkle.s3{ animation-delay:1.2s; }
  @keyframes twinkle{
    0%,100%{ opacity:0.25; transform:scale(0.8) rotate(0deg); }
    50%{ opacity:1; transform:scale(1.1) rotate(12deg); }
  }

  .scrap{
    position:absolute;
    background:var(--cream-2);
    box-shadow:0 6px 14px rgba(0,0,0,0.18);
    opacity:0.9;
    pointer-events:none;
    z-index:0;
  }

  .tape{
    position:absolute;
    width:74px; height:26px;
    background:linear-gradient(180deg, rgba(246,236,201,0.92), rgba(246,236,201,0.75));
    box-shadow:0 2px 4px rgba(0,0,0,0.12);
    opacity:0.85;
  }

  .clip{
    position:absolute;
    width:34px; height:52px;
    z-index:3;
  }
  .clip::before, .clip::after{
    content:'';
    position:absolute; left:50%;
    transform:translateX(-50%);
    border:3px solid var(--ink);
    border-radius:6px;
  }
  .clip::before{ width:22px; height:44px; top:0; }
  .clip::after{ width:12px; height:30px; top:0; border-color:var(--ink); background:transparent; }

  /* ============ HEADER ============ */
  header{
    position:fixed; top:0; left:0; right:0;
    z-index:100;
    display:flex; align-items:center; justify-content:space-between;
    padding: 1rem var(--pad);
    background:rgba(114,109,140,0.82);
    backdrop-filter: blur(6px);
    border-bottom:1px solid rgba(243,241,232,0.14);
  }
  .logo{
    font-family:var(--font-script);
    font-style:italic;
    font-weight:700;
    letter-spacing:-0.01em;
    font-size:1.25rem;
    color:var(--cream);
    display:flex; align-items:baseline; gap:0.3rem;
  }
  .logo .dot{ color:var(--yellow); }

  nav.desktop-nav{ display:flex; gap:2rem; }
  nav.desktop-nav a{
    font-family:var(--font-mono);
    font-size:0.76rem;
    text-transform:uppercase;
    letter-spacing:0.06em;
    text-decoration:none;
    color:var(--cream);
    position:relative;
    padding-bottom:3px;
  }
  nav.desktop-nav a::after{
    content:''; position:absolute; left:0; bottom:0; width:0; height:1.5px;
    background:var(--yellow); transition:width .25s ease;
  }
  nav.desktop-nav a:hover::after{ width:100%; }

  .menu-btn{ display:none; background:none; border:none; width:34px; height:26px; position:relative; cursor:pointer; padding:0; }
  .menu-btn span{ position:absolute; left:0; right:0; height:2px; background:var(--cream); transition: transform .3s ease, opacity .3s ease, top .3s ease; }
  .menu-btn span:nth-child(1){ top:2px; }
  .menu-btn span:nth-child(2){ top:12px; }
  .menu-btn span:nth-child(3){ top:22px; }
  .menu-btn.open span:nth-child(1){ top:12px; transform:rotate(45deg); }
  .menu-btn.open span:nth-child(2){ opacity:0; }
  .menu-btn.open span:nth-child(3){ top:12px; transform:rotate(-45deg); }

  .mobile-nav{
    position:fixed; inset:0; background:var(--violet); color:var(--cream); z-index:90;
    display:flex; flex-direction:column; align-items:flex-start; justify-content:center; gap:1.6rem;
    padding: 2rem var(--pad);
    transform:translateY(-100%);
    transition:transform .45s cubic-bezier(.65,0,.35,1);
  }
  .mobile-nav.open{ transform:translateY(0); }
  .mobile-nav a{
    font-family:var(--font-script); font-style:italic; font-weight:700;
    font-size:clamp(1.8rem,8vw,3rem); text-decoration:none;
  }

  /* ============ HERO — folder ============ */
  .hero{ min-height:100vh; display:flex; flex-direction:column; justify-content:center; align-items:center; padding: 7rem var(--pad) 3rem; position:relative; }

  .hero-eyebrow{
    font-family:var(--font-mono); font-size:0.72rem; letter-spacing:0.14em; text-transform:uppercase;
    color:rgba(243,241,232,0.75); margin-bottom:1.4rem;
  }

  .folder{
    position:relative;
    width:min(560px, 92vw);
    padding: 3.4rem 2rem 2.6rem;
    background:var(--folder);
    border-radius: 4px 14px 4px 4px;
    box-shadow: 0 22px 40px rgba(0,0,0,0.28);
  }
  .folder::before{ /* tab */
    content:'';
    position:absolute; top:-22px; left:8%;
    width:38%; height:26px;
    background:var(--folder);
    clip-path: polygon(6% 100%, 0 0, 88% 0, 100% 100%);
  }
  .folder-paper{
    position:absolute; top:-14px; left:6%; right:6%;
    height:46px;
    background:
      repeating-linear-gradient(var(--cream), var(--cream) 7px, #e3e0d2 8px);
    border-radius:2px 2px 0 0;
    box-shadow:0 -2px 0 rgba(0,0,0,0.05) inset;
    z-index:0;
  }
  .folder-inner{ position:relative; z-index:2; }

  .folder .paperclip{ position:absolute; top:-30px; right:10%; width:40px; height:74px; transform:rotate(8deg); z-index:4; }

  h1.hero-title{
    font-family:var(--font-display); font-weight:800;
    font-size:var(--fs-hero); line-height:1.02; letter-spacing:-0.01em;
    margin:0 0 0.3rem; color:var(--ink);
  }
  h1.hero-title .accent{
    display:block;
    font-family:var(--font-script); font-style:italic; font-weight:700;
    font-size:1.18em; color:var(--violet); margin-top:0.15em;
  }

  .typed-line{
    font-family:var(--font-mono); font-size:0.92rem; min-height:1.6em; margin-top:1.3rem; color:rgba(57,56,58,0.85);
  }
  .typed-line .cursor{ display:inline-block; width:0.55ch; background:var(--violet); margin-left:2px; animation: blink 1s step-end infinite; }
  @keyframes blink{ 50%{ opacity:0; } }

  .hero-sub{ margin-top:1.1rem; font-size:0.98rem; max-width:44ch; color:rgba(57,56,58,0.82); }

  .hero-ctas{ margin-top:1.8rem; display:flex; flex-wrap:wrap; gap:0.9rem; }

  .btn{
    font-family:var(--font-mono); font-size:0.82rem; text-transform:uppercase; letter-spacing:0.04em;
    text-decoration:none; padding:0.85rem 1.4rem; border-radius:var(--radius); display:inline-block;
    transition: transform .18s ease, box-shadow .18s ease; cursor:pointer;
    border:1.5px solid var(--ink); background:transparent; color:var(--ink);
  }
  .btn:hover{ transform:translate(-2px,-2px); box-shadow:3px 3px 0 var(--ink); }
  .btn-primary{ background:var(--violet); border-color:var(--violet); color:var(--cream); }
  .btn-primary:hover{ box-shadow:3px 3px 0 var(--ink); }
  .btn-stamp.stamped{ animation: stamp .32s ease; }
  @keyframes stamp{ 0%{ transform:scale(1) rotate(0); } 35%{ transform:scale(0.9) rotate(-3deg); } 100%{ transform:scale(1) rotate(0); } }

  .scroll-cue{
    margin-top:3rem;
    font-family:var(--font-mono); font-size:0.68rem; letter-spacing:0.08em; text-transform:uppercase;
    color:rgba(243,241,232,0.6); display:flex; align-items:center; gap:0.5rem;
  }
  .scroll-cue::after{ content:'↓'; animation: bob 1.6s ease-in-out infinite; }
  @keyframes bob{ 0%,100%{ transform:translateY(0); } 50%{ transform:translateY(5px); } }

  /* ============ SECTION shared ============ */
  section{ padding: 5rem var(--pad); position:relative; scroll-margin-top:80px; }
  .section-head{ margin-bottom:2.6rem; max-width:60ch; position:relative; }
  .section-tag{ font-family:var(--font-mono); font-size:0.72rem; text-transform:uppercase; letter-spacing:0.1em; color:var(--yellow); margin-bottom:0.6rem; display:block; }
  h2{ font-family:var(--font-display); font-weight:800; letter-spacing:-0.01em; font-size:var(--fs-h2); margin:0 0 0.6rem; line-height:1.05; color:var(--cream); }
  h2 em{ font-family:var(--font-script); font-style:italic; color:var(--yellow); }
  .section-desc{ font-size:1rem; color:rgba(243,241,232,0.78); }

  .reveal{ opacity:0; transform:translateY(24px); transition: opacity .7s ease, transform .7s ease; }
  .reveal.is-visible{ opacity:1; transform:translateY(0); }

  /* ============ FICHERO (notas de catálogo) ============ */
  .fichero-wrap{ position:relative; }
  .fichero-track{
    display:flex; gap:2.2rem; overflow-x:auto; overflow-y:visible;
    scroll-snap-type:x proximity; padding: 1.6rem 1rem 2.4rem; cursor:grab;
    -ms-overflow-style:none; scrollbar-width:none; user-select:none;
  }
  .fichero-track::-webkit-scrollbar{ display:none; }
  .fichero-track.grabbing{ cursor:grabbing; }

  .ficha{
    scroll-snap-align:start; flex:0 0 auto; width:min(300px, 76vw);
    background:var(--cream); border-radius:2px;
    padding:1.6rem 1.35rem 1.6rem;
    position:relative; transform-style:preserve-3d;
    transition: transform .25s ease, box-shadow .25s ease;
    will-change: transform;
    box-shadow:0 12px 26px rgba(0,0,0,0.22);
  }
  .ficha:nth-child(1){ transform:rotate(-2.2deg); }
  .ficha:nth-child(2){ transform:rotate(1.4deg); }
  .ficha:nth-child(3){ transform:rotate(-1deg); }
  .ficha:nth-child(4){ transform:rotate(2deg); }
  .ficha:hover{ box-shadow:0 18px 32px rgba(0,0,0,0.3); }

  .ficha .tape{ top:-14px; left:50%; transform:translateX(-50%) rotate(-3deg); }
  .ficha .clip{ top:-18px; right:14px; transform:rotate(-6deg); }

  .ficha-code{ font-family:var(--font-mono); font-size:0.68rem; letter-spacing:0.04em; color:rgba(57,56,58,0.5); margin-bottom:1.2rem; }
  .ficha h3{ font-family:var(--font-display); font-weight:800; font-size:1.2rem; letter-spacing:-0.01em; margin:0 0 0.55rem; color:var(--ink); }
  .ficha p{ font-size:0.9rem; line-height:1.5; color:rgba(57,56,58,0.85); margin:0 0 1rem; }
  .ficha .price{ font-family:var(--font-script); font-style:italic; font-weight:700; color:var(--violet); font-size:1.05rem; }

  .fichero-hint{ font-family:var(--font-mono); font-size:0.7rem; color:rgba(243,241,232,0.55); margin-top:0.4rem; text-align:center; }

  /* ============ PARA QUIÉN — notas sueltas ============ */
  .chips{ display:flex; flex-wrap:wrap; gap:1.4rem 1.1rem; }
  .chip{
    font-family:var(--font-mono); font-size:0.82rem; padding:0.9rem 1.2rem;
    background:var(--cream); color:var(--ink); border-radius:2px;
    box-shadow:0 8px 16px rgba(0,0,0,0.2);
    position:relative;
    transition: transform .2s ease;
  }
  .chip:nth-child(6n+1){ transform:rotate(-2deg); }
  .chip:nth-child(6n+2){ transform:rotate(1.6deg); background:var(--yellow); }
  .chip:nth-child(6n+3){ transform:rotate(-1deg); }
  .chip:nth-child(6n+4){ transform:rotate(2deg); background:var(--lilac); color:var(--cream); }
  .chip:nth-child(6n+5){ transform:rotate(-1.6deg); }
  .chip:hover{ transform:scale(1.05) rotate(0deg); }

  /* ============ PROCESO — fichas tipo carpeta con pestañas ============ */
  .proceso-list{ display:flex; flex-direction:column; gap:0.9rem; }
  .proceso-item{
    background:var(--cream); border-radius:2px; box-shadow:0 8px 18px rgba(0,0,0,0.2);
    position:relative; padding-left:3.6rem;
  }
  .proceso-item::before{
    content: attr(data-code);
    position:absolute; left:0; top:0; bottom:0; width:3.2rem;
    background:var(--folder-dark); color:var(--cream);
    display:flex; align-items:center; justify-content:center;
    font-family:var(--font-mono); font-weight:700; font-size:0.95rem;
    border-radius:2px 0 0 2px;
  }
  .proceso-head{
    display:flex; align-items:center; gap:1rem; padding:1.15rem 1.2rem;
    cursor:pointer; background:none; border:none; width:100%; text-align:left;
    font-family:var(--font-body); color:var(--ink);
  }
  .proceso-title{ font-family:var(--font-display); font-weight:800; font-size:clamp(1.05rem,2.4vw,1.35rem); letter-spacing:-0.01em; flex:1; }
  .proceso-icon{ font-family:var(--font-mono); font-size:1.15rem; transition:transform .3s ease; color:var(--violet); }
  .proceso-item.open .proceso-icon{ transform:rotate(45deg); }
  .proceso-body{ max-height:0; overflow:hidden; transition:max-height .35s ease; }
  .proceso-body p{ padding: 0 1.2rem 1.2rem; max-width:60ch; font-size:0.92rem; color:rgba(57,56,58,0.8); margin:0; }

  /* ============ CTA / FOOTER ============ */
  .cta{ padding-top:5rem; padding-bottom:2.5rem; }
  .cta-folder{
    position:relative; max-width:640px; margin:0 auto;
    background:var(--folder); border-radius:4px 14px 4px 4px;
    padding: 3.2rem 2rem 2.4rem;
    box-shadow:0 22px 40px rgba(0,0,0,0.3);
  }
  .cta-folder::before{
    content:''; position:absolute; top:-22px; left:8%; width:36%; height:26px;
    background:var(--folder); clip-path: polygon(6% 100%, 0 0, 88% 0, 100% 100%);
  }
  .cta-eyebrow{
    font-family:var(--font-script); font-style:italic; font-weight:700; color:var(--violet);
    font-size:1.15rem; margin-bottom:0.6rem;
  }
  .megaphone{ width:70px; height:70px; margin-bottom:1rem; }
  .cta-note{
    background:var(--cream); border-radius:2px; padding:1.6rem 1.5rem; margin-top:1.4rem;
    box-shadow:0 10px 20px rgba(0,0,0,0.18); transform:rotate(-1deg);
    max-width:70ch;
  }
  .cta-note p{ margin:0 0 0.9rem; font-size:1rem; color:var(--ink); }
  .cta-note .dm{
    font-family:var(--font-script); font-style:italic; font-weight:700; color:var(--violet);
    font-size:1.15rem; display:inline-block; position:relative;
  }
  .cta-note .dm::after{
    content:''; position:absolute; left:0; right:-6px; bottom:-4px; height:6px;
    background:none; border-bottom:2px solid var(--yellow); border-radius:50%;
  }

  footer{
    margin-top:3.5rem; padding-top:1.6rem; border-top:1px solid rgba(243,241,232,0.2);
    display:flex; flex-wrap:wrap; gap:1.2rem; justify-content:space-between; align-items:center;
    font-family:var(--font-mono); font-size:0.75rem; color:rgba(243,241,232,0.6);
  }
  .social-links{ display:flex; gap:1.1rem; }
  .social-links a{ text-decoration:none; color:rgba(243,241,232,0.85); }
  .social-links a:hover{ color:var(--yellow); }

  @media (max-width: 760px){
    nav.desktop-nav{ display:none; }
    .menu-btn{ display:block; }
    .scrap, .sparkle{ display:none; }
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

<section class="hero">
  <span class="hero-eyebrow">@hski.studio</span>

  <div class="folder">
    <div class="folder-paper"></div>
    <svg class="paperclip" viewBox="0 0 40 74" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 8C12 4 15 1 19 1C23 1 26 4 26 8V52C26 57 22 61 17 61C12 61 8 57 8 52V16" stroke="#9a9a9a" stroke-width="3.5" stroke-linecap="round"/>
    </svg>

    <div class="sparkle s1" style="top:-4px; left:-6px;"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 0 L14 10 L24 12 L14 14 L12 24 L10 14 L0 12 L10 10 Z"/></svg></div>
    <div class="sparkle s2" style="bottom:14%; left:2%;"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 0 L14 10 L24 12 L14 14 L12 24 L10 14 L0 12 L10 10 Z"/></svg></div>

    <div class="folder-inner">
      <h1 class="hero-title">¿Tu marca está<span class="accent">estancada?</span></h1>
      <p class="typed-line" id="typedLine"><span class="cursor">&nbsp;</span></p>
      <p class="hero-sub">Soy Lara, diseñadora multimedial formada en la UNLP. Diseñemos juntas la cara de tu proyecto: identidad, piezas gráficas y gestión de redes.</p>
      <div class="hero-ctas">
        <a href="#fichero" class="btn btn-primary">Ver el fichero</a>
        <a href="#contacto" class="btn">Escribinos</a>
      </div>
    </div>
  </div>

  <span class="scroll-cue">Desplegá el archivo</span>
</section>

<section id="fichero" class="reveal">
  <div class="section-head">
    <span class="section-tag">Servicios y precios actuales</span>
    <h2>El <em>fichero</em></h2>
    <p class="section-desc">Cuatro archivos, un criterio: elegí servicios sueltos o armamos un pack a medida. Arrastrá para ver el catálogo completo.</p>
  </div>

  <div class="fichero-wrap">
    <div class="fichero-track" id="fichaTrack">
      <div class="ficha">
        <div class="tape"></div>
        <div class="ficha-code">FICHA N.º 01</div>
        <h3>Contenido y Redes</h3>
        <p>Edición de reels y video, retoque de imagen, placas gráficas, copywriting, subida programada y gestión como community manager.</p>
        <div class="price">desde $8.000</div>
      </div>
      <div class="ficha">
        <div class="clip"></div>
        <div class="ficha-code">FICHA N.º 02</div>
        <h3>Identidad Visual</h3>
        <p>Logotipos y sus aplicaciones, kit de inicio de marca, rediseño de logo o una identidad completa de punta a punta.</p>
        <div class="price">desde $56.000</div>
      </div>
      <div class="ficha">
        <div class="tape"></div>
        <div class="ficha-code">FICHA N.º 03</div>
        <h3>Papelería</h3>
        <p>Tarjetas personales o de eventos, etiquetas y packaging, folletos y menús, infografías, posters y banners.</p>
        <div class="price">desde $18.000</div>
      </div>
      <div class="ficha">
        <div class="clip"></div>
        <div class="ficha-code">FICHA N.º 04</div>
        <h3>Digital</h3>
        <p>Prototipado y diseño de interfaces (UX/UI), landing pages, formularios web, infografías interactivas e ilustración.</p>
        <div class="price">desde $35.000</div>
      </div>
    </div>
    <p class="fichero-hint">← desliza para ver el archivo completo →</p>
  </div>
  <p class="section-desc" style="margin-top:1.4rem; font-size:0.88rem;">* Los packs semanales y mensuales de reels, historias y posteos se arman a medida — escribime para cotizar el tuyo.</p>
</section>

<section class="reveal">
  <div class="section-head">
    <span class="section-tag">Archivo 02 — Destinatarios</span>
    <h2>¿Para <em>quién</em> es esto?</h2>
    <p class="section-desc">Servicios sueltos o packs a medida: elegís vos por dónde empezamos.</p>
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
    <h2>Cómo se arma la <em>ficha</em></h2>
    <p class="section-desc">Sin vueltas raras. Cuatro pasos, en orden, sin saltarse ninguno.</p>
  </div>
  <div class="proceso-list" id="procesoList">
    <div class="proceso-item open" data-code="A">
      <button class="proceso-head">
        <span class="proceso-title">Diagnóstico</span>
        <span class="proceso-icon">+</span>
      </button>
      <div class="proceso-body"><p>Miramos qué tenés, qué falta y qué está compitiendo contra vos sin que te des cuenta.</p></div>
    </div>
    <div class="proceso-item" data-code="B">
      <button class="proceso-head">
        <span class="proceso-title">Boceto</span>
        <span class="proceso-icon">+</span>
      </button>
      <div class="proceso-body"><p>Proponemos una dirección visual concreta: paleta, tipografía y formatos, antes de producir nada.</p></div>
    </div>
    <div class="proceso-item" data-code="C">
      <button class="proceso-head">
        <span class="proceso-title">Producción</span>
        <span class="proceso-icon">+</span>
      </button>
      <div class="proceso-body"><p>Se arman las piezas y el calendario. Vos revisás, ajustamos, y queda listo para publicar.</p></div>
    </div>
    <div class="proceso-item" data-code="D">
      <button class="proceso-head">
        <span class="proceso-title">Entrega</span>
        <span class="proceso-icon">+</span>
      </button>
      <div class="proceso-body"><p>Te llega todo catalogado y listo para usar, con criterio para seguir solo si así lo preferís.</p></div>
    </div>
  </div>
</section>

<section id="contacto" class="cta reveal">
  <div class="cta-folder">
    <div class="cta-eyebrow">¿Lista para el siguiente nivel?</div>
    <svg class="megaphone" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M4 26L34 10V54L4 38V26Z" fill="var(--ink)"/>
      <rect x="34" y="24" width="8" height="16" fill="var(--ink)"/>
      <path d="M46 20L60 14M46 32L62 32M46 44L60 50" stroke="var(--violet)" stroke-width="4" stroke-linecap="round"/>
      <rect x="4" y="38" width="8" height="14" rx="2" fill="var(--ink)"/>
    </svg>
    <h2 style="color:var(--ink);">¿Hacemos que tu feed diga algo?</h2>

    <div class="cta-note">
      <p>Charlemos de tus objetivos y armemos una propuesta a medida para tu marca.</p>
      <a href="mailto:horianskilara@gmail.com" class="dm btn-stamp" id="stampBtn">mandame un mensaje y arrancamos</a>
    </div>
  </div>

  <footer>
    <span>hski.studio © 2026 — diseño · redes · multimedia</span>
    <div class="social-links">
      <a href="https://www.instagram.com/hski.studio" target="_blank" rel="noopener">Instagram</a>
      <a href="https://www.behance.net/horianski" target="_blank" rel="noopener">Behance</a>
      <a href="https://wa.me/5491122475964" target="_blank" rel="noopener">WhatsApp</a>
    </div>
  </footer>
</section>

<script>
(function(){
  var reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  var typedEl = document.getElementById('typedLine');
  var text = "Diseñemos juntas la cara de tu proyecto.";
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

  var track = document.getElementById('fichaTrack');
  var isDown = false, startX, scrollLeft;
  track.addEventListener('pointerdown', function(e){
    isDown = true; track.classList.add('grabbing');
    startX = e.pageX - track.offsetLeft; scrollLeft = track.scrollLeft;
  });
  window.addEventListener('pointerup', function(){ isDown = false; track.classList.remove('grabbing'); });
  track.addEventListener('pointermove', function(e){
    if(!isDown) return;
    e.preventDefault();
    var x = e.pageX - track.offsetLeft;
    var walk = (x - startX) * 1.2;
    track.scrollLeft = scrollLeft - walk;
  });

  if(!reduceMotion){
    track.querySelectorAll('.ficha').forEach(function(card){
      var base = card.style.transform;
      card.addEventListener('pointermove', function(e){
        var rect = card.getBoundingClientRect();
        var x = (e.clientX - rect.left) / rect.width - 0.5;
        var y = (e.clientY - rect.top) / rect.height - 0.5;
        card.style.transform = 'rotateY(' + (x * 8) + 'deg) rotateX(' + (y * -8) + 'deg) translateY(-2px)';
      });
      card.addEventListener('pointerleave', function(){ card.style.transform = ''; });
    });
  }

  var items = document.querySelectorAll('.proceso-item');
  function setBodyHeight(item, open){
    var body = item.querySelector('.proceso-body');
    body.style.maxHeight = open ? body.scrollHeight + 'px' : 0;
  }
  items.forEach(function(item){
    setBodyHeight(item, item.classList.contains('open'));
    item.querySelector('.proceso-head').addEventListener('click', function(){
      var willOpen = !item.classList.contains('open');
      items.forEach(function(other){ other.classList.remove('open'); setBodyHeight(other, false); });
      if(willOpen){ item.classList.add('open'); setBodyHeight(item, true); }
    });
  });
  window.addEventListener('resize', function(){
    items.forEach(function(item){ if(item.classList.contains('open')) setBodyHeight(item, true); });
  });

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
