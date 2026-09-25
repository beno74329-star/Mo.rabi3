# Mo.rabi3
هل عبارة عن موقع خاص ب مادة التاريخ ل مستر محمد ربيع 
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>أ. محمد ربيع | دروس التاريخ</title>
<meta name="description" content="دروس تاريخ مجانية مع أ. محمد ربيع">
<link href="https://fonts.googleapis.com/css2?family=Amiri:wght@400;700&family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
<style>
:root{--bg:#f6efe1;--card:#fffaf0;--ink:#2b2118;--muted:#6b5b4a;--accent:#9a5b1f;--onaccent:#fff;--line:#dccfb6}
@media (prefers-color-scheme:dark){:root{--bg:#1a1510;--card:#241d16;--ink:#f1e6d2;--muted:#b7a68d;--accent:#d9a45f;--onaccent:#1a1510;--line:#3a3025}}
*{box-sizing:border-box}
html{scroll-behavior:smooth}
body{margin:0;background:var(--bg);color:var(--ink);font-family:'Tajawal',Tahoma,sans-serif;line-height:1.8}
h1,h2,.serif{font-family:'Amiri','Traditional Arabic',serif}
.wrap{max-width:760px;margin:0 auto;padding:0 20px}
.hero{text-align:center;padding:56px 0 36px}
.badge{display:inline-block;color:var(--accent);border:1px solid var(--accent);border-radius:99px;padding:2px 14px;font-size:14px}
h1{font-size:clamp(38px,9vw,60px);margin:14px 0 4px;line-height:1.3}
.sub{color:var(--muted);font-size:18px;margin:0 0 22px}
.btn{display:inline-block;background:var(--accent);color:var(--onaccent);border-radius:12px;padding:12px 26px;font:700 17px 'Tajawal',sans-serif;text-decoration:none}
section{padding:32px 0;border-top:1px solid var(--line)}
h2{font-size:30px;margin:0 0 14px;color:var(--accent)}
#viewer{display:none;background:var(--card);border:1px solid var(--accent);border-radius:14px;padding:16px;margin-bottom:16px}
#viewer b{font-size:19px}
.player{aspect-ratio:16/9;background:#000;border-radius:10px;margin-top:10px;overflow:hidden;display:grid;place-items:center;color:#fff}
.player iframe{width:100%;height:100%;border:0}
.list{display:grid;gap:10px}
.lesson{display:flex;align-items:center;gap:12px;background:var(--card);border:1px solid var(--line);border-radius:12px;padding:14px 16px;cursor:pointer;text-align:right;font:500 17px 'Tajawal',sans-serif;color:var(--ink);width:100%}
.lesson:active{border-color:var(--accent)}
.n{flex:0 0 34px;height:34px;border-radius:50%;background:var(--accent);color:var(--onaccent);display:grid;place-items:center;font-weight:700}
.tag{font-size:13px;border-radius:99px;padding:1px 10px;border:1px solid var(--line);color:var(--muted);white-space:nowrap}
.t{flex:1}
footer{text-align:center;color:var(--muted);padding:26px 0 40px;border-top:1px solid var(--line)}
</style>
</head>
<body>
<div class="wrap">

<div class="hero">
  <span class="badge">دروس مجانية</span>
  <h1>أ. محمد ربيع</h1>
  <p class="sub">التاريخ حكاية بتتفهم، مش معلومات بتتحفظ</p>
  <a class="btn" href="#lessons">ابدأ الدروس</a>
</div>

<section id="lessons">
  <h2>الدروس</h2>
  <div id="viewer">
    <b id="vt"></b>
    <div class="player" id="vp"></div>
  </div>
  <div class="list" id="list"></div>
</section>

<footer>
  <div class="serif" style="font-size:22px;color:var(--accent)">أ. محمد ربيع</div>
  <div>مدرس التاريخ</div>
</footer>
</div>

<script>
/* ===== عدّل الدروس من هنا =====
   title: اسم الدرس
   video: رابط الفيديو من يوتيوب (سيبه فاضي "" لو لسه مرفعتوش) */
const LESSONS = [
  { title: "مقدمة: ليه بندرس التاريخ؟", video: "" },
  { title: "الحضارة المصرية القديمة",   video: "" },
  { title: "العصر اليوناني والروماني",   video: "" },
  { title: "الفتح الإسلامي",             video: "" },
  { title: "العصور الوسطى",              video: "" },
  { title: "التاريخ الحديث",             video: "" }
];
/* ============================== */

function ytId(u){
  const m = u.match(/(?:youtu\.be\/|v=|embed\/|shorts\/)([\w-]{11})/);
  return m ? m[1] : null;
}
const list = document.getElementById('list'),
      viewer = document.getElementById('viewer'),
      vt = document.getElementById('vt'),
      vp = document.getElementById('vp');

LESSONS.forEach((l, i) => {
  const id = l.video ? ytId(l.video) : null;
  const b = document.createElement('button');
  b.className = 'lesson';
  b.innerHTML = '<span class="n">' + (i + 1) + '</span><span class="t"></span><span class="tag">' + (id ? '▶ شاهد' : 'قريبًا') + '</span>';
  b.querySelector('.t').textContent = l.title;
  b.onclick = () => {
    viewer.style.display = 'block';
    vt.textContent = l.title;
    vp.innerHTML = '';
    if (id) {
      const f = document.createElement('iframe');
      f.src = 'https://www.youtube-nocookie.com/embed/' + id;
      f.allow = 'accelerometer; autoplay; encrypted-media; picture-in-picture';
      f.allowFullscreen = true;
      vp.appendChild(f);
    } else {
      vp.textContent = 'الفيديو هيتضاف قريبًا';
    }
    viewer.scrollIntoView({ behavior: 'smooth', block: 'center' });
  };
  list.appendChild(b);
});
</script>
</body>
</html>

https://github.com/user-attachments/assets/971b97e6-e4a1-4454-8458-370fc4ff2a86

