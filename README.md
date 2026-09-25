<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Ein Tag für Papa</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600&family=Karla:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    box-sizing:border-box;
    padding-top:env(safe-area-inset-top,0px);
    padding-bottom:env(safe-area-inset-bottom,0px);
    --bg:#FBF0E4; --fg:#3B2A1D; --accent:#E0834F; --sub:#8A6F58;
  }
  html{scroll-padding-top:env(safe-area-inset-top,0px);}
  *,*::before,*::after{box-sizing:inherit;}
  html,body{height:100%;margin:0;}
  body{ font-family:'Karla',sans-serif; color:var(--fg); min-height:100%; }
  #bg{ position:fixed; inset:0; background:var(--bg); z-index:-1; }
  main{ position:relative; }
  .stage{
    min-height:100vh;
    display:flex; align-items:center; justify-content:center;
    padding:3rem 1.6rem;
  }
  .content{
    width:100%; max-width:540px; text-align:center;
    opacity:0; transform:translateY(26px);
    transition:opacity 0.8s ease, transform 0.8s ease;
  }
  .content.visible{ opacity:1; transform:translateY(0); }

  .photo{
    width:100%; max-width:420px; aspect-ratio:4/3;
    margin:0 auto 1.6rem; border-radius:14px; overflow:hidden;
  }
  .photo img{ width:100%; height:100%; object-fit:cover; display:block; }

  .logo{
    width:110px; margin:1.6rem auto 0;
  }
  .logo img{ width:100%; height:auto; display:block; object-fit:contain; }

  .photo-pair{
    display:flex; gap:1rem; justify-content:center;
    max-width:420px; margin:0 auto 1.6rem;
  }
  .photo-pair .item{ flex:1 1 0; min-width:0; }
  .photo-pair .frame{
    width:100%; aspect-ratio:3/4; border-radius:14px; overflow:hidden;
  }
  .photo-pair .frame img{ width:100%; height:100%; object-fit:cover; display:block; }
  .photo-pair figcaption{
    margin-top:0.5rem; font-size:0.9rem; color:var(--sub); transition:color 0.7s ease;
  }

  h1{
    font-family:'Fraunces',serif; font-weight:500;
    font-size:clamp(1.9rem,6vw,2.8rem); line-height:1.15; margin:0 0 1rem;
  }
  p.desc{
    font-size:1.05rem; line-height:1.6; opacity:0.86;
    max-width:36ch; margin:0 auto;
  }

  /* nested sport carousel */
  .carousel{
    display:flex; align-items:center; justify-content:center; gap:1.4rem;
    margin-top:0.6rem;
  }
  .carousel button.nav{
    appearance:none; border:none; background:var(--accent); color:var(--bg);
    width:46px; height:46px; border-radius:50%;
    display:flex; align-items:center; justify-content:center;
    cursor:pointer; transition:transform 0.15s ease, background 0.7s ease;
    flex-shrink:0;
  }
  .carousel button.nav:hover{ transform:scale(1.06); }
  .carousel button.nav:focus-visible{ outline:2px solid var(--fg); outline-offset:3px; }
  .carousel button.nav svg{ width:18px; height:18px; }
  .word-wrap{ min-width:0; }
  .word{
    font-family:'Fraunces',serif; font-weight:500;
    font-size:clamp(1.8rem,7vw,3rem);
    transition:opacity 0.25s ease;
  }
  .word.final{ font-family:'Karla',sans-serif; font-weight:500; font-size:1.15rem; line-height:1.55; max-width:32ch; }
  .dots-inline{ display:flex; justify-content:center; gap:6px; margin-top:1.4rem; }
  .dots-inline span{ width:6px; height:6px; border-radius:50%; background:var(--fg); opacity:0.2; transition:opacity 0.3s ease; }
  .dots-inline span.active{ opacity:0.9; }

  .dates{
    list-style:none; margin:1.8rem 0 0; padding:0;
    display:flex; flex-direction:column; gap:0.65rem;
    max-width:320px; margin-left:auto; margin-right:auto;
  }
  .dates li{
    border:1.5px solid var(--accent);
    border-radius:999px;
    padding:0.7rem 1.3rem;
    font-weight:600;
    transition:border-color 0.7s ease;
  }

  @media (prefers-reduced-motion:reduce){
    .content{ transition:opacity 0.2s linear; transform:none; }
  }
</style>
</head>
<body>

<div id="bg"></div>
<main id="main"></main>

<script>
const stages = [
  {
    kind:'cover',
    title:'Ein Tag. Du und ich.',
    desc:'Viel Spaß. Hoffentlich.',
    bg:'#FBF0E4', fg:'#3B2A1D', accent:'#E0834F', sub:'#8A6F58',
    photos:[
      {src:'img/du.jpg', caption:'Du'},
      {src:'img/ich.jpg', caption:'Ich'}
    ]
  },
  {
    title:'Was leckeres frühstücken.',
    desc:'Bei dir, bei mir, auswärts, alles möglich.',
    bg:'#FAEBD9', fg:'#3B2A1D', accent:'#E0834F', sub:'#8A6F58',
    photo:'img/fruehstueck.jpg'
  },
  {
    kind:'sport',
    title:'Sportlich sein',
    bg:'#E9F3F7', fg:'#16303F', accent:'#2F86B5', sub:'#5C7E8E',
    words:[
      {text:'Fußball?', photo:'img/sport-fussball.jpg', aspect:'3/4.3'},
      {text:'Tennis?', photo:'img/sport-tennis.jpg'},
      {text:'TISCHTennis?', photo:'img/sport-tischtennis.jpg'},
      {text:'Padel?', photo:'img/sport-padel.jpg'},
      {text:'LAUFEN???', photo:'img/sport-laufen.jpg'}
    ],
    final:{text:'Wir werden schon was finden, wo wir uns messen können.', photo:'img/sport-final.jpg'}
  },
  {
    title:'Bisschen chillen',
    desc:'Haben wir uns aber auch wirklich verdient. Vielleicht was kleines essen, was nettes spielen.',
    bg:'#FBF1DA', fg:'#3A2A0E', accent:'#C0812C', sub:'#8F7442',
    photo:'img/chillen.jpg'
  },
  {
    title:'Fußball gucken!',
    desc:'Ein Tag ohne Fußball geht gar nicht! Ab an die Adolf-Jäger-Kampfbahn und endlich mal richtigen Fußball gucken.',
    bg:'#12302A', fg:'#F4EFD9', accent:'#F0C24C', sub:'#B9C9B8',
    photo:'img/fussball-gucken.jpg',
    logo:'img/altona93-logo.png'
  },
  {
    title:'Tag vorbei',
    desc:'Reicht ja dann auch mal. Na gut, vielleicht noch ein Abschlussbierchen in ner Kneipe.',
    bg:'#2B2040', fg:'#F1E9F5', accent:'#E58A56', sub:'#B7A9C7',
    photo:'img/tag-vorbei.jpg'
  },
  {
    kind:'dates',
    title:'Wann geht´s los?',
    desc:'Du kannst es sicher gar nicht mehr abwarten und willst wissen, wanns endlich losgeht.',
    bg:'#221A34', fg:'#F1E9F5', accent:'#F2C14E', sub:'#B7A9C7',
    dates:['Samstag, 10.10.2026','Dienstag, 20.10.2026','Samstag, 24.10.2026','Samstag, 07.11.2026']
  }
];

const main = document.getElementById('main');

function photoHTML(src, aspect){
  if(!src) return '';
  const ratio = aspect || '4/3';
  return `<div class="photo" style="aspect-ratio:${ratio}"><img src="${src}" alt="" onerror="this.closest('.photo').style.display='none'"></div>`;
}

function photoPairHTML(photos){
  if(!photos || !photos.length) return '';
  const items = photos.map(p => `
    <figure class="item">
      <div class="frame"><img src="${p.src}" alt="" onerror="this.closest('.item').style.display='none'"></div>
      <figcaption>${p.caption}</figcaption>
    </figure>
  `).join('');
  return `<div class="photo-pair">${items}</div>`;
}

function logoHTML(src){
  if(!src) return '';
  return `<div class="logo"><img src="${src}" alt="" onerror="this.closest('.logo').style.display='none'"></div>`;
}

stages.forEach((s, idx) => {
  const section = document.createElement('section');
  section.className = 'stage';
  section.id = 'stage-' + idx;
  section.dataset.index = idx;

  if(s.kind === 'sport'){
    section.innerHTML = `
      <div class="content">
        <h1>${s.title}</h1>
        <div class="carousel">
          <button class="nav" id="sportPrev" aria-label="Vorheriges Wort">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 5 L8 12 L15 19" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </button>
          <div class="word-wrap"><div class="word" id="sportWord"></div></div>
          <button class="nav" id="sportNext" aria-label="Nächstes Wort">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 5 L16 12 L9 19" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </button>
        </div>
        <div id="sportPhotoSlot"></div>
        <div class="dots-inline" id="sportDots"></div>
      </div>
    `;
  } else if(s.kind === 'dates'){
    section.innerHTML = `
      <div class="content">
        <h1>${s.title}</h1>
        <p class="desc">${s.desc}</p>
        <ul class="dates">${s.dates.map(d => `<li>${d}</li>`).join('')}</ul>
      </div>
    `;
  } else {
    section.innerHTML = `
      <div class="content">
        ${s.kind === 'cover' ? photoPairHTML(s.photos) : photoHTML(s.photo)}
        <h1>${s.title}</h1>
        <p class="desc">${s.desc}</p>
        ${logoHTML(s.logo)}
      </div>
    `;
  }
  main.appendChild(section);
});

// sport nested carousel
(function(){
  const sportStage = stages.find(s => s.kind === 'sport');
  const items = [...sportStage.words, sportStage.final];
  let si = 0;
  const wordEl = document.getElementById('sportWord');
  const dotsEl = document.getElementById('sportDots');
  const photoSlot = document.getElementById('sportPhotoSlot');
  items.forEach((_, k) => {
    const d = document.createElement('span');
    d.dataset.k = k;
    dotsEl.appendChild(d);
  });
  function renderSport(){
    const isFinal = si === items.length - 1;
    wordEl.textContent = items[si].text;
    wordEl.className = 'word' + (isFinal ? ' final' : '');
    photoSlot.innerHTML = photoHTML(items[si].photo, items[si].aspect);
    Array.from(dotsEl.children).forEach((d,k) => d.classList.toggle('active', k === si));
    document.getElementById('sportPrev').disabled = si === 0;
  }
  document.getElementById('sportNext').addEventListener('click', () => {
    si = Math.min(si + 1, items.length - 1); renderSport();
  });
  document.getElementById('sportPrev').addEventListener('click', () => {
    si = Math.max(si - 1, 0); renderSport();
  });
  document.addEventListener('keydown', (e) => {
    const rect = document.getElementById('stage-2').getBoundingClientRect();
    const inView = rect.top < window.innerHeight * 0.6 && rect.bottom > window.innerHeight * 0.4;
    if(!inView) return;
    if(e.key === 'ArrowRight'){ si = Math.min(si + 1, items.length - 1); renderSport(); }
    if(e.key === 'ArrowLeft'){ si = Math.max(si - 1, 0); renderSport(); }
  });
  renderSport();
})();

// reveal-on-view
const io = new IntersectionObserver((entries) => {
  entries.forEach(e => { if(e.isIntersecting) e.target.querySelector('.content').classList.add('visible'); });
}, {threshold:0.3});
document.querySelectorAll('.stage').forEach(s => io.observe(s));

// continuous background color interpolation tied to scroll
function hexToRgb(hex){ const n = parseInt(hex.slice(1), 16); return [(n>>16)&255,(n>>8)&255,n&255]; }
function rgbToHex(r,g,b){ return '#' + [r,g,b].map(v => Math.round(v).toString(16).padStart(2,'0')).join(''); }
function lerpColor(a,b,t){ const ca=hexToRgb(a), cb=hexToRgb(b); return rgbToHex(ca[0]+(cb[0]-ca[0])*t, ca[1]+(cb[1]-ca[1])*t, ca[2]+(cb[2]-ca[2])*t); }

const sections = () => Array.from(document.querySelectorAll('.stage'));

let ticking = false;
function updateScroll(){
  ticking = false;
  const els = sections();
  const centerY = window.scrollY + window.innerHeight / 2;
  let idx = 0, frac = 0;
  for(let k = 0; k < els.length; k++){
    const top = els[k].offsetTop, height = els[k].offsetHeight;
    if(centerY >= top && centerY < top + height){ idx = k; frac = (centerY - top) / height; break; }
    if(k === els.length - 1){ idx = k; frac = 1; }
  }
  const cur = stages[idx], next = stages[Math.min(idx+1, stages.length-1)];
  const t = Math.min(Math.max(frac,0),1);
  document.documentElement.style.setProperty('--bg', lerpColor(cur.bg, next.bg, t));
  document.documentElement.style.setProperty('--fg', lerpColor(cur.fg, next.fg, t));
  document.documentElement.style.setProperty('--accent', lerpColor(cur.accent, next.accent, t));
  document.documentElement.style.setProperty('--sub', lerpColor(cur.sub, next.sub, t));
}
window.addEventListener('scroll', () => { if(!ticking){ requestAnimationFrame(updateScroll); ticking = true; } }, {passive:true});
window.addEventListener('resize', updateScroll);
updateScroll();
</script>
</body>
</html>
