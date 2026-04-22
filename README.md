<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>2 DUDES — Wear Confidence. Own the Street.</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;0,700;1,300;1,400&family=Bebas+Neue&family=Montserrat:wght@200;300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --gold: #C9A84C;
    --gold-light: #E8C97A;
    --gold-dark: #8B6914;
    --black: #050505;
    --black-2: #0D0D0D;
    --black-3: #141414;
    --white: #F5F0E8;
    --white-dim: rgba(245,240,232,0.06);
    --glass: rgba(245,240,232,0.04);
    --border: rgba(201,168,76,0.2);
    --border-bright: rgba(201,168,76,0.5);
  }

  *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: 'Montserrat', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* ── CUSTOM CURSOR ── */
  #cursor {
    position: fixed; width: 10px; height: 10px;
    background: var(--gold); border-radius: 50%;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform .1s, width .3s, height .3s, background .3s;
  }
  #cursor-ring {
    position: fixed; width: 36px; height: 36px;
    border: 1px solid rgba(201,168,76,0.5); border-radius: 50%;
    pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform .15s ease-out, width .3s, height .3s;
  }
  body:hover #cursor { opacity:1; }

  /* ── GRAIN OVERLAY ── */
  body::before {
    content:''; position:fixed; inset:0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 0; opacity:.4;
  }

  /* ── NAVBAR ── */
  nav {
    position: fixed; top:0; left:0; right:0; z-index:1000;
    padding: 22px 5%;
    display: flex; align-items: center; justify-content: space-between;
    background: rgba(5,5,5,0.2);
    backdrop-filter: blur(24px) saturate(180%);
    -webkit-backdrop-filter: blur(24px) saturate(180%);
    border-bottom: 1px solid var(--border);
    transition: all .4s;
  }
  nav.scrolled {
    background: rgba(5,5,5,0.85);
    padding: 14px 5%;
  }
  .nav-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2rem; letter-spacing: .2em;
    background: linear-gradient(135deg, var(--gold-light), var(--gold), var(--gold-dark));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    text-decoration: none;
  }
  .nav-links { display:flex; gap:2.5rem; list-style:none; }
  .nav-links a {
    font-size: .68rem; letter-spacing: .18em; text-transform: uppercase;
    color: rgba(245,240,232,.6); text-decoration:none;
    position: relative; padding-bottom: 4px;
    transition: color .3s;
  }
  .nav-links a::after {
    content:''; position:absolute; bottom:0; left:0; right:0; height:1px;
    background: var(--gold); transform: scaleX(0); transition: transform .3s;
  }
  .nav-links a:hover { color: var(--white); }
  .nav-links a:hover::after { transform: scaleX(1); }
  .nav-cta {
    padding: 10px 24px;
    border: 1px solid var(--gold); color: var(--gold);
    font-size: .68rem; letter-spacing: .18em; text-transform: uppercase;
    text-decoration: none; transition: all .3s;
    position: relative; overflow: hidden;
  }
  .nav-cta::before {
    content:''; position:absolute; inset:0;
    background: var(--gold); transform: translateX(-101%);
    transition: transform .35s cubic-bezier(.7,0,.3,1);
  }
  .nav-cta:hover::before { transform: translateX(0); }
  .nav-cta:hover { color: var(--black); }
  .nav-cta span { position:relative; z-index:1; }
  .hamburger { display:none; flex-direction:column; gap:5px; cursor:pointer; }
  .hamburger span { width:24px; height:1px; background:var(--gold); transition:.3s; display:block; }

  /* ── HERO ── */
  #hero {
    min-height: 100vh; position: relative;
    display: flex; align-items: center; justify-content: center;
    overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset:0;
    background: radial-gradient(ellipse 80% 60% at 50% 40%, rgba(201,168,76,.07) 0%, transparent 70%),
                linear-gradient(180deg, #050505 0%, #0a0a0a 50%, #050505 100%);
  }

  /* 3D Rotating Scene */
  .scene-3d {
    position: absolute; inset:0;
    display: flex; align-items: center; justify-content: center;
    perspective: 1200px;
  }
  .mannequin-wrapper {
    transform-style: preserve-3d;
    animation: floatRotate 12s ease-in-out infinite;
    position: relative;
  }
  @keyframes floatRotate {
    0%   { transform: rotateY(0deg) translateY(0px); }
    25%  { transform: rotateY(8deg) translateY(-18px); }
    50%  { transform: rotateY(0deg) translateY(0px); }
    75%  { transform: rotateY(-8deg) translateY(-12px); }
    100% { transform: rotateY(0deg) translateY(0px); }
  }

  /* SVG Mannequin */
  .mannequin-svg {
    width: min(380px, 60vw);
    filter: drop-shadow(0 0 60px rgba(201,168,76,.18)) drop-shadow(0 0 120px rgba(201,168,76,.08));
  }

  /* Orbiting rings */
  .orbit-ring {
    position: absolute; border-radius: 50%; border: 1px solid;
    top:50%; left:50%;
    transform-style: preserve-3d;
  }
  .orbit-ring-1 {
    width: 480px; height: 480px;
    margin: -240px 0 0 -240px;
    border-color: rgba(201,168,76,.12);
    animation: orbitSpin 18s linear infinite;
    transform: rotateX(70deg);
  }
  .orbit-ring-2 {
    width: 360px; height: 360px;
    margin: -180px 0 0 -180px;
    border-color: rgba(201,168,76,.08);
    animation: orbitSpin 12s linear infinite reverse;
    transform: rotateX(70deg) rotateZ(30deg);
  }
  @keyframes orbitSpin { to { transform: rotateX(70deg) rotateZ(360deg); } }

  /* Floating particles */
  .particle {
    position: absolute;
    background: var(--gold);
    border-radius: 50%;
    animation: particleDrift linear infinite;
    opacity: 0;
  }
  @keyframes particleDrift {
    0%   { transform: translateY(0) translateX(0); opacity: 0; }
    10%  { opacity: .8; }
    90%  { opacity: .4; }
    100% { transform: translateY(-120px) translateX(var(--drift)); opacity: 0; }
  }

  .hero-content {
    position: relative; z-index:10;
    text-align: center;
    max-width: 900px; padding: 0 5%;
  }
  .hero-badge {
    display: inline-flex; align-items: center; gap: 10px;
    border: 1px solid var(--border); padding: 7px 18px;
    margin-bottom: 2.5rem;
    font-size: .6rem; letter-spacing: .25em; text-transform: uppercase;
    color: var(--gold); background: rgba(201,168,76,.05);
    animation: fadeInUp .8s .2s both;
  }
  .hero-badge::before, .hero-badge::after {
    content:''; width:20px; height:1px; background:var(--gold);
  }
  .hero-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(5rem, 15vw, 13rem);
    line-height: .9;
    letter-spacing: .05em;
    background: linear-gradient(180deg, #fff 0%, var(--gold-light) 40%, var(--gold) 70%, var(--gold-dark) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    animation: fadeInUp .8s .35s both;
    position: relative;
  }
  .hero-title .title-stroke {
    -webkit-text-stroke: 1px rgba(201,168,76,.3);
    -webkit-text-fill-color: transparent;
    display: block;
    font-size: clamp(2.5rem, 7vw, 6rem);
    letter-spacing: .3em;
  }
  .hero-tagline {
    font-size: clamp(.75rem, 2vw, 1rem);
    letter-spacing: .25em; text-transform: uppercase;
    color: rgba(245,240,232,.5);
    margin: 1.5rem 0 3rem;
    animation: fadeInUp .8s .5s both;
  }
  .hero-tagline em {
    font-style: normal;
    background: linear-gradient(90deg, var(--gold), var(--gold-light));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  .hero-btns {
    display: flex; gap:1.5rem; justify-content: center; flex-wrap: wrap;
    animation: fadeInUp .8s .65s both;
  }
  .btn-primary {
    padding: 16px 44px;
    background: linear-gradient(135deg, var(--gold), var(--gold-dark));
    color: var(--black); font-size: .7rem; letter-spacing: .2em;
    text-transform: uppercase; text-decoration: none; font-weight: 600;
    position: relative; overflow:hidden; transition: all .3s;
    box-shadow: 0 8px 40px rgba(201,168,76,.3);
  }
  .btn-primary::after {
    content:''; position:absolute; inset:0;
    background: linear-gradient(135deg, var(--gold-light), var(--gold));
    opacity:0; transition: opacity .3s;
  }
  .btn-primary:hover::after { opacity:1; }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 14px 50px rgba(201,168,76,.45); }
  .btn-primary span { position:relative; z-index:1; }
  .btn-ghost {
    padding: 16px 44px;
    border: 1px solid rgba(201,168,76,.4); color: var(--gold);
    font-size: .7rem; letter-spacing: .2em; text-transform: uppercase;
    text-decoration: none; transition: all .3s; background: transparent;
  }
  .btn-ghost:hover {
    background: rgba(201,168,76,.08); border-color: var(--gold);
    transform: translateY(-2px);
  }

  .hero-scroll-hint {
    position: absolute; bottom: 3rem; left:50%; transform: translateX(-50%);
    display:flex; flex-direction:column; align-items:center; gap:10px;
    color: rgba(245,240,232,.3); font-size:.6rem; letter-spacing:.2em; text-transform:uppercase;
    animation: fadeInUp 1s 1.2s both;
  }
  .scroll-line {
    width:1px; height:50px;
    background: linear-gradient(to bottom, var(--gold), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }
  @keyframes scrollPulse {
    0%,100% { opacity:.4; transform:scaleY(1); }
    50% { opacity:1; transform:scaleY(.7); }
  }

  @keyframes fadeInUp {
    from { opacity:0; transform:translateY(30px); }
    to   { opacity:1; transform:translateY(0); }
  }

  /* ── MARQUEE ── */
  .marquee-section {
    position: relative; z-index:5;
    padding: 20px 0;
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    background: rgba(201,168,76,.03);
    overflow: hidden;
  }
  .marquee-track {
    display: flex; gap:0; white-space: nowrap;
    animation: marqueeScroll 30s linear infinite;
  }
  .marquee-item {
    display: inline-flex; align-items: center; gap: 2rem;
    padding: 0 2rem;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.1rem; letter-spacing: .2em;
    color: rgba(201,168,76,.5);
  }
  .marquee-item .dot { color: var(--gold); font-size: 1.5rem; }
  @keyframes marqueeScroll { to { transform: translateX(-50%); } }

  /* ── SECTION COMMONS ── */
  section { position:relative; z-index:2; }
  .section-label {
    font-size:.6rem; letter-spacing:.3em; text-transform:uppercase;
    color: var(--gold); display:flex; align-items:center; gap:12px;
    margin-bottom:1.2rem;
  }
  .section-label::before { content:''; width:30px; height:1px; background:var(--gold); }
  .section-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(2.5rem, 6vw, 5rem);
    font-weight: 300; line-height:1.1;
    letter-spacing: .02em;
  }
  .section-title strong {
    font-weight: 700; font-style: italic;
    background: linear-gradient(135deg, var(--gold-light), var(--gold));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
  }
  .reveal {
    opacity:0; transform:translateY(40px);
    transition: opacity .9s cubic-bezier(.2,.8,.3,1), transform .9s cubic-bezier(.2,.8,.3,1);
  }
  .reveal.visible { opacity:1; transform:translateY(0); }
  .reveal-delay-1 { transition-delay:.1s; }
  .reveal-delay-2 { transition-delay:.2s; }
  .reveal-delay-3 { transition-delay:.3s; }
  .reveal-delay-4 { transition-delay:.4s; }

  /* ── STATS BAR ── */
  .stats-bar {
    padding: 5rem 5%;
    display: grid; grid-template-columns: repeat(4, 1fr);
    gap: 2px;
    background: var(--border);
  }
  .stat-item {
    background: var(--black-2);
    padding: 3rem 2rem; text-align:center;
    position:relative; overflow:hidden;
    transition: background .3s;
  }
  .stat-item::before {
    content:''; position:absolute; top:0; left:0; right:0; height:2px;
    background: linear-gradient(90deg, transparent, var(--gold), transparent);
    transform: scaleX(0); transition: transform .5s;
  }
  .stat-item:hover::before { transform: scaleX(1); }
  .stat-item:hover { background: rgba(201,168,76,.04); }
  .stat-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 3.5rem; letter-spacing:.05em;
    background: linear-gradient(135deg, var(--gold-light), var(--gold));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
    line-height:1;
  }
  .stat-label {
    font-size:.65rem; letter-spacing:.2em; text-transform:uppercase;
    color: rgba(245,240,232,.4); margin-top:.5rem;
  }

  /* ── COLLECTIONS ── */
  #collections { padding: 8rem 5%; }
  .collections-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5px;
    margin-top: 4rem;
    background: var(--border);
  }
  .collection-card {
    background: var(--black-2);
    padding: 4rem 3rem;
    position: relative; overflow: hidden;
    cursor: pointer; transition: background .4s;
    min-height: 380px;
    display: flex; flex-direction:column; justify-content:flex-end;
  }
  .collection-card::before {
    content:''; position:absolute; inset:0;
    background: linear-gradient(135deg, rgba(201,168,76,.05), transparent);
    opacity:0; transition: opacity .5s;
  }
  .collection-card:hover::before { opacity:1; }
  .collection-card:hover { background: var(--black-3); }
  .card-number {
    position:absolute; top:2rem; right:2rem;
    font-family:'Bebas Neue', sans-serif; font-size:5rem;
    color: rgba(201,168,76,.06); line-height:1;
    transition: color .4s, transform .4s;
  }
  .collection-card:hover .card-number {
    color: rgba(201,168,76,.12);
    transform: scale(1.1);
  }
  .card-icon {
    font-size:2.5rem; margin-bottom:1.5rem;
    filter: grayscale(1) brightness(.7);
    transition: filter .4s, transform .4s;
    display: inline-block;
  }
  .collection-card:hover .card-icon {
    filter: grayscale(0) brightness(1);
    transform: translateY(-5px);
  }
  .card-category {
    font-size:.6rem; letter-spacing:.25em; text-transform:uppercase;
    color: var(--gold); margin-bottom:.8rem;
  }
  .card-title {
    font-family:'Cormorant Garamond', serif;
    font-size:2.2rem; font-weight:600;
    line-height:1.2; margin-bottom:.8rem;
    transition: color .3s;
  }
  .collection-card:hover .card-title { color: var(--gold-light); }
  .card-desc {
    font-size:.75rem; line-height:1.8;
    color:rgba(245,240,232,.45); max-width:280px;
    margin-bottom:1.5rem;
  }
  .card-link {
    display:inline-flex; align-items:center; gap:10px;
    font-size:.65rem; letter-spacing:.18em; text-transform:uppercase;
    color: var(--gold); text-decoration:none;
    transition: gap .3s;
  }
  .card-link:hover { gap:18px; }
  .card-link::after { content:'→'; }

  /* Decorative lines on cards */
  .collection-card .card-line {
    position:absolute; bottom:0; left:0; right:0; height:1px;
    background: linear-gradient(90deg, transparent, var(--gold), transparent);
    transform: scaleX(0); transition: transform .6s;
  }
  .collection-card:hover .card-line { transform: scaleX(1); }

  /* ── PRODUCTS ── */
  #products { padding: 8rem 5%; background: var(--black-2); }
  .products-grid {
    display:grid; grid-template-columns:repeat(3,1fr); gap:1.5px;
    background: var(--border); margin-top:4rem;
  }
  .product-card {
    background: var(--black);
    position:relative; overflow:hidden;
    cursor:pointer;
    aspect-ratio: 3/4;
    display:flex; flex-direction:column; justify-content:flex-end;
  }
  .product-visual {
    position:absolute; inset:0;
    display:flex; align-items:center; justify-content:center;
    background: linear-gradient(180deg, var(--black-3) 0%, var(--black) 100%);
    transition: transform .6s cubic-bezier(.2,.8,.3,1);
  }
  .product-card:hover .product-visual { transform: scale(1.04); }
  .product-visual svg {
    width: 65%; opacity: .7;
    filter: drop-shadow(0 20px 40px rgba(201,168,76,.2));
    transition: opacity .4s, filter .4s, transform .6s;
  }
  .product-card:hover .product-visual svg {
    opacity:1;
    filter: drop-shadow(0 30px 60px rgba(201,168,76,.4));
    transform: translateY(-10px);
  }
  .product-overlay {
    position:absolute; inset:0;
    background: linear-gradient(to top, rgba(5,5,5,.95) 0%, rgba(5,5,5,.3) 50%, transparent 100%);
  }
  .product-info {
    position:relative; z-index:2; padding:1.8rem;
    transform: translateY(10px); transition: transform .4s;
  }
  .product-card:hover .product-info { transform: translateY(0); }
  .product-tag {
    font-size:.55rem; letter-spacing:.2em; text-transform:uppercase;
    color:var(--gold); margin-bottom:.4rem;
  }
  .product-name {
    font-family:'Cormorant Garamond', serif;
    font-size:1.4rem; font-weight:600; margin-bottom:.3rem;
  }
  .product-price {
    font-size:.8rem; letter-spacing:.1em;
    color:rgba(245,240,232,.6);
  }
  .product-price span { color:var(--gold); }
  .product-badge {
    position:absolute; top:1.2rem; right:1.2rem; z-index:3;
    padding:5px 12px;
    border:1px solid var(--gold); color:var(--gold);
    font-size:.5rem; letter-spacing:.2em; text-transform:uppercase;
    background: rgba(5,5,5,.7); backdrop-filter:blur(10px);
  }
  .add-btn {
    position:absolute; bottom:1.8rem; right:1.5rem; z-index:3;
    width:42px; height:42px;
    border:1px solid rgba(201,168,76,.3);
    background:rgba(5,5,5,.8); backdrop-filter:blur(10px);
    color:var(--gold); font-size:1.2rem;
    display:flex; align-items:center; justify-content:center;
    opacity:0; transform:scale(.8) translateY(10px);
    transition: all .3s;
    cursor:pointer;
  }
  .product-card:hover .add-btn {
    opacity:1; transform:scale(1) translateY(0);
  }
  .add-btn:hover { background:var(--gold); color:var(--black); }

  /* ── ABOUT ── */
  #about {
    padding: 10rem 5%;
    display:grid; grid-template-columns:1fr 1fr; gap:8rem;
    align-items:center;
  }
  .about-visual {
    position:relative; height:600px;
  }
  .about-frame {
    position:absolute; inset:0;
    border: 1px solid var(--border);
    overflow:hidden;
    display:flex; align-items:center; justify-content:center;
    background: var(--black-2);
  }
  .about-frame::before {
    content:''; position:absolute; inset:0;
    background: radial-gradient(ellipse 60% 60% at 50% 50%, rgba(201,168,76,.08), transparent);
  }
  .about-frame-inner {
    width:80%; aspect-ratio:1;
    border-radius:50%;
    border:1px solid rgba(201,168,76,.12);
    display:flex; align-items:center; justify-content:center;
    animation:slowRotate 20s linear infinite;
  }
  .about-frame-inner-2 {
    width:70%; aspect-ratio:1;
    border-radius:50%;
    border:1px solid rgba(201,168,76,.08);
    display:flex; align-items:center; justify-content:center;
    animation:slowRotate 14s linear infinite reverse;
  }
  .about-center-icon { font-size:5rem; }
  @keyframes slowRotate { to { transform:rotate(360deg); } }
  .about-tag {
    position:absolute; padding:12px 20px;
    background: rgba(5,5,5,.9); backdrop-filter:blur(20px);
    border:1px solid var(--border);
    font-size:.6rem; letter-spacing:.15em; text-transform:uppercase;
  }
  .about-tag-1 { top:10%; left:-10%; color:var(--gold); }
  .about-tag-2 { bottom:15%; right:-8%; }
  .about-tag-3 { bottom:35%; left:-15%; }

  .about-content {}
  .about-content .section-title { margin-bottom:2rem; }
  .about-lead {
    font-family:'Cormorant Garamond', serif;
    font-size:1.4rem; font-style:italic; font-weight:300;
    line-height:1.8; color:rgba(245,240,232,.7);
    border-left:2px solid var(--gold); padding-left:1.5rem;
    margin-bottom:2rem;
  }
  .about-text {
    font-size:.8rem; line-height:2; color:rgba(245,240,232,.45);
    margin-bottom:1.5rem;
  }
  .about-values {
    display:grid; grid-template-columns:1fr 1fr; gap:1.5rem;
    margin-top:2.5rem;
  }
  .value-item {
    padding:1.5rem; border:1px solid var(--border);
    background: var(--glass); transition: border-color .3s, background .3s;
  }
  .value-item:hover { border-color:var(--gold); background:rgba(201,168,76,.04); }
  .value-icon { font-size:1.3rem; margin-bottom:.8rem; }
  .value-title {
    font-size:.65rem; letter-spacing:.15em; text-transform:uppercase;
    color:var(--gold); margin-bottom:.4rem;
  }
  .value-text { font-size:.72rem; color:rgba(245,240,232,.4); line-height:1.7; }

  /* ── TESTIMONIALS ── */
  #testimonials { padding:8rem 5%; background:var(--black-2); overflow:hidden; }
  .testimonials-track-wrapper { overflow:hidden; margin-top:4rem; }
  .testimonials-track {
    display:flex; gap:1.5rem;
    animation:testimonialsScroll 35s linear infinite;
    width:max-content;
  }
  .testimonials-track:hover { animation-play-state:paused; }
  @keyframes testimonialsScroll { to { transform:translateX(-50%); } }
  .testimonial-card {
    width:360px; flex-shrink:0;
    background: var(--black);
    border:1px solid var(--border);
    padding:2.5rem;
    position:relative; overflow:hidden;
    transition: border-color .3s;
  }
  .testimonial-card:hover { border-color:rgba(201,168,76,.4); }
  .testimonial-card::before {
    content:'"'; position:absolute; top:-.5rem; right:1.5rem;
    font-family:'Cormorant Garamond', serif; font-size:8rem; font-weight:700;
    color:rgba(201,168,76,.06); line-height:1;
  }
  .stars {
    color:var(--gold); font-size:.9rem; letter-spacing:.1em;
    margin-bottom:1rem;
  }
  .testimonial-text {
    font-family:'Cormorant Garamond', serif;
    font-size:1.05rem; font-style:italic; line-height:1.8;
    color:rgba(245,240,232,.7); margin-bottom:1.5rem;
  }
  .testimonial-author {
    display:flex; align-items:center; gap:1rem;
    padding-top:1rem; border-top:1px solid var(--border);
  }
  .author-avatar {
    width:40px; height:40px; border-radius:50%;
    background: linear-gradient(135deg, var(--gold-dark), var(--gold));
    display:flex; align-items:center; justify-content:center;
    font-size:.9rem; font-weight:700; color:var(--black);
    flex-shrink:0;
  }
  .author-name { font-size:.7rem; letter-spacing:.1em; text-transform:uppercase; color:var(--white); }
  .author-loc { font-size:.6rem; color:rgba(245,240,232,.35); margin-top:.2rem; }

  /* ── CONTACT ── */
  #contact { padding:8rem 5%; }
  .contact-inner {
    max-width:900px; margin:0 auto; text-align:center;
  }
  .contact-inner .section-label { justify-content:center; }
  .contact-inner .section-label::before { display:none; }
  .contact-subtitle {
    font-size:.85rem; color:rgba(245,240,232,.4);
    line-height:2; max-width:500px; margin:1.5rem auto 3.5rem;
  }
  .contact-cards {
    display:grid; grid-template-columns:1fr 1fr; gap:1.5px;
    background:var(--border); margin-bottom:3rem;
  }
  .contact-card {
    background:var(--black-2); padding:3rem 2rem;
    display:flex; flex-direction:column; align-items:center; gap:1rem;
    text-decoration:none; transition: background .3s;
    position:relative; overflow:hidden;
  }
  .contact-card::before {
    content:''; position:absolute; bottom:0; left:0; right:0; height:2px;
    background: linear-gradient(90deg, transparent, var(--gold), transparent);
    transform:scaleX(0); transition:transform .4s;
  }
  .contact-card:hover::before { transform:scaleX(1); }
  .contact-card:hover { background:rgba(201,168,76,.04); }
  .contact-card-icon { font-size:2rem; }
  .contact-card-label {
    font-size:.6rem; letter-spacing:.2em; text-transform:uppercase;
    color:var(--gold);
  }
  .contact-card-value {
    font-family:'Cormorant Garamond', serif;
    font-size:1.3rem; color:var(--white);
  }
  .contact-card-action {
    font-size:.6rem; letter-spacing:.15em; text-transform:uppercase;
    color:rgba(245,240,232,.3); margin-top:.5rem;
  }

  /* ── FOOTER ── */
  footer {
    background:var(--black-2);
    border-top:1px solid var(--border);
    padding:5rem 5% 2rem;
  }
  .footer-top {
    display:grid; grid-template-columns:2fr 1fr 1fr 1fr; gap:5rem;
    margin-bottom:4rem;
  }
  .footer-brand-name {
    font-family:'Bebas Neue', sans-serif; font-size:3rem;
    letter-spacing:.15em;
    background: linear-gradient(135deg, var(--gold-light), var(--gold));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
    margin-bottom:1rem;
  }
  .footer-brand-text {
    font-size:.72rem; color:rgba(245,240,232,.35); line-height:1.9;
    max-width:260px;
  }
  .footer-socials {
    display:flex; gap:1rem; margin-top:2rem;
  }
  .social-btn {
    width:40px; height:40px;
    border:1px solid var(--border);
    display:flex; align-items:center; justify-content:center;
    color:rgba(245,240,232,.4); font-size:.9rem;
    text-decoration:none; transition: all .3s;
  }
  .social-btn:hover { border-color:var(--gold); color:var(--gold); background:rgba(201,168,76,.08); }
  .footer-col h4 {
    font-size:.6rem; letter-spacing:.25em; text-transform:uppercase;
    color:var(--gold); margin-bottom:1.5rem;
  }
  .footer-col ul { list-style:none; }
  .footer-col ul li { margin-bottom:.8rem; }
  .footer-col ul a {
    font-size:.72rem; color:rgba(245,240,232,.35); text-decoration:none;
    transition:color .3s; letter-spacing:.05em;
  }
  .footer-col ul a:hover { color:var(--gold); }
  .footer-bottom {
    padding-top:2rem; border-top:1px solid var(--border);
    display:flex; align-items:center; justify-content:space-between;
    font-size:.6rem; letter-spacing:.12em; text-transform:uppercase;
    color:rgba(245,240,232,.2);
  }

  /* ── MOBILE NAV ── */
  @media(max-width:768px) {
    .nav-links, .nav-cta { display:none; }
    .hamburger { display:flex; }
    .mobile-menu {
      position:fixed; inset:0; z-index:999;
      background:rgba(5,5,5,.97); backdrop-filter:blur(30px);
      display:flex; flex-direction:column; align-items:center; justify-content:center;
      gap:2rem; transform:translateX(100%); transition:transform .5s cubic-bezier(.7,0,.3,1);
    }
    .mobile-menu.open { transform:translateX(0); }
    .mobile-menu a {
      font-family:'Bebas Neue', sans-serif; font-size:3rem;
      letter-spacing:.1em; color:var(--white); text-decoration:none;
      transition:color .3s;
    }
    .mobile-menu a:hover { color:var(--gold); }

    .stats-bar { grid-template-columns:1fr 1fr; }
    .collections-grid { grid-template-columns:1fr; }
    .products-grid { grid-template-columns:1fr 1fr; }
    #about { grid-template-columns:1fr; gap:4rem; }
    .about-visual { height:350px; }
    .about-tag-1, .about-tag-2, .about-tag-3 { display:none; }
    .about-values { grid-template-columns:1fr; }
    .contact-cards { grid-template-columns:1fr; }
    .footer-top { grid-template-columns:1fr 1fr; gap:3rem; }
    .orbit-ring-1 { width:300px; height:300px; margin:-150px 0 0 -150px; }
    .orbit-ring-2 { width:220px; height:220px; margin:-110px 0 0 -110px; }
  }
  @media(max-width:480px) {
    .products-grid { grid-template-columns:1fr; }
    .footer-top { grid-template-columns:1fr; }
    .hero-btns { flex-direction:column; align-items:center; }
  }

  /* Scanline effect for dark sections */
  .scanlines::after {
    content:''; position:absolute; inset:0; pointer-events:none;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(5,5,5,.03) 2px, rgba(5,5,5,.03) 4px);
  }
</style>
</head>
<body>

<!-- Custom Cursor -->
<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- Mobile Menu -->
<div class="mobile-menu" id="mobileMenu">
  <a href="#collections">Collections</a>
  <a href="#products">Products</a>
  <a href="#about">About</a>
  <a href="#testimonials">Reviews</a>
  <a href="#contact">Contact</a>
</div>

<!-- NAVBAR -->
<nav id="navbar">
  <a href="#" class="nav-logo">2 DUDES</a>
  <ul class="nav-links">
    <li><a href="#collections">Collections</a></li>
    <li><a href="#products">Products</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#testimonials">Reviews</a></li>
  </ul>
  <a href="#contact" class="nav-cta"><span>Shop Now</span></a>
  <div class="hamburger" id="hamburger">
    <span></span><span></span><span></span>
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-bg"></div>

  <div class="scene-3d">
    <div class="mannequin-wrapper">
      <!-- Orbit rings -->
      <div class="orbit-ring orbit-ring-1"></div>
      <div class="orbit-ring orbit-ring-2"></div>

      <!-- SVG Mannequin / Fashion Figure -->
      <svg class="mannequin-svg" viewBox="0 0 300 600" fill="none" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <linearGradient id="bodyGrad" x1="0" y1="0" x2="1" y2="1">
            <stop offset="0%" stop-color="#E8C97A"/>
            <stop offset="50%" stop-color="#C9A84C"/>
            <stop offset="100%" stop-color="#8B6914"/>
          </linearGradient>
          <linearGradient id="fabricGrad" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#1a1a1a"/>
            <stop offset="100%" stop-color="#0d0d0d"/>
          </linearGradient>
          <linearGradient id="shineGrad" x1="0" y1="0" x2="1" y2="0">
            <stop offset="0%" stop-color="rgba(232,201,122,0)"/>
            <stop offset="50%" stop-color="rgba(232,201,122,0.15)"/>
            <stop offset="100%" stop-color="rgba(232,201,122,0)"/>
          </linearGradient>
          <filter id="glow">
            <feGaussianBlur stdDeviation="3" result="blur"/>
            <feComposite in="SourceGraphic" in2="blur" operator="over"/>
          </filter>
        </defs>

        <!-- Head -->
        <circle cx="150" cy="52" r="36" fill="url(#bodyGrad)" opacity=".9"/>
        <circle cx="150" cy="52" r="32" fill="#1a1408" opacity=".3"/>
        <!-- Neck -->
        <rect x="140" y="84" width="20" height="24" fill="url(#bodyGrad)" opacity=".8"/>

        <!-- Premium Jacket/Outfit -->
        <!-- Torso base -->
        <path d="M90 108 Q95 100 110 100 L150 96 L190 100 Q205 100 210 108 L220 200 Q218 230 200 240 L100 240 Q82 230 80 200Z" fill="url(#fabricGrad)" stroke="rgba(201,168,76,0.3)" stroke-width="1"/>

        <!-- Lapels -->
        <path d="M110 100 L150 140 L150 100Z" fill="#111" stroke="url(#bodyGrad)" stroke-width=".5"/>
        <path d="M190 100 L150 140 L150 100Z" fill="#111" stroke="url(#bodyGrad)" stroke-width=".5"/>

        <!-- Gold jacket trim -->
        <path d="M90 108 Q95 100 110 100 L150 96" stroke="url(#bodyGrad)" stroke-width="2" fill="none"/>
        <path d="M190 100 Q205 100 210 108" stroke="url(#bodyGrad)" stroke-width="2" fill="none"/>

        <!-- Shine on jacket -->
        <path d="M90 108 L100 240" stroke="url(#shineGrad)" stroke-width="15" fill="none"/>

        <!-- Pocket square -->
        <path d="M178 128 L188 120 L192 130 L182 134Z" fill="url(#bodyGrad)" opacity=".7"/>

        <!-- Left arm -->
        <path d="M90 108 Q70 130 65 180 Q63 200 70 220 L90 224 Q88 200 92 175 Q98 145 100 120Z" fill="url(#fabricGrad)" stroke="rgba(201,168,76,0.2)" stroke-width="1"/>
        <!-- Right arm -->
        <path d="M210 108 Q230 130 235 180 Q237 200 230 220 L210 224 Q212 200 208 175 Q202 145 200 120Z" fill="url(#fabricGrad)" stroke="rgba(201,168,76,0.2)" stroke-width="1"/>

        <!-- Hands -->
        <ellipse cx="76" cy="228" rx="14" ry="10" fill="url(#bodyGrad)" opacity=".8"/>
        <ellipse cx="224" cy="228" rx="14" ry="10" fill="url(#bodyGrad)" opacity=".8"/>

        <!-- Belt -->
        <rect x="80" y="238" width="140" height="10" fill="#0d0d0d" stroke="url(#bodyGrad)" stroke-width="1"/>
        <rect x="144" y="237" width="12" height="12" fill="url(#bodyGrad)" rx="1"/>

        <!-- Pants -->
        <path d="M80 248 L85 400 L130 400 L150 320 L170 400 L215 400 L220 248Z" fill="#0f0f0f" stroke="rgba(201,168,76,0.15)" stroke-width="1"/>

        <!-- Pants crease -->
        <line x1="115" y1="248" x2="110" y2="400" stroke="rgba(201,168,76,0.08)" stroke-width="1"/>
        <line x1="185" y1="248" x2="190" y2="400" stroke="rgba(201,168,76,0.08)" stroke-width="1"/>

        <!-- Shoes -->
        <path d="M85 400 Q80 420 78 435 Q76 445 90 448 L130 448 Q138 445 136 430 L130 400Z" fill="#0a0a0a" stroke="rgba(201,168,76,0.3)" stroke-width="1"/>
        <path d="M215 400 Q220 420 222 435 Q224 445 210 448 L170 448 Q162 445 164 430 L170 400Z" fill="#0a0a0a" stroke="rgba(201,168,76,0.3)" stroke-width="1"/>

        <!-- Shoe accent -->
        <path d="M78 442 Q84 448 130 448" stroke="url(#bodyGrad)" stroke-width="1.5" fill="none" opacity=".5"/>
        <path d="M222 442 Q216 448 170 448" stroke="url(#bodyGrad)" stroke-width="1.5" fill="none" opacity=".5"/>

        <!-- Gold accents / cufflinks -->
        <circle cx="68" cy="216" r="4" fill="url(#bodyGrad)" filter="url(#glow)"/>
        <circle cx="232" cy="216" r="4" fill="url(#bodyGrad)" filter="url(#glow)"/>

        <!-- Logo on jacket -->
        <text x="150" y="188" text-anchor="middle" font-family="'Bebas Neue', sans-serif" font-size="11" fill="url(#bodyGrad)" opacity=".5" letter-spacing="3">2D</text>
      </svg>
    </div>
  </div>

  <!-- Floating particles -->
  <div id="particles"></div>

  <!-- Hero Content -->
  <div class="hero-content">
    <div class="hero-badge">New Collection 2025</div>
    <h1 class="hero-title">
      <span class="title-stroke">Wear</span>
      2 DUDES
    </h1>
    <p class="hero-tagline">Wear <em>Confidence.</em> Own the <em>Street.</em></p>
    <div class="hero-btns">
      <a href="#collections" class="btn-primary"><span>Explore Collection</span></a>
      <a href="#about" class="btn-ghost">Our Story</a>
    </div>
  </div>

  <div class="hero-scroll-hint">
    <div class="scroll-line"></div>
    Scroll
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-section">
  <div class="marquee-track" id="marqueeTrack">
    <span class="marquee-item">Premium Quality <span class="dot">✦</span></span>
    <span class="marquee-item">Streetwear Luxury <span class="dot">✦</span></span>
    <span class="marquee-item">Own The Street <span class="dot">✦</span></span>
    <span class="marquee-item">Wear Confidence <span class="dot">✦</span></span>
    <span class="marquee-item">2 Dudes Fashion <span class="dot">✦</span></span>
    <span class="marquee-item">Exclusive Fits <span class="dot">✦</span></span>
    <span class="marquee-item">Born To Stand Out <span class="dot">✦</span></span>
    <span class="marquee-item">Premium Quality <span class="dot">✦</span></span>
    <span class="marquee-item">Streetwear Luxury <span class="dot">✦</span></span>
    <span class="marquee-item">Own The Street <span class="dot">✦</span></span>
    <span class="marquee-item">Wear Confidence <span class="dot">✦</span></span>
    <span class="marquee-item">2 Dudes Fashion <span class="dot">✦</span></span>
    <span class="marquee-item">Exclusive Fits <span class="dot">✦</span></span>
    <span class="marquee-item">Born To Stand Out <span class="dot">✦</span></span>
  </div>
</div>

<!-- STATS -->
<div class="stats-bar">
  <div class="stat-item reveal">
    <div class="stat-num" data-count="2400">0</div>
    <div class="stat-label">Happy Customers</div>
  </div>
  <div class="stat-item reveal reveal-delay-1">
    <div class="stat-num" data-count="150">0</div>
    <div class="stat-label">Premium Designs</div>
  </div>
  <div class="stat-item reveal reveal-delay-2">
    <div class="stat-num" data-count="4">0</div>
    <div class="stat-label">Exclusive Collections</div>
  </div>
  <div class="stat-item reveal reveal-delay-3">
    <div class="stat-num" data-count="5">0</div>
    <div class="stat-label">Years of Excellence</div>
  </div>
</div>

<!-- COLLECTIONS -->
<section id="collections">
  <div style="max-width:1400px; margin:0 auto;">
    <div class="reveal">
      <div class="section-label">Our Signature Lines</div>
      <h2 class="section-title">Curated <strong>Collections</strong><br>for Every Occasion</h2>
    </div>
    <div class="collections-grid">

      <div class="collection-card reveal">
        <div class="card-number">01</div>
        <div class="card-line"></div>
        <div class="card-icon">🏙️</div>
        <div class="card-category">Urban Edge</div>
        <h3 class="card-title">Streetwear<br>Collection</h3>
        <p class="card-desc">Dominate the urban landscape. Bold graphics, oversized silhouettes, and raw energy that commands every street corner.</p>
        <a href="#products" class="card-link">Explore Line</a>
      </div>

      <div class="collection-card reveal reveal-delay-1">
        <div class="card-number">02</div>
        <div class="card-line"></div>
        <div class="card-icon">☀️</div>
        <div class="card-category">Everyday Ease</div>
        <h3 class="card-title">Casual<br>Wear</h3>
        <p class="card-desc">Effortless style for the modern man. Premium fabrics that feel as good as they look — from dawn to dusk.</p>
        <a href="#products" class="card-link">Explore Line</a>
      </div>

      <div class="collection-card reveal reveal-delay-2">
        <div class="card-number">03</div>
        <div class="card-line"></div>
        <div class="card-icon">💎</div>
        <div class="card-category">The Elite Range</div>
        <h3 class="card-title">Premium<br>Fits</h3>
        <p class="card-desc">Reserved for those who demand the extraordinary. Tailored perfection meets street sensibility in our most exclusive range.</p>
        <a href="#products" class="card-link">Explore Line</a>
      </div>

      <div class="collection-card reveal reveal-delay-3">
        <div class="card-number">04</div>
        <div class="card-line"></div>
        <div class="card-icon">🥂</div>
        <div class="card-category">Night Edition</div>
        <h3 class="card-title">Party<br>Collection</h3>
        <p class="card-desc">Be the room. Iridescent fabrics, sharp cuts and statement pieces designed to own every celebration you walk into.</p>
        <a href="#products" class="card-link">Explore Line</a>
      </div>

    </div>
  </div>
</section>

<!-- PRODUCTS -->
<section id="products">
  <div style="max-width:1400px; margin:0 auto; padding:8rem 5%; background:var(--black-2);">
    <div class="reveal">
      <div class="section-label">This Season's Drops</div>
      <h2 class="section-title">Featured <strong>Pieces</strong></h2>
    </div>
    <div class="products-grid">

      <!-- Product 1 -->
      <div class="product-card reveal">
        <div class="product-visual">
          <svg viewBox="0 0 200 260" fill="none" xmlns="http://www.w3.org/2000/svg">
            <defs>
              <linearGradient id="jGrad" x1="0" y1="0" x2="1" y2="1">
                <stop offset="0%" stop-color="#1a1a1a"/>
                <stop offset="100%" stop-color="#0a0a0a"/>
              </linearGradient>
            </defs>
            <path d="M40 40 L50 10 L100 20 L150 10 L160 40 L180 160 L160 180 L40 180 L20 160Z" fill="url(#jGrad)" stroke="rgba(201,168,76,0.4)" stroke-width="1.5"/>
            <path d="M60 10 L100 60 L140 10" stroke="rgba(201,168,76,0.3)" stroke-width="1" fill="none"/>
            <path d="M50 10 L20 160" stroke="rgba(201,168,76,0.1)" stroke-width="8" fill="none"/>
            <rect x="88" y="12" width="24" height="40" fill="#111" stroke="rgba(201,168,76,0.3)" stroke-width="1"/>
            <text x="100" y="130" text-anchor="middle" font-family="monospace" font-size="14" fill="rgba(201,168,76,0.4)" letter-spacing="3">2D</text>
            <circle cx="100" cy="20" r="3" fill="#C9A84C"/>
            <path d="M30 180 L30 250 L80 250" stroke="rgba(201,168,76,0.2)" stroke-width="1.5" fill="none"/>
            <path d="M170 180 L170 250 L120 250" stroke="rgba(201,168,76,0.2)" stroke-width="1.5" fill="none"/>
          </svg>
        </div>
        <div class="product-overlay"></div>
        <div class="product-badge">New Drop</div>
        <button class="add-btn">+</button>
        <div class="product-info">
          <div class="product-tag">Streetwear</div>
          <div class="product-name">Apex Bomber Jacket</div>
          <div class="product-price">Starting <span>₹2,499</span></div>
        </div>
      </div>

      <!-- Product 2 -->
      <div class="product-card reveal reveal-delay-1">
        <div class="product-visual">
          <svg viewBox="0 0 200 260" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M60 20 L100 30 L140 20 L155 80 L160 220 L40 220 L45 80Z" fill="#111" stroke="rgba(201,168,76,0.35)" stroke-width="1.5"/>
            <line x1="60" y1="20" x2="45" y2="80" stroke="rgba(201,168,76,0.25)" stroke-width="1"/>
            <line x1="140" y1="20" x2="155" y2="80" stroke="rgba(201,168,76,0.25)" stroke-width="1"/>
            <line x1="100" y1="30" x2="100" y2="220" stroke="rgba(201,168,76,0.1)" stroke-width="1" stroke-dasharray="4,4"/>
            <rect x="86" y="34" width="28" height="32" rx="14" fill="rgba(201,168,76,0.08)" stroke="rgba(201,168,76,0.3)" stroke-width="1"/>
            <text x="100" y="150" text-anchor="middle" font-family="monospace" font-size="11" fill="rgba(201,168,76,0.35)" letter-spacing="2">2DUDES</text>
          </svg>
        </div>
        <div class="product-overlay"></div>
        <button class="add-btn">+</button>
        <div class="product-info">
          <div class="product-tag">Casual</div>
          <div class="product-name">Signature Oversized Tee</div>
          <div class="product-price">Starting <span>₹899</span></div>
        </div>
      </div>

      <!-- Product 3 -->
      <div class="product-card reveal reveal-delay-2">
        <div class="product-visual">
          <svg viewBox="0 0 200 260" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M50 10 L70 0 L130 0 L150 10 L165 50 L155 220 L45 220 L35 50Z" fill="#0f0f0f" stroke="rgba(201,168,76,0.45)" stroke-width="1.5"/>
            <path d="M50 10 L35 50" stroke="rgba(201,168,76,0.3)" stroke-width="1"/>
            <path d="M150 10 L165 50" stroke="rgba(201,168,76,0.3)" stroke-width="1"/>
            <path d="M70 0 L80 30 L100 20 L120 30 L130 0" stroke="rgba(201,168,76,0.4)" stroke-width="1" fill="rgba(201,168,76,0.04)"/>
            <line x1="45" y1="220" x2="45" y2="260" stroke="rgba(201,168,76,0.2)" stroke-width="8" stroke-linecap="round"/>
            <line x1="155" y1="220" x2="155" y2="260" stroke="rgba(201,168,76,0.2)" stroke-width="8" stroke-linecap="round"/>
            <text x="100" y="140" text-anchor="middle" font-family="monospace" font-size="10" fill="rgba(201,168,76,0.4)" letter-spacing="3">PREMIUM</text>
          </svg>
        </div>
        <div class="product-overlay"></div>
        <div class="product-badge">Best Seller</div>
        <button class="add-btn">+</button>
        <div class="product-info">
          <div class="product-tag">Premium</div>
          <div class="product-name">Elite Tailored Suit</div>
          <div class="product-price">Starting <span>₹5,999</span></div>
        </div>
      </div>

      <!-- Product 4 -->
      <div class="product-card reveal reveal-delay-3">
        <div class="product-visual">
          <svg viewBox="0 0 200 260" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M70 5 L130 5 L140 80 L150 240 L50 240 L60 80Z" fill="#111" stroke="rgba(201,168,76,0.3)" stroke-width="1.5"/>
            <path d="M70 5 L60 80" stroke="rgba(201,168,76,0.2)" stroke-width="8" fill="none"/>
            <path d="M130 5 L140 80" stroke="rgba(201,168,76,0.2)" stroke-width="8" fill="none"/>
            <rect x="60" y="80" width="80" height="3" fill="rgba(201,168,76,0.3)"/>
            <text x="100" y="170" text-anchor="middle" font-family="monospace" font-size="12" fill="rgba(201,168,76,0.35)" letter-spacing="2">CARGØ</text>
          </svg>
        </div>
        <div class="product-overlay"></div>
        <button class="add-btn">+</button>
        <div class="product-info">
          <div class="product-tag">Streetwear</div>
          <div class="product-name">Urban Cargo Pants</div>
          <div class="product-price">Starting <span>₹1,799</span></div>
        </div>
      </div>

      <!-- Product 5 -->
      <div class="product-card reveal">
        <div class="product-visual">
          <svg viewBox="0 0 200 260" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M40 50 L60 10 L100 25 L140 10 L160 50 L170 80 L30 80Z" fill="#111" stroke="rgba(201,168,76,0.4)" stroke-width="1.5"/>
            <path d="M30 80 L35 240 L90 240 L100 160 L110 240 L165 240 L170 80Z" fill="#0f0f0f" stroke="rgba(201,168,76,0.25)" stroke-width="1"/>
            <path d="M60 10 L40 50" stroke="rgba(201,168,76,0.2)" stroke-width="6" stroke-linecap="round" fill="none"/>
            <path d="M140 10 L160 50" stroke="rgba(201,168,76,0.2)" stroke-width="6" stroke-linecap="round" fill="none"/>
            <text x="100" y="130" text-anchor="middle" font-family="monospace" font-size="10" fill="rgba(201,168,76,0.4)" letter-spacing="2">HOODIE</text>
          </svg>
        </div>
        <div class="product-overlay"></div>
        <div class="product-badge">Limited</div>
        <button class="add-btn">+</button>
        <div class="product-info">
          <div class="product-tag">Party</div>
          <div class="product-name">Gold Edition Hoodie</div>
          <div class="product-price">Starting <span>₹2,199</span></div>
        </div>
      </div>

      <!-- Product 6 -->
      <div class="product-card reveal reveal-delay-1">
        <div class="product-visual">
          <svg viewBox="0 0 200 260" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M55 0 L145 0 L160 60 L160 240 L40 240 L40 60Z" fill="#111" stroke="rgba(201,168,76,0.35)" stroke-width="1.5"/>
            <path d="M80 0 L85 40 L100 30 L115 40 L120 0" fill="rgba(201,168,76,0.04)" stroke="rgba(201,168,76,0.4)" stroke-width="1"/>
            <rect x="40" y="100" width="120" height="1" fill="rgba(201,168,76,0.15)"/>
            <rect x="40" y="170" width="120" height="1" fill="rgba(201,168,76,0.15)"/>
            <text x="100" y="140" text-anchor="middle" font-family="monospace" font-size="10" fill="rgba(201,168,76,0.35)" letter-spacing="2">TRACKSUIT</text>
          </svg>
        </div>
        <div class="product-overlay"></div>
        <button class="add-btn">+</button>
        <div class="product-info">
          <div class="product-tag">Casual</div>
          <div class="product-name">Velour Tracksuit Set</div>
          <div class="product-price">Starting <span>₹3,299</span></div>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-visual reveal">
    <div class="about-frame">
      <div class="about-frame-inner">
        <div class="about-frame-inner-2">
          <div class="about-center-icon">👑</div>
        </div>
      </div>
    </div>
    <div class="about-tag about-tag-1">✦ Est. 2020</div>
    <div class="about-tag about-tag-2">Premium Quality →</div>
    <div class="about-tag about-tag-3">← 2400+ Happy Clients</div>
  </div>

  <div class="about-content">
    <div class="reveal">
      <div class="section-label">Our Story</div>
      <h2 class="section-title">Born from the<br><strong>Streets</strong>,<br>Built for Kings</h2>
    </div>
    <div class="about-lead reveal reveal-delay-1">
      "We didn't just start a clothing brand. We started a movement — a declaration that every man deserves to dress like he owns the world."
    </div>
    <p class="about-text reveal reveal-delay-2">
      2 Dudes was born in the streets of passion and ambition. Two friends, one vision — to create fashion that doesn't just cover your body, but tells your story. Every stitch is a statement. Every fabric choice, a philosophy.
    </p>
    <p class="about-text reveal reveal-delay-3">
      We source the finest materials, collaborate with avant-garde designers, and push the boundaries of what streetwear can be. From casual Sundays to charged Friday nights — we dress the moments that matter.
    </p>
    <div class="about-values reveal reveal-delay-4">
      <div class="value-item">
        <div class="value-icon">🧵</div>
        <div class="value-title">Craftsmanship</div>
        <div class="value-text">Every piece hand-inspected for flawless finish and premium quality.</div>
      </div>
      <div class="value-item">
        <div class="value-icon">🔥</div>
        <div class="value-title">Edge & Identity</div>
        <div class="value-text">Designs that speak before you do — fearless, bold, iconic.</div>
      </div>
      <div class="value-item">
        <div class="value-icon">♻️</div>
        <div class="value-title">Conscious Fashion</div>
        <div class="value-text">Sustainably sourced fabrics for a wardrobe you're proud of.</div>
      </div>
      <div class="value-item">
        <div class="value-icon">🌍</div>
        <div class="value-title">Global Vision</div>
        <div class="value-text">Local roots, global standards — fashion without borders.</div>
      </div>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section id="testimonials">
  <div style="max-width:1400px; margin:0 auto; padding:0 5%;">
    <div class="reveal">
      <div class="section-label">What People Say</div>
      <h2 class="section-title">Voices of the <strong>Street</strong></h2>
    </div>
  </div>
  <div class="testimonials-track-wrapper" style="margin-top:4rem;">
    <div class="testimonials-track" id="testimonialsTrack">

      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"I wore the Premium Fit suit to a wedding and people thought I was from Milan. The quality is absolutely insane for this price. 2 Dudes is a revelation."</p>
        <div class="testimonial-author">
          <div class="author-avatar">AK</div>
          <div>
            <div class="author-name">Arjun Kapoor</div>
            <div class="author-loc">Mumbai, Maharashtra</div>
          </div>
        </div>
      </div>

      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"The Streetwear collection hits different. Every piece has this raw energy. People stop me on the road to ask where I got my jacket. Always 2 Dudes."</p>
        <div class="testimonial-author">
          <div class="author-avatar">RV</div>
          <div>
            <div class="author-name">Rohan Verma</div>
            <div class="author-loc">Delhi, NCR</div>
          </div>
        </div>
      </div>

      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"Ordered the Gold Edition Hoodie for my birthday night out. My entire squad was jealous. The fit, the fabric, the feel — nothing compares. Worth every rupee."</p>
        <div class="testimonial-author">
          <div class="author-avatar">SK</div>
          <div>
            <div class="author-name">Samarth Kulkarni</div>
            <div class="author-loc">Pune, Maharashtra</div>
          </div>
        </div>
      </div>

      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"The casual wear is genuinely high quality — I've washed it 20 times and it still looks fresh. This is what fashion should feel like. 2 Dudes is my go-to forever."</p>
        <div class="testimonial-author">
          <div class="author-avatar">MS</div>
          <div>
            <div class="author-name">Mihir Shah</div>
            <div class="author-loc">Ahmedabad, Gujarat</div>
          </div>
        </div>
      </div>

      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"I was skeptical at first — but then I saw the tailoring. This isn't just a brand, it's an experience. The Party Collection made me look like a Bollywood star."</p>
        <div class="testimonial-author">
          <div class="author-avatar">NP</div>
          <div>
            <div class="author-name">Nikhil Patil</div>
            <div class="author-loc">Nagpur, Maharashtra</div>
          </div>
        </div>
      </div>

      <!-- Duplicate for seamless loop -->
      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"I wore the Premium Fit suit to a wedding and people thought I was from Milan. The quality is absolutely insane for this price. 2 Dudes is a revelation."</p>
        <div class="testimonial-author">
          <div class="author-avatar">AK</div>
          <div>
            <div class="author-name">Arjun Kapoor</div>
            <div class="author-loc">Mumbai, Maharashtra</div>
          </div>
        </div>
      </div>
      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"The Streetwear collection hits different. Every piece has this raw energy. People stop me on the road to ask where I got my jacket. Always 2 Dudes."</p>
        <div class="testimonial-author">
          <div class="author-avatar">RV</div>
          <div>
            <div class="author-name">Rohan Verma</div>
            <div class="author-loc">Delhi, NCR</div>
          </div>
        </div>
      </div>
      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"Ordered the Gold Edition Hoodie for my birthday night out. My entire squad was jealous. The fit, the fabric, the feel — nothing compares. Worth every rupee."</p>
        <div class="testimonial-author">
          <div class="author-avatar">SK</div>
          <div>
            <div class="author-name">Samarth Kulkarni</div>
            <div class="author-loc">Pune, Maharashtra</div>
          </div>
        </div>
      </div>
      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"The casual wear is genuinely high quality — I've washed it 20 times and it still looks fresh. This is what fashion should feel like. 2 Dudes is my go-to forever."</p>
        <div class="testimonial-author">
          <div class="author-avatar">MS</div>
          <div>
            <div class="author-name">Mihir Shah</div>
            <div class="author-loc">Ahmedabad, Gujarat</div>
          </div>
        </div>
      </div>
      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"I was skeptical at first — but then I saw the tailoring. This isn't just a brand, it's an experience. The Party Collection made me look like a Bollywood star."</p>
        <div class="testimonial-author">
          <div class="author-avatar">NP</div>
          <div>
            <div class="author-name">Nikhil Patil</div>
            <div class="author-loc">Nagpur, Maharashtra</div>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-inner">
    <div class="reveal">
      <div class="section-label">Get In Touch</div>
      <h2 class="section-title">Ready to<br><strong>Own the Street?</strong></h2>
      <p class="contact-subtitle">Reach out to us directly. Our team responds fast. Whether it's custom orders, bulk enquiries, or just good vibes — we're here.</p>
    </div>
    <div class="contact-cards reveal reveal-delay-1">
      <a href="https://wa.me/919999999999?text=Hey%202%20Dudes!%20I%20want%20to%20shop%20your%20collection%20🔥" target="_blank" class="contact-card">
        <div class="contact-card-icon">💬</div>
        <div class="contact-card-label">WhatsApp</div>
        <div class="contact-card-value">Chat With Us</div>
        <div class="contact-card-action">Tap to open WhatsApp →</div>
      </a>
      <a href="https://instagram.com/2dudesofficial" target="_blank" class="contact-card">
        <div class="contact-card-icon">📸</div>
        <div class="contact-card-label">Instagram</div>
        <div class="contact-card-value">@2dudesofficial</div>
        <div class="contact-card-action">Follow for drops & exclusives →</div>
      </a>
    </div>
    <div class="reveal reveal-delay-2">
      <a href="https://wa.me/919999999999?text=Hey%202%20Dudes!%20I%20want%20to%20shop%20your%20collection%20🔥" target="_blank" class="btn-primary" style="display:inline-block; text-decoration:none;">
        <span>Shop Now on WhatsApp</span>
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-top">
    <div>
      <div class="footer-brand-name">2 DUDES</div>
      <p class="footer-brand-text">Wear Confidence. Own the Street. Premium fashion crafted for those who dare to stand apart from the crowd.</p>
      <div class="footer-socials">
        <a href="https://instagram.com" target="_blank" class="social-btn" title="Instagram">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg>
        </a>
        <a href="https://wa.me/919999999999" target="_blank" class="social-btn" title="WhatsApp">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
        </a>
      </div>
    </div>
    <div class="footer-col">
      <h4>Collections</h4>
      <ul>
        <li><a href="#collections">Streetwear</a></li>
        <li><a href="#collections">Casual Wear</a></li>
        <li><a href="#collections">Premium Fits</a></li>
        <li><a href="#collections">Party Collection</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Company</h4>
      <ul>
        <li><a href="#about">Our Story</a></li>
        <li><a href="#products">New Arrivals</a></li>
        <li><a href="#testimonials">Reviews</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Support</h4>
      <ul>
        <li><a href="#">Size Guide</a></li>
        <li><a href="#">Shipping Policy</a></li>
        <li><a href="#">Returns</a></li>
        <li><a href="#">Track Order</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <span>© 2025 2 Dudes. All Rights Reserved.</span>
    <span style="color:rgba(201,168,76,.3);">Wear Confidence. Own the Street.</span>
  </div>
</footer>

<script>
// ── CUSTOM CURSOR ──
const cursor = document.getElementById('cursor');
const cursorRing = document.getElementById('cursor-ring');
let mx=0, my=0, rx=0, ry=0;
document.addEventListener('mousemove', e => { mx=e.clientX; my=e.clientY; });
(function loop(){
  rx += (mx-rx)*.18; ry += (my-ry)*.18;
  cursor.style.left = mx+'px'; cursor.style.top = my+'px';
  cursorRing.style.left = rx+'px'; cursorRing.style.top = ry+'px';
  requestAnimationFrame(loop);
})();
document.querySelectorAll('a, button, .collection-card, .product-card').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.width='6px'; cursor.style.height='6px';
    cursorRing.style.width='60px'; cursorRing.style.height='60px';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.width='10px'; cursor.style.height='10px';
    cursorRing.style.width='36px'; cursorRing.style.height='36px';
  });
});

// ── NAVBAR SCROLL ──
const nav = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 80);
});

// ── MOBILE MENU ──
const hamburger = document.getElementById('hamburger');
const mobileMenu = document.getElementById('mobileMenu');
hamburger.addEventListener('click', () => {
  mobileMenu.classList.toggle('open');
});
mobileMenu.querySelectorAll('a').forEach(a => a.addEventListener('click', () => mobileMenu.classList.remove('open')));

// ── SCROLL REVEAL ──
const revealEls = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => { if(e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.12 });
revealEls.forEach(el => observer.observe(el));

// ── COUNT UP ──
const countEls = document.querySelectorAll('[data-count]');
const countObserver = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (!e.isIntersecting) return;
    const el = e.target;
    const target = +el.dataset.count;
    let cur = 0;
    const step = target / 60;
    const interval = setInterval(() => {
      cur = Math.min(cur + step, target);
      el.textContent = (cur >= 1000 ? Math.round(cur/100)*100 : Math.round(cur));
      if (cur >= target) {
        el.textContent = target >= 1000 ? (target/1000).toFixed(1)+'K+' : target+'+';
        clearInterval(interval);
      }
    }, 20);
    countObserver.unobserve(el);
  });
}, { threshold: .5 });
countEls.forEach(el => countObserver.observe(el));

// ── PARTICLES ──
const particleContainer = document.getElementById('particles');
for(let i=0; i<20; i++) {
  const p = document.createElement('div');
  p.className = 'particle';
  const size = Math.random() * 3 + 1;
  p.style.cssText = `
    width:${size}px; height:${size}px;
    left:${Math.random()*100}%;
    bottom:${Math.random()*40}%;
    --drift:${(Math.random()-0.5)*60}px;
    animation-duration:${3+Math.random()*4}s;
    animation-delay:${Math.random()*5}s;
  `;
  particleContainer.appendChild(p);
}

// ── PARALLAX ──
document.addEventListener('mousemove', e => {
  const cx = window.innerWidth/2, cy = window.innerHeight/2;
  const dx = (e.clientX-cx)/cx, dy = (e.clientY-cy)/cy;
  const mannequin = document.querySelector('.mannequin-wrapper');
  if (mannequin) {
    mannequin.style.transform = `perspective(1200px) rotateY(${dx*5}deg) rotateX(${-dy*3}deg) translateY(0px)`;
  }
});

// ── SMOOTH ANCHOR SCROLL ──
document.querySelectorAll('a[href^="#"]').forEach(a => {
  a.addEventListener('click', e => {
    const target = document.querySelector(a.getAttribute('href'));
    if(target) { e.preventDefault(); target.scrollIntoView({behavior:'smooth'}); }
  });
});

// ── PARALLAX SECTIONS ──
window.addEventListener('scroll', () => {
  const sy = window.scrollY;
  const heroBg = document.querySelector('.hero-bg');
  if (heroBg) heroBg.style.transform = `translateY(${sy*.3}px)`;
});
</script>
</body>
</html>
