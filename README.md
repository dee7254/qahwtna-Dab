<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1.0" />
  <title>قَهوتنا (Qahwatna)</title>
  <link rel="stylesheet" href="style.css" />
</head>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');

:root {
  --bg-dark: #1a120b;
  --bg-dark-day: #3a2a17;
  --bg-card: rgba(40, 28, 18, 0.6);
  --text-main: #f5e9d3;
  --text-dim: #bfae96;
  --accent: #d9b060;
  --accent-soft: rgba(217, 176, 96, 0.15);
  --radius: 20px;
  --blur-card: blur(10px);
  --border-card: rgba(255,255,255,0.08);
}

/* RESET */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "Cairo", system-ui, sans-serif;
}

body {
  background-color: var(--bg-dark);
  color: var(--text-main);
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
  transition: background-color .25s linear;
}

/* وضع النهار */
body.day-mode {
  background-color: var(--bg-dark-day);
}
body.day-mode .main-header {
  background: rgba(58, 42, 23, 0.6);
}

/* إضافة وصف مزاج */
body.day-mode .tagline::after {
  content: " • مزاج صباحي 🌤";
  color: var(--accent);
  font-weight: 600;
  margin-right: .3rem;
  font-size: .7rem;
}
body:not(.day-mode) .tagline::after {
  content: " • مزاج مسائي 🌙";
  color: var(--accent);
  font-weight: 600;
  margin-right: .3rem;
  font-size: .7rem;
}

/* خلفية النجوم */
#stars-bg {
  position: fixed;
  inset: 0;
  z-index: 0;
}

/* طبقة الوهج اللي تتبع الماوس */
.page-glow-layer {
  pointer-events: none;
  position: fixed;
  inset: 0;
  z-index: 5;
  mix-blend-mode: screen;
}
.page-glow-spot {
  position: absolute;
  width: 180px;
  height: 180px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(217,176,96,0.25) 0%, rgba(0,0,0,0) 70%);
  filter: blur(40px);
  opacity: .25;
  transition: transform .05s linear;
}

/* الهيدر */
.main-header {
  position: sticky;
  top: 0;
  z-index: 10;
  background: rgba(20, 14, 9, 0.6);
  backdrop-filter: blur(8px);
  border-bottom: 1px solid rgba(255,255,255,0.07);
  display: flex;
  flex-wrap: wrap;
  gap: .8rem 1rem;
  justify-content: space-between;
  align-items: flex-start;
  padding: .8rem 1.2rem;
}

.logo-area {
  display: flex;
  align-items: flex-start;
  gap: .6rem;
  min-width: 160px;
}

.dallah-emoji {
  font-size: 1.8rem;
  filter: drop-shadow(0 0 4px rgba(255,255,255,0.3));
}

.brand {
  display: grid;
  gap: .2rem;
  line-height: 1.2;
}

/* العنوان مع اللمعة */
.brand-title {
  position: relative;
  overflow: hidden;
  font-size: 1rem;
  font-weight: 700;
  color: var(--accent);
  line-height: 1.1;
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: .4rem;
}
.brand-main {
  font-weight: 700;
  color: var(--accent);
}
.brand-alt {
  font-weight: 600;
  color: var(--text-main);
  font-size: .8rem;
  opacity: .8;
}

/* لمعة العنوان */
.brand-title::after {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;
  width: 50%;
  height: 100%;
  background: linear-gradient(
    120deg,
    transparent,
    rgba(255,255,255,0.7),
    transparent
  );
  animation: shine 4s linear infinite;
}
@keyframes shine {
  0% { left: -100%; }
  50% { left: 150%; }
  100% { left: 150%; }
}

.tagline {
  font-size: .7rem;
  font-weight: 400;
  color: var(--text-dim);
  line-height: 1.2;
  min-height: 1.4em;
}

.main-nav {
  display: flex;
  flex-wrap: wrap;
  gap: .8rem;
  font-size: .8rem;
  align-items: flex-start;
  min-width: 180px;
}
.main-nav a {
  color: var(--text-main);
  text-decoration: none;
  position: relative;
}
.main-nav a::after {
  content: "";
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0%;
  height: 2px;
  background: var(--accent);
  transition: width .2s;
}
.main-nav a:hover::after {
  width: 100%;
}

/* أزرار الهيدر (الوضع واللغة) */
.header-buttons {
  display: flex;
  gap: .5rem;
  margin-inline-start: auto;
}

.mood-toggle-btn,
.lang-toggle-btn {
  background: rgba(0,0,0,.4);
  border: 1px solid var(--accent);
  color: var(--accent);
  font-size: .8rem;
  line-height: 1;
  padding: .5rem .7rem;
  border-radius: 12px;
  cursor: pointer;
  box-shadow: 0 20px 40px rgba(0,0,0,.8);
  transition: all .15s;
  min-width: 44px;
  text-align: center;
}
.mood-toggle-btn:hover,
.lang-toggle-btn:hover {
  background: rgba(217,176,96,0.08);
  box-shadow: 0 15px 30px rgba(217,176,96,0.4);
}

/* hero */
.hero {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1fr;
  padding: 3rem 1.2rem 4rem;
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.hero-content h2 {
  font-size: clamp(1.4rem, 1.2vw + 1rem, 2rem);
  color: var(--accent);
  margin-bottom: .8rem;
  font-weight: 700;
}
.hero-content p {
  color: var(--text-dim);
  font-size: 1rem;
  line-height: 1.8;
  max-width: 40ch;
}

.hero-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: .6rem;
  margin-top: 1.2rem;
}

.primary-btn,
.secondary-btn {
  cursor: pointer;
  border-radius: var(--radius);
  border: 1px solid var(--accent);
  background: var(--accent-soft);
  color: var(--text-main);
  font-size: .8rem;
  padding: .6rem .9rem;
  font-weight: 600;
  transition: all .15s;
}

.primary-btn:hover {
  box-shadow: 0 8px 24px rgba(217,176,96,0.4);
  transform: translateY(-2px) scale(1.02);
}
.secondary-btn {
  border-color: rgba(255,255,255,.2);
  background: rgba(255,255,255,0.05);
  color: var(--text-dim);
}
.secondary-btn:hover {
  background: rgba(255,255,255,0.1);
}

/* الفنجال */
.hero-art {
  display: flex;
  justify-content: center;
  align-items: flex-start;
}

.cup-wrapper {
  position: relative;
  width: 180px;
  max-width: 60vw;
  text-align: center;
  animation: floaty 3s ease-in-out infinite;
}
@keyframes floaty {
  0% { transform: translateY(0px); }
  50% { transform: translateY(-6px); }
  100% { transform: translateY(0px); }
}

.coffee-cup {
  width: 100%;
  filter: drop-shadow(0 20px 25px rgba(0,0,0,.8));
  transform-origin: center;
  transition: transform .15s;
}

.cup-wrapper.shake .coffee-cup {
  animation: shakeCup .3s linear;
}
@keyframes shakeCup {
  0%,100% { transform: rotate(0deg) translateX(0); }
  20% { transform: rotate(-4deg) translateX(-2px); }
  40% { transform: rotate(4deg) translateX(2px); }
  60% { transform: rotate(-3deg) translateX(-1px); }
  80% { transform: rotate(3deg) translateX(1px); }
}

#steam-canvas {
  position: absolute;
  left: 50%;
  top: -20px;
  transform: translateX(-50%);
  width: 200px;
  height: 200px;
  pointer-events: none;
}

.cup-hint {
  color: var(--text-dim);
  font-size: .7rem;
  margin-top: .4rem;
  user-select: none;
}

/* sections structure */
.section {
  position: relative;
  z-index: 1;
  padding: 3rem 1.2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.content-card {
  background: var(--bg-card);
  border: 1px solid var(--border-card);
  border-radius: var(--radius);
  padding: 1.5rem;
  box-shadow: 0 30px 100px rgba(0,0,0,.8);
  backdrop-filter: var(--blur-card);
}

.content-card h3 {
  color: var(--accent);
  font-size: 1.2rem;
  margin-bottom: 1rem;
  font-weight: 700;
}

/* الأرقام (عن التراث/المكونات/الكرم) */
.facts-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(100px,1fr));
  gap: 1rem;
  text-align: center;
  margin-top: 2rem;
}
.fact-box {
  background: rgba(0,0,0,.3);
  border-radius: var(--radius);
  padding: .8rem .5rem;
  border: 1px solid rgba(255,255,255,0.05);
}
.fact-number {
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--accent);
  line-height: 1;
  text-shadow: 0 10px 30px rgba(217,176,96,.4);
}
.fact-label {
  font-size: .7rem;
  color: var(--text-dim);
}

/* المكونات */
.ingredients-list {
  display: grid;
  gap: 1rem;
}
.ing-item {
  display: flex;
  gap: .8rem;
  align-items: flex-start;
  background: rgba(0,0,0,.3);
  padding: .8rem 1rem;
  border-radius: var(--radius);
  border: 1px solid rgba(255,255,255,0.05);
  transition: box-shadow .2s;
}
.ing-icon {
  font-size: 1.4rem;
  line-height: 1;
}
.ing-text h4 {
  font-size: 1rem;
  line-height: 1.3;
  color: var(--text-main);
  font-weight: 600;
  margin-bottom: .3rem;
}
.ing-text p {
  color: var(--text-dim);
  font-size: .8rem;
  line-height: 1.6;
}

/* نبضة "الهيل" (JS يضيف/يشيل hail-pulse) */
@keyframes pulse-hail {
  0%   { box-shadow: 0 0 20px rgba(217,176,96,0); }
  50%  { box-shadow: 0 0 25px rgba(217,176,96,.5); }
  100% { box-shadow: 0 0 20px rgba(217,176,96,0); }
}
.hail-pulse {
  animation: pulse-hail 1s ease-in-out;
  border-color: rgba(217,176,96,0.6) !important;
}

/* عداد الفناجيل */
.counter-hint {
  font-size: .8rem;
  color: var(--text-dim);
  margin-bottom: .8rem;
  text-align: center;
}
.counter-box {
  text-align: center;
}
#count-display {
  font-size: 3rem;
  font-weight: 700;
  color: var(--accent);
  line-height: 1;
  margin-bottom: 1rem;
  text-shadow: 0 10px 30px rgba(217,176,96,.4);
  transition: .2s;
}
.counter-buttons {
  display: flex;
  gap: .6rem;
  justify-content: center;
  flex-wrap: wrap;
}
.small {
  font-size: .7rem;
  padding: .45rem .7rem;
}
.counter-status {
  font-size: .8rem;
  color: var(--text-dim);
  margin-top: 1rem;
  text-align: center;
  min-height: 1.2em;
}
/* لو تشرب كثير 😭 */
.counter-box.too-much #count-display {
  text-shadow: 0 0 15px rgba(255,0,0,.7), 0 0 40px rgba(255,0,0,.4);
  color: #ff6868;
  transition: .2s;
}

/* المناطق بدون سلايدر */
.regions-grid {
  display: grid;
  gap: 1.5rem;
  margin-top: 1.5rem;
}

@media(min-width:700px){
  .regions-grid {
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  }
}

/* نفس تصميم الكروت الذهبية للمناطق */
.region-card {
  background: rgba(20,14,9,.6);
  border: 1px solid rgba(255,255,255,0.07);
  box-shadow: 0 25px 70px rgba(0,0,0,.9);
  border-radius: var(--radius);
  padding: 1rem 1.2rem 1.5rem;
  display: grid;
  gap: .8rem;
  position: relative;

  /* حركة الظهور كبخار */
  opacity: 0;
  animation: float-up 1s ease forwards;
}
.region-card:nth-child(1){animation-delay:0.1s;}
.region-card:nth-child(2){animation-delay:0.3s;}
.region-card:nth-child(3){animation-delay:0.5s;}
.region-card:nth-child(4){animation-delay:0.7s;}
.region-card:nth-child(5){animation-delay:0.9s;}

@keyframes float-up {
  from {
    opacity: 0;
    transform: translateY(40px) scale(0.97);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

/* الهالة الذهبية فوق كل كرت */
.region-card::before {
  content: "";
  position: absolute;
  top: -30px;
  left: 50%;
  transform: translateX(-50%);
  width: 160px;
  height: 160px;
  background: radial-gradient(circle at 50% 30%, rgba(217,176,96,0.25) 0%, rgba(0,0,0,0) 70%);
  filter: blur(30px);
  z-index: -1;
  pointer-events: none;
}

.card-header {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: .6rem .8rem;
}
.card-title {
  color: var(--accent);
  font-weight: 700;
  font-size: 1rem;
}
.card-badge {
  background: var(--accent-soft);
  border: 1px solid rgba(217,176,96,0.4);
  color: var(--accent);
  font-size: .7rem;
  font-weight: 600;
  line-height: 1.4;
  padding: .3rem .5rem;
  border-radius: 10px;
}

.card-desc {
  color: var(--text-dim);
  font-size: .8rem;
  line-height: 1.7;
  max-width: 70ch;
}

.card-points {
  list-style: none;
  display: grid;
  gap: .4rem;
  background: rgba(0,0,0,.2);
  border-radius: var(--radius);
  border: 1px solid rgba(255,255,255,0.05);
  padding: .8rem 1rem;
  font-size: .8rem;
  line-height: 1.5;
  color: var(--text-main);
}
.card-points li span:first-child {
  color: var(--accent);
  font-weight: 600;
  margin-left: .3rem;
}

/* لما نمر على الكرت نخليه يبرق لحظة (JS يضيف .flash) */
.region-card.flash {
  box-shadow:
    0 0 30px rgba(217,176,96,.6),
    0 0 80px rgba(217,176,96,.3),
    0 25px 70px rgba(0,0,0,.9);
  transition: box-shadow .2s;
}

/* الفوتر */
.main-footer {
  position: relative;
  z-index: 1;
  padding: 2rem 1.2rem 4rem;
  text-align: center;
  font-size: .7rem;
  color: var(--text-dim);
}
.footer-brand {
  color: var(--accent);
  font-weight: 700;
  font-size: .9rem;
}
.footer-tagline {
  font-size: .7rem;
  color: var(--text-dim);
  margin-top: .2rem;
}
.year-line {
  color: var(--accent);
  margin-top: .6rem;
  font-weight: 600;
  font-size: .7rem;
}

/* reveal-on-scroll (hero/about/etc.) */
.reveal {
  opacity: 0;
  transform: translateY(30px) scale(.98);
  transition: all .6s cubic-bezier(.16,1,.3,1);
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0) scale(1);
}

/* responsive tweaks */
@media(min-width:768px){
  .main-header {
    align-items: flex-start;
  }

  .hero {
    grid-template-columns: 1fr 1fr;
    align-items: center;
  }

  .hero-content p {
    font-size: 1.05rem;
  }

  .content-card {
    padding: 2rem;
  }
}

</style>

<body>
  <!-- خلفية النجوم -->
  <canvas id="stars-bg"></canvas>

  <!-- طبقة الإضاءة اللي تتبع الماوس -->
  <div class="page-glow-layer">
    <div class="page-glow-spot" id="page-glow"></div>
  </div>

  <!-- الهيدر -->
  <header class="main-header">
    <div class="logo-area">
      <div class="dallah-emoji">☕</div>
      <div class="brand">
        <h1 class="brand-title">
          <span class="brand-main" data-i18n="brand_main">قَهوتنا</span>
          <span class="brand-alt" data-i18n="brand_alt">(Qahwatna)</span>
        </h1>
        <p class="tagline" data-i18n="brand_tagline">نكهات من كل منطقة سعودية</p>
      </div>
    </div>

    <nav class="main-nav">
      <a href="#about" data-i18n="nav_about">وش يعني قَهوتنا؟</a>
      <a href="#ingredients" data-i18n="nav_ing">مكونات القهوة</a>
      <a href="#regions" data-i18n="nav_regions">أذواق المناطق</a>
      <a href="#counter" data-i18n="nav_counter">عداد الفناجيل</a>
    </nav>

    <div class="header-buttons">
      <button class="mood-toggle-btn" id="mood-toggle">🌙</button>
      <button class="lang-toggle-btn" id="lang-toggle">EN</button>
    </div>
  </header>

  <!-- القسم الرئيسي -->
  <section class="hero" id="hero">
    <div class="hero-content reveal">
      <h2 data-i18n="hero_title">
        القهوة مَو بس مشروب.. القهوة موقف
      </h2>
      <p data-i18n="hero_desc">
        القهوة السعودية عادة اجتماعية. ريحة الهيل والزعفران تعلن الضيافة حتى
        قبل الكلام. من أول فنجال تسمعين: "تشرّفنا".
      </p>

      <div class="hero-buttons">
        <button id="pour-btn" class="primary-btn" data-i18n="btn_pour">🔊 اسمع صوت صب القهوة</button>
        <button id="stop-btn" class="secondary-btn" data-i18n="btn_stop">🔇 أوقف الصوت</button>
      </div>

<audio id="coffee-audio" src="كيف تصب القهوة من الدلة.mp3"></audio>
    </div>

    <div class="hero-art reveal">
      <div class="cup-wrapper" id="cup">
        <img
  class="coffee-cup"
  src="تنزيل-removebg-preview.png"
  alt="فنجال قهوة عربية"

        />
        <canvas id="steam-canvas"></canvas>
        <div class="cup-hint" data-i18n="cup_hint">مرري الماوس هنا 👆</div>
      </div>
    </div>
  </section>

  <!-- ما هي القهوة السعودية -->
  <section class="section about-section" id="about">
    <div class="content-card reveal">
      <h3 data-i18n="about_title">وش يعني "قَهوتنا"؟</h3>
      <p data-i18n="about_text">
        القهوة السعودية (اللي كثير يسمونها القهوة العربية) تنحّمص خفيف عشان
        يطلع لونها ذهبي مو أسود، وتُنكّه بالهيل، وأحياناً زعفران أو قرنفل
        أو مستكة حسب المنطقة. تنصب من الدلة في فنجال صغير بدون سكر، ومعها تمر.
        معناها الحقيقي: كرم، احترام، ترحيب.
      </p>

      <div class="facts-grid">
        <div class="fact-box">
          <span class="fact-number" data-target="100">0</span>
          <span class="fact-label" data-i18n="fact1_label">+ سنة من تراث الضيافة</span>
        </div>

        <div class="fact-box">
          <span class="fact-number" data-target="3">0</span>
          <span class="fact-label" data-i18n="fact2_label">مكونات أساسية</span>
        </div>

        <div class="fact-box">
          <span class="fact-number" data-target="1">0</span>
          <span class="fact-label" data-i18n="fact3_label">رمز للكرم</span>
        </div>
      </div>
    </div>
  </section>

  <!-- المكونات -->
  <section class="section ingredients-section" id="ingredients">
    <div class="content-card reveal">
      <h3 data-i18n="ingredients_title">مكوّنات القهوة السعودية</h3>

      <div class="ingredients-list">
        <div class="ing-item">
          <div class="ing-icon">🥄</div>
          <div class="ing-text">
            <h4 data-i18n="ing1_title">حب قهوة محمص فاتح</h4>
            <p data-i18n="ing1_desc">
              مو مثل البن التركي أو الفرنسي الغامق. هنا البن لونه ذهبي تقريباً.
              الطعم أنعم، مو مُر بزيادة.
            </p>
          </div>
        </div>

        <div class="ing-item" id="card-hail">
          <div class="ing-icon">🌿</div>
          <div class="ing-text">
            <h4 data-i18n="ing2_title">هيل</h4>
            <p data-i18n="ing2_desc">
              الهيل هو الهوية. من أول ريحة تعرفين في أحد صب قهوة، حتى لو ما شفتي
              الدلة.
            </p>
          </div>
        </div>

        <div class="ing-item">
          <div class="ing-icon">✨</div>
          <div class="ing-text">
            <h4 data-i18n="ing3_title">زعفران (أحيانًا)</h4>
            <p data-i18n="ing3_desc">
              يعطي لون ذهبي خفيف وإحساس فخامة. غالبًا يطلع في القهوة اللي
              للضيوف المهمين.
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- عداد الفناجيل -->
  <section class="section counter-section" id="counter">
    <div class="content-card reveal">
      <h3 data-i18n="counter_title">كم فنجال شربت اليوم؟</h3>

      <p class="counter-hint" data-i18n="counter_hint">
        الصدق؟ إحنا ما نحكم 👀
      </p>

      <div class="counter-box">
        <div id="count-display">0</div>

        <div class="counter-buttons">
          <button class="primary-btn small" id="inc-btn" data-i18n="counter_inc">+ زيادة فنجال</button>
          <button class="secondary-btn small" id="dec-btn" data-i18n="counter_dec">- أقلل</button>
          <button class="secondary-btn small" id="reset-btn" data-i18n="counter_reset">↺ تصفير</button>
        </div>

        <p class="counter-status" id="counter-status">
          ممتاز. جرعة هيل طبيعية 👌
        </p>
      </div>
    </div>
  </section>

  <!-- أذواق المناطق -->
  <section class="section regions-section" id="regions">
    <div class="content-card reveal">
      <h3 data-i18n="regions_title">نكهات القهوة في مناطق المملكة</h3>

      <div class="regions-grid">
        <!-- نجد -->
        <div class="region-card static-region">
          <div class="card-header">
            <div class="card-title" data-i18n="r1_name">نجد (المنطقة الوسطى)</div>
            <div class="card-badge" data-i18n="r1_badge">لون فاتح • هيل • زعفران</div>
          </div>
          <p class="card-desc" data-i18n="r1_desc">
            قهوة نجد غالبًا هي الصورة "الكلاسيك" عند الناس عن القهوة السعودية.
            البن خفيف التحميص (لون ذهبي مو بني غامق)، الهيل كثير وواضح، وأحياناً
            يضاف زعفران عشان اللون والطعم. تتقدم مع تمر سكري، وبدون سكر بالقهوة.
          </p>
          <ul class="card-points">
            <li><span data-i18n="r_label_beans">البن:</span> <span data-i18n="r1_beans">تحميص فاتح ذهبي</span></li>
            <li><span data-i18n="r_label_flavor">النكهات:</span> <span data-i18n="r1_flavor">هيل قوي، زعفران أحياناً</span></li>
            <li><span data-i18n="r_label_vibe">الجو:</span> <span data-i18n="r1_vibe">قهوة ضيف محترم</span></li>
          </ul>
        </div>

        <!-- الحجاز -->
        <div class="region-card static-region">
          <div class="card-header">
            <div class="card-title" data-i18n="r2_name">الحجاز (مكة والمدينة)</div>
            <div class="card-badge" data-i18n="r2_badge">هيل • قرنفل • قرفة</div>
          </div>
          <p class="card-desc" data-i18n="r2_desc">
            الحجاز يحبون البهارات الدافئة. القهوة أغمق شوي من النجدية،
            وفيها قرنفل وقرفة وأحياناً لمسة زنجبيل. تحسّينها قهوة لمّة
            عائلة ومعمول.
          </p>
          <ul class="card-points">
            <li><span data-i18n="r_label_beans">البن:</span> <span data-i18n="r2_beans">متوسط إلى أغمق</span></li>
            <li><span data-i18n="r_label_flavor">النكهات:</span> <span data-i18n="r2_flavor">قرنفل، قرفة، أحياناً زنجبيل</span></li>
            <li><span data-i18n="r_label_vibe">الجو:</span> <span data-i18n="r2_vibe">لمّة بيت</span></li>
          </ul>
        </div>

        <!-- الجنوب -->
        <div class="region-card static-region">
          <div class="card-header">
            <div class="card-title" data-i18n="r3_name">الجنوب (عسير • جازان • نجران)</div>
            <div class="card-badge" data-i18n="r3_badge">بن ثقيل • قشر بن</div>
          </div>
          <p class="card-desc" data-i18n="r3_desc">
            القهوة الجنوبية قوية وصريحة. تشبه القهوة اليمنية، أحياناً تنعمل مع
            قشر البن (قشر الحبة)، وتركّز على طعم البن نفسه أكثر من البهارات.
            أقل دلع، أكثر شخصية.
          </p>
          <ul class="card-points">
            <li><span data-i18n="r_label_beans">البن:</span> <span data-i18n="r3_beans">غامق وثقيل</span></li>
            <li><span data-i18n="r_label_flavor">النكهات:</span> <span data-i18n="r3_flavor">قشر البن، بهارات خفيفة أو بدون</span></li>
            <li><span data-i18n="r_label_vibe">الجو:</span> <span data-i18n="r3_vibe">جبلية وأصلية</span></li>
          </ul>
        </div>

        <!-- الشرقية -->
        <div class="region-card static-region">
          <div class="card-header">
            <div class="card-title" data-i18n="r4_name">الشرقية</div>
            <div class="card-badge" data-i18n="r4_badge">هيل • زعفران • لمسة ورد</div>
          </div>
          <p class="card-desc" data-i18n="r4_desc">
            الشرقية قريبة من النجدية في اللون الفاتح، لكن أحياناً فيها ورد،
            مستكة، أو زعفران واضح. الإحساس نظيف وناعم وعطري.
          </p>
          <ul class="card-points">
            <li><span data-i18n="r_label_beans">البن:</span> <span data-i18n="r4_beans">فاتح ذهبي</span></li>
            <li><span data-i18n="r_label_flavor">النكهات:</span> <span data-i18n="r4_flavor">هيل، زعفران، ورد/مستكة</span></li>
            <li><span data-i18n="r_label_vibe">الجو:</span> <span data-i18n="r4_vibe">VIP ✨</span></li>
          </ul>
        </div>

        <!-- الشمال -->
        <div class="region-card static-region">
          <div class="card-header">
            <div class="card-title" data-i18n="r5_name">الشمال (حائل • الجوف)</div>
            <div class="card-badge" data-i18n="r5_badge">هيل كثير • زعفران • قرنفل</div>
          </div>
          <p class="card-desc" data-i18n="r5_desc">
            أهل الشمال معروفين بالكرم الرسمي الفخم. القهوة تكون ثقيلة بالهيل،
            والزعفران والقرنفل واضحين. وعادة الإهتمام بالتقديم عالي:
            دلال مزخرفة وفناجيل مرتبة.
          </p>
          <ul class="card-points">
            <li><span data-i18n="r_label_beans">البن:</span> <span data-i18n="r5_beans">فاتح إلى متوسط</span></li>
            <li><span data-i18n="r_label_flavor">النكهات:</span> <span data-i18n="r5_flavor">هيل ثقيل، زعفران، قرنفل</span></li>
            <li><span data-i18n="r_label_vibe">الجو:</span> <span data-i18n="r5_vibe">ضيف عزيز لازم يكرم</span></li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <!-- الفوتر -->
  <footer class="main-footer">
    <p class="footer-brand" data-i18n="footer_brand">قَهوتنا (Qahwatna)</p>
    <p class="footer-tagline" data-i18n="footer_tagline">نكهات من كل منطقة سعودية</p>
    <p class="year-line">© <span id="year"></span> <span data-i18n="footer_rights">جميع الحقوق محفوظة</span></p>
  </footer>

  <script src="script.js"></script>
</body>

<script>
// -----------------------------
// الترجمة (عربي / إنجليزي فاخر)
// -----------------------------
const translations = {
  ar: {
    brand_main: "قَهوتنا",
    brand_alt: "(Qahwatna)",
    brand_tagline: "نكهات من كل منطقة سعودية",

    nav_about: "وش يعني قَهوتنا؟",
    nav_ing: "مكونات القهوة",
    nav_regions: "أذواق المناطق",
    nav_counter: "عداد الفناجيل",

    hero_title: "القهوة مَو بس مشروب.. القهوة موقف",
    hero_desc:
      "القهوة السعودية عادة اجتماعية. ريحة الهيل والزعفران تعلن الضيافة حتى قبل الكلام. من أول فنجال تسمعين: \"تشرّفنا\".",
    btn_pour: "🔊 اسمع صوت صب القهوة",
    btn_stop: "🔇 أوقف الصوت",
    cup_hint: "مرري الماوس هنا 👆",

    about_title: "وش يعني \"قَهوتنا\"؟",
    about_text:
      "القهوة السعودية (اللي كثير يسمونها القهوة العربية) تنحّمص خفيف عشان يطلع لونها ذهبي مو أسود، وتُنكّه بالهيل، وأحياناً زعفران أو قرنفل أو مستكة حسب المنطقة. تنصب من الدلة في فنجال صغير بدون سكر، ومعها تمر. معناها الحقيقي: كرم، احترام، ترحيب.",

    fact1_label: "+ سنة من تراث الضيافة",
    fact2_label: "مكونات أساسية",
    fact3_label: "رمز للكرم",

    ingredients_title: "مكوّنات القهوة السعودية",
    ing1_title: "حب قهوة محمص فاتح",
    ing1_desc:
      "مو مثل البن التركي أو الفرنسي الغامق. هنا البن لونه ذهبي تقريباً. الطعم أنعم، مو مُر بزيادة.",
    ing2_title: "هيل",
    ing2_desc:
      "الهيل هو الهوية. من أول ريحة تعرفين في أحد صب قهوة، حتى لو ما شفتي الدلة.",
    ing3_title: "زعفران (أحيانًا)",
    ing3_desc:
      "يعطي لون ذهبي خفيف وإحساس فخامة. غالبًا يطلع في القهوة اللي للضيوف المهمين.",

    counter_title: "كم فنجال شربت اليوم؟",
    counter_hint: "الصدق؟ إحنا ما نحكم 👀",
    counter_inc: "+ زيادة فنجال",
    counter_dec: "- أقلل",
    counter_reset: "↺ تصفير",

    regions_title: "نكهات القهوة في مناطق المملكة",

    r_label_beans: "البن:",
    r_label_flavor: "النكهات:",
    r_label_vibe: "الجو:",

    r1_name: "نجد (المنطقة الوسطى)",
    r1_badge: "لون فاتح • هيل • زعفران",
    r1_desc:
      "قهوة نجد غالبًا هي الصورة \"الكلاسيك\" عند الناس عن القهوة السعودية. البن خفيف التحميص (لون ذهبي مو بني غامق)، الهيل كثير وواضح، وأحياناً يضاف زعفران عشان اللون والطعم. تتقدم مع تمر سكري، وبدون سكر بالقهوة.",
    r1_beans: "تحميص فاتح ذهبي",
    r1_flavor: "هيل قوي، زعفران أحياناً",
    r1_vibe: "قهوة ضيف محترم",

    r2_name: "الحجاز (مكة والمدينة)",
    r2_badge: "هيل • قرنفل • قرفة",
    r2_desc:
      "الحجاز يحبون البهارات الدافئة. القهوة أغمق شوي من النجدية، وفيها قرنفل وقرفة وأحياناً لمسة زنجبيل. تحسّينها قهوة لمّة عائلة ومعمول.",
    r2_beans: "متوسط إلى أغمق",
    r2_flavor: "قرنفل، قرفة، أحياناً زنجبيل",
    r2_vibe: "لمّة بيت",

    r3_name: "الجنوب (عسير • جازان • نجران)",
    r3_badge: "بن ثقيل • قشر بن",
    r3_desc:
      "القهوة الجنوبية قوية وصريحة. تشبه القهوة اليمنية، أحياناً تنعمل مع قشر البن (قشر الحبة)، وتركّز على طعم البن نفسه أكثر من البهارات. أقل دلع، أكثر شخصية.",
    r3_beans: "غامق وثقيل",
    r3_flavor: "قشر البن، بهارات خفيفة أو بدون",
    r3_vibe: "جبلية وأصلية",

    r4_name: "الشرقية",
    r4_badge: "هيل • زعفران • لمسة ورد",
    r4_desc:
      "الشرقية قريبة من النجدية في اللون الفاتح، لكن أحياناً فيها ورد، مستكة، أو زعفران واضح. الإحساس نظيف وناعم وعطري.",
    r4_beans: "فاتح ذهبي",
    r4_flavor: "هيل، زعفران، ورد/مستكة",
    r4_vibe: "VIP ✨",

    r5_name: "الشمال (حائل • الجوف)",
    r5_badge: "هيل كثير • زعفران • قرنفل",
    r5_desc:
      "أهل الشمال معروفين بالكرم الرسمي الفخم. القهوة تكون ثقيلة بالهيل، والزعفران والقرنفل واضحين. وعادة الإهتمام بالتقديم عالي: دلال مزخرفة وفناجيل مرتبة.",
    r5_beans: "فاتح إلى متوسط",
    r5_flavor: "هيل ثقيل، زعفران، قرنفل",
    r5_vibe: "ضيف عزيز لازم يكرم",

    footer_brand: "قَهوتنا (Qahwatna)",
    footer_tagline: "نكهات من كل منطقة سعودية",
    footer_rights: "جميع الحقوق محفوظة",
  },

  en: {
    brand_main: "Qahwatna",
    brand_alt: "(Our Coffee)",
    brand_tagline: "Flavors from every Saudi region",

    nav_about: "What is Qahwatna?",
    nav_ing: "Core Ingredients",
    nav_regions: "Regional Styles",
    nav_counter: "Cup Counter",

    hero_title: "Saudi coffee isn't just a drink — it's a welcome.",
    hero_desc:
      "In Saudi tradition, coffee is hospitality made liquid. Cardamom and saffron announce that you're honored here before a single word is spoken.",
    btn_pour: "🔊 Pouring sound",
    btn_stop: "🔇 Stop audio",
    cup_hint: "Hover here 👆",

    about_title: "What is 'Qahwatna'?",
    about_text:
      "Saudi coffee is lightly roasted to a warm golden color, not dark. It's infused with cardamom, sometimes saffron, clove, or mastic depending on the region. It's poured from a brass dallah into a tiny cup with no sugar — always served beside dates. It's not just caffeine. It's respect.",

    fact1_label: "+ years of shared hospitality",
    fact2_label: "core ingredients",
    fact3_label: "a cultural symbol",

    ingredients_title: "What goes into Saudi coffee?",
    ing1_title: "Lightly roasted coffee beans",
    ing1_desc:
      "Not like dark Turkish or French roasts. The beans are almost golden. The taste is softer, less bitter, more perfume than punch.",
    ing2_title: "Cardamom",
    ing2_desc:
      "Cardamom is identity. You smell it and you already know: someone is pouring coffee – someone is welcoming.",
    ing3_title: "Saffron (sometimes)",
    ing3_desc:
      "A touch of saffron gives this quiet golden hue and a sense of ceremony. It's often reserved for honored guests.",

    counter_title: "How many cups did you have today?",
    counter_hint: "No judgment here 👀",
    counter_inc: "+ Another cup",
    counter_dec: "- Little less",
    counter_reset: "↺ Reset",

    regions_title: "Saudi coffee across the regions",

    r_label_beans: "Roast:",
    r_label_flavor: "Notes:",
    r_label_vibe: "Vibe:",

    r1_name: "Najd (Central Region)",
    r1_badge: "Light roast • Cardamom • Saffron",
    r1_desc:
      "Najdi-style coffee is what many people imagine when they say 'Saudi coffee': pale-golden roast, heavy cardamom, sometimes saffron for color and warmth. Always served with sweet dates instead of sugar.",
    r1_beans: "Very light, golden roast",
    r1_flavor: "Bold cardamom, touch of saffron",
    r1_vibe: "Formal hospitality",

    r2_name: "Hijaz (Makkah & Madinah)",
    r2_badge: "Cardamom • Clove • Cinnamon",
    r2_desc:
      "Hijazi coffee leans warmer and deeper. You'll taste clove, cinnamon, sometimes a whisper of ginger. It's comfort coffee — the kind you drink with family and maamoul cookies.",
    r2_beans: "Medium to darker roast",
    r2_flavor: "Clove, cinnamon, hint of ginger",
    r2_vibe: "Family gathering energy",

    r3_name: "The South (Asir • Jazan • Najran)",
    r3_badge: "Heavy roast • Coffee husk",
    r3_desc:
      "Southern coffee is strong, honest, and very close to Yemeni traditions. Sometimes it's brewed with the coffee husk itself. Less spice, more bean. No flirting. Just depth.",
    r3_beans: "Dark, intense roast",
    r3_flavor: "Coffee husk, minimal spice",
    r3_vibe: "Mountain boldness",

    r4_name: "The Eastern Province",
    r4_badge: "Cardamom • Saffron • Rose",
    r4_desc:
      "Eastern Saudi coffee often mirrors Najd's pale roast but adds a soft floral elegance — rose, mastic, or clear saffron. It's refined, perfumed, intentional.",
    r4_beans: "Light golden roast",
    r4_flavor: "Cardamom, saffron, hint of rose or mastic",
    r4_vibe: "VIP service ✨",

    r5_name: "The North (Ha'il • Al-Jawf)",
    r5_badge: "Heavy cardamom • Saffron • Clove",
    r5_desc:
      "Northern coffee is ceremonial. Strong on cardamom, with saffron and clove showing up proudly. The serving itself is part of the honor: ornate dallahs, perfect little cups.",
    r5_beans: "Light to medium roast",
    r5_flavor: "Intense cardamom, saffron, clove",
    r5_vibe: "Guest of honor",

    footer_brand: "Qahwatna",
    footer_tagline: "Flavors from every Saudi region",
    footer_rights: "All rights reserved",
  },
};

// -----------------------------
// هيلبر للغة
// -----------------------------
function applyLanguage(lang) {
  // غير اتجاه الصفحة
  const htmlEl = document.documentElement;
  if (lang === "ar") {
    htmlEl.setAttribute("dir", "rtl");
    htmlEl.setAttribute("lang", "ar");
  } else {
    htmlEl.setAttribute("dir", "ltr");
    htmlEl.setAttribute("lang", "en");
  }

  // عدل كل العناصر اللي عليها data-i18n
  const nodes = document.querySelectorAll("[data-i18n]");
  nodes.forEach(node => {
    const key = node.getAttribute("data-i18n");
    if (translations[lang][key] !== undefined) {
      node.textContent = translations[lang][key];
    }
  });

  // لو غيّرنا اللغة، لازم نحدّث نص حالة العداد الحالي بالإنجليزي/العربي
  updateCounterUI(cupsCount, lang);

  // غيّر زر اللغة نفسه: يخبرك وش اللغة الجاية لو تضغطيه
  if (langToggle) {
    langToggle.textContent = lang === "ar" ? "EN" : "AR";
  }

  // خزن اللغة
  localStorage.setItem("q_lang", lang);
}

// نقرأ اللغة المخزنة أو نبدأ عربي
function getSavedLang() {
  return localStorage.getItem("q_lang") || "ar";
}

// -----------------------------
// خلفية النجوم
// -----------------------------
const starCanvas = document.getElementById("stars-bg");
const starCtx = starCanvas.getContext("2d");
let stars = [];

function initStars() {
  starCanvas.width = window.innerWidth;
  starCanvas.height = window.innerHeight;

  stars = [];
  const count = Math.floor((window.innerWidth + window.innerHeight) / 4);
  for (let i = 0; i < count; i++) {
    stars.push({
      x: Math.random() * starCanvas.width,
      y: Math.random() * starCanvas.height,
      size: Math.random() * 1.5 + 0.2,
      speed: Math.random() * 0.2 + 0.05,
    });
  }
}
function drawStars() {
  starCtx.clearRect(0,0,starCanvas.width,starCanvas.height);
  starCtx.fillStyle = "rgba(255,255,255,0.6)";
  stars.forEach(s => {
    starCtx.beginPath();
    starCtx.arc(s.x, s.y, s.size, 0, Math.PI*2);
    starCtx.fill();

    s.y += s.speed;
    if (s.y > starCanvas.height) {
      s.y = 0;
      s.x = Math.random() * starCanvas.width;
    }
  });
  requestAnimationFrame(drawStars);
}
initStars();
drawStars();
window.addEventListener("resize", initStars);

// -----------------------------
// بخار القهوة
// -----------------------------
const steamCanvas = document.getElementById("steam-canvas");
const steamCtx = steamCanvas.getContext("2d");

steamCanvas.width = 200;
steamCanvas.height = 200;

let puffs = [];
function newPuff() {
  puffs.push({
    x: steamCanvas.width/2 + (Math.random()*10-5),
    y: steamCanvas.height/2 + 20,
    radius: 6 + Math.random()*4,
    alpha: 0.4 + Math.random()*0.3,
    vy: - (0.5 + Math.random()*0.5),
    vx: (Math.random()*0.4-0.2),
    growth: 0.07 + Math.random()*0.05
  });
}
function drawSteam() {
  steamCtx.clearRect(0,0,steamCanvas.width,steamCanvas.height);

  if (Math.random() < 0.2) {
    newPuff();
  }

  puffs.forEach(p => {
    steamCtx.beginPath();
    steamCtx.fillStyle = `rgba(255,255,255,${p.alpha})`;
    steamCtx.shadowColor = "rgba(255,255,255,0.5)";
    steamCtx.shadowBlur = 20;
    steamCtx.arc(p.x, p.y, p.radius, 0, Math.PI*2);
    steamCtx.fill();

    p.y += p.vy;
    p.x += p.vx;
    p.radius += p.growth;
    p.alpha -= 0.005;
  });

  puffs = puffs.filter(p => p.alpha > 0);

  requestAnimationFrame(drawSteam);
}
drawSteam();

const cupWrapper = document.getElementById("cup");
cupWrapper.addEventListener("mousemove", () => {
  for (let i = 0; i < 3; i++) newPuff();
});
cupWrapper.addEventListener("mouseenter", () => {
  cupWrapper.classList.add("shake");
});
cupWrapper.addEventListener("animationend", () => {
  cupWrapper.classList.remove("shake");
});

// -----------------------------
// صوت القهوة
// -----------------------------
const coffeeAudio = document.getElementById("coffee-audio");
const pourBtn = document.getElementById("pour-btn");
const stopBtn = document.getElementById("stop-btn");

pourBtn.addEventListener("click", () => {
  coffeeAudio.currentTime = 0;
  coffeeAudio.play().catch(()=>{});
});
stopBtn.addEventListener("click", () => {
  coffeeAudio.pause();
});

// -----------------------------
// reveal on scroll
// -----------------------------
const revealEls = document.querySelectorAll(".reveal");
function revealOnScroll() {
  const triggerBottom = window.innerHeight * 0.9;
  revealEls.forEach(el => {
    const rect = el.getBoundingClientRect();
    if (rect.top < triggerBottom) {
      el.classList.add("visible");
    }
  });
}
window.addEventListener("scroll", revealOnScroll);
window.addEventListener("load", revealOnScroll);

// -----------------------------
// عداد الأرقام التراث/المكونات/الكرم
// -----------------------------
const factNumbers = document.querySelectorAll(".fact-number");
let factsAnimated = false;
function animateFacts() {
  if (factsAnimated) return;

  const aboutSection = document.getElementById("about");
  const rect = aboutSection.getBoundingClientRect();
  const triggerBottom = window.innerHeight * 0.8;

  if (rect.top < triggerBottom) {
    factsAnimated = true;
    factNumbers.forEach(el => {
      const target = parseInt(el.getAttribute("data-target"),10);
      let current = 0;
      const duration = 1200;
      const startTime = performance.now();

      function updateNum(now) {
        const progress = Math.min((now - startTime)/duration, 1);
        current = Math.floor(progress * target);
        el.textContent = current;
        if (progress < 1) {
          requestAnimationFrame(updateNum);
        } else {
          el.textContent = target;
        }
      }
      requestAnimationFrame(updateNum);
    });
  }
}
window.addEventListener("scroll", animateFacts);
window.addEventListener("load", animateFacts);

// -----------------------------
// عداد الفناجيل مع localStorage
// -----------------------------
const countDisplay = document.getElementById("count-display");
const incBtn = document.getElementById("inc-btn");
const decBtn = document.getElementById("dec-btn");
const resetBtn = document.getElementById("reset-btn");
const counterBox = document.querySelector(".counter-box");
const counterStatus = document.getElementById("counter-status");

function getStoredCount() {
  const saved = localStorage.getItem("cupsCount");
  return saved ? parseInt(saved,10) : 0;
}
function saveCount(n) {
  localStorage.setItem("cupsCount", String(n));
}

// نحدّث الرسالة حسب اللغة
function getStatusText(n, lang) {
  if (lang === "en") {
    if (n === 0) return "Clean start 👑";
    if (n === 1) return "Just a warm-up cup ☕";
    if (n <= 3) return "Balanced. You're in control 😌";
    if (n <= 6) return "Serious focus mode, huh? 😏";
    return "Your heart is not an espresso machine 😭";
  } else {
    if (n === 0) return "بداية نظيفة 👑";
    if (n === 1) return "مزاج فنجال واحد ☕";
    if (n <= 3) return "معتدل. كل شيء تحت السيطرة 😌";
    if (n <= 6) return "شكلك قاعد/ـة تذاكرين؟ 😏";
    return "اهدّي يا بطلة.. قلبك مو ماكينة إسبرسو 😭";
  }
}

function updateCounterUI(n, langOverride) {
  const langNow = langOverride || getSavedLang();
  countDisplay.textContent = n;
  counterStatus.textContent = getStatusText(n, langNow);

  if (n >= 7) {
    counterBox.classList.add("too-much");
  } else {
    counterBox.classList.remove("too-much");
  }
}

let cupsCount = getStoredCount();
updateCounterUI(cupsCount);

incBtn.addEventListener("click", () => {
  cupsCount++;
  saveCount(cupsCount);
  updateCounterUI(cupsCount);
});
decBtn.addEventListener("click", () => {
  cupsCount--;
  if (cupsCount < 0) cupsCount = 0;
  saveCount(cupsCount);
  updateCounterUI(cupsCount);
});
resetBtn.addEventListener("click", () => {
  cupsCount = 0;
  saveCount(cupsCount);
  updateCounterUI(cupsCount);
});

// -----------------------------
// وهج ماوس فاخر
// -----------------------------
const pageGlow = document.getElementById("page-glow");
document.addEventListener("pointermove", (e) => {
  pageGlow.style.transform = `translate(${e.clientX - 90}px, ${e.clientY - 90}px)`;
});

// -----------------------------
// لمعة بطاقات المناطق عند الهوفر
// -----------------------------
const regionCards = document.querySelectorAll(".region-card");
regionCards.forEach(card => {
  card.addEventListener("mouseenter", () => {
    card.classList.add("flash");
    setTimeout(() => card.classList.remove("flash"), 200);
  });
});

// -----------------------------
// نبضة "الهيل" كل فترة
// -----------------------------
const hailCard = document.getElementById("card-hail");
function pulseHail() {
  hailCard.classList.add("hail-pulse");
  setTimeout(() => {
    hailCard.classList.remove("hail-pulse");
  }, 1000);
}
setInterval(pulseHail, 5000);

// -----------------------------
// زر تغيير المزاج نهار/ليل
// -----------------------------
const moodToggle = document.getElementById("mood-toggle");

function getMood() {
  return localStorage.getItem("q_mood") || "night";
}
function setMood(mode) {
  localStorage.setItem("q_mood", mode);
}
function applyMood(mode) {
  if (mode === "day") {
    document.body.classList.add("day-mode");
    moodToggle.textContent = "☀️";
  } else {
    document.body.classList.remove("day-mode");
    moodToggle.textContent = "🌙";
  }
}
let currentMood = getMood();
applyMood(currentMood);

moodToggle.addEventListener("click", () => {
  currentMood = currentMood === "day" ? "night" : "day";
  applyMood(currentMood);
  setMood(currentMood);
});

// -----------------------------
// زر تغيير اللغة AR / EN
// -----------------------------
const langToggle = document.getElementById("lang-toggle");

// أول ما تفتح الصفحة نطبّق اللغة المحفوظة
let currentLang = getSavedLang();
applyLanguage(currentLang);

// لما يضغط الزر، نقلب اللغة
langToggle.addEventListener("click", () => {
  currentLang = currentLang === "ar" ? "en" : "ar";
  applyLanguage(currentLang);
});

// -----------------------------
// سنة الفوتر
// -----------------------------
document.getElementById("year").textContent = new Date().getFullYear();

</script>

</body>
</html>
