<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SIRUP'S ROOTS</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;900&family=Bebas+Neue&display=swap');

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg: #0a0a0f;
    --dark: #0d0d1a;
    --accent1: #c94b4b;
    --accent2: #4b6cb7;
    --accent3: #a855f7;
    --text: #e8e8f0;
    --muted: #888;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Inter', sans-serif;
    background: var(--bg);
    color: var(--text);
    overflow-x: hidden;
  }

  /* ===== SCROLLBAR ===== */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--accent1); border-radius: 2px; }

  /* ===== NOISE OVERLAY ===== */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 9999;
    opacity: 0.4;
  }

  /* ===== PAGES ===== */
  .page { display: none; min-height: 100vh; }
  .page.active { display: block; animation: fadeInUp 0.6s ease forwards; }

  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ===== HEADER ===== */
  header {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 1000;
    padding: 20px 40px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: linear-gradient(to bottom, rgba(10,10,15,0.95) 0%, transparent 100%);
    backdrop-filter: blur(0px);
  }

  .header-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 22px;
    letter-spacing: 4px;
    color: var(--text);
    cursor: pointer;
    transition: color 0.3s;
  }
  .header-logo:hover { color: var(--accent1); }

  nav {
    display: flex;
    align-items: center;
    gap: 36px;
  }

  nav a {
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.6);
    text-decoration: none;
    cursor: pointer;
    transition: color 0.3s;
    position: relative;
  }

  nav a::after {
    content: '';
    position: absolute;
    bottom: -4px;
    left: 0; right: 0;
    height: 1px;
    background: var(--accent1);
    transform: scaleX(0);
    transition: transform 0.3s ease;
  }

  nav a:hover, nav a.active {
    color: var(--text);
  }
  nav a:hover::after, nav a.active::after { transform: scaleX(1); }

  .menu-btn {
    display: none;
    flex-direction: column;
    gap: 5px;
    cursor: pointer;
    padding: 5px;
  }
  .menu-btn span {
    display: block;
    width: 28px; height: 2px;
    background: var(--text);
    transition: all 0.3s;
  }

  /* ===== MOBILE MENU ===== */
  .mobile-menu {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(10,10,15,0.98);
    z-index: 999;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 40px;
  }
  .mobile-menu.open { display: flex; animation: fadeInUp 0.3s ease; }
  .mobile-menu a {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 48px;
    letter-spacing: 8px;
    color: var(--text);
    text-decoration: none;
    cursor: pointer;
    transition: color 0.3s;
  }
  .mobile-menu a:hover { color: var(--accent1); }
  .close-menu {
    position: absolute;
    top: 24px; right: 40px;
    font-size: 32px;
    cursor: pointer;
    color: var(--text);
  }

  /* ===== HOME PAGE ===== */
  #home {
    position: relative;
    min-height: 100vh;
    overflow: hidden;
  }

  .home-bg {
    position: absolute;
    inset: 0;
    background: 
      radial-gradient(ellipse 60% 80% at 80% 50%, rgba(74,107,183,0.35) 0%, transparent 70%),
      radial-gradient(ellipse 50% 60% at 20% 80%, rgba(201,75,75,0.4) 0%, transparent 60%),
      radial-gradient(ellipse 40% 40% at 50% 20%, rgba(168,85,247,0.15) 0%, transparent 50%),
      linear-gradient(135deg, #0a0a0f 0%, #141428 100%);
  }

  /* Big circle */
  .home-circle {
    position: absolute;
    bottom: -10%;
    left: -5%;
    width: 55vw;
    height: 55vw;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(30,30,60,0.8) 0%, rgba(15,15,30,0.4) 60%, transparent 100%);
    border: 1px solid rgba(255,255,255,0.04);
    animation: rotateSlow 30s linear infinite;
  }

  @keyframes rotateSlow {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  .hero-content {
    position: relative;
    z-index: 10;
    padding: 140px 60px 60px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    align-items: center;
    min-height: 100vh;
  }

  .hero-left {}

  .hero-subtitle {
    font-size: 11px;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.45);
    margin-bottom: 16px;
    font-weight: 400;
  }

  .hero-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(80px, 12vw, 180px);
    line-height: 0.9;
    letter-spacing: 2px;
    background: linear-gradient(135deg, #ffffff 0%, rgba(255,255,255,0.6) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 24px;
    position: relative;
  }

  .hero-title::before {
    content: 'ROOTS';
    position: absolute;
    top: 4px; left: 4px;
    background: linear-gradient(135deg, rgba(201,75,75,0.4) 0%, transparent 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    z-index: -1;
  }

  .hero-sirup {
    font-size: 13px;
    letter-spacing: 8px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.5);
    margin-bottom: 32px;
    font-weight: 300;
  }

  .hero-desc {
    font-size: 14px;
    line-height: 2;
    color: rgba(232,232,240,0.55);
    max-width: 440px;
    margin-bottom: 48px;
    font-weight: 300;
  }

  .hero-cta-group {
    display: flex;
    align-items: center;
    gap: 24px;
    flex-wrap: wrap;
  }

  .btn-primary {
    background: transparent;
    border: 1px solid rgba(232,232,240,0.3);
    color: var(--text);
    padding: 14px 36px;
    font-size: 10px;
    letter-spacing: 4px;
    text-transform: uppercase;
    cursor: pointer;
    transition: all 0.4s;
    position: relative;
    overflow: hidden;
    text-decoration: none;
    display: inline-block;
  }

  .btn-primary::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, var(--accent1), var(--accent2));
    transform: translateX(-100%);
    transition: transform 0.4s ease;
    z-index: -1;
  }

  .btn-primary:hover { border-color: transparent; color: white; }
  .btn-primary:hover::before { transform: translateX(0); }

  .btn-circle {
    width: 120px; height: 120px;
    border-radius: 50%;
    background: rgba(20,20,40,0.6);
    border: 1px solid rgba(255,255,255,0.1);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-size: 9px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.7);
    cursor: pointer;
    transition: all 0.4s;
    text-align: center;
    line-height: 1.8;
  }

  .btn-circle:hover {
    background: rgba(201,75,75,0.2);
    border-color: var(--accent1);
    color: var(--text);
    transform: scale(1.05);
  }

  /* Vertical text right side */
  .vertical-text {
    position: absolute;
    right: 0;
    top: 50%;
    transform: translateY(-50%) rotate(90deg);
    font-size: 10px;
    letter-spacing: 6px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.2);
    white-space: nowrap;
    transform-origin: right center;
  }

  .hero-right {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 16px;
    position: relative;
  }

  .hero-img-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
    width: 100%;
  }

  .hero-img-item {
    aspect-ratio: 3/4;
    overflow: hidden;
    position: relative;
    background: #1a1a2e;
  }

  .hero-img-item img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.6s ease;
    filter: grayscale(20%) contrast(1.1);
  }

  .hero-img-item:hover img { transform: scale(1.05); }

  .hero-img-item::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(to bottom, transparent 60%, rgba(10,10,20,0.6) 100%);
  }

  /* Placeholder images */
  .img-placeholder {
    width: 100%;
    height: 100%;
    background: linear-gradient(135deg, #1a1a30, #2d2d50);
    display: flex;
    align-items: center;
    justify-content: center;
    color: rgba(255,255,255,0.1);
    font-size: 32px;
  }

  /* Scrolling ticker */
  .ticker-wrap {
    position: relative;
    overflow: hidden;
    background: rgba(201,75,75,0.12);
    border-top: 1px solid rgba(201,75,75,0.2);
    border-bottom: 1px solid rgba(201,75,75,0.2);
    padding: 14px 0;
    margin-top: 40px;
  }

  .ticker {
    display: flex;
    white-space: nowrap;
    animation: ticker 20s linear infinite;
    gap: 60px;
  }

  @keyframes ticker {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }

  .ticker span {
    font-size: 11px;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.4);
  }

  .ticker .dot {
    color: var(--accent1);
    font-size: 16px;
  }

  /* ===== ABOUT PAGE ===== */
  #about {
    padding: 120px 60px 80px;
    position: relative;
    min-height: 100vh;
  }

  #about::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 50% 50% at 90% 10%, rgba(168,85,247,0.15) 0%, transparent 60%),
      radial-gradient(ellipse 40% 60% at 10% 90%, rgba(74,107,183,0.2) 0%, transparent 60%);
    pointer-events: none;
  }

  .section-header {
    display: flex;
    align-items: flex-end;
    gap: 24px;
    margin-bottom: 80px;
  }

  .section-number {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 120px;
    line-height: 1;
    color: rgba(255,255,255,0.04);
    letter-spacing: -4px;
  }

  .section-title-block {}

  .section-label {
    font-size: 10px;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: var(--accent1);
    margin-bottom: 8px;
  }

  .section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(48px, 6vw, 80px);
    letter-spacing: 4px;
    line-height: 1;
  }

  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: start;
  }

  .about-img-wrap {
    position: relative;
  }

  .about-img {
    width: 100%;
    aspect-ratio: 3/4;
    background: linear-gradient(135deg, #1a1a2e 0%, #2d1f3d 100%);
    overflow: hidden;
    position: relative;
  }

  .about-img::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(201,75,75,0.2), rgba(74,107,183,0.2));
    z-index: 1;
  }

  .about-img-placeholder {
    width: 100%; height: 100%;
    background: linear-gradient(160deg, #151525 0%, #2a1a3a 50%, #1a2535 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 80px;
    color: rgba(255,255,255,0.05);
  }

  .about-img-tag {
    position: absolute;
    bottom: -20px;
    right: -20px;
    background: var(--accent1);
    padding: 20px 24px;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 14px;
    letter-spacing: 3px;
    z-index: 2;
  }

  .about-content {}

  .about-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 52px;
    letter-spacing: 4px;
    margin-bottom: 8px;
    background: linear-gradient(135deg, #fff, rgba(255,255,255,0.6));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .about-genre {
    font-size: 11px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--accent2);
    margin-bottom: 32px;
  }

  .about-bio {
    font-size: 14px;
    line-height: 2;
    color: rgba(232,232,240,0.6);
    margin-bottom: 24px;
    font-weight: 300;
  }

  .about-stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
    margin: 48px 0;
    padding: 32px 0;
    border-top: 1px solid rgba(255,255,255,0.06);
    border-bottom: 1px solid rgba(255,255,255,0.06);
  }

  .stat-item {}

  .stat-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 48px;
    line-height: 1;
    background: linear-gradient(135deg, var(--accent1), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 4px;
  }

  .stat-label {
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.4);
  }

  .influence-list {
    margin-top: 40px;
  }

  .influence-label {
    font-size: 10px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.35);
    margin-bottom: 16px;
  }

  .influence-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .tag {
    padding: 8px 18px;
    border: 1px solid rgba(255,255,255,0.1);
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.5);
    transition: all 0.3s;
    cursor: default;
  }

  .tag:hover {
    border-color: var(--accent1);
    color: var(--text);
    background: rgba(201,75,75,0.08);
  }

  /* ===== MUSIC PAGE ===== */
  #music {
    padding: 120px 60px 80px;
    min-height: 100vh;
    position: relative;
  }

  #music::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 60% 40% at 50% 0%, rgba(201,75,75,0.12) 0%, transparent 60%);
    pointer-events: none;
  }

  .music-featured {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
    margin-bottom: 60px;
  }

  .featured-track {
    position: relative;
    aspect-ratio: 1;
    overflow: hidden;
    cursor: pointer;
  }

  .featured-track:first-child {
    grid-row: span 2;
    aspect-ratio: auto;
  }

  .track-bg {
    width: 100%;
    height: 100%;
    background: linear-gradient(135deg, #1a1a2e, #2a1535);
    transition: transform 0.6s ease;
  }

  .featured-track:hover .track-bg { transform: scale(1.03); }

  .track-overlay {
    position: absolute;
    inset: 0;
    background: linear-gradient(to top, rgba(5,5,15,0.9) 0%, transparent 60%);
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 32px;
  }

  .track-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 80px;
    color: rgba(255,255,255,0.05);
    line-height: 1;
    margin-bottom: -20px;
  }

  .track-info {}

  .track-type {
    font-size: 9px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--accent1);
    margin-bottom: 8px;
  }

  .track-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 36px;
    letter-spacing: 2px;
    margin-bottom: 8px;
  }

  .track-desc {
    font-size: 12px;
    color: rgba(232,232,240,0.45);
    line-height: 1.6;
  }

  .play-btn {
    position: absolute;
    top: 24px; right: 24px;
    width: 48px; height: 48px;
    border-radius: 50%;
    border: 1px solid rgba(255,255,255,0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s;
    background: rgba(0,0,0,0.3);
    backdrop-filter: blur(10px);
    font-size: 16px;
  }

  .play-btn:hover {
    background: var(--accent1);
    border-color: var(--accent1);
  }

  /* Playlist grid */
  .music-subheader {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 32px;
  }

  .music-subheader h3 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 28px;
    letter-spacing: 3px;
    color: rgba(232,232,240,0.7);
  }

  .see-all {
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent1);
    cursor: pointer;
    transition: opacity 0.3s;
  }
  .see-all:hover { opacity: 0.7; }

  .playlist-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 20px;
  }

  .playlist-card {
    cursor: pointer;
    transition: transform 0.3s;
  }

  .playlist-card:hover { transform: translateY(-8px); }

  .playlist-cover {
    aspect-ratio: 1;
    background: linear-gradient(135deg, #1a1530, #2a2040);
    margin-bottom: 14px;
    overflow: hidden;
    position: relative;
  }

  .playlist-cover-inner {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 48px;
    color: rgba(255,255,255,0.05);
    transition: transform 0.4s;
  }

  .playlist-card:hover .playlist-cover-inner { transform: scale(1.05); }

  .playlist-cover::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(201,75,75,0.15), rgba(74,107,183,0.15));
    opacity: 0;
    transition: opacity 0.3s;
  }

  .playlist-card:hover .playlist-cover::after { opacity: 1; }

  .playlist-name {
    font-size: 13px;
    font-weight: 600;
    margin-bottom: 4px;
    letter-spacing: 0.5px;
  }

  .playlist-detail {
    font-size: 11px;
    color: rgba(232,232,240,0.4);
    letter-spacing: 1px;
  }

  /* Tracklist */
  .tracklist {
    margin-top: 60px;
    border-top: 1px solid rgba(255,255,255,0.05);
  }

  .track-row {
    display: grid;
    grid-template-columns: 40px 1fr auto auto;
    gap: 20px;
    align-items: center;
    padding: 18px 0;
    border-bottom: 1px solid rgba(255,255,255,0.04);
    cursor: pointer;
    transition: all 0.3s;
  }

  .track-row:hover { background: rgba(255,255,255,0.02); padding-left: 12px; }

  .track-idx {
    font-size: 13px;
    color: rgba(232,232,240,0.2);
    text-align: center;
    font-weight: 500;
  }

  .track-row:hover .track-idx { color: var(--accent1); }

  .track-name-col { font-size: 14px; font-weight: 400; }
  .track-artist { font-size: 12px; color: rgba(232,232,240,0.4); margin-top: 3px; }
  .track-duration { font-size: 12px; color: rgba(232,232,240,0.35); letter-spacing: 2px; }
  .track-badge {
    font-size: 9px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 4px 10px;
    border: 1px solid rgba(201,75,75,0.4);
    color: var(--accent1);
  }

  /* ===== GALLERY PAGE ===== */
  #gallery {
    padding: 120px 60px 80px;
    min-height: 100vh;
  }

  .gallery-masonry {
    columns: 3;
    column-gap: 12px;
    margin-top: 60px;
  }

  .gallery-item {
    break-inside: avoid;
    margin-bottom: 12px;
    overflow: hidden;
    position: relative;
    cursor: pointer;
  }

  .gallery-item-inner {
    width: 100%;
    transition: transform 0.5s ease;
  }

  .gallery-item:hover .gallery-item-inner { transform: scale(1.03); }

  .gallery-img-ph {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, #1a1a2e, #2a1535);
    color: rgba(255,255,255,0.04);
    font-size: 60px;
  }

  .gallery-img-ph.tall { aspect-ratio: 2/3; font-size: 80px; }
  .gallery-img-ph.wide { aspect-ratio: 4/3; font-size: 50px; }
  .gallery-img-ph.square { aspect-ratio: 1; font-size: 60px; }

  .gallery-item-overlay {
    position: absolute;
    inset: 0;
    background: linear-gradient(to top, rgba(5,5,15,0.8) 0%, transparent 50%);
    opacity: 0;
    transition: opacity 0.4s;
    display: flex;
    align-items: flex-end;
    padding: 20px;
  }

  .gallery-item:hover .gallery-item-overlay { opacity: 1; }

  .gallery-caption {
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.7);
  }

  /* Gallery filters */
  .gallery-filters {
    display: flex;
    gap: 4px;
    margin-bottom: 0;
  }

  .filter-btn {
    padding: 10px 24px;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    background: transparent;
    border: 1px solid rgba(255,255,255,0.08);
    color: rgba(232,232,240,0.4);
    cursor: pointer;
    transition: all 0.3s;
  }

  .filter-btn.active, .filter-btn:hover {
    background: var(--accent1);
    border-color: var(--accent1);
    color: white;
  }

  /* ===== CONTACT PAGE ===== */
  #contact {
    padding: 120px 60px 80px;
    min-height: 100vh;
    position: relative;
  }

  #contact::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 50% 60% at 80% 80%, rgba(74,107,183,0.2) 0%, transparent 60%);
    pointer-events: none;
  }

  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    margin-top: 60px;
  }

  .contact-info {}

  .contact-text {
    font-size: 14px;
    line-height: 2;
    color: rgba(232,232,240,0.55);
    margin-bottom: 48px;
    font-weight: 300;
  }

  .contact-links {
    display: flex;
    flex-direction: column;
    gap: 24px;
  }

  .contact-link {
    display: flex;
    align-items: center;
    gap: 20px;
    padding: 20px 0;
    border-bottom: 1px solid rgba(255,255,255,0.05);
    cursor: pointer;
    transition: all 0.3s;
    text-decoration: none;
    color: var(--text);
  }

  .contact-link:hover { padding-left: 16px; }

  .contact-link-icon {
    width: 44px; height: 44px;
    border: 1px solid rgba(255,255,255,0.1);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    transition: all 0.3s;
    flex-shrink: 0;
  }

  .contact-link:hover .contact-link-icon {
    background: var(--accent1);
    border-color: var(--accent1);
  }

  .contact-link-text { flex: 1; }
  .contact-link-platform {
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.35);
    margin-bottom: 4px;
  }
  .contact-link-handle { font-size: 15px; font-weight: 500; }

  .contact-link-arrow { color: rgba(232,232,240,0.2); transition: all 0.3s; }
  .contact-link:hover .contact-link-arrow { color: var(--accent1); transform: translateX(6px); }

  /* Form */
  .contact-form {}

  .form-group {
    margin-bottom: 24px;
  }

  .form-label {
    display: block;
    font-size: 9px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: rgba(232,232,240,0.35);
    margin-bottom: 10px;
  }

  .form-input, .form-textarea {
    width: 100%;
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.08);
    color: var(--text);
    padding: 14px 18px;
    font-family: 'Inter', sans-serif;
    font-size: 14px;
    transition: all 0.3s;
    outline: none;
  }

  .form-input:focus, .form-textarea:focus {
    border-color: rgba(201,75,75,0.5);
    background: rgba(201,75,75,0.04);
  }

  .form-textarea {
    height: 140px;
    resize: vertical;
  }

  .form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  .form-submit {
    width: 100%;
    padding: 16px;
    background: linear-gradient(135deg, var(--accent1), var(--accent2));
    border: none;
    color: white;
    font-family: 'Inter', sans-serif;
    font-size: 10px;
    letter-spacing: 5px;
    text-transform: uppercase;
    cursor: pointer;
    transition: all 0.4s;
    margin-top: 8px;
  }

  .form-submit:hover {
    transform: translateY(-2px);
    box-shadow: 0 20px 60px rgba(201,75,75,0.3);
  }

  /* ===== FOOTER ===== */
  footer {
    background: rgba(5,5,12,0.8);
    border-top: 1px solid rgba(255,255,255,0.05);
    padding: 40px 60px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .footer-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 20px;
    letter-spacing: 5px;
    color: rgba(232,232,240,0.3);
  }

  .footer-copy {
    font-size: 11px;
    letter-spacing: 2px;
    color: rgba(232,232,240,0.2);
  }

  .footer-links {
    display: flex;
    gap: 28px;
  }

  .footer-links a {
    font-size: 10px;
    letter-spacing: 2px;
    color: rgba(232,232,240,0.25);
    text-decoration: none;
    text-transform: uppercase;
    transition: color 0.3s;
    cursor: pointer;
  }
  .footer-links a:hover { color: var(--accent1); }

  /* ===== CURSOR ===== */
  .cursor {
    position: fixed;
    width: 8px; height: 8px;
    background: var(--accent1);
    border-radius: 50%;
    pointer-events: none;
    z-index: 99999;
    transition: transform 0.1s ease;
    transform: translate(-50%, -50%);
  }

  .cursor-ring {
    position: fixed;
    width: 36px; height: 36px;
    border: 1px solid rgba(201,75,75,0.4);
    border-radius: 50%;
    pointer-events: none;
    z-index: 99998;
    transition: all 0.15s ease;
    transform: translate(-50%, -50%);
  }

  /* ===== PAGE TRANSITION ===== */
  .page-transition {
    position: fixed;
    inset: 0;
    background: var(--accent1);
    z-index: 9998;
    transform: scaleY(0);
    transform-origin: top;
  }

  .page-transition.animating {
    animation: wipeDown 0.5s ease forwards;
  }

  @keyframes wipeDown {
    0% { transform: scaleY(0); transform-origin: top; }
    50% { transform: scaleY(1); transform-origin: top; }
    51% { transform-origin: bottom; }
    100% { transform: scaleY(0); transform-origin: bottom; }
  }

  /* ===== RESPONSIVE ===== */
  @media (max-width: 1024px) {
    .hero-content { grid-template-columns: 1fr; padding: 120px 40px 60px; }
    .hero-img-grid { grid-template-columns: repeat(4, 1fr); }
    .hero-right { align-items: flex-start; }
    .about-grid { grid-template-columns: 1fr; }
    .music-featured { grid-template-columns: 1fr; }
    .featured-track:first-child { grid-row: auto; }
    .contact-grid { grid-template-columns: 1fr; }
    .gallery-masonry { columns: 2; }
    .playlist-grid { grid-template-columns: repeat(2, 1fr); }
  }

  @media (max-width: 768px) {
    header { padding: 16px 20px; }
    nav { display: none; }
    .menu-btn { display: flex; }
    .hero-content { padding: 100px 20px 40px; }
    .hero-title { font-size: 80px; }
    #about, #music, #gallery, #contact { padding: 100px 20px 60px; }
    footer { flex-direction: column; gap: 20px; text-align: center; padding: 30px 20px; }
    .gallery-masonry { columns: 2; }
    .playlist-grid { grid-template-columns: repeat(2, 1fr); }
    .about-stats { grid-template-columns: repeat(3, 1fr); }
    .form-row { grid-template-columns: 1fr; }
  }

  @media (max-width: 480px) {
    .gallery-masonry { columns: 1; }
    .playlist-grid { grid-template-columns: 1fr; }
  }

  /* ===== LOADING ===== */
  .loader {
    position: fixed;
    inset: 0;
    background: var(--bg);
    z-index: 99997;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    transition: opacity 0.8s ease;
  }

  .loader.hidden { opacity: 0; pointer-events: none; }

  .loader-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 80px;
    letter-spacing: 8px;
    color: white;
    clip-path: inset(0 100% 0 0);
    animation: revealText 1.2s ease 0.3s forwards;
  }

  .loader-sub {
    font-size: 10px;
    letter-spacing: 8px;
    text-transform: uppercase;
    color: rgba(255,255,255,0.3);
    margin-top: 16px;
    opacity: 0;
    animation: fadeIn 0.6s ease 1.2s forwards;
  }

  .loader-bar {
    width: 200px; height: 1px;
    background: rgba(255,255,255,0.1);
    margin-top: 48px;
    position: relative;
    overflow: hidden;
  }

  .loader-bar::after {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 0; height: 100%;
    background: var(--accent1);
    animation: loadBar 1.5s ease 0.2s forwards;
  }

  @keyframes revealText {
    to { clip-path: inset(0 0% 0 0); }
  }

  @keyframes fadeIn {
    to { opacity: 1; }
  }

  @keyframes loadBar {
    to { width: 100%; }
  }
</style>
</head>
<body>

<!-- LOADER -->
<div class="loader" id="loader">
  <div class="loader-title">ROOTS</div>
  <div class="loader-sub">SIRUP</div>
  <div class="loader-bar"></div>
</div>

<!-- CURSOR -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- PAGE TRANSITION -->
<div class="page-transition" id="pageTransition"></div>

<!-- HEADER -->
<header id="header">
  <div class="header-logo" onclick="navigateTo('home')">SIRUP</div>
  <nav id="mainNav">
    <a onclick="navigateTo('home')" class="active" data-page="home">Home</a>
    <a onclick="navigateTo('about')" data-page="about">About</a>
    <a onclick="navigateTo('music')" data-page="music">Music</a>
    <a onclick="navigateTo('gallery')" data-page="gallery">Gallery</a>
    <a onclick="navigateTo('contact')" data-page="contact">Contact</a>
  </nav>
  <div class="menu-btn" id="menuBtn" onclick="toggleMenu()">
    <span></span><span></span><span></span>
  </div>
</header>

<!-- MOBILE MENU -->
<div class="mobile-menu" id="mobileMenu">
  <div class="close-menu" onclick="toggleMenu()">✕</div>
  <a onclick="navigateTo('home'); toggleMenu()">Home</a>
  <a onclick="navigateTo('about'); toggleMenu()">About</a>
  <a onclick="navigateTo('music'); toggleMenu()">Music</a>
  <a onclick="navigateTo('gallery'); toggleMenu()">Gallery</a>
  <a onclick="navigateTo('contact'); toggleMenu()">Contact</a>
</div>

<!-- ============ HOME PAGE ============ -->
<div id="home" class="page active">
  <div class="home-bg"></div>
  <div class="home-circle"></div>
  <div class="vertical-text">Soul and R&amp;B and Hip-hop</div>

  <div class="hero-content">
    <div class="hero-left">
      <div class="hero-subtitle">SIRUP'S</div>
      <h1 class="hero-title">ROOTS</h1>
      <div class="hero-sirup">Music Roots Playlist</div>
      <p class="hero-desc">
        かつて掘り下げたネオソウルの楽曲から始まり<br>
        自身の"歌"のスタイルを確立する上で大きな影響を受けた<br>
        同時代のアーティストまで。<br>
        ラッパー、R&Bシンガー、バンドなど様々なジャンルの<br>
        アーティストと共演するSIRUPを理解するための<br>
        ヒントとなる楽曲をプレイリストとして振り返る。
      </p>
      <div class="hero-cta-group">
        <a class="btn-primary" onclick="navigateTo('music')">Listen Now</a>
        <div class="btn-circle" onclick="navigateTo('music')">
          ROOTS<br>PLAYLIST
        </div>
      </div>
    </div>

    <div class="hero-right">
      <div class="hero-img-grid">
        <div class="hero-img-item">
          <div class="img-placeholder" style="background:linear-gradient(160deg,#1a1535,#2d1a45);">🎵</div>
        </div>
        <div class="hero-img-item">
          <div class="img-placeholder" style="background:linear-gradient(160deg,#1a2535,#152535);">🎤</div>
        </div>
        <div class="hero-img-item">
          <div class="img-placeholder" style="background:linear-gradient(160deg,#251520,#3d1525);">🎧</div>
        </div>
        <div class="hero-img-item">
          <div class="img-placeholder" style="background:linear-gradient(160deg,#152020,#15302a);">🎶</div>
        </div>
      </div>
    </div>
  </div>

  <!-- Ticker -->
  <div class="ticker-wrap">
    <div class="ticker">
      <span>NEO SOUL</span><span class="dot">·</span>
      <span>R&amp;B</span><span class="dot">·</span>
      <span>HIP HOP</span><span class="dot">·</span>
      <span>SIRUP'S ROOTS</span><span class="dot">·</span>
      <span>PLAYLIST</span><span class="dot">·</span>
      <span>MUSIC</span><span class="dot">·</span>
      <span>SOUL</span><span class="dot">·</span>
      <span>NEO SOUL</span><span class="dot">·</span>
      <span>R&amp;B</span><span class="dot">·</span>
      <span>HIP HOP</span><span class="dot">·</span>
      <span>SIRUP'S ROOTS</span><span class="dot">·</span>
      <span>PLAYLIST</span><span class="dot">·</span>
      <span>MUSIC</span><span class="dot">·</span>
      <span>SOUL</span><span class="dot">·</span>
    </div>
  </div>

  <footer>
    <div class="footer-logo">SIRUP'S ROOTS</div>
    <div class="footer-copy">© 2024 SIRUP. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('about')">About</a>
      <a onclick="navigateTo('music')">Music</a>
      <a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ ABOUT PAGE ============ -->
<div id="about" class="page">
  <div class="section-header">
    <div class="section-number">01</div>
    <div class="section-title-block">
      <div class="section-label">Artist</div>
      <h2 class="section-title">ABOUT SIRUP</h2>
    </div>
  </div>

  <div class="about-grid">
    <div class="about-img-wrap">
      <div class="about-img">
        <div class="about-img-placeholder">♪</div>
      </div>
      <div class="about-img-tag">OSAKA, JAPAN</div>
    </div>

    <div class="about-content">
      <div class="about-name">SIRUP</div>
      <div class="about-genre">Neo Soul / R&amp;B / Hip-Hop</div>

      <p class="about-bio">
        SIRUPは大阪出身のシンガーソングライター。繊細なファルセットと深みのあるグルーヴが融合した独自のサウンドで、ジャンルの境界を超えたリスナーを魅了し続けている。
      </p>
      <p class="about-bio">
        ネオソウルのルーツから始まり、現代のR&amp;Bとヒップホップの影響を受けながら、彼は自身だけの音楽世界を構築してきた。その歌声は、聴く者の心の深いところに届く。
      </p>

      <div class="about-stats">
        <div class="stat-item">
          <div class="stat-num">5+</div>
          <div class="stat-label">Studio Albums</div>
        </div>
        <div class="stat-item">
          <div class="stat-num">50M</div>
          <div class="stat-label">Streams</div>
        </div>
        <div class="stat-item">
          <div class="stat-num">2015</div>
          <div class="stat-label">Debut Year</div>
        </div>
      </div>

      <div class="influence-list">
        <div class="influence-label">Musical Influences</div>
        <div class="influence-tags">
          <span class="tag">D'Angelo</span>
          <span class="tag">Frank Ocean</span>
          <span class="tag">Anderson Paak</span>
          <span class="tag">Kendrick Lamar</span>
          <span class="tag">Erykah Badu</span>
          <span class="tag">J Dilla</span>
          <span class="tag">Sade</span>
          <span class="tag">Thundercat</span>
          <span class="tag">H.E.R.</span>
          <span class="tag">SZA</span>
        </div>
      </div>
    </div>
  </div>

  <footer>
    <div class="footer-logo">SIRUP'S ROOTS</div>
    <div class="footer-copy">© 2024 SIRUP. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('home')">Home</a>
      <a onclick="navigateTo('music')">Music</a>
      <a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ MUSIC PAGE ============ -->
<div id="music" class="page">
  <div class="section-header">
    <div class="section-number">02</div>
    <div class="section-title-block">
      <div class="section-label">Discography</div>
      <h2 class="section-title">MUSIC</h2>
    </div>
  </div>

  <div class="music-featured">
    <div class="featured-track" style="min-height:400px;">
      <div class="track-bg" style="background:linear-gradient(135deg,#1a0a2e,#2d1545,#1a1535);min-height:400px;"></div>
      <div class="track-overlay">
        <div class="track-num">01</div>
        <div class="track-info">
          <div class="track-type">Latest Release</div>
          <div class="track-title">SIRUP'S ROOTS PLAYLIST</div>
          <div class="track-desc">A journey through the music that shaped SIRUP's sound — from neo-soul classics to modern R&amp;B.</div>
        </div>
      </div>
      <div class="play-btn">▶</div>
    </div>
    <div class="featured-track">
      <div class="track-bg" style="background:linear-gradient(135deg,#0a1a2e,#1a2545);aspect-ratio:1;"></div>
      <div class="track-overlay">
        <div class="track-num">02</div>
        <div class="track-info">
          <div class="track-type">Album</div>
          <div class="track-title">FEEL GOOD</div>
          <div class="track-desc">Sophomore album exploring love and loss.</div>
        </div>
      </div>
      <div class="play-btn">▶</div>
    </div>
    <div class="featured-track">
      <div class="track-bg" style="background:linear-gradient(135deg,#1a2a0a,#253020);aspect-ratio:1;"></div>
      <div class="track-overlay">
        <div class="track-num">03</div>
        <div class="track-info">
          <div class="track-type">EP</div>
          <div class="track-title">LOOP (FOREVER)</div>
          <div class="track-desc">An introspective journey in 5 tracks.</div>
        </div>
      </div>
      <div class="play-btn">▶</div>
    </div>
  </div>

  <!-- Playlist section -->
  <div class="music-subheader">
    <h3>ROOTS PLAYLIST</h3>
    <span class="see-all">See All ↗</span>
  </div>

  <div class="playlist-grid">
    <div class="playlist-card">
      <div class="playlist-cover">
        <div class="playlist-cover-inner" style="background:linear-gradient(135deg,#2d1535,#1a0a2e);">🎵</div>
      </div>
      <div class="playlist-name">Neo Soul Roots</div>
      <div class="playlist-detail">Vol. 1 · 18 tracks</div>
    </div>
    <div class="playlist-card">
      <div class="playlist-cover">
        <div class="playlist-cover-inner" style="background:linear-gradient(135deg,#0a1a35,#1a2545);">🎧</div>
      </div>
      <div class="playlist-name">R&amp;B Influences</div>
      <div class="playlist-detail">Vol. 2 · 24 tracks</div>
    </div>
    <div class="playlist-card">
      <div class="playlist-cover">
        <div class="playlist-cover-inner" style="background:linear-gradient(135deg,#1a1a0a,#2a2515);">🎤</div>
      </div>
      <div class="playlist-name">Hip Hop Vibes</div>
      <div class="playlist-detail">Vol. 3 · 16 tracks</div>
    </div>
    <div class="playlist-card">
      <div class="playlist-cover">
        <div class="playlist-cover-inner" style="background:linear-gradient(135deg,#0a1a1a,#152525);">🎶</div>
      </div>
      <div class="playlist-name">Collaborations</div>
      <div class="playlist-detail">Vol. 4 · 12 tracks</div>
    </div>
  </div>

  <!-- Tracklist -->
  <div class="tracklist">
    <div style="font-size:10px;letter-spacing:4px;text-transform:uppercase;color:rgba(232,232,240,0.25);padding:20px 0 12px;border-bottom:1px solid rgba(255,255,255,0.05);">Featured Tracks</div>

    <div class="track-row">
      <div class="track-idx">01</div>
      <div class="track-name-col">
        <div>Do Well</div>
        <div class="track-artist">SIRUP</div>
      </div>
      <div class="track-badge">NEW</div>
      <div class="track-duration">3:42</div>
    </div>
    <div class="track-row">
      <div class="track-idx">02</div>
      <div class="track-name-col">
        <div>Right Here Right Now</div>
        <div class="track-artist">SIRUP feat. Sik-K</div>
      </div>
      <div></div>
      <div class="track-duration">4:15</div>
    </div>
    <div class="track-row">
      <div class="track-idx">03</div>
      <div class="track-name-col">
        <div>Permanent</div>
        <div class="track-artist">SIRUP</div>
      </div>
      <div></div>
      <div class="track-duration">3:58</div>
    </div>
    <div class="track-row">
      <div class="track-idx">04</div>
      <div class="track-name-col">
        <div>Be Yourself</div>
        <div class="track-artist">SIRUP feat. Chanmina</div>
      </div>
      <div></div>
      <div class="track-duration">4:28</div>
    </div>
    <div class="track-row">
      <div class="track-idx">05</div>
      <div class="track-name-col">
        <div>Loop (Forever)</div>
        <div class="track-artist">SIRUP</div>
      </div>
      <div></div>
      <div class="track-duration">5:02</div>
    </div>
    <div class="track-row">
      <div class="track-idx">06</div>
      <div class="track-name-col">
        <div>Feel Good</div>
        <div class="track-artist">SIRUP</div>
      </div>
      <div></div>
      <div class="track-duration">3:33</div>
    </div>
    <div class="track-row">
      <div class="track-idx">07</div>
      <div class="track-name-col">
        <div>Overload</div>
        <div class="track-artist">SIRUP</div>
      </div>
      <div></div>
      <div class="track-duration">4:07</div>
    </div>
    <div class="track-row">
      <div class="track-idx">08</div>
      <div class="track-name-col">
        <div>Morning</div>
        <div class="track-artist">SIRUP feat. STG</div>
      </div>
      <div></div>
      <div class="track-duration">3:51</div>
    </div>
  </div>

  <footer>
    <div class="footer-logo">SIRUP'S ROOTS</div>
    <div class="footer-copy">© 2024 SIRUP. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('home')">Home</a>
      <a onclick="navigateTo('about')">About</a>
      <a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ GALLERY PAGE ============ -->
<div id="gallery" class="page">
  <div style="display:flex;align-items:flex-end;justify-content:space-between;margin-bottom:40px;">
    <div style="display:flex;align-items:flex-end;gap:24px;">
      <div class="section-number">03</div>
      <div class="section-title-block">
        <div class="section-label">Visual</div>
        <h2 class="section-title">GALLERY</h2>
      </div>
    </div>
    <div class="gallery-filters">
      <button class="filter-btn active" onclick="filterGallery(this)">All</button>
      <button class="filter-btn" onclick="filterGallery(this)">Live</button>
      <button class="filter-btn" onclick="filterGallery(this)">Studio</button>
      <button class="filter-btn" onclick="filterGallery(this)">Press</button>
    </div>
  </div>

  <div class="gallery-masonry">
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph tall" style="background:linear-gradient(160deg,#1a0a2e,#2d1545);">♪</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Live — Tokyo 2024</span></div>
    </div>
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph wide" style="background:linear-gradient(160deg,#0a1a2e,#152535);">🎤</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Studio Session</span></div>
    </div>
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph square" style="background:linear-gradient(160deg,#1a2a0a,#253020);">🎵</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Press — Osaka</span></div>
    </div>
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph wide" style="background:linear-gradient(160deg,#2a1a0a,#3d2515);">🎧</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Live — Osaka 2023</span></div>
    </div>
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph tall" style="background:linear-gradient(160deg,#0a2a1a,#153525);">🎶</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Press Shoot 2024</span></div>
    </div>
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph square" style="background:linear-gradient(160deg,#1a1a2e,#2d2545);">🎹</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Studio — Album Recording</span></div>
    </div>
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph wide" style="background:linear-gradient(160deg,#2a0a1a,#3d152a);">🎸</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Live — Fuji Rock 2023</span></div>
    </div>
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph tall" style="background:linear-gradient(160deg,#0a0a2e,#151540);">🎺</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Press — Magazine</span></div>
    </div>
    <div class="gallery-item">
      <div class="gallery-item-inner">
        <div class="gallery-img-ph square" style="background:linear-gradient(160deg,#1a2a1a,#253525);">🥁</div>
      </div>
      <div class="gallery-item-overlay"><span class="gallery-caption">Live — Summer Sonic</span></div>
    </div>
  </div>

  <footer>
    <div class="footer-logo">SIRUP'S ROOTS</div>
    <div class="footer-copy">© 2024 SIRUP. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('home')">Home</a>
      <a onclick="navigateTo('music')">Music</a>
      <a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ CONTACT PAGE ============ -->
<div id="contact" class="page">
  <div class="section-header">
    <div class="section-number">04</div>
    <div class="section-title-block">
      <div class="section-label">Get in Touch</div>
      <h2 class="section-title">CONTACT</h2>
    </div>
  </div>

  <div class="contact-grid">
    <div class="contact-info">
      <p class="contact-text">
        For bookings, press inquiries, and collaborations — reach out through the form or connect via social media. SIRUP's team will get back to you as soon as possible.
      </p>

      <div class="contact-links">
        <a class="contact-link" href="https://instagram.com/sirup_music" target="_blank">
          <div class="contact-link-icon">📸</div>
          <div class="contact-link-text">
            <div class="contact-link-platform">Instagram</div>
            <div class="contact-link-handle">@sirup_music</div>
          </div>
          <span class="contact-link-arrow">→</span>
        </a>
        <a class="contact-link" href="https://twitter.com/sirup_music" target="_blank">
          <div class="contact-link-icon">𝕏</div>
          <div class="contact-link-text">
            <div class="contact-link-platform">Twitter / X</div>
            <div class="contact-link-handle">@sirup_music</div>
          </div>
          <span class="contact-link-arrow">→</span>
        </a>
        <a class="contact-link" href="https://open.spotify.com" target="_blank">
          <div class="contact-link-icon">🎵</div>
          <div class="contact-link-text">
            <div class="contact-link-platform">Spotify</div>
            <div class="contact-link-handle">SIRUP Official</div>
          </div>
          <span class="contact-link-arrow">→</span>
        </a>
        <a class="contact-link" href="https://youtube.com" target="_blank">
          <div class="contact-link-icon">▶</div>
          <div class="contact-link-text">
            <div class="contact-link-platform">YouTube</div>
            <div class="contact-link-handle">SIRUP OFFICIAL</div>
          </div>
          <span class="contact-link-arrow">→</span>
        </a>
        <div class="contact-link" style="cursor:default;">
          <div class="contact-link-icon">✉</div>
          <div class="contact-link-text">
            <div class="contact-link-platform">Booking &amp; Press</div>
            <div class="contact-link-handle">info@sirup-official.com</div>
          </div>
        </div>
      </div>
    </div>

    <div class="contact-form">
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">First Name</label>
          <input class="form-input" type="text" placeholder="Your name">
        </div>
        <div class="form-group">
          <label class="form-label">Last Name</label>
          <input class="form-input" type="text" placeholder="Last name">
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Email Address</label>
        <input class="form-input" type="email" placeholder="your@email.com">
      </div>
      <div class="form-group">
        <label class="form-label">Subject</label>
        <input class="form-input" type="text" placeholder="Booking / Press / Collab">
      </div>
      <div class="form-group">
        <label class="form-label">Message</label>
        <textarea class="form-textarea" placeholder="Tell us about your inquiry..."></textarea>
      </div>
      <button class="form-submit" onclick="submitForm(this)">Send Message</button>
    </div>
  </div>

  <footer>
    <div class="footer-logo">SIRUP'S ROOTS</div>
    <div class="footer-copy">© 2024 SIRUP. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('home')">Home</a>
      <a onclick="navigateTo('about')">About</a>
      <a onclick="navigateTo('music')">Music</a>
    </div>
  </footer>
</div>

<script>
  // ===== LOADER =====
  window.addEventListener('load', () => {
    setTimeout(() => {
      document.getElementById('loader').classList.add('hidden');
      setTimeout(() => document.getElementById('loader').remove(), 800);
    }, 2000);
  });

  // ===== CURSOR =====
  const cursor = document.getElementById('cursor');
  const cursorRing = document.getElementById('cursorRing');
  let mouseX = 0, mouseY = 0;
  let ringX = 0, ringY = 0;

  document.addEventListener('mousemove', (e) => {
    mouseX = e.clientX;
    mouseY = e.clientY;
    cursor.style.left = mouseX + 'px';
    cursor.style.top = mouseY + 'px';
  });

  function animateRing() {
    ringX += (mouseX - ringX) * 0.12;
    ringY += (mouseY - ringY) * 0.12;
    cursorRing.style.left = ringX + 'px';
    cursorRing.style.top = ringY + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.addEventListener('mousedown', () => {
    cursor.style.transform = 'translate(-50%, -50%) scale(1.8)';
    cursorRing.style.transform = 'translate(-50%, -50%) scale(0.7)';
  });
  document.addEventListener('mouseup', () => {
    cursor.style.transform = 'translate(-50%, -50%) scale(1)';
    cursorRing.style.transform = 'translate(-50%, -50%) scale(1)';
  });

  // ===== NAVIGATION =====
  let currentPage = 'home';

  function navigateTo(pageId) {
    if (pageId === currentPage) return;

    const transition = document.getElementById('pageTransition');
    transition.classList.add('animating');

    setTimeout(() => {
      // Hide all pages
      document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
      
      // Show target page
      document.getElementById(pageId).classList.add('active');
      
      // Update nav
      document.querySelectorAll('nav a').forEach(a => {
        a.classList.toggle('active', a.dataset.page === pageId);
      });

      currentPage = pageId;
      window.scrollTo(0, 0);

      transition.classList.remove('animating');
    }, 250);
  }

  // ===== MOBILE MENU =====
  function toggleMenu() {
    const menu = document.getElementById('mobileMenu');
    menu.classList.toggle('open');
  }

  // ===== GALLERY FILTER =====
  function filterGallery(btn) {
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
  }

  // ===== FORM SUBMIT =====
  function submitForm(btn) {
    btn.textContent = 'Sending...';
    btn.style.opacity = '0.7';
    setTimeout(() => {
      btn.textContent = 'Message Sent ✓';
      btn.style.background = 'linear-gradient(135deg, #2d6a4f, #52b788)';
      btn.style.opacity = '1';
      setTimeout(() => {
        btn.textContent = 'Send Message';
        btn.style.background = '';
      }, 3000);
    }, 1200);
  }

  // ===== SCROLL HEADER =====
  let lastScroll = 0;
  const header = document.getElementById('header');
  window.addEventListener('scroll', () => {
    const current = window.scrollY;
    if (current > 100) {
      header.style.background = 'rgba(10,10,15,0.95)';
      header.style.backdropFilter = 'blur(20px)';
    } else {
      header.style.background = 'linear-gradient(to bottom, rgba(10,10,15,0.95) 0%, transparent 100%)';
      header.style.backdropFilter = 'blur(0px)';
    }
    lastScroll = current;
  });

  // ===== PLAY BUTTON ANIMATION =====
  document.querySelectorAll('.play-btn').forEach(btn => {
    btn.addEventListener('click', (e) => {
      e.stopPropagation();
      const original = btn.textContent;
      btn.textContent = '⏸';
      setTimeout(() => btn.textContent = original, 2000);
    });
  });
</script>
</body>
</html>
