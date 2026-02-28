<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=DM+Sans:wght@200;300;400;500&family=Bebas+Neue&family=Cormorant+Garamond:ital,wght@0,300;0,600;0,700;1,300;1,600;1,700&family=Unbounded:wght@200;400;700;900&display=swap');

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg: #080810;
    --dark: #0d0d1a;
    --accent1: #e05c7a;
    --accent2: #5b78c9;
    --accent3: #c77dff;
    --gold: #c9a84c;
    --text: #ece8f0;
    --muted: #7a7a9a;
    /* singer page vars */
    --red:   #c94040;
    --blue:  #3a5fa8;
    --purple:#9b59d0;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    overflow-x: hidden;
    width: 100%;
    cursor: none;
  }

  ::-webkit-scrollbar { width: 3px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--accent1); border-radius: 2px; }
  .markdown-body img { background: transparent !important; }
  .container-lg { max-width: 100% !important; }
  .container-lg.px-3.my-5.markdown-body h1:first-child { display: none !important;}

  /* NOISE */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.035'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 9999; opacity: 0.5;
  }

  /* CURSOR */
  .cursor, .cursor-ring {
    position: fixed; border-radius: 50%;
    pointer-events: none; z-index: 99999;
    transform: translate(-50%, -50%);
  }
  .cursor { width: 7px; height: 7px; background: var(--accent1); }
  .cursor-ring { width: 32px; height: 32px; border: 1px solid rgba(224,92,122,0.35); transition: all 0.14s ease; }

  /* ===== PAGES ===== */
  .page { display: none; min-height: 100vh; width: 100%; }
  .page.active { display: block; animation: fadeUp 0.7s cubic-bezier(0.16,1,0.3,1) forwards; }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ===== HEADER ===== */
  header {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 1000; padding: 22px 48px;
    display: flex; align-items: center; justify-content: space-between;
    background: linear-gradient(to bottom, rgba(8,8,16,0.97) 0%, transparent 100%);
    transition: background 0.4s;
  }

  .header-logo {
    font-family: 'Bebas Neue', sans-serif; font-size: 20px;
    letter-spacing: 5px; color: var(--text); cursor: pointer; transition: color 0.3s;
  }
  .header-logo:hover { color: var(--accent1); }

  nav { display: flex; align-items: center; gap: 32px; }
  nav a {
    font-size: 10px; letter-spacing: 3px; text-transform: uppercase;
    color: rgba(236,232,240,0.5); text-decoration: none; cursor: pointer;
    transition: color 0.3s; position: relative; font-weight: 500;
  }
  nav a::after {
    content: ''; position: absolute; bottom: -5px; left: 0; right: 0;
    height: 1px; background: var(--accent1); transform: scaleX(0);
    transition: transform 0.3s ease; transform-origin: left;
  }
  nav a:hover, nav a.active { color: var(--text); }
  nav a:hover::after, nav a.active::after { transform: scaleX(1); }

  .menu-btn {
    display: none; flex-direction: column; gap: 5px;
    cursor: pointer; padding: 5px; z-index: 1001;
  }
  .menu-btn span {
    display: block; width: 26px; height: 2px;
    background: var(--text); transition: all 0.3s; border-radius: 2px;
  }
  .menu-btn.open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
  .menu-btn.open span:nth-child(2) { opacity: 0; }
  .menu-btn.open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

  /* MOBILE MENU */
  .mobile-menu {
    display: none; position: fixed; inset: 0;
    background: rgba(8,8,16,0.98); z-index: 999;
    flex-direction: column; align-items: center; justify-content: center; gap: 36px;
  }
  .mobile-menu.open { display: flex; animation: fadeUp 0.3s ease; }
  .mobile-menu a {
    font-family: 'Bebas Neue', sans-serif; font-size: 52px;
    letter-spacing: 8px; color: var(--text); text-decoration: none;
    cursor: pointer; transition: color 0.3s;
  }
  .mobile-menu a:hover { color: var(--accent1); }

  /* ===== MUSIC ANIMATION ===== */
  .music-anim { position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden; }
  .note {
    position: absolute; opacity: 0; font-size: 20px;
    animation: floatNote var(--dur) ease-in-out var(--delay) infinite;
    color: rgba(224, 92, 122, 0.15); user-select: none;
  }
  @keyframes floatNote {
    0%   { opacity: 0; transform: translateY(0) rotate(0deg) scale(0.5); }
    15%  { opacity: 1; }
    85%  { opacity: 0.5; }
    100% { opacity: 0; transform: translateY(-80vh) rotate(180deg) scale(1.2); }
  }

  /* WAVEFORM */
  .waveform-bg {
    position: fixed; bottom: 0; left: 0; right: 0; height: 80px;
    display: flex; align-items: flex-end; justify-content: center;
    gap: 3px; pointer-events: none; z-index: 0; opacity: 0.06; padding: 0 20px;
  }
  .wave-bar {
    width: 3px; background: var(--accent1); border-radius: 2px 2px 0 0;
    animation: waveAnim var(--spd) ease-in-out var(--dly) infinite alternate;
  }
  @keyframes waveAnim {
    from { height: var(--min-h); }
    to   { height: var(--max-h); }
  }

  /* ===== LOADER ===== */
  .loader {
    position: fixed; inset: 0; background: var(--bg); z-index: 99997;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    transition: opacity 0.8s ease;
  }
  .loader.hidden { opacity: 0; pointer-events: none; }
  .loader-title {
    font-family: 'Playfair Display', serif; font-size: 72px; font-style: italic;
    font-weight: 900; letter-spacing: 4px; color: white;
    clip-path: inset(0 100% 0 0); animation: revealText 1.2s ease 0.3s forwards;
  }
  .loader-sub {
    font-size: 9px; letter-spacing: 8px; text-transform: uppercase;
    color: rgba(255,255,255,0.25); margin-top: 14px; opacity: 0;
    animation: fadeInEl 0.6s ease 1.2s forwards; font-weight: 500;
  }
  .loader-bar { width: 180px; height: 1px; background: rgba(255,255,255,0.08); margin-top: 44px; position: relative; overflow: hidden; }
  .loader-bar::after { content: ''; position: absolute; top: 0; left: 0; width: 0; height: 100%; background: var(--accent1); animation: loadBar 1.5s ease 0.2s forwards; }
  @keyframes revealText { to { clip-path: inset(0 0% 0 0); } }
  @keyframes fadeInEl  { to { opacity: 1; } }
  @keyframes loadBar   { to { width: 100%; } }

  /* ===== SECTION COMMONS ===== */
  .section-header { display: flex; align-items: flex-end; gap: 20px; margin-bottom: 72px; }
  .section-number { font-family: 'Bebas Neue', sans-serif; font-size: 110px; line-height: 1; color: rgba(255,255,255,0.03); letter-spacing: -4px; }
  .section-label  { font-size: 9px; letter-spacing: 5px; text-transform: uppercase; color: var(--accent1); margin-bottom: 8px; font-weight: 500; }
  .section-title  { font-family: 'Playfair Display', serif; font-size: clamp(42px,5.5vw,76px); letter-spacing: 1px; line-height: 1; font-weight: 700; font-style: italic; }

  .img-placeholder {
    width: 100%; height: 100%;
    display: flex; align-items: center; justify-content: center;
    color: rgba(255,255,255,0.06); font-size: 28px;
    font-family: 'Playfair Display', serif;
  }

  /* ===================================================================
     SINGER PAGE — scroll-based, full SIRUP-style design (Document 2)
  =================================================================== */
  #singer { overflow-y: auto; }
  #singer section { width: 100%; position: relative; overflow: hidden; }

  /* ── S1 Anniversary Hero ── */
  .sg-s1 {
    min-height: 100vh;
    background:
      radial-gradient(ellipse 60% 80% at 80% 50%, rgba(58,95,168,.5) 0%, transparent 65%),
      radial-gradient(ellipse 55% 60% at 20% 70%, rgba(201,64,64,.55) 0%, transparent 60%),
      radial-gradient(ellipse 40% 40% at 55% 10%, rgba(155,89,208,.2) 0%, transparent 50%),
      linear-gradient(160deg,#0a080e 0%,#14102a 60%,#0e080a 100%);
  }
  .sg-s1-wrap { width:100%; min-height:100vh; position:relative; display:flex; align-items:center; justify-content:center; }

  .sg-s1-bgtext { position:absolute; inset:0; display:flex; flex-direction:column; align-items:center; justify-content:center; pointer-events:none; user-select:none; overflow:hidden; }
  .sg-s1-bdate { font-family:'Unbounded',sans-serif; font-size:clamp(52px,9vw,150px); font-weight:900; color:rgba(242,238,232,.055); letter-spacing:-2px; line-height:1; white-space:nowrap; }
  .sg-s1-b5th  { font-family:'Unbounded',sans-serif; font-size:clamp(80px,16vw,260px); font-weight:900; color:rgba(242,238,232,.04); line-height:.9; letter-spacing:-4px; }
  .sg-s1-banni { font-family:'Unbounded',sans-serif; font-size:clamp(36px,6vw,100px); font-weight:900; color:rgba(242,238,232,.04); letter-spacing:8px; text-transform:uppercase; white-space:nowrap; }

  .sg-s1-circle {
    position:absolute; width:min(54vw,540px); height:min(54vw,540px); border-radius:50%;
    background:radial-gradient(circle,rgba(38,34,70,.75) 0%,rgba(18,14,38,.38) 55%,transparent 100%);
    left:50%; top:50%; transform:translate(-50%,-50%);
    border:1px solid rgba(255,255,255,.035);
    animation:sgSpin 60s linear infinite;
  }
  @keyframes sgSpin { to { transform:translate(-50%,-50%) rotate(360deg); } }

  .sg-s1-photo { position:absolute; bottom:0; left:50%; transform:translateX(-50%); width:min(36vw,400px); z-index:10; }
  .sg-s1-ph { width:100%; height:min(68vh,620px); position:relative; overflow:hidden; }
  .sg-s1-ph::before {
    content:''; position:absolute; bottom:0; left:50%; transform:translateX(-50%);
    width:60%; height:95%;
    background:linear-gradient(180deg,rgba(60,50,100,.35) 0%,rgba(14,10,26,.92) 100%);
    border-radius:48% 48% 0 0 / 18% 18% 0 0;
    box-shadow:0 0 80px rgba(155,89,208,.18);
  }
  .sg-s1-ph::after { content:''; position:absolute; inset:0; background:linear-gradient(to top,rgba(10,8,14,1) 0%,transparent 40%); }
  .sg-s1-ph img { width:100%; height:100%; object-fit:cover; object-position:top; position:relative; z-index:1;  }

  .sg-s1-strip {
    position:absolute; top:0; left:0; bottom:0; width:28px;
    background:rgba(201,64,64,.1); border-right:1px solid rgba(201,64,64,.2);
    display:flex; align-items:center; justify-content:center;
    writing-mode:vertical-rl; font-size:8px; letter-spacing:3px; text-transform:uppercase;
    color:rgba(242,238,232,.45); font-weight:500;
  }
  .sg-s1-left { position:absolute; left:48px; top:50%; transform:translateY(-50%); z-index:20; }
  .sg-s1-sm   { font-size:10px; letter-spacing:5px; text-transform:uppercase; color:rgba(242,238,232,.32); margin-bottom:6px; font-weight:400; }
  .sg-s1-rel  { font-size:12px; color:rgba(242,238,232,.42); line-height:2; font-weight:300; }
  .sg-s1-rtext {
    position:absolute; right:20px; top:50%; writing-mode:vertical-rl; transform:translateY(-50%);
    font-size:9px; letter-spacing:6px; text-transform:uppercase; color:rgba(242,238,232,.15); font-weight:400;
    display:flex; flex-direction:column; align-items:center; gap:10px;
  }
  .sg-s1-rtext::before { content:''; display:block; width:1px; height:36px; background:rgba(242,238,232,.15); }
  .sg-s1-bottom {
    position:absolute; bottom:0; left:0; right:0; padding:0 48px 32px;
    display:flex; align-items:flex-end; justify-content:space-between; z-index:20;
  }
  .sg-s1-bigyear { font-family:'Unbounded',sans-serif; font-size:clamp(32px,5.5vw,80px); font-weight:900; line-height:1; color:rgba(242,238,232,.06); letter-spacing:-2px; }
  .sg-s1-desc { max-width:320px; text-align:right; font-size:12px; line-height:2; color:rgba(242,238,232,.42); font-weight:300; }

  /* ── Singer Ticker ── */
  .sg-ticker-wrap { overflow:hidden; background:rgba(201,64,64,.07); border-top:1px solid rgba(201,64,64,.14); border-bottom:1px solid rgba(201,64,64,.14); padding:12px 0; position:relative; z-index:2; }
  .sg-ticker { display:flex; white-space:nowrap; animation:sgTick 24s linear infinite; gap:48px; }
  @keyframes sgTick { from{transform:translateX(0)} to{transform:translateX(-50%)} }
  .sg-ticker span { font-size:9px; letter-spacing:5px; text-transform:uppercase; color:rgba(242,238,232,.28); font-weight:500; }
  .sg-ticker .dot { color:var(--red); font-size:12px; }

  /* ── S2 Roots ── */
  .sg-s2 {
    min-height:100vh;
    background:
      radial-gradient(ellipse 70% 70% at 50% 50%, rgba(38,34,98,.48) 0%, transparent 70%),
      radial-gradient(ellipse 55% 60% at 85% 28%, rgba(58,95,168,.34) 0%, transparent 58%),
      radial-gradient(ellipse 50% 55% at 14% 72%, rgba(201,64,64,.38) 0%, transparent 55%),
      radial-gradient(ellipse 40% 40% at 50% 92%, rgba(155,89,208,.18) 0%, transparent 50%),
      linear-gradient(150deg,#0e0a1a 0%,#12102a 40%,#0a0810 100%);
  }
  .sg-s2-wrap { width:100%; min-height:100vh; position:relative; display:flex; align-items:center; }
  .sg-s2-circle {
    position:absolute; left:50%; top:50%; transform:translate(-50%,-50%);
    width:min(74vw,790px); height:min(74vw,790px); border-radius:50%;
    background:radial-gradient(circle,rgba(28,22,58,.58) 0%,rgba(13,10,28,.28) 55%,transparent 100%);
    border:1px solid rgba(255,255,255,.028);
  }
  .sg-s2-artist { position:absolute; left:50%; bottom:0; transform:translateX(-50%); width:min(32vw,360px); z-index:5; }
  .sg-s2-artph  { width:100%; height:min(92vh,700px); position:relative; overflow:hidden; border-radius:38% 38% 0 0 / 12% 12% 0 0; }
  .sg-s2-artph::before { content:''; position:absolute; bottom:0; left:50%; transform:translateX(-50%); width:72%; height:100%; background:linear-gradient(180deg,rgba(76,56,138,.3) 0%,rgba(10,8,22,.9) 100%); }
  .sg-s2-artph::after  { content:''; position:absolute; inset:0; background:linear-gradient(to top,rgba(10,8,14,1) 0%,transparent 35%); }
  .sg-s2-artph img { width:100%; height:100%; object-fit:cover; object-position:top; position:relative; z-index:1; mix-blend-mode:luminosity; opacity:.8; filter:contrast(1.1) grayscale(10%); }
  .sg-s2-left { position:absolute; left:48px; top:50%; transform:translateY(-50%); z-index:10; max-width:400px; }
  .sg-s2-kick  { font-family:'Unbounded',sans-serif; font-size:clamp(12px,1.6vw,20px); font-weight:200; letter-spacing:4px; color:rgba(242,238,232,.56); margin-bottom:4px; }
  .sg-s2-title {
    font-family:'Unbounded',sans-serif; font-size:clamp(56px,10.5vw,170px); font-weight:900;
    line-height:.88; letter-spacing:-2px; color:var(--text);
    text-shadow:4px 4px 0 rgba(201,64,64,.28); margin-bottom:28px;
  }
  .sg-s2-body  { font-size:13px; line-height:2.1; color:rgba(242,238,232,.43); font-weight:300; max-width:350px; margin-bottom:36px; }
  .sg-s2-btn {
    width:124px; height:124px; border-radius:50%;
    background:rgba(18,14,38,.72); border:1px solid rgba(255,255,255,.1);
    display:flex; flex-direction:column; align-items:center; justify-content:center;
    font-size:8px; letter-spacing:4px; text-transform:uppercase;
    color:rgba(242,238,232,.6); cursor:pointer; transition:all .4s;
    text-align:center; line-height:2.1; font-weight:500;
  }
  .sg-s2-btn:hover { background:rgba(201,64,64,.18); border-color:var(--red); color:var(--text); transform:scale(1.06) rotate(-3deg); }
  .sg-s2-photos {
    position:absolute; right:48px; top:50%; transform:translateY(-50%);
    display:grid; grid-template-columns:repeat(4,1fr); gap:6px;
    width:min(42vw,460px); z-index:10;
  }
  .sg-s2-ph-item { aspect-ratio:3/4; overflow:hidden; position:relative; background:#1a1535; }
  .sg-s2-ph-item::after { content:''; position:absolute; inset:0; background:linear-gradient(to bottom,transparent 50%,rgba(10,8,20,.62) 100%); }
  .sg-s2-ph-item img { width:100%; height:100%; object-fit:cover; filter:grayscale(20%) contrast(1.1); transition:transform .6s; }
  .sg-s2-ph-item:hover img { transform:scale(1.06); }
  .sg-s2-ph-box { width:100%; height:100%; display:flex; align-items:center; justify-content:center; font-size:22px; color:rgba(255,255,255,.055); background:linear-gradient(160deg,#1a1535,#2d1a45); }
  .sg-s2-vt    { position:absolute; right:16px; top:50%; writing-mode:vertical-rl; transform:translateY(-50%); font-size:9px; letter-spacing:6px; text-transform:uppercase; color:rgba(242,238,232,.13); font-weight:400; }

  /* ── S3 Album Card ── */
  .sg-s3 {
    min-height:100vh;
    background:
      radial-gradient(ellipse 50% 60% at 70% 50%,rgba(120,38,38,.33) 0%,transparent 65%),
      radial-gradient(ellipse 40% 40% at 28% 50%,rgba(58,28,78,.28) 0%,transparent 55%),
      linear-gradient(135deg,#0a0808 0%,#1a1010 50%,#0d0808 100%);
  }
  .sg-s3-wrap { width:100%; min-height:100vh; position:relative; display:flex; align-items:center; justify-content:center; }
  .sg-s3-bgtext { position:absolute; inset:0; overflow:hidden; display:flex; flex-direction:column; align-items:center; justify-content:center; pointer-events:none; user-select:none; }
  .sg-s3-bgl { font-family:'Unbounded',sans-serif; font-size:clamp(54px,9vw,140px); font-weight:900; color:rgba(242,238,232,.038); letter-spacing:4px; text-transform:uppercase; line-height:1.04; white-space:nowrap; }
  .sg-s3-bgl:nth-child(2){ color:rgba(201,64,64,.055); margin-top:-4px; }
  .sg-s3-bgl:nth-child(3){ color:rgba(242,238,232,.025); margin-top:-4px; }
  .sg-s3-card { position:relative; z-index:10; width:min(30vw,330px); transform:rotate(-6deg); box-shadow:-28px 28px 72px rgba(0,0,0,.72),-10px 10px 28px rgba(0,0,0,.5); transition:transform .4s ease; cursor:pointer; }
  .sg-s3-card:hover { transform:rotate(-3deg) scale(1.04); }
  .sg-s3-card-inner { width:100%; background:linear-gradient(135deg,#1a0808,#2d1010,#3d2010); position:relative; overflow:hidden; aspect-ratio:3/4; }
  .sg-s3-clabel   { position:absolute; left:0; top:0; bottom:0; width:30px; background:rgba(0,0,0,.48); display:flex; align-items:center; justify-content:center; writing-mode:vertical-rl; font-size:7px; letter-spacing:3px; text-transform:uppercase; color:rgba(242,238,232,.3); font-weight:500; }
  .sg-s3-ccontent { padding:28px 18px 28px 46px; height:100%; display:flex; flex-direction:column; justify-content:space-between; }
  .sg-s3-cdate    { font-family:'Unbounded',sans-serif; font-size:clamp(24px,3.8vw,54px); font-weight:900; line-height:1; color:var(--red); }
  .sg-s3-cday     { font-size:12px; letter-spacing:3px; text-transform:uppercase; color:rgba(242,238,232,.46); margin-top:4px; font-weight:400; }
  .sg-s3-clogo    { font-family:'Cormorant Garamond',serif; font-size:clamp(32px,4.5vw,68px); font-style:italic; font-weight:700; color:var(--text); line-height:1.06; }
  .sg-s3-cvenue   { font-size:10px; letter-spacing:4px; text-transform:uppercase; color:rgba(242,238,232,.46); font-weight:500; }
  .sg-s3-info     { position:absolute; left:48px; bottom:72px; z-index:20; }
  .sg-s3-ilabel   { font-size:8px; letter-spacing:5px; text-transform:uppercase; color:rgba(242,238,232,.28); margin-bottom:7px; font-weight:500; }
  .sg-s3-ititle   { font-family:'Cormorant Garamond',serif; font-size:clamp(26px,3.2vw,46px); font-style:italic; font-weight:700; color:rgba(242,238,232,.65); }
  .sg-s3-sound    { position:absolute; top:30px; right:34px; z-index:20; cursor:pointer; width:38px; height:38px; border:1px solid rgba(255,255,255,.14); border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:15px; transition:all .3s; }
  .sg-s3-sound:hover { background:var(--red); border-color:var(--red); }

  /* ── S6 Next/Footer (Singer last section) ── */
  .sg-s6 {
    min-height:100vh;
    background:
      radial-gradient(ellipse 70% 60% at 50% 42%,rgba(155,89,208,.44) 0%,transparent 60%),
      radial-gradient(ellipse 60% 55% at 80% 62%,rgba(58,95,168,.38) 0%,transparent 55%),
      radial-gradient(ellipse 55% 50% at 18% 62%,rgba(201,64,64,.44) 0%,transparent 55%),
      radial-gradient(ellipse 38% 38% at 50% 8%,rgba(240,180,80,.13) 0%,transparent 50%),
      linear-gradient(160deg,#1a0e1e 0%,#0e1020 50%,#1a0a10 100%);
    display:flex; flex-direction:column; position:relative; overflow:hidden;
  }
  .sg-s6-roll { position:absolute; inset:0; display:flex; flex-direction:column; justify-content:center; pointer-events:none; overflow:hidden; }
  .sg-rrow { font-family:'Unbounded',sans-serif; font-size:clamp(56px,9vw,132px); font-weight:900; color:rgba(242,238,232,.066); letter-spacing:6px; white-space:nowrap; line-height:1.06; animation:sgRl 18s linear infinite; }
  .sg-rrow:nth-child(2){ animation:sgRr 22s linear infinite; color:rgba(201,64,64,.078); }
  .sg-rrow:nth-child(3){ animation:sgRl 20s linear infinite; animation-delay:-4s; }
  @keyframes sgRl { from{transform:translateX(0)}   to{transform:translateX(-50%)} }
  @keyframes sgRr { from{transform:translateX(-50%)} to{transform:translateX(0)} }
  .sg-s6-next   { position:absolute; top:56px; left:50%; transform:translateX(-50%); font-size:9px; letter-spacing:8px; text-transform:uppercase; color:rgba(242,238,232,.38); z-index:20; font-weight:400; }
  .sg-s6-center { position:absolute; left:50%; top:50%; transform:translate(-50%,-50%); z-index:10; }
  .sg-s6-ring   { width:min(42vw,430px); height:min(42vw,430px); border-radius:50%; background:radial-gradient(circle,rgba(240,236,228,.07) 0%,rgba(240,236,228,.018) 55%,transparent 100%); border:1px solid rgba(255,255,255,.055); position:relative; overflow:hidden; display:flex; align-items:flex-end; justify-content:center; }
  .sg-s6-artph  { width:74%; height:84%; background:linear-gradient(180deg,rgba(78,58,118,.2) 0%,rgba(14,10,24,.68) 100%); border-radius:50% 50% 0 0 / 28% 28% 0 0; position:relative; }
  .sg-s6-artph::before { content:''; position:absolute; bottom:0; left:50%; transform:translateX(-50%); width:70%; height:90%; background:linear-gradient(180deg,rgba(100,80,156,.24) 0%,rgba(10,8,20,.88) 100%); }
  .sg-s6-artph img { width:100%; height:100%; object-fit:cover; object-position:top; mix-blend-mode:luminosity; opacity:.75; filter:grayscale(15%) contrast(1.1); }
  .sg-s6-foot   { position:absolute; bottom:0; left:0; right:0; padding:22px 46px; display:flex; align-items:center; justify-content:space-between; border-top:1px solid rgba(255,255,255,.055); background:rgba(10,8,14,.38); backdrop-filter:blur(12px); z-index:20; flex-wrap:wrap; gap:10px; }
  .sg-s6-site   { font-size:9px; letter-spacing:3px; text-transform:uppercase; color:rgba(242,238,232,.36); font-weight:500; }
  .sg-s6-soc    { display:flex; gap:20px; }
  .sg-s6-soc a  { font-size:12px; color:rgba(242,238,232,.36); text-decoration:none; cursor:pointer; transition:color .3s; }
  .sg-s6-soc a:hover { color:var(--text); }
  .sg-s6-copy   { font-size:9px; letter-spacing:2px; color:rgba(242,238,232,.22); }

  /* ===================================================================
     HOME PAGE (old home kept intact)
  =================================================================== */
  #home { position: relative; min-height: 100vh; width: 100%; overflow: hidden; }
  .home-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 65% 75% at 75% 45%, rgba(91,120,201,0.3) 0%, transparent 65%),
      radial-gradient(ellipse 55% 65% at 25% 75%, rgba(224,92,122,0.35) 0%, transparent 60%),
      radial-gradient(ellipse 40% 40% at 55% 15%, rgba(199,125,255,0.12) 0%, transparent 50%),
      linear-gradient(160deg, #080810 0%, #12122a 60%, #0a0818 100%);
  }
  .home-orb {
    position: absolute; bottom: -15%; left: -8%;
    width: 60vw; height: 60vw; border-radius: 50%;
    background: radial-gradient(circle, rgba(25,25,55,0.6) 0%, rgba(12,12,28,0.3) 60%, transparent 100%);
    border: 1px solid rgba(255,255,255,0.03);
    animation: rotateSlow 40s linear infinite; pointer-events: none;
  }
  @keyframes rotateSlow { from{transform:rotate(0deg)} to{transform:rotate(360deg)} }
  .hero-content {
    position: relative; z-index: 10; padding: 140px 60px 60px;
    display: grid; grid-template-columns: 1.1fr 1fr; gap: 40px;
    align-items: center; min-height: 100vh; width: 100%;
  }
  .hero-subtitle { font-size: 10px; letter-spacing: 6px; text-transform: uppercase; color: rgba(236,232,240,0.4); margin-bottom: 14px; font-weight: 400; }
  .hero-title {
    font-family: 'Playfair Display', serif; font-size: clamp(72px,10vw,160px); line-height: 0.88; font-style: italic; font-weight: 900;
    background: linear-gradient(135deg, #ffffff 0%, rgba(255,255,255,0.55) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    margin-bottom: 20px; position: relative;
  }
  .hero-title-shadow {
    position: absolute; top: 5px; left: 5px;
    font-family: 'Playfair Display', serif; font-size: inherit; line-height: 0.88; font-style: italic; font-weight: 900;
    background: linear-gradient(135deg, rgba(224,92,122,0.35) 0%, transparent 60%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    z-index: -1; pointer-events: none;
  }
  .hero-artist { font-size: 11px; letter-spacing: 8px; text-transform: uppercase; color: rgba(236,232,240,0.45); margin-bottom: 28px; font-weight: 300; }
  .hero-desc   { font-size: 14px; line-height: 2; color: rgba(236,232,240,0.5); max-width: 460px; margin-bottom: 44px; font-weight: 300; }
  .hero-cta-group { display: flex; align-items: center; gap: 20px; flex-wrap: wrap; }
  .btn-primary {
    background: transparent; border: 1px solid rgba(236,232,240,0.25); color: var(--text);
    padding: 14px 38px; font-size: 10px; letter-spacing: 4px; text-transform: uppercase;
    cursor: pointer; transition: all 0.4s; position: relative; overflow: hidden;
    text-decoration: none; display: inline-block; font-family: 'DM Sans', sans-serif; font-weight: 500;
  }
  .btn-primary::before { content: ''; position: absolute; inset: 0; background: linear-gradient(135deg, var(--accent1), var(--accent2)); transform: translateX(-100%); transition: transform 0.4s ease; z-index: -1; }
  .btn-primary:hover { border-color: transparent; color: white; }
  .btn-primary:hover::before { transform: translateX(0); }
  .btn-circle {
    width: 110px; height: 110px; border-radius: 50%;
    background: rgba(15,15,35,0.7); border: 1px solid rgba(255,255,255,0.08);
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    font-size: 8px; letter-spacing: 3px; text-transform: uppercase;
    color: rgba(236,232,240,0.6); cursor: pointer; transition: all 0.4s;
    text-align: center; line-height: 2; font-weight: 500;
  }
  .btn-circle:hover { background: rgba(224,92,122,0.15); border-color: var(--accent1); color: var(--text); transform: scale(1.05); }
  .vertical-text {
    position: absolute; right: 24px; top: 50%; font-size: 9px; letter-spacing: 6px;
    text-transform: uppercase; color: rgba(236,232,240,0.15); white-space: nowrap;
    writing-mode: vertical-rl; transform: translateY(-50%) rotate(180deg);
  }
  .hero-right { display: flex; flex-direction: column; align-items: flex-end; gap: 14px; position: relative; }
  .hero-img-grid { display: grid; grid-template-columns: repeat(4,1fr); gap: 8px; width: 100%; }
  .hero-img-item { aspect-ratio: 3/4; overflow: hidden; position: relative; background: #1a1a2e; }
  .hero-img-item img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.6s ease; filter: grayscale(15%) contrast(1.1); }
  .hero-img-item:hover img { transform: scale(1.06); }
  .hero-img-item::after { content: ''; position: absolute; inset: 0; background: linear-gradient(to bottom, transparent 55%, rgba(8,8,16,0.65) 100%); }

  /* HOME Ticker */
  .ticker-wrap {
    position: relative; overflow: hidden;
    background: rgba(224,92,122,0.08);
    border-top: 1px solid rgba(224,92,122,0.18);
    border-bottom: 1px solid rgba(224,92,122,0.18);
    padding: 13px 0; margin-top: 32px; width: 100%;
  }
  .ticker { display: flex; white-space: nowrap; animation: ticker 22s linear infinite; gap: 56px; }
  @keyframes ticker { from{transform:translateX(0)} to{transform:translateX(-50%)} }
  .ticker span { font-size: 10px; letter-spacing: 5px; text-transform: uppercase; color: rgba(236,232,240,0.35); font-weight: 500; }
  .ticker .dot  { color: var(--accent1); font-size: 14px; }

  /* ===== ABOUT PAGE ===== */
  #about { padding: 120px 60px 80px; position: relative; min-height: 100vh; width: 100%; }
  #about::before { content: ''; position: fixed; inset: 0; background: radial-gradient(ellipse 50% 50% at 88% 12%, rgba(199,125,255,0.12) 0%, transparent 55%), radial-gradient(ellipse 40% 55% at 12% 88%, rgba(91,120,201,0.18) 0%, transparent 55%); pointer-events: none; }
  .about-grid { display: grid; grid-template-columns: 1fr 1.2fr; gap: 72px; align-items: start; }
  .about-img { width: 100%; aspect-ratio: 3/4; background: linear-gradient(160deg,#151525,#2a1a3a,#1a2535); overflow: hidden; position: relative; }
  .about-img::before { content: ''; position: absolute; inset: 0; background: linear-gradient(135deg, rgba(224,92,122,0.18), rgba(91,120,201,0.18)); z-index: 1; }
  .about-img img { width: 100%; height: 100%; object-fit: cover; filter: grayscale(10%) contrast(1.05); }
  .about-img-tag { position: absolute; bottom: -18px; right: -18px; background: var(--accent1); padding: 18px 22px; font-family: 'Bebas Neue', sans-serif; font-size: 13px; letter-spacing: 3px; z-index: 2; }
  .about-name  { font-family: 'Playfair Display', serif; font-size: 52px; letter-spacing: 1px; margin-bottom: 6px; font-style: italic; font-weight: 900; background: linear-gradient(135deg,#fff,rgba(255,255,255,.55)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
  .about-genre { font-size: 10px; letter-spacing: 4px; text-transform: uppercase; color: var(--accent2); margin-bottom: 28px; font-weight: 500; }
  .about-bio   { font-size: 14px; line-height: 2; color: rgba(236,232,240,0.58); margin-bottom: 20px; font-weight: 300; }
  .about-stats { display: grid; grid-template-columns: repeat(3,1fr); gap: 20px; margin: 44px 0; padding: 28px 0; border-top: 1px solid rgba(255,255,255,0.05); border-bottom: 1px solid rgba(255,255,255,0.05); }
  .stat-num    { font-family: 'Playfair Display', serif; font-size: 44px; line-height: 1; font-style: italic; background: linear-gradient(135deg, var(--accent1), var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; margin-bottom: 4px; }
  .stat-label  { font-size: 9px; letter-spacing: 3px; text-transform: uppercase; color: rgba(236,232,240,0.35); font-weight: 500; }
  .influence-label { font-size: 9px; letter-spacing: 4px; text-transform: uppercase; color: rgba(236,232,240,0.3); margin-bottom: 14px; margin-top: 36px; font-weight: 500; }
  .influence-tags  { display: flex; flex-wrap: wrap; gap: 8px; }
  .tag { padding: 7px 16px; border: 1px solid rgba(255,255,255,0.08); font-size: 9px; letter-spacing: 2px; text-transform: uppercase; color: rgba(236,232,240,0.45); transition: all 0.3s; cursor: default; font-weight: 500; }
  .tag:hover { border-color: var(--accent1); color: var(--text); background: rgba(224,92,122,0.07); }

  /* ===== PORTFOLIO PAGE ===== */
  #portfolio { padding: 120px 60px 80px; min-height: 100vh; width: 100%; position: relative; }
  #portfolio::before { content: ''; position: fixed; inset: 0; background: radial-gradient(ellipse 55% 40% at 50% 0%, rgba(201,168,76,0.08) 0%, transparent 55%); pointer-events: none; }
  .portfolio-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 2px; margin-bottom: 60px; }
  .portfolio-item { position: relative; overflow: hidden; cursor: pointer; aspect-ratio: 4/5; background: linear-gradient(135deg,#141428,#1e1535); }
  .portfolio-item:first-child { grid-column: span 2; aspect-ratio: 16/9; }
  .portfolio-img-ph { width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; font-size: 60px; color: rgba(255,255,255,0.04); transition: transform 0.6s ease; }
  .portfolio-item:hover .portfolio-img-ph { transform: scale(1.04); }
  .portfolio-overlay { position: absolute; inset: 0; background: linear-gradient(to top, rgba(8,8,16,0.92) 0%, rgba(8,8,16,0.2) 50%, transparent 100%); display: flex; flex-direction: column; justify-content: flex-end; padding: 28px; opacity: 0; transition: opacity 0.4s; }
  .portfolio-item:hover .portfolio-overlay { opacity: 1; }
  .portfolio-item:first-child .portfolio-overlay { opacity: 1; }
  .portfolio-cat  { font-size: 8px; letter-spacing: 4px; text-transform: uppercase; color: var(--accent1); margin-bottom: 6px; font-weight: 500; }
  .portfolio-name { font-family: 'Playfair Display', serif; font-size: 28px; font-style: italic; font-weight: 700; margin-bottom: 6px; }
  .portfolio-desc { font-size: 12px; color: rgba(236,232,240,0.5); line-height: 1.6; }
  .portfolio-play { position: absolute; top: 20px; right: 20px; width: 44px; height: 44px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.2); display: flex; align-items: center; justify-content: center; background: rgba(0,0,0,0.3); backdrop-filter: blur(8px); cursor: pointer; font-size: 14px; opacity: 0; transition: opacity 0.3s, background 0.3s; }
  .portfolio-item:hover .portfolio-play { opacity: 1; }
  .portfolio-play:hover { background: var(--accent1); border-color: var(--accent1); }
  .awards-strip { display: grid; grid-template-columns: repeat(4,1fr); gap: 1px; background: rgba(255,255,255,0.05); margin-top: 60px; }
  .award-item  { background: var(--bg); padding: 32px 28px; transition: background 0.3s; }
  .award-item:hover { background: rgba(224,92,122,0.05); }
  .award-year  { font-size: 9px; letter-spacing: 3px; text-transform: uppercase; color: var(--accent1); margin-bottom: 10px; font-weight: 500; }
  .award-name  { font-family: 'Playfair Display', serif; font-size: 18px; font-style: italic; margin-bottom: 6px; }
  .award-body  { font-size: 11px; color: rgba(236,232,240,0.35); letter-spacing: 1px; }

  /* ===== MUSIC PAGE ===== */
  #music { padding: 120px 60px 80px; min-height: 100vh; position: relative; width: 100%; }
  #music::before { content: ''; position: fixed; inset: 0; background: radial-gradient(ellipse 55% 35% at 50% 0%, rgba(224,92,122,0.1) 0%, transparent 55%); pointer-events: none; }
  .music-featured { display: grid; grid-template-columns: 1fr 1fr; gap: 2px; margin-bottom: 56px; }
  .featured-track { position: relative; overflow: hidden; cursor: pointer; }
  .featured-track:first-child { grid-row: span 2; min-height: 420px; }
  .track-bg { width: 100%; height: 100%; min-height: inherit; transition: transform 0.6s ease; }
  .featured-track:hover .track-bg { transform: scale(1.03); }
  .track-overlay { position: absolute; inset: 0; background: linear-gradient(to top, rgba(5,5,15,0.92) 0%, transparent 55%); display: flex; flex-direction: column; justify-content: flex-end; padding: 30px; }
  .track-num   { font-family: 'Bebas Neue', sans-serif; font-size: 70px; color: rgba(255,255,255,0.04); line-height: 1; margin-bottom: -16px; }
  .track-type  { font-size: 8px; letter-spacing: 4px; text-transform: uppercase; color: var(--accent1); margin-bottom: 7px; font-weight: 500; }
  .track-title { font-family: 'Playfair Display', serif; font-size: 30px; font-style: italic; font-weight: 700; margin-bottom: 7px; }
  .track-desc  { font-size: 12px; color: rgba(236,232,240,0.4); line-height: 1.6; }
  .play-btn { position: absolute; top: 22px; right: 22px; width: 46px; height: 46px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.18); display: flex; align-items: center; justify-content: center; cursor: pointer; background: rgba(0,0,0,0.3); backdrop-filter: blur(8px); font-size: 14px; transition: all 0.3s; }
  .play-btn:hover { background: var(--accent1); border-color: var(--accent1); }
  .music-subheader { display: flex; align-items: center; justify-content: space-between; margin-bottom: 28px; }
  .music-subheader h3 { font-family: 'Playfair Display', serif; font-size: 26px; font-style: italic; color: rgba(236,232,240,0.65); }
  .see-all { font-size: 9px; letter-spacing: 3px; text-transform: uppercase; color: var(--accent1); cursor: pointer; transition: opacity 0.3s; font-weight: 500; }
  .see-all:hover { opacity: 0.6; }
  .playlist-grid { display: grid; grid-template-columns: repeat(4,1fr); gap: 18px; }
  .playlist-card { cursor: pointer; transition: transform 0.3s; }
  .playlist-card:hover { transform: translateY(-7px); }
  .playlist-cover { aspect-ratio: 1; background: linear-gradient(135deg,#1a1530,#2a2040); margin-bottom: 12px; overflow: hidden; position: relative; }
  .playlist-cover-inner { width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; font-size: 46px; color: rgba(255,255,255,0.04); transition: transform 0.4s; }
  .playlist-card:hover .playlist-cover-inner { transform: scale(1.06); }
  .playlist-cover::after { content: ''; position: absolute; inset: 0; background: linear-gradient(135deg,rgba(224,92,122,0.12),rgba(91,120,201,0.12)); opacity: 0; transition: opacity 0.3s; }
  .playlist-card:hover .playlist-cover::after { opacity: 1; }
  .playlist-name   { font-size: 13px; font-weight: 500; margin-bottom: 3px; }
  .playlist-detail { font-size: 11px; color: rgba(236,232,240,0.38); letter-spacing: 1px; }
  .tracklist { margin-top: 56px; border-top: 1px solid rgba(255,255,255,0.05); }
  .tracklist-header { font-size: 9px; letter-spacing: 4px; text-transform: uppercase; color: rgba(236,232,240,0.22); padding: 18px 0 10px; border-bottom: 1px solid rgba(255,255,255,0.04); font-weight: 500; }
  .track-row { display: grid; grid-template-columns: 38px 1fr auto auto; gap: 18px; align-items: center; padding: 16px 0; border-bottom: 1px solid rgba(255,255,255,0.035); cursor: pointer; transition: all 0.3s; }
  .track-row:hover { background: rgba(255,255,255,0.018); padding-left: 10px; }
  .track-idx      { font-size: 12px; color: rgba(236,232,240,0.18); text-align: center; font-weight: 500; }
  .track-row:hover .track-idx { color: var(--accent1); }
  .track-name-col { font-size: 14px; font-weight: 400; }
  .track-artist   { font-size: 11px; color: rgba(236,232,240,0.38); margin-top: 3px; }
  .track-duration { font-size: 11px; color: rgba(236,232,240,0.3); letter-spacing: 2px; }
  .track-badge    { font-size: 8px; letter-spacing: 2px; text-transform: uppercase; padding: 4px 9px; border: 1px solid rgba(224,92,122,0.4); color: var(--accent1); font-weight: 500; }

  /* ===== GALLERY PAGE ===== */
  #gallery { padding: 120px 60px 80px; min-height: 100vh; width: 100%; }
  .gallery-masonry { columns: 3; column-gap: 10px; margin-top: 56px; }
  .gallery-item { break-inside: avoid; margin-bottom: 10px; overflow: hidden; position: relative; cursor: pointer; }
  .gallery-item-inner { width: 100%; transition: transform 0.5s ease; }
  .gallery-item:hover .gallery-item-inner { transform: scale(1.03); }
  .gallery-img-ph { width: 100%; display: flex; align-items: center; justify-content: center; background: linear-gradient(135deg,#1a1a2e,#2a1535); color: rgba(255,255,255,0.03); font-size: 56px; }
  .gallery-img-ph.tall   { aspect-ratio: 2/3; font-size: 72px; }
  .gallery-img-ph.wide   { aspect-ratio: 4/3; font-size: 46px; }
  .gallery-img-ph.square { aspect-ratio: 1; font-size: 56px; }
  .gallery-item-overlay { position: absolute; inset: 0; background: linear-gradient(to top, rgba(5,5,15,0.82) 0%, transparent 50%); opacity: 0; transition: opacity 0.4s; display: flex; align-items: flex-end; padding: 18px; }
  .gallery-item:hover .gallery-item-overlay { opacity: 1; }
  .gallery-caption { font-size: 10px; letter-spacing: 2px; text-transform: uppercase; color: rgba(236,232,240,0.65); font-weight: 500; }
  .gallery-filters { display: flex; gap: 3px; }
  .filter-btn { padding: 9px 22px; font-size: 9px; letter-spacing: 3px; text-transform: uppercase; background: transparent; border: 1px solid rgba(255,255,255,0.07); color: rgba(236,232,240,0.38); cursor: pointer; transition: all 0.3s; font-family: 'DM Sans', sans-serif; font-weight: 500; }
  .filter-btn.active, .filter-btn:hover { background: var(--accent1); border-color: var(--accent1); color: white; }

  /* ===== CONTACT PAGE ===== */
  #contact { padding: 120px 60px 80px; min-height: 100vh; position: relative; width: 100%; }
  #contact::before { content: ''; position: fixed; inset: 0; background: radial-gradient(ellipse 45% 55% at 80% 80%, rgba(91,120,201,0.18) 0%, transparent 55%); pointer-events: none; }
  .contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 72px; margin-top: 56px; }
  .contact-text { font-size: 14px; line-height: 2; color: rgba(236,232,240,0.5); margin-bottom: 44px; font-weight: 300; }
  .contact-links { display: flex; flex-direction: column; gap: 0; }
  .contact-link { display: flex; align-items: center; gap: 18px; padding: 18px 0; border-bottom: 1px solid rgba(255,255,255,0.04); cursor: pointer; transition: all 0.3s; text-decoration: none; color: var(--text); }
  .contact-link:hover { padding-left: 14px; }
  .contact-link-icon { width: 42px; height: 42px; border: 1px solid rgba(255,255,255,0.08); display: flex; align-items: center; justify-content: center; font-size: 17px; transition: all 0.3s; flex-shrink: 0; }
  .contact-link:hover .contact-link-icon { background: var(--accent1); border-color: var(--accent1); }
  .contact-link-platform { font-size: 9px; letter-spacing: 3px; text-transform: uppercase; color: rgba(236,232,240,0.3); margin-bottom: 3px; font-weight: 500; }
  .contact-link-handle   { font-size: 14px; font-weight: 400; }
  .contact-link-arrow    { color: rgba(236,232,240,0.18); transition: all 0.3s; margin-left: auto; }
  .contact-link:hover .contact-link-arrow { color: var(--accent1); transform: translateX(5px); }
  .form-group   { margin-bottom: 22px; }
  .form-label   { display: block; font-size: 8px; letter-spacing: 4px; text-transform: uppercase; color: rgba(236,232,240,0.3); margin-bottom: 9px; font-weight: 500; }
  .form-input, .form-textarea { width: 100%; background: rgba(255,255,255,0.025); border: 1px solid rgba(255,255,255,0.07); color: var(--text); padding: 13px 16px; font-family: 'DM Sans', sans-serif; font-size: 14px; transition: all 0.3s; outline: none; }
  .form-input:focus, .form-textarea:focus { border-color: rgba(224,92,122,0.45); background: rgba(224,92,122,0.03); }
  .form-textarea { height: 130px; resize: vertical; }
  .form-row    { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  .form-submit { width: 100%; padding: 15px; background: linear-gradient(135deg, var(--accent1), var(--accent2)); border: none; color: white; font-family: 'DM Sans', sans-serif; font-size: 9px; letter-spacing: 5px; text-transform: uppercase; cursor: pointer; transition: all 0.4s; margin-top: 6px; font-weight: 600; }
  .form-submit:hover { transform: translateY(-2px); box-shadow: 0 20px 50px rgba(224,92,122,0.28); }

  /* ===== FOOTER ===== */
  footer { background: rgba(4,4,10,0.85); border-top: 1px solid rgba(255,255,255,0.04); padding: 36px 60px; display: flex; align-items: center; justify-content: space-between; width: 100%; }
  .footer-logo  { font-family: 'Bebas Neue', sans-serif; font-size: 18px; letter-spacing: 5px; color: rgba(236,232,240,0.25); }
  .footer-copy  { font-size: 10px; letter-spacing: 2px; color: rgba(236,232,240,0.18); }
  .footer-links { display: flex; gap: 24px; }
  .footer-links a { font-size: 9px; letter-spacing: 2px; color: rgba(236,232,240,0.22); text-decoration: none; text-transform: uppercase; transition: color 0.3s; cursor: pointer; font-weight: 500; }
  .footer-links a:hover { color: var(--accent1); }

  /* ===== RESPONSIVE ===== */
  @media (max-width: 1100px) {
    .portfolio-grid { grid-template-columns: repeat(2,1fr); }
    .portfolio-item:first-child { grid-column: span 2; aspect-ratio: 16/9; }
    .awards-strip { grid-template-columns: repeat(2,1fr); }
    .sg-s2-photos { display: none; }
  }
  @media (max-width: 1024px) {
    .hero-content { grid-template-columns: 1fr; padding: 120px 40px 60px; }
    .hero-right { align-items: flex-start; }
    .about-grid { grid-template-columns: 1fr; }
    .music-featured { grid-template-columns: 1fr; }
    .featured-track:first-child { grid-row: auto; }
    .contact-grid { grid-template-columns: 1fr; }
    .gallery-masonry { columns: 2; }
    .playlist-grid { grid-template-columns: repeat(2,1fr); }
    .portfolio-grid { grid-template-columns: repeat(2,1fr); }
    .portfolio-item:first-child { grid-column: span 2; }
    .sg-s1-left, .sg-s1-strip { display: none; }
  }
  @media (max-width: 768px) {
    header { padding: 16px 20px; }
    nav { display: none; }
    .menu-btn { display: flex; }
    .hero-content { padding: 100px 20px 40px; }
    #about, #music, #gallery, #contact, #portfolio { padding: 100px 20px 60px; }
    footer { flex-direction: column; gap: 16px; text-align: center; padding: 28px 20px; }
    .gallery-masonry { columns: 2; }
    .playlist-grid { grid-template-columns: repeat(2,1fr); }
    .about-stats { grid-template-columns: repeat(3,1fr); }
    .form-row { grid-template-columns: 1fr; }
    .portfolio-grid { grid-template-columns: 1fr; }
    .portfolio-item:first-child { grid-column: span 1; aspect-ratio: 4/3; }
    .awards-strip { grid-template-columns: 1fr 1fr; }
    .section-number { font-size: 72px; }
    .sg-s1-bottom { padding: 0 20px 22px; flex-direction: column; align-items: flex-start; gap: 10px; }
    .sg-s2-wrap { flex-direction: column; }
    .sg-s2-left { position: relative; left: auto; top: auto; transform: none; padding: 130px 20px 60px; }
    .sg-s2-circle { width: 80vw; height: 80vw; }
    .sg-s3-card { width: 68vw; }
    .sg-s6-foot { padding: 18px 20px; }
    .sg-s6-ring { width: 78vw; height: 78vw; }
  }
  @media (max-width: 767px) {
    .gallery-masonry { columns: 1; }
    .playlist-grid { grid-template-columns: 1fr; }
    .awards-strip { grid-template-columns: 1fr; }
    .hero-img-grid { grid-template-columns: repeat(2,1fr); }
    .sg-s1-photo {
    left: unset;
    transform: unset;
    width: unset;
}
  }


  
</style>
</head>
<body>

<!-- LOADER -->
<div class="loader" id="loader">
  <div class="loader-title">Roots</div>
  <div class="loader-sub">Kreeshna Patel</div>
  <div class="loader-bar"></div>
</div>

<!-- CURSOR -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- MUSIC ANIMATION -->
<div class="music-anim" id="musicAnim"></div>

<!-- WAVEFORM BG -->
<div class="waveform-bg" id="waveformBg"></div>

<!-- ===== HEADER ===== -->
<header id="header">
  <div class="header-logo" onclick="navigateTo('singer')">KREESHNA</div>
  <nav id="mainNav">
    <a onclick="navigateTo('singer')"    class="active" data-page="singer">Singer</a>
    <a onclick="navigateTo('home')"      data-page="home">Home</a>
    <a onclick="navigateTo('about')"     data-page="about">About</a>
    <a onclick="navigateTo('portfolio')" data-page="portfolio">Portfolio</a>
    <a onclick="navigateTo('music')"     data-page="music">Music</a>
    <a onclick="navigateTo('gallery')"   data-page="gallery">Gallery</a>
    <a onclick="navigateTo('contact')"   data-page="contact">Contact</a>
  </nav>
  <div class="menu-btn" id="menuBtn" onclick="toggleMenu()">
    <span></span><span></span><span></span>
  </div>
</header>

<!-- MOBILE MENU -->
<div class="mobile-menu" id="mobileMenu">
  <a onclick="navigateTo('singer');toggleMenu()">Singer</a>
  <a onclick="navigateTo('home');toggleMenu()">Home</a>
  <a onclick="navigateTo('about');toggleMenu()">About</a>
  <a onclick="navigateTo('portfolio');toggleMenu()">Portfolio</a>
  <a onclick="navigateTo('music');toggleMenu()">Music</a>
  <a onclick="navigateTo('gallery');toggleMenu()">Gallery</a>
  <a onclick="navigateTo('contact');toggleMenu()">Contact</a>
</div>

<!-- ============================================================
     SINGER PAGE (Home Page — SIRUP scroll design)
============================================================ -->
<div id="singer" class="page active">

  <!-- S1: Anniversary Hero -->
  <section class="sg-s1">
    <div class="sg-s1-wrap">
      <div class="sg-s1-bgtext">
        <div class="sg-s1-bdate">2018 — 2025</div>
        <div class="sg-s1-b5th">5th</div>
        <div class="sg-s1-banni">Anniversary</div>
      </div>
      <div class="sg-s1-circle"></div>
      <div class="sg-s1-photo">
        <div class="sg-s1-ph">
          <!-- Replace src with Kreeshna's actual photo -->
          <img src="https://cdn.shopify.com/s/files/1/0971/9250/9808/files/New_music_soon__Pic_cr_-__rishiitomar-removebg-preview.png?v=1772306393" alt="Kreeshna Patel" onerror="this.style.display='none'">
        </div>
      </div>
      <div class="sg-s1-strip">BLU-RAY &amp; DVD · NOW ON SALE!</div>
      <div class="sg-s1-left">
        <div class="sg-s1-sm">2018.9.15 "Siren"</div>
        <div class="sg-s1-sm" style="margin-bottom:14px;">digital single release</div>
        <div class="sg-s1-rel">From debut single "Siren" in 2018,<br>2 full albums and 3 EPs released.<br>Kreeshna Patel celebrates<br>his 5th Anniversary.</div>
      </div>
      <div class="sg-s1-rtext">SCROLL</div>
      <div class="sg-s1-bottom">
        <div class="sg-s1-bigyear">2018-2025</div>
        <div class="sg-s1-desc">Kreeshna Patel marks 5 years of boundary-pushing neo-soul and Desi fusion music, celebrating with a landmark roots playlist.</div>
      </div>
    </div>
  </section>

  <!-- Ticker 1 -->
  <div class="sg-ticker-wrap">
    <div class="sg-ticker">
      <span>NEO SOUL</span><span class="dot">·</span><span>R&amp;B</span><span class="dot">·</span><span>HIP HOP</span><span class="dot">·</span><span>DESI FUSION</span><span class="dot">·</span><span>KREESHNA PATEL</span><span class="dot">·</span><span>ROOTS PLAYLIST</span><span class="dot">·</span><span>SOUL</span><span class="dot">·</span>
      <span>NEO SOUL</span><span class="dot">·</span><span>R&amp;B</span><span class="dot">·</span><span>HIP HOP</span><span class="dot">·</span><span>DESI FUSION</span><span class="dot">·</span><span>KREESHNA PATEL</span><span class="dot">·</span><span>ROOTS PLAYLIST</span><span class="dot">·</span><span>SOUL</span><span class="dot">·</span>
    </div>
  </div>

  <!-- S2: Roots -->
  <section class="sg-s2">
    <div class="sg-s2-wrap">
      <div class="sg-s2-circle"></div>
      <div class="sg-s2-artist">
        <div class="sg-s2-artph">
          <img src="" alt="Kreeshna Patel" onerror="this.style.display='none'">
        </div>
      </div>
      <div class="sg-s2-left">
        <div class="sg-s2-kick">KREESHNA PATEL'S</div>
        <div class="sg-s2-title">ROOTS</div>
        <p class="sg-s2-body">From the neo-soul records he grew up on to the contemporary R&amp;B and Desi fusion artists who shaped his voice — rappers, bands, soulful singers and everything in between.</p>
        <div class="sg-s2-btn" onclick="navigateTo('music')">ROOTS<br>PLAYLIST</div>
      </div>
      <div class="sg-s2-photos">
        <div class="sg-s2-ph-item"><div class="sg-s2-ph-box">♪</div></div>
        <div class="sg-s2-ph-item"><div class="sg-s2-ph-box">🎤</div></div>
        <div class="sg-s2-ph-item"><div class="sg-s2-ph-box">🎧</div></div>
        <div class="sg-s2-ph-item"><div class="sg-s2-ph-box">🎶</div></div>
      </div>
      <div class="sg-s2-vt">Soul and R&amp;B and Hip-hop</div>
    </div>
  </section>

  <!-- Ticker 2 (reverse) -->
  <div class="sg-ticker-wrap">
    <div class="sg-ticker" style="animation-direction:reverse;">
      <span>MERE NAAL</span><span class="dot">·</span><span>TU MERA NAIYO HO SAKDA</span><span class="dot">·</span><span>DIL WALA</span><span class="dot">·</span><span>AFTERGLOW</span><span class="dot">·</span><span>ROOH</span><span class="dot">·</span><span>GOLDEN HOUR</span><span class="dot">·</span><span>SIREN</span><span class="dot">·</span>
      <span>MERE NAAL</span><span class="dot">·</span><span>TU MERA NAIYO HO SAKDA</span><span class="dot">·</span><span>DIL WALA</span><span class="dot">·</span><span>AFTERGLOW</span><span class="dot">·</span><span>ROOH</span><span class="dot">·</span><span>GOLDEN HOUR</span><span class="dot">·</span><span>SIREN</span><span class="dot">·</span>
    </div>
  </div>

  <!-- S3: Album Card -->
  <section class="sg-s3">
    <div class="sg-s3-wrap">
      <div class="sg-s3-bgtext">
        <div class="sg-s3-bgl">ROOTS &amp; BOUNCE · KREESHNA PATEL</div>
        <div class="sg-s3-bgl">ROOTS &amp; BOUNCE · KREESHNA PATEL</div>
        <div class="sg-s3-bgl">ROOTS &amp; BOUNCE · KREESHNA PATEL</div>
      </div>
      <div class="sg-s3-card">
        <div class="sg-s3-card-inner">
          <div class="sg-s3-clabel">5th ANNIVERSARY LIVE  2025.03.15</div>
          <div class="sg-s3-ccontent">
            <div>
              <div class="sg-s3-cdate">03.15<br>2025</div>
              <div class="sg-s3-cday">SATURDAY</div>
            </div>
            <div>
              <div class="sg-s3-clogo">Roots &amp;<br>Bounce</div>
              <div style="height:14px;"></div>
              <div class="sg-s3-cvenue">JIOHQ DOME<br>MUMBAI</div>
            </div>
          </div>
        </div>
      </div>
      <div class="sg-s3-info">
        <div class="sg-s3-ilabel">5th Anniversary Live</div>
        <div class="sg-s3-ititle">Roots &amp; Bounce</div>
      </div>
      <div class="sg-s3-sound" id="snd">🔊</div>
    </div>
  </section>

  <!-- S6: Next / Footer -->
  <section class="sg-s6">
    <div class="sg-s6-roll">
      <div class="sg-rrow">ROOTS &amp; BOUNCE · KREESHNA PATEL · ROOTS &amp; BOUNCE · KREESHNA PATEL · ROOTS &amp; BOUNCE · KREESHNA PATEL · </div>
      <div class="sg-rrow">MERE NAAL · TU MERA NAIYO · DIL WALA · AFTERGLOW · MERE NAAL · TU MERA NAIYO · DIL WALA · AFTERGLOW · </div>
      <div class="sg-rrow">ROOTS &amp; BOUNCE · KREESHNA PATEL · ROOTS &amp; BOUNCE · KREESHNA PATEL · ROOTS &amp; BOUNCE · KREESHNA PATEL · </div>
    </div>
    <div class="sg-s6-next">NEXT</div>
    <div class="sg-s6-center">
      <div class="sg-s6-ring">
        <div class="sg-s6-artph">
          <img src="" alt="Kreeshna Patel" onerror="this.style.display='none'">
        </div>
      </div>
    </div>
    <div class="sg-s6-foot">
      <div style="display:flex;gap:28px;flex-wrap:wrap;">
        <div class="sg-s6-site">KREESHNA PATEL OFFICIAL SITE</div>
        <div class="sg-s6-site">CHANNEL KP</div>
      </div>
      <div class="sg-s6-soc">
        <a href="#">𝕏</a><a href="#">📸</a><a href="#">▶</a><a href="#">🎵</a><a href="#">🎧</a>
      </div>
      <div class="sg-s6-copy">© KREESHNA PATEL 2025</div>
    </div>
  </section>

</div><!-- /singer -->

<!-- ============================================================
     HOME PAGE (original — kept exactly as was)
============================================================ -->
<div id="home" class="page">
  <div class="home-bg"></div>
  <div class="home-orb"></div>
  <div class="vertical-text">Soul · R&amp;B · Hip-Hop · Desi Fusion</div>

  <div class="hero-content">
    <div class="hero-left">
      <div class="hero-subtitle">Kreeshna Patel's</div>
      <h1 class="hero-title">
        <span style="position:relative;">Roots
          <span class="hero-title-shadow" aria-hidden="true">Roots</span>
        </span>
      </h1>
      <div class="hero-artist">Music Roots Playlist</div>
      <p class="hero-desc">
        From the neo-soul records he grew up on to the contemporary R&amp;B and Desi fusion
        artists who shaped his voice — Kreeshna Patel's musical DNA laid bare in one playlist.
        Rappers, bands, soulful singers, and everything in between.
      </p>
      <div class="hero-cta-group">
        <a class="btn-primary" onclick="navigateTo('music')">Listen Now</a>
        <div class="btn-circle" onclick="navigateTo('music')">ROOTS<br>PLAYLIST</div>
      </div>
    </div>
    <div class="hero-right">
      <div class="hero-img-grid">
        <div class="hero-img-item"><div class="img-placeholder" style="background:linear-gradient(160deg,#1a1535,#2d1a45);">♪</div></div>
        <div class="hero-img-item"><div class="img-placeholder" style="background:linear-gradient(160deg,#1a2535,#152535);">🎤</div></div>
        <div class="hero-img-item"><div class="img-placeholder" style="background:linear-gradient(160deg,#251520,#3d1525);">🎧</div></div>
        <div class="hero-img-item"><div class="img-placeholder" style="background:linear-gradient(160deg,#152020,#15302a);">🎶</div></div>
      </div>
    </div>
  </div>

  <div class="ticker-wrap">
    <div class="ticker">
      <span>NEO SOUL</span><span class="dot"> · </span><span>R&amp;B</span><span class="dot"> · </span><span>HIP HOP</span><span class="dot"> · </span><span>DESI FUSION</span><span class="dot"> · </span><span>KREESHNA PATEL</span><span class="dot"> · </span><span>PLAYLIST</span><span class="dot"> · </span><span>SOUL</span><span class="dot"> · </span>
      <span>NEO SOUL</span><span class="dot"> · </span><span>R&amp;B</span><span class="dot"> · </span><span>HIP HOP</span><span class="dot"> · </span><span>DESI FUSION</span><span class="dot"> · </span><span>KREESHNA PATEL</span><span class="dot"> · </span><span>PLAYLIST</span><span class="dot"> · </span><span>SOUL</span><span class="dot"> · </span>
    </div>
  </div>

  <footer>
    <div class="footer-logo">KREESHNA PATEL</div>
    <div class="footer-copy">© 2025 Kreeshna Patel. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('about')">About</a>
      <a onclick="navigateTo('music')">Music</a>
      <a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ ABOUT ============ -->
<div id="about" class="page">
  <div class="section-header">
    <div class="section-number">01</div>
    <div><div class="section-label">Artist</div><h2 class="section-title">About</h2></div>
  </div>
  <div class="about-grid">
    <div style="position:relative;">
      <div class="about-img">
        <div class="img-placeholder" style="font-size:80px;background:linear-gradient(160deg,#151525,#2a1a3a,#1a2535);">♪</div>
      </div>
      <div class="about-img-tag">MUMBAI, INDIA</div>
    </div>
    <div>
      <div class="about-name">Kreeshna Patel</div>
      <div class="about-genre">Neo Soul / R&amp;B / Desi Fusion</div>
      <p class="about-bio">Kreeshna Patel is a Mumbai-born singer-songwriter whose voice sits at the crossroads of neo-soul and contemporary R&amp;B, shot through with threads of Desi folk and Bollywood classicism.</p>
      <p class="about-bio">His falsetto — delicate yet deeply felt — has made him a sought-after collaborator across genres. From stadium rappers to intimate jazz ensembles, Kreeshna moves between worlds with rare ease, always bringing something unmistakably his own.</p>
      <p class="about-bio">"Mere Naal" and "Tu Mera Naiyo Ho Sakda" marked his mainstream arrival. His debut album cemented a sound no one had heard quite like before.</p>
      <div class="about-stats">
        <div><div class="stat-num">4+</div><div class="stat-label">Studio Albums</div></div>
        <div><div class="stat-num">80M</div><div class="stat-label">Streams</div></div>
        <div><div class="stat-num">2018</div><div class="stat-label">Debut Year</div></div>
      </div>
      <div class="influence-label">Musical Influences</div>
      <div class="influence-tags">
        <span class="tag">D'Angelo</span><span class="tag">Frank Ocean</span><span class="tag">Anderson Paak</span>
        <span class="tag">Kendrick Lamar</span><span class="tag">Erykah Badu</span><span class="tag">Arijit Singh</span>
        <span class="tag">A.R. Rahman</span><span class="tag">Thundercat</span><span class="tag">SZA</span><span class="tag">Lucky Ali</span>
      </div>
    </div>
  </div>
  <footer>
    <div class="footer-logo">KREESHNA PATEL</div>
    <div class="footer-copy">© 2025 Kreeshna Patel. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('singer')">Singer</a><a onclick="navigateTo('music')">Music</a><a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ PORTFOLIO ============ -->
<div id="portfolio" class="page">
  <div class="section-header">
    <div class="section-number">02</div>
    <div><div class="section-label">Projects &amp; Releases</div><h2 class="section-title">Portfolio</h2></div>
  </div>
  <div class="portfolio-grid">
    <div class="portfolio-item" style="background:linear-gradient(140deg,#1a0a2e,#2d1545,#180e2a);">
      <div class="portfolio-img-ph" style="font-size:100px;">♫</div>
      <div class="portfolio-overlay"><div class="portfolio-cat">Debut Album · 2022</div><div class="portfolio-name">Roots</div><div class="portfolio-desc">A 12-track journey through neo-soul and Desi fusion — the record that introduced the world to Kreeshna Patel's singular voice.</div></div>
      <div class="portfolio-play">▶</div>
    </div>
    <div class="portfolio-item" style="background:linear-gradient(140deg,#0a1a30,#152545,#0e1a30);">
      <div class="portfolio-img-ph">🎙</div>
      <div class="portfolio-overlay"><div class="portfolio-cat">Single · 2023</div><div class="portfolio-name">Mere Naal</div><div class="portfolio-desc">The breakthrough hit that redefined Punjabi-soul. Over 30M streams in its first month.</div></div>
      <div class="portfolio-play">▶</div>
    </div>
    <div class="portfolio-item" style="background:linear-gradient(140deg,#2a1a0a,#3d2515,#281508);">
      <div class="portfolio-img-ph">🎶</div>
      <div class="portfolio-overlay"><div class="portfolio-cat">Single · 2023</div><div class="portfolio-name">Tu Mera Naiyo Ho Sakda</div><div class="portfolio-desc">A heartbreak ballad wrapped in acoustic guitar and layered harmonics.</div></div>
      <div class="portfolio-play">▶</div>
    </div>
    <div class="portfolio-item" style="background:linear-gradient(140deg,#0a2a1a,#153525,#082015);">
      <div class="portfolio-img-ph">🎸</div>
      <div class="portfolio-overlay"><div class="portfolio-cat">EP · 2024</div><div class="portfolio-name">Afterglow</div><div class="portfolio-desc">Six tracks exploring late-night introspection and city lights.</div></div>
      <div class="portfolio-play">▶</div>
    </div>
    <div class="portfolio-item" style="background:linear-gradient(140deg,#1a1a0a,#2a2515,#181800);">
      <div class="portfolio-img-ph">🎹</div>
      <div class="portfolio-overlay"><div class="portfolio-cat">Collaboration · 2024</div><div class="portfolio-name">Dil Wala</div><div class="portfolio-desc">A genre-crossing collaboration with rapper AP Dhillon and producer FalakShabbir.</div></div>
      <div class="portfolio-play">▶</div>
    </div>
  </div>
  <div style="font-size:9px;letter-spacing:5px;text-transform:uppercase;color:rgba(236,232,240,0.25);margin:60px 0 0;font-weight:500;">Recognition</div>
  <div class="awards-strip">
    <div class="award-item"><div class="award-year">2023</div><div class="award-name">Best New Artist</div><div class="award-body">MTV India Music Awards</div></div>
    <div class="award-item"><div class="award-year">2023</div><div class="award-name">Song of the Year</div><div class="award-body">Mirchi Music Awards — Mere Naal</div></div>
    <div class="award-item"><div class="award-year">2024</div><div class="award-name">Best R&amp;B Album</div><div class="award-body">Global Indian Music Academy</div></div>
    <div class="award-item"><div class="award-year">2024</div><div class="award-name">Breakthrough Artist</div><div class="award-body">Rolling Stone India</div></div>
  </div>
  <footer>
    <div class="footer-logo">KREESHNA PATEL</div>
    <div class="footer-copy">© 2025 Kreeshna Patel. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('singer')">Singer</a><a onclick="navigateTo('music')">Music</a><a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ MUSIC ============ -->
<div id="music" class="page">
  <div class="section-header">
    <div class="section-number">03</div>
    <div><div class="section-label">Discography</div><h2 class="section-title">Music</h2></div>
  </div>
  <div class="music-featured">
    <div class="featured-track" style="min-height:420px;">
      <div class="track-bg" style="background:linear-gradient(135deg,#1a0a2e,#2d1545,#1a1535);min-height:420px;"></div>
      <div class="track-overlay"><div class="track-num">01</div><div><div class="track-type">Latest Release</div><div class="track-title">Roots Playlist</div><div class="track-desc">A journey through the music that shaped Kreeshna Patel's sound — from neo-soul classics to Desi fusion.</div></div></div>
      <div class="play-btn">▶</div>
    </div>
    <div class="featured-track">
      <div class="track-bg" style="background:linear-gradient(135deg,#0a1a2e,#1a2545);aspect-ratio:1;"></div>
      <div class="track-overlay"><div class="track-num">02</div><div><div class="track-type">Album</div><div class="track-title">Afterglow</div><div class="track-desc">Six tracks of late-night introspection.</div></div></div>
      <div class="play-btn">▶</div>
    </div>
    <div class="featured-track">
      <div class="track-bg" style="background:linear-gradient(135deg,#1a2a0a,#253020);aspect-ratio:1;"></div>
      <div class="track-overlay"><div class="track-num">03</div><div><div class="track-type">EP</div><div class="track-title">Dil Wala</div><div class="track-desc">Genre-crossing collab with AP Dhillon.</div></div></div>
      <div class="play-btn">▶</div>
    </div>
  </div>
  <div class="music-subheader"><h3>Roots Playlist</h3><span class="see-all">See All ↗</span></div>
  <div class="playlist-grid">
    <div class="playlist-card"><div class="playlist-cover"><div class="playlist-cover-inner" style="background:linear-gradient(135deg,#2d1535,#1a0a2e);">🎵</div></div><div class="playlist-name">Neo Soul Roots</div><div class="playlist-detail">Vol. 1 · 18 tracks</div></div>
    <div class="playlist-card"><div class="playlist-cover"><div class="playlist-cover-inner" style="background:linear-gradient(135deg,#0a1a35,#1a2545);">🎧</div></div><div class="playlist-name">R&amp;B Influences</div><div class="playlist-detail">Vol. 2 · 24 tracks</div></div>
    <div class="playlist-card"><div class="playlist-cover"><div class="playlist-cover-inner" style="background:linear-gradient(135deg,#1a1a0a,#2a2515);">🥁</div></div><div class="playlist-name">Desi Fusion Vibes</div><div class="playlist-detail">Vol. 3 · 16 tracks</div></div>
    <div class="playlist-card"><div class="playlist-cover"><div class="playlist-cover-inner" style="background:linear-gradient(135deg,#0a1a1a,#152525);">🎶</div></div><div class="playlist-name">Collaborations</div><div class="playlist-detail">Vol. 4 · 12 tracks</div></div>
  </div>
  <div class="tracklist">
    <div class="tracklist-header">Featured Tracks</div>
    <div class="track-row"><div class="track-idx">01</div><div class="track-name-col"><div>Mere Naal</div><div class="track-artist">Kreeshna Patel</div></div><div class="track-badge">HIT</div><div class="track-duration">3:52</div></div>
    <div class="track-row"><div class="track-idx">02</div><div class="track-name-col"><div>Tu Mera Naiyo Ho Sakda</div><div class="track-artist">Kreeshna Patel</div></div><div></div><div class="track-duration">4:18</div></div>
    <div class="track-row"><div class="track-idx">03</div><div class="track-name-col"><div>Dil Wala</div><div class="track-artist">Kreeshna Patel feat. AP Dhillon</div></div><div></div><div class="track-duration">4:05</div></div>
    <div class="track-row"><div class="track-idx">04</div><div class="track-name-col"><div>Afterglow</div><div class="track-artist">Kreeshna Patel</div></div><div></div><div class="track-duration">3:44</div></div>
    <div class="track-row"><div class="track-idx">05</div><div class="track-name-col"><div>Rooh</div><div class="track-artist">Kreeshna Patel</div></div><div class="track-badge">NEW</div><div class="track-duration">5:10</div></div>
    <div class="track-row"><div class="track-idx">06</div><div class="track-name-col"><div>Golden Hour</div><div class="track-artist">Kreeshna Patel feat. Ritviz</div></div><div></div><div class="track-duration">3:38</div></div>
    <div class="track-row"><div class="track-idx">07</div><div class="track-name-col"><div>Midnight Raag</div><div class="track-artist">Kreeshna Patel</div></div><div></div><div class="track-duration">4:22</div></div>
    <div class="track-row"><div class="track-idx">08</div><div class="track-name-col"><div>Siren</div><div class="track-artist">Kreeshna Patel feat. DIVINE</div></div><div></div><div class="track-duration">3:57</div></div>
  </div>
  <footer>
    <div class="footer-logo">KREESHNA PATEL</div>
    <div class="footer-copy">© 2025 Kreeshna Patel. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('singer')">Singer</a><a onclick="navigateTo('about')">About</a><a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ GALLERY ============ -->
<div id="gallery" class="page">
  <div style="display:flex;align-items:flex-end;justify-content:space-between;margin-bottom:36px;flex-wrap:wrap;gap:16px;padding:120px 60px 0;">
    <div style="display:flex;align-items:flex-end;gap:20px;">
      <div class="section-number">04</div>
      <div><div class="section-label">Visual</div><h2 class="section-title">Gallery</h2></div>
    </div>
    <div class="gallery-filters">
      <button class="filter-btn active" onclick="filterGallery(this)">All</button>
      <button class="filter-btn" onclick="filterGallery(this)">Live</button>
      <button class="filter-btn" onclick="filterGallery(this)">Studio</button>
      <button class="filter-btn" onclick="filterGallery(this)">Press</button>
    </div>
  </div>
  <div style="padding:0 60px 80px;">
    <div class="gallery-masonry">
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph tall" style="background:linear-gradient(160deg,#1a0a2e,#2d1545);">♪</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Live — Mumbai 2024</span></div></div>
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph wide" style="background:linear-gradient(160deg,#0a1a2e,#152535);">🎤</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Studio Session</span></div></div>
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph square" style="background:linear-gradient(160deg,#1a2a0a,#253020);">🎵</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Press — Delhi</span></div></div>
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph wide" style="background:linear-gradient(160deg,#2a1a0a,#3d2515);">🎧</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Live — Pune 2023</span></div></div>
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph tall" style="background:linear-gradient(160deg,#0a2a1a,#153525);">🎶</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Press Shoot 2024</span></div></div>
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph square" style="background:linear-gradient(160deg,#1a1a2e,#2d2545);">🎹</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Studio — Album Recording</span></div></div>
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph wide" style="background:linear-gradient(160deg,#2a0a1a,#3d152a);">🎸</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Live — NH7 Weekender 2023</span></div></div>
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph tall" style="background:linear-gradient(160deg,#0a0a2e,#151540);">🎺</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Press — Magazine Feature</span></div></div>
      <div class="gallery-item"><div class="gallery-item-inner"><div class="gallery-img-ph square" style="background:linear-gradient(160deg,#1a2a1a,#253525);">🥁</div></div><div class="gallery-item-overlay"><span class="gallery-caption">Live — Lollapalooza India</span></div></div>
    </div>
  </div>
  <footer>
    <div class="footer-logo">KREESHNA PATEL</div>
    <div class="footer-copy">© 2025 Kreeshna Patel. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('singer')">Singer</a><a onclick="navigateTo('music')">Music</a><a onclick="navigateTo('contact')">Contact</a>
    </div>
  </footer>
</div>

<!-- ============ CONTACT ============ -->
<div id="contact" class="page">
  <div class="section-header">
    <div class="section-number">05</div>
    <div><div class="section-label">Get in Touch</div><h2 class="section-title">Contact</h2></div>
  </div>
  <div class="contact-grid">
    <div>
      <p class="contact-text">For bookings, press enquiries, and collaborations — reach out through the form or connect via social media. Kreeshna Patel's team will respond as soon as possible.</p>
      <div class="contact-links">
        <a class="contact-link" href="https://instagram.com" target="_blank"><div class="contact-link-icon">📸</div><div><div class="contact-link-platform">Instagram</div><div class="contact-link-handle">@kreeshna_music</div></div><span class="contact-link-arrow">→</span></a>
        <a class="contact-link" href="https://twitter.com" target="_blank"><div class="contact-link-icon">𝕏</div><div><div class="contact-link-platform">Twitter / X</div><div class="contact-link-handle">@kreeshnapatel</div></div><span class="contact-link-arrow">→</span></a>
        <a class="contact-link" href="https://open.spotify.com" target="_blank"><div class="contact-link-icon">🎵</div><div><div class="contact-link-platform">Spotify</div><div class="contact-link-handle">Kreeshna Patel Official</div></div><span class="contact-link-arrow">→</span></a>
        <a class="contact-link" href="https://youtube.com" target="_blank"><div class="contact-link-icon">▶</div><div><div class="contact-link-platform">YouTube</div><div class="contact-link-handle">KREESHNA PATEL OFFICIAL</div></div><span class="contact-link-arrow">→</span></a>
        <div class="contact-link" style="cursor:default;"><div class="contact-link-icon">✉</div><div><div class="contact-link-platform">Booking &amp; Press</div><div class="contact-link-handle">info@kreeshnapatel.com</div></div></div>
      </div>
    </div>
    <div>
      <div class="form-row">
        <div class="form-group"><label class="form-label">First Name</label><input class="form-input" type="text" placeholder="Your name"></div>
        <div class="form-group"><label class="form-label">Last Name</label><input class="form-input" type="text" placeholder="Last name"></div>
      </div>
      <div class="form-group"><label class="form-label">Email Address</label><input class="form-input" type="email" placeholder="your@email.com"></div>
      <div class="form-group"><label class="form-label">Subject</label><input class="form-input" type="text" placeholder="Booking / Press / Collab"></div>
      <div class="form-group"><label class="form-label">Message</label><textarea class="form-textarea" placeholder="Tell us about your inquiry..."></textarea></div>
      <button class="form-submit" onclick="submitForm(this)">Send Message</button>
    </div>
  </div>
  <footer>
    <div class="footer-logo">KREESHNA PATEL</div>
    <div class="footer-copy">© 2025 Kreeshna Patel. All rights reserved.</div>
    <div class="footer-links">
      <a onclick="navigateTo('singer')">Singer</a><a onclick="navigateTo('about')">About</a><a onclick="navigateTo('music')">Music</a>
    </div>
  </footer>
</div>

<script>
  // LOADER
  window.addEventListener('load', () => {
    setTimeout(() => {
      document.getElementById('loader').classList.add('hidden');
      setTimeout(() => document.getElementById('loader').remove(), 800);
    }, 2000);
  });

  // CURSOR
  const cursor = document.getElementById('cursor');
  const cursorRing = document.getElementById('cursorRing');
  let mouseX = 0, mouseY = 0, ringX = 0, ringY = 0;
  document.addEventListener('mousemove', (e) => {
    mouseX = e.clientX; mouseY = e.clientY;
    cursor.style.left = mouseX + 'px'; cursor.style.top = mouseY + 'px';
  });
  (function animateRing() {
    ringX += (mouseX - ringX) * 0.13;
    ringY += (mouseY - ringY) * 0.13;
    cursorRing.style.left = ringX + 'px'; cursorRing.style.top = ringY + 'px';
    requestAnimationFrame(animateRing);
  })();
  document.addEventListener('mousedown', () => { cursor.style.transform = 'translate(-50%,-50%) scale(1.8)'; cursorRing.style.transform = 'translate(-50%,-50%) scale(0.7)'; });
  document.addEventListener('mouseup',   () => { cursor.style.transform = 'translate(-50%,-50%) scale(1)';   cursorRing.style.transform = 'translate(-50%,-50%) scale(1)'; });

  // FLOATING NOTES
  const noteChars = ['♩','♪','♫','♬','𝄞','𝄢','🎵','🎶'];
  const animContainer = document.getElementById('musicAnim');
  function spawnNote() {
    const el = document.createElement('div');
    el.className = 'note';
    el.textContent = noteChars[Math.floor(Math.random() * noteChars.length)];
    el.style.setProperty('--dur', (8 + Math.random() * 10) + 's');
    el.style.setProperty('--delay', (Math.random() * 6) + 's');
    el.style.left = (Math.random() * 98) + '%';
    el.style.bottom = (Math.random() * 20) + '%';
    el.style.fontSize = (14 + Math.random() * 22) + 'px';
    animContainer.appendChild(el);
    setTimeout(() => el.remove(), 20000);
  }
  setInterval(spawnNote, 800);
  for (let i = 0; i < 8; i++) setTimeout(spawnNote, i * 200);

  // WAVEFORM
  const waveEl = document.getElementById('waveformBg');
  const barCount = Math.floor(window.innerWidth / 6);
  for (let i = 0; i < barCount; i++) {
    const bar = document.createElement('div');
    bar.className = 'wave-bar';
    const minH = 4 + Math.random() * 12;
    const maxH = minH + 20 + Math.random() * 40;
    bar.style.setProperty('--min-h', minH + 'px');
    bar.style.setProperty('--max-h', maxH + 'px');
    bar.style.setProperty('--spd', (0.6 + Math.random() * 1.2) + 's');
    bar.style.setProperty('--dly', (Math.random() * 1.5) + 's');
    waveEl.appendChild(bar);
  }

  // NAVIGATION
  let currentPage = 'singer';
  function navigateTo(pageId) {
    if (pageId === currentPage) return;
    document.getElementById(currentPage).classList.remove('active');
    document.getElementById(pageId).classList.add('active');
    document.querySelectorAll('nav a').forEach(a => a.classList.toggle('active', a.dataset.page === pageId));
    currentPage = pageId;
    window.scrollTo(0, 0);
  }

  // MOBILE MENU
  function toggleMenu() {
    document.getElementById('mobileMenu').classList.toggle('open');
    document.getElementById('menuBtn').classList.toggle('open');
  }

  // SOUND TOGGLE (Singer page)
  document.getElementById('snd').addEventListener('click', function() {
    this.textContent = this.textContent === '🔊' ? '🔇' : '🔊';
  });

  // GALLERY FILTER
  function filterGallery(btn) {
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
  }

  // FORM SUBMIT
  function submitForm(btn) {
    btn.textContent = 'Sending...'; btn.style.opacity = '0.7';
    setTimeout(() => {
      btn.textContent = 'Message Sent ✓';
      btn.style.background = 'linear-gradient(135deg,#2d6a4f,#52b788)'; btn.style.opacity = '1';
      setTimeout(() => { btn.textContent = 'Send Message'; btn.style.background = ''; }, 3000);
    }, 1200);
  }

  // SCROLL HEADER
  const header = document.getElementById('header');
  window.addEventListener('scroll', () => {
    header.style.background = window.scrollY > 80 ? 'rgba(8,8,16,0.96)' : 'linear-gradient(to bottom,rgba(8,8,16,0.97) 0%,transparent 100%)';
    header.style.backdropFilter = window.scrollY > 80 ? 'blur(18px)' : 'blur(0px)';
  });

  // PLAY BUTTONS
  document.querySelectorAll('.play-btn,.portfolio-play').forEach(btn => {
    btn.addEventListener('click', (e) => {
      e.stopPropagation();
      const orig = btn.textContent;
      btn.textContent = '⏸';
      setTimeout(() => btn.textContent = orig, 2000);
    });
  });
</script>
</body>
</html>
