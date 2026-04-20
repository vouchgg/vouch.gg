<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>vouch.gg — Your identity, fully vouched.</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,400&display=swap" rel="stylesheet">
<style>
/* ===== RESET & ROOT ===== */
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
:root {
  --bg:      #080810;
  --bg2:     #0f0f1a;
  --bg3:     #14141f;
  --bg4:     #1a1a28;
  --bg5:     #222235;
  --border:  #1e1e30;
  --border2: #2a2a40;
  --border3: #383858;
  --text:    #eeeeff;
  --text2:   #9898bb;
  --text3:   #55556a;
  --accent:  #7c5cfc;
  --accent2: #5c8afc;
  --accent3: #fc5c8a;
  --gold:    #ffc857;
  --green:   #4ade80;
  --nitro:   #ff73fa;
  --r: 12px; --r2: 8px; --r3: 20px; --r4: 16px;
}
html { scroll-behavior: smooth; }
body {
  background: var(--bg);
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  min-height: 100vh;
  overflow-x: hidden;
  line-height: 1.6;
}
a { color: inherit; text-decoration: none; }
button { font-family: 'DM Sans', sans-serif; cursor: pointer; }
input, textarea, select { font-family: 'DM Sans', sans-serif; }
img { max-width: 100%; }

/* ===== SCROLLBAR ===== */
::-webkit-scrollbar { width: 6px; height: 6px; }
::-webkit-scrollbar-track { background: var(--bg2); }
::-webkit-scrollbar-thumb { background: var(--border3); border-radius: 3px; }

/* ===== LOADING SCREEN ===== */
#loading-screen {
  position: fixed; inset: 0; z-index: 9999;
  background: var(--bg);
  display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 28px;
  transition: opacity 0.6s ease, visibility 0.6s ease;
}
#loading-screen.fade-out { opacity: 0; visibility: hidden; }
.load-logo {
  width: 80px; height: 80px;
  background: linear-gradient(135deg, var(--accent), var(--accent2));
  border-radius: 22px;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif; font-size: 32px; font-weight: 800; color: #fff;
  animation: logoPulse 1.6s ease-in-out infinite;
  box-shadow: 0 0 60px rgba(124,92,252,0.35);
}
@keyframes logoPulse {
  0%,100% { transform: scale(1); box-shadow: 0 0 40px rgba(124,92,252,0.3); }
  50%      { transform: scale(1.06); box-shadow: 0 0 80px rgba(124,92,252,0.55); }
}
.load-name {
  font-family: 'Syne', sans-serif; font-size: 36px; font-weight: 800;
  letter-spacing: -1.5px;
  background: linear-gradient(135deg, #fff 30%, var(--accent));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.load-bar-wrap { width: 220px; height: 3px; background: var(--bg4); border-radius: 3px; overflow: hidden; }
.load-bar { height: 100%; width: 0; background: linear-gradient(90deg, var(--accent), var(--accent2)); border-radius: 3px; animation: loadFill 1.8s ease forwards; }
@keyframes loadFill { from { width: 0 } to { width: 100% } }
.load-tagline { font-size: 14px; color: var(--text3); }

/* ===== NAV ===== */
#main-nav {
  position: sticky; top: 0; z-index: 500;
  height: 62px;
  background: rgba(8,8,16,0.82);
  backdrop-filter: blur(18px);
  border-bottom: 1px solid var(--border);
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 32px;
}
.nav-left { display: flex; align-items: center; gap: 32px; }
.nav-brand { display: flex; align-items: center; gap: 10px; cursor: pointer; }
.nav-logomark {
  width: 34px; height: 34px; border-radius: 9px;
  background: linear-gradient(135deg, var(--accent), var(--accent2));
  display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif; font-size: 14px; font-weight: 800; color: #fff;
}
.nav-wordmark { font-family: 'Syne', sans-serif; font-size: 19px; font-weight: 700; letter-spacing: -0.5px; }
.nav-links { display: flex; gap: 2px; }
.nav-link {
  padding: 7px 15px; border-radius: var(--r2); font-size: 14px; font-weight: 500;
  color: var(--text2); cursor: pointer; border: none; background: transparent;
  transition: color 0.15s, background 0.15s;
}
.nav-link:hover { color: var(--text); background: var(--bg3); }
.nav-link.active { color: #fff; background: var(--bg4); }
.nav-right { display: flex; align-items: center; gap: 10px; }

/* ===== BUTTONS ===== */
.btn {
  padding: 9px 20px; border-radius: var(--r3); font-size: 14px; font-weight: 600;
  border: none; transition: all 0.18s; display: inline-flex; align-items: center; gap: 6px;
}
.btn-sm { padding: 6px 14px; font-size: 13px; }
.btn-lg { padding: 14px 34px; font-size: 16px; }
.btn-primary { background: linear-gradient(135deg, var(--accent), var(--accent2)); color: #fff; }
.btn-primary:hover { opacity: 0.88; transform: translateY(-1px); box-shadow: 0 8px 24px rgba(124,92,252,0.35); }
.btn-ghost { background: transparent; color: var(--text2); border: 1px solid var(--border2); }
.btn-ghost:hover { color: var(--text); border-color: var(--border3); background: var(--bg3); }
.btn-accent3 { background: linear-gradient(135deg, var(--accent3), #fc8c5c); color: #fff; }
.btn-discord { background: #5865f2; color: #fff; }
.btn-discord:hover { background: #4752c4; }

/* ===== PAGES ===== */
.page { display: none; }
.page.active { display: block; animation: pageIn 0.3s ease; }
@keyframes pageIn { from { opacity:0; transform: translateY(10px); } to { opacity:1; transform:translateY(0); } }

/* ===== SECTION WRAPPER ===== */
.wrap { max-width: 1120px; margin: 0 auto; padding: 0 24px; }
.section { padding: 48px 0; }
.section-title {
  font-family: 'Syne', sans-serif; font-size: 22px; font-weight: 700;
  letter-spacing: -0.5px; margin-bottom: 20px;
}
.section-title span { color: var(--accent); }

/* ===== CARDS ===== */
.card {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 20px; transition: border-color 0.18s;
}
.card:hover { border-color: var(--border2); }

/* ===== BADGES ===== */
.badge {
  display: inline-flex; align-items: center; justify-content: center;
  width: 17px; height: 17px; border-radius: 50%; font-size: 9px; font-weight: 700;
  flex-shrink: 0; cursor: default;
}
.badge-verified { background: var(--accent); color: #fff; }
.badge-official { background: var(--gold); color: #000; }

/* ===== TAGS ===== */
.tag {
  display: inline-flex; align-items: center; gap: 5px;
  padding: 4px 12px; border-radius: 20px;
  font-size: 12px; font-weight: 500; cursor: default;
}
.tag-purple { background: rgba(124,92,252,0.14); color: var(--accent); border: 1px solid rgba(124,92,252,0.25); }
.tag-blue   { background: rgba(92,138,252,0.14); color: var(--accent2); border: 1px solid rgba(92,138,252,0.25); }
.tag-green  { background: rgba(74,222,128,0.12); color: var(--green); border: 1px solid rgba(74,222,128,0.22); }
.tag-gold   { background: rgba(255,200,87,0.12); color: var(--gold); border: 1px solid rgba(255,200,87,0.22); }
.tag-pink   { background: rgba(252,92,138,0.12); color: var(--accent3); border: 1px solid rgba(252,92,138,0.22); }
.tag-nitro  { background: rgba(255,115,250,0.12); color: var(--nitro); border: 1px solid rgba(255,115,250,0.22); }
.tag-discord{ background: rgba(88,101,242,0.14); color: #8891f2; border: 1px solid rgba(88,101,242,0.28); }

/* ===========================
   PAGE: HOME
   =========================== */
.hero {
  padding: 96px 24px 72px;
  text-align: center;
  position: relative; overflow: hidden;
}
.hero-glow {
  position: absolute; width: 700px; height: 700px; pointer-events: none;
  background: radial-gradient(circle, rgba(124,92,252,0.13) 0%, transparent 65%);
  top: 50%; left: 50%; transform: translate(-50%,-55%);
}
.hero-h1 {
  font-family: 'Syne', sans-serif;
  font-size: clamp(44px, 7vw, 80px);
  font-weight: 800; line-height: 1.04; letter-spacing: -3px;
  margin-bottom: 22px; position: relative;
}
.hero-h1 .grad {
  background: linear-gradient(135deg, var(--accent) 10%, var(--accent2) 50%, var(--accent3) 90%);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.hero-sub { font-size: 18px; color: var(--text2); max-width: 500px; margin: 0 auto 38px; line-height: 1.65; }
.hero-ctas { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
.hero-stats {
  display: flex; gap: 0; justify-content: center; flex-wrap: wrap;
  margin-top: 72px; padding-top: 48px; border-top: 1px solid var(--border);
}
.stat { padding: 0 40px; text-align: center; border-right: 1px solid var(--border); }
.stat:last-child { border-right: none; }
.stat-n {
  font-family: 'Syne', sans-serif; font-size: 30px; font-weight: 700;
  background: linear-gradient(135deg, #fff, var(--accent2));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.stat-l { font-size: 13px; color: var(--text3); margin-top: 3px; }

/* Claim username box */
.claim-box {
  background: linear-gradient(135deg, rgba(124,92,252,0.1), rgba(92,138,252,0.07));
  border: 1px solid rgba(124,92,252,0.22);
  border-radius: var(--r4); padding: 40px; text-align: center; margin-top: 48px;
}
.claim-box h2 { font-family: 'Syne', sans-serif; font-size: 26px; font-weight: 700; margin-bottom: 8px; }
.claim-box p  { font-size: 15px; color: var(--text2); margin-bottom: 24px; }
.claim-row { display: flex; gap: 10px; max-width: 440px; margin: 0 auto; }
.claim-prefix {
  background: var(--bg3); border: 1px solid var(--border2); border-right: none;
  border-radius: var(--r2) 0 0 var(--r2); padding: 0 14px;
  font-size: 14px; color: var(--text3); display: flex; align-items: center;
  white-space: nowrap;
}
.claim-input {
  flex: 1; background: var(--bg3); border: 1px solid var(--border2);
  border-radius: 0 var(--r2) var(--r2) 0; padding: 11px 14px;
  font-size: 14px; color: var(--text); outline: none;
  transition: border-color 0.15s;
}
.claim-input:focus { border-color: var(--accent); }

/* Featured profiles row */
.fp-row { display: flex; gap: 14px; overflow-x: auto; padding: 4px 0; margin-top: 8px; }
.fp-row::-webkit-scrollbar { height: 4px; }
.fp-card {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 18px 20px; min-width: 170px; flex-shrink: 0;
  text-align: center; cursor: pointer; transition: all 0.2s;
}
.fp-card:hover { border-color: var(--accent); transform: translateY(-3px); box-shadow: 0 12px 32px rgba(0,0,0,0.3); }
.fp-av {
  width: 54px; height: 54px; border-radius: 50%;
  margin: 0 auto 10px;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif; font-size: 20px; font-weight: 700; color: #fff;
}
.fp-name { font-size: 14px; font-weight: 600; display: flex; align-items: center; justify-content: center; gap: 5px; }
.fp-handle { font-size: 12px; color: var(--text3); margin-top: 3px; }
.fp-badge { margin-top: 8px; }

/* ===========================
   PAGE: FEED
   =========================== */
.feed-layout { display: grid; grid-template-columns: 1fr 310px; gap: 22px; }
.feed-posts { display: flex; flex-direction: column; gap: 14px; }
.post-card { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); padding: 20px; transition: border-color 0.18s; }
.post-card:hover { border-color: var(--border2); }
.post-card.official { border-color: rgba(255,200,87,0.3); background: rgba(255,200,87,0.025); }
.post-header { display: flex; align-items: center; gap: 12px; margin-bottom: 13px; }
.post-av {
  width: 42px; height: 42px; border-radius: 50%; flex-shrink: 0;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif; font-size: 15px; font-weight: 700; color: #fff;
}
.post-meta { flex: 1; }
.post-name { font-size: 14px; font-weight: 600; display: flex; align-items: center; gap: 6px; }
.post-time { font-size: 12px; color: var(--text3); margin-top: 1px; }
.post-body { font-size: 14px; line-height: 1.65; color: var(--text2); margin-bottom: 15px; }
.post-body strong { color: var(--text); }
.reactions { display: flex; gap: 7px; flex-wrap: wrap; }
.reaction {
  display: inline-flex; align-items: center; gap: 4px;
  padding: 5px 11px; border-radius: 20px;
  background: var(--bg3); border: 1px solid var(--border);
  font-size: 13px; color: var(--text2); cursor: pointer; transition: all 0.15s;
}
.reaction:hover, .reaction.active {
  background: rgba(124,92,252,0.15); border-color: var(--accent); color: var(--accent);
}
.reaction .emoji { font-size: 15px; line-height: 1; }
.new-post-box { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); padding: 18px; }
.new-post-row { display: flex; gap: 12px; }
.np-av { width: 40px; height: 40px; border-radius: 50%; background: linear-gradient(135deg, var(--accent), var(--accent2)); display: flex; align-items: center; justify-content: center; font-family: 'Syne', sans-serif; font-size: 15px; font-weight: 700; color: #fff; flex-shrink: 0; }
.np-inner { flex: 1; }
.np-textarea { width: 100%; background: var(--bg3); border: 1px solid var(--border); border-radius: var(--r2); padding: 11px 14px; font-size: 14px; color: var(--text); resize: none; outline: none; transition: border-color 0.15s; min-height: 80px; }
.np-textarea:focus { border-color: var(--accent); }
.np-footer { display: flex; justify-content: space-between; align-items: center; margin-top: 10px; }
.np-emojis { display: flex; gap: 8px; }
.np-emoji { font-size: 18px; cursor: pointer; opacity: 0.6; transition: opacity 0.15s; }
.np-emoji:hover { opacity: 1; }

/* Feed sidebar */
.feed-sidebar { display: flex; flex-direction: column; gap: 16px; }
.sidebar-card { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); padding: 18px; }
.sidebar-title { font-size: 12px; font-weight: 600; color: var(--text3); text-transform: uppercase; letter-spacing: 0.9px; margin-bottom: 14px; }
.update-item { padding: 11px 0; border-bottom: 1px solid var(--border); }
.update-item:last-child { border-bottom: none; padding-bottom: 0; }
.update-item:first-child { padding-top: 0; }
.update-item h4 { font-size: 13px; font-weight: 600; margin-bottom: 3px; }
.update-item p { font-size: 12px; color: var(--text3); line-height: 1.4; }
.update-item .date { font-size: 11px; color: var(--text3); margin-top: 4px; }
.online-row { display: flex; align-items: center; gap: 10px; padding: 7px 0; border-bottom: 1px solid var(--border); }
.online-row:last-child { border-bottom: none; }
.online-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--green); flex-shrink: 0; box-shadow: 0 0 6px var(--green); }
.online-name { font-size: 13px; flex: 1; }
.online-tag { font-size: 11px; color: var(--text3); }

/* ===========================
   PAGE: MARKET
   =========================== */
.market-filters { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 24px; }
.market-filter { padding: 7px 16px; border-radius: 20px; font-size: 13px; font-weight: 500; border: 1px solid var(--border2); background: transparent; color: var(--text2); cursor: pointer; transition: all 0.15s; }
.market-filter:hover, .market-filter.active { background: rgba(124,92,252,0.15); border-color: var(--accent); color: var(--accent); }
.market-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 16px; }
.market-card {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r4); padding: 22px; cursor: pointer;
  transition: all 0.22s; position: relative; overflow: hidden; display: flex; flex-direction: column; gap: 13px;
}
.market-card::before {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(135deg, rgba(124,92,252,0.04), transparent);
  pointer-events: none;
}
.market-card:hover { border-color: var(--accent); transform: translateY(-3px); box-shadow: 0 16px 40px rgba(0,0,0,0.35); }
.market-card-badge { position: absolute; top: 14px; right: 14px; }
.market-icon {
  width: 54px; height: 54px; border-radius: 14px;
  display: flex; align-items: center; justify-content: center; font-size: 26px;
}
.mi-purple { background: rgba(124,92,252,0.15); }
.mi-blue   { background: rgba(92,138,252,0.15); }
.mi-gold   { background: rgba(255,200,87,0.15); }
.mi-pink   { background: rgba(252,92,138,0.15); }
.mi-green  { background: rgba(74,222,128,0.12); }
.market-name { font-size: 15px; font-weight: 600; }
.market-desc { font-size: 13px; color: var(--text3); line-height: 1.5; flex: 1; }
.market-footer { display: flex; align-items: center; justify-content: space-between; margin-top: 4px; }
.market-price { font-family: 'Syne', sans-serif; font-size: 19px; font-weight: 700; color: var(--accent); }
.market-buy {
  background: rgba(124,92,252,0.13); border: 1px solid rgba(124,92,252,0.4);
  color: var(--accent); border-radius: var(--r2); padding: 7px 16px;
  font-size: 13px; font-weight: 600; cursor: pointer; transition: all 0.15s;
}
.market-buy:hover { background: var(--accent); color: #fff; }
.market-owned { background: rgba(74,222,128,0.1); border-color: rgba(74,222,128,0.3); color: var(--green); }
.market-owned:hover { background: rgba(74,222,128,0.2); }

/* ===========================
   PAGE: NEWS
   =========================== */
.news-featured {
  background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r4);
  overflow: hidden; margin-bottom: 24px; display: grid; grid-template-columns: 1fr 1fr; cursor: pointer; transition: border-color 0.18s;
}
.news-featured:hover { border-color: var(--accent2); }
.news-featured-thumb {
  height: 260px; background: linear-gradient(135deg, #0f0a2a, #0a1a3a, #1a0a2a);
  display: flex; align-items: center; justify-content: center; font-size: 72px;
  position: relative; overflow: hidden;
}
.news-featured-thumb::after {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(135deg, rgba(124,92,252,0.25), rgba(92,138,252,0.15));
}
.news-featured-body { padding: 32px; display: flex; flex-direction: column; justify-content: center; gap: 12px; }
.news-label {
  display: inline-flex; align-items: center; gap: 5px;
  padding: 4px 10px; border-radius: 10px; font-size: 11px; font-weight: 600;
}
.nl-update   { background: rgba(74,222,128,0.13);  color: var(--green); }
.nl-feature  { background: rgba(124,92,252,0.13);  color: var(--accent); }
.nl-announce { background: rgba(255,200,87,0.13);  color: var(--gold); }
.nl-official { background: rgba(255,200,87,0.15); color: var(--gold); }
.news-featured-title { font-family: 'Syne', sans-serif; font-size: 22px; font-weight: 700; line-height: 1.3; }
.news-featured-excerpt { font-size: 14px; color: var(--text2); line-height: 1.65; }
.news-featured-meta { font-size: 12px; color: var(--text3); display: flex; align-items: center; gap: 8px; }
.news-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 16px; }
.news-card { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); overflow: hidden; cursor: pointer; transition: all 0.2s; }
.news-card:hover { border-color: var(--accent2); transform: translateY(-2px); }
.news-thumb { height: 130px; display: flex; align-items: center; justify-content: center; font-size: 44px; background: var(--bg3); }
.news-body { padding: 16px; }
.news-title { font-size: 14px; font-weight: 600; line-height: 1.4; margin: 8px 0 6px; }
.news-excerpt { font-size: 13px; color: var(--text3); line-height: 1.5; }
.news-date { font-size: 11px; color: var(--text3); margin-top: 10px; }
.official-news-author { display: flex; align-items: center; gap: 6px; font-size: 12px; color: var(--text3); }
.official-av { width: 20px; height: 20px; border-radius: 50%; background: linear-gradient(135deg, var(--accent), var(--accent2)); display: flex; align-items: center; justify-content: center; font-size: 9px; font-weight: 800; color: #fff; }

/* ===========================
   PAGE: PROFILE
   =========================== */
.profile-banner {
  width: 100%; height: 200px; border-radius: var(--r) var(--r) 0 0;
  background: linear-gradient(135deg, #120a2e, #0a1535, #0e2518);
  position: relative; overflow: hidden;
}
.profile-banner-overlay { position: absolute; inset: 0; background: linear-gradient(135deg, rgba(124,92,252,0.35), rgba(92,138,252,0.2), rgba(252,92,138,0.1)); }
.profile-outer { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); overflow: hidden; max-width: 760px; }
.profile-info-wrap { padding: 62px 28px 24px; position: relative; }
.profile-avatar-wrap { position: absolute; top: -52px; left: 24px; }
.profile-avatar {
  width: 96px; height: 96px; border-radius: 50%;
  border: 4px solid var(--bg2); display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif; font-size: 30px; font-weight: 700; color: #fff;
  background: linear-gradient(135deg, var(--accent), var(--accent2));
}
.profile-name-row { display: flex; align-items: center; gap: 8px; flex-wrap: wrap; margin-bottom: 4px; }
.profile-name { font-family: 'Syne', sans-serif; font-size: 24px; font-weight: 700; }
.profile-handle { font-size: 14px; color: var(--text3); margin-bottom: 12px; font-family: monospace; }
.profile-bio { font-size: 14px; color: var(--text2); line-height: 1.65; margin-bottom: 16px; max-width: 500px; }
.profile-tags-row { display: flex; gap: 7px; flex-wrap: wrap; margin-bottom: 16px; }
.profile-discord-row { display: flex; flex-wrap: wrap; gap: 8px; align-items: center; margin-bottom: 16px; }
.discord-link-badge { display: inline-flex; align-items: center; gap: 7px; padding: 6px 14px; background: rgba(88,101,242,0.13); border: 1px solid rgba(88,101,242,0.28); border-radius: 20px; font-size: 13px; font-weight: 500; }
.discord-icon { width: 18px; height: 18px; background: #5865f2; border-radius: 4px; display: flex; align-items: center; justify-content: center; font-size: 10px; color: #fff; font-weight: 700; }
.profile-stats { display: grid; grid-template-columns: repeat(4,1fr); padding: 18px 28px; border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); gap: 8px; }
.pstat { text-align: center; }
.pstat-val { font-family: 'Syne', sans-serif; font-size: 20px; font-weight: 700; }
.pstat-lbl { font-size: 11px; color: var(--text3); margin-top: 2px; }
.profile-tabs { display: flex; gap: 4px; padding: 16px 28px 0; border-bottom: 1px solid var(--border); }
.ptab {
  padding: 8px 18px; border-radius: var(--r2) var(--r2) 0 0;
  font-size: 13px; font-weight: 500; cursor: pointer; transition: all 0.15s;
  color: var(--text3); border: 1px solid transparent; border-bottom: none; background: transparent;
}
.ptab:hover { color: var(--text2); }
.ptab.active { color: #fff; background: var(--bg3); border-color: var(--border); }
.profile-tab-content { padding: 22px 28px; }
.tab-pane { display: none; }
.tab-pane.active { display: block; }

/* Music player */
.music-player {
  background: var(--bg3); border: 1px solid var(--border);
  border-radius: var(--r2); padding: 14px 16px;
  display: flex; align-items: center; gap: 14px; margin-bottom: 18px;
}
.music-thumb {
  width: 46px; height: 46px; border-radius: 9px; flex-shrink: 0;
  background: linear-gradient(135deg, var(--accent), var(--accent3));
  display: flex; align-items: center; justify-content: center; font-size: 22px;
}
.music-info { flex: 1; }
.music-title { font-size: 13px; font-weight: 600; }
.music-artist { font-size: 12px; color: var(--text3); margin-top: 2px; }
.music-bar-wrap { height: 3px; background: var(--bg5); border-radius: 3px; margin-top: 8px; }
.music-bar-fill { height: 100%; width: 42%; background: linear-gradient(90deg, var(--accent), var(--accent2)); border-radius: 3px; }
.music-controls { display: flex; gap: 8px; align-items: center; }
.mc-btn { width: 30px; height: 30px; border-radius: 50%; background: var(--bg4); border: none; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 12px; color: var(--text2); transition: all 0.15s; }
.mc-btn:hover { background: var(--bg5); color: var(--text); }
.mc-btn.play { width: 38px; height: 38px; background: var(--accent); color: #fff; font-size: 14px; }
.mc-btn.play:hover { background: var(--accent2); }

/* Portfolio grid */
.portfolio-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 13px; }
.portfolio-item { background: var(--bg3); border: 1px solid var(--border); border-radius: var(--r2); overflow: hidden; cursor: pointer; transition: all 0.18s; }
.portfolio-item:hover { border-color: var(--accent); transform: translateY(-2px); }
.portfolio-thumb { height: 100px; display: flex; align-items: center; justify-content: center; font-size: 36px; }
.portfolio-info { padding: 12px; }
.portfolio-name { font-size: 13px; font-weight: 600; }
.portfolio-type { font-size: 11px; color: var(--text3); margin-top: 2px; }

/* Server list */
.server-list { display: flex; flex-direction: column; gap: 8px; }
.server-item { display: flex; align-items: center; gap: 12px; padding: 10px 12px; background: var(--bg3); border-radius: var(--r2); border: 1px solid var(--border); transition: border-color 0.15s; }
.server-item:hover { border-color: var(--border2); }
.server-icon { width: 40px; height: 40px; border-radius: 11px; display: flex; align-items: center; justify-content: center; font-size: 18px; flex-shrink: 0; }
.server-info { flex: 1; }
.server-name { font-size: 13px; font-weight: 600; }
.server-members { font-size: 11px; color: var(--text3); margin-top: 2px; }
.server-owner-badge { font-size: 11px; font-weight: 600; color: var(--gold); }

/* About tab */
.about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.about-item h4 { font-size: 11px; color: var(--text3); text-transform: uppercase; letter-spacing: 0.7px; font-weight: 600; margin-bottom: 5px; }
.about-item p { font-size: 14px; font-weight: 500; }

/* ===========================
   PAGE: DASHBOARD
   =========================== */
.dash-layout { display: grid; grid-template-columns: 220px 1fr; gap: 22px; align-items: start; }
.dash-sidebar { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); padding: 14px; position: sticky; top: 80px; }
.dash-nav-item {
  display: flex; align-items: center; gap: 9px;
  padding: 9px 12px; border-radius: var(--r2); font-size: 14px; cursor: pointer;
  color: var(--text2); transition: all 0.15s; border: none; background: transparent;
  width: 100%; text-align: left; margin-bottom: 2px;
}
.dash-nav-item:hover { color: var(--text); background: var(--bg3); }
.dash-nav-item.active { color: #fff; background: rgba(124,92,252,0.18); font-weight: 500; }
.dash-nav-item .dni { font-size: 17px; width: 22px; text-align: center; }
.dash-nav-divider { height: 1px; background: var(--border); margin: 10px 0; }
.dash-content { display: flex; flex-direction: column; gap: 16px; }
.dash-pane { display: none; }
.dash-pane.active { display: flex; flex-direction: column; gap: 16px; }
.dcard { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); padding: 22px; }
.dcard-title { font-size: 15px; font-weight: 600; margin-bottom: 18px; display: flex; align-items: center; gap: 9px; }
.dcard-title .icon { font-size: 18px; }

/* Form elements */
.f-row { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-bottom: 14px; }
.f-field { display: flex; flex-direction: column; gap: 6px; margin-bottom: 14px; }
.f-field:last-child { margin-bottom: 0; }
.f-label { font-size: 11px; font-weight: 600; color: var(--text3); text-transform: uppercase; letter-spacing: 0.7px; }
.f-input {
  background: var(--bg3); border: 1px solid var(--border2);
  border-radius: var(--r2); padding: 10px 14px; font-size: 14px; color: var(--text);
  outline: none; transition: border-color 0.15s; width: 100%;
}
.f-input:focus { border-color: var(--accent); }
.f-input.readonly { color: var(--text3); cursor: default; }
textarea.f-input { resize: vertical; min-height: 82px; }
.f-hint { font-size: 12px; color: var(--text3); margin-top: 4px; }

/* Color swatches */
.swatches { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 6px; }
.swatch { width: 30px; height: 30px; border-radius: 8px; cursor: pointer; border: 2px solid transparent; transition: all 0.15s; }
.swatch:hover, .swatch.active { transform: scale(1.18); border-color: rgba(255,255,255,0.6); }

/* Banner preview */
.banner-prev {
  width: 100%; height: 110px; border-radius: var(--r2); margin-bottom: 12px;
  background: linear-gradient(135deg, #120a2e, #0a1535);
  overflow: hidden; position: relative; cursor: pointer;
  display: flex; align-items: center; justify-content: center;
}
.banner-prev::after { content: 'Click to change'; position: absolute; inset: 0; background: rgba(0,0,0,0.5); display: flex; align-items: center; justify-content: center; font-size: 13px; color: #fff; opacity: 0; transition: opacity 0.2s; border-radius: var(--r2); }
.banner-prev:hover::after { opacity: 1; }
.banner-prev-overlay { position: absolute; inset: 0; background: linear-gradient(135deg, rgba(124,92,252,0.3), rgba(92,138,252,0.2)); }

/* Avatar upload */
.av-upload {
  width: 72px; height: 72px; border-radius: 50%;
  border: 2px dashed var(--border2); cursor: pointer;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  font-size: 11px; color: var(--text3); gap: 4px; transition: all 0.15s;
}
.av-upload:hover { border-color: var(--accent); color: var(--accent); }
.av-upload .icon { font-size: 22px; }

/* Toggle */
.toggle-list { display: flex; flex-direction: column; }
.toggle-row { display: flex; align-items: center; justify-content: space-between; padding: 13px 0; border-bottom: 1px solid var(--border); }
.toggle-row:last-child { border-bottom: none; }
.toggle-info h4 { font-size: 14px; font-weight: 500; }
.toggle-info p { font-size: 12px; color: var(--text3); margin-top: 2px; }
.toggle-switch {
  width: 42px; height: 24px; background: var(--bg5); border-radius: 20px;
  position: relative; cursor: pointer; border: none; flex-shrink: 0; transition: background 0.2s;
}
.toggle-switch.on { background: var(--accent); }
.toggle-switch::after {
  content: ''; position: absolute; width: 18px; height: 18px;
  background: #fff; border-radius: 50%; top: 3px; left: 3px; transition: transform 0.2s;
}
.toggle-switch.on::after { transform: translateX(18px); }

/* Discord connect */
.discord-connect {
  background: rgba(88,101,242,0.08); border: 1px solid rgba(88,101,242,0.22);
  border-radius: var(--r); padding: 24px; text-align: center;
}
.discord-connect h3 { font-size: 17px; font-weight: 600; margin-bottom: 7px; }
.discord-connect p { font-size: 13px; color: var(--text3); margin-bottom: 18px; line-height: 1.5; }
.discord-connected { display: flex; align-items: center; gap: 12px; background: rgba(88,101,242,0.08); border: 1px solid rgba(88,101,242,0.2); border-radius: var(--r2); padding: 14px; }
.dc-av { width: 44px; height: 44px; border-radius: 50%; background: #5865f2; display: flex; align-items: center; justify-content: center; font-family: 'Syne', sans-serif; font-size: 16px; font-weight: 700; color: #fff; }
.dc-info { flex: 1; }
.dc-name { font-size: 14px; font-weight: 600; }
.dc-handle { font-size: 12px; color: var(--text3); font-family: monospace; }
.dc-badges { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 6px; }

/* Profile link box */
.profile-link-box { background: var(--bg3); border: 1px solid var(--border); border-radius: var(--r2); padding: 14px 16px; display: flex; align-items: center; gap: 12px; }
.plb-url { flex: 1; font-size: 14px; font-family: monospace; color: var(--accent); }
.copy-btn { padding: 7px 16px; background: rgba(124,92,252,0.13); border: 1px solid rgba(124,92,252,0.3); color: var(--accent); border-radius: var(--r2); font-size: 13px; font-weight: 600; cursor: pointer; transition: all 0.15s; }
.copy-btn:hover { background: var(--accent); color: #fff; border-color: var(--accent); }

/* Stats row */
.stats-row { display: grid; grid-template-columns: repeat(4,1fr); gap: 14px; }
.stat-card { background: var(--bg3); border-radius: var(--r2); padding: 16px; text-align: center; }
.sc-val { font-family: 'Syne', sans-serif; font-size: 24px; font-weight: 700; }
.sc-lbl { font-size: 12px; color: var(--text3); margin-top: 3px; }
.sc-trend { font-size: 11px; color: var(--green); margin-top: 4px; }

/* ===========================
   MODAL
   =========================== */
.modal-overlay {
  position: fixed; inset: 0; z-index: 800;
  background: rgba(0,0,0,0.72); backdrop-filter: blur(6px);
  display: flex; align-items: center; justify-content: center; padding: 20px;
}
.modal-overlay.hidden { display: none; }
.modal {
  background: var(--bg2); border: 1px solid var(--border2);
  border-radius: var(--r4); padding: 32px; max-width: 500px; width: 100%;
  position: relative; animation: modalIn 0.22s ease;
}
@keyframes modalIn { from { opacity:0; transform:scale(0.94) translateY(10px); } to { opacity:1; transform:scale(1) translateY(0); } }
.modal-close { position: absolute; top: 18px; right: 18px; background: transparent; border: none; color: var(--text3); font-size: 22px; cursor: pointer; line-height: 1; padding: 4px; transition: color 0.15s; }
.modal-close:hover { color: var(--text); }
.modal-title { font-family: 'Syne', sans-serif; font-size: 22px; font-weight: 700; margin-bottom: 6px; }
.modal-sub { font-size: 14px; color: var(--text3); margin-bottom: 26px; line-height: 1.5; }
.modal-steps { display: flex; gap: 8px; margin-bottom: 24px; }
.mstep { flex: 1; height: 3px; border-radius: 3px; background: var(--border2); transition: background 0.3s; }
.mstep.done { background: var(--accent); }

/* ===========================
   TOAST
   =========================== */
.toast {
  position: fixed; bottom: 28px; right: 28px; z-index: 9000;
  background: var(--bg3); border: 1px solid var(--green);
  color: var(--green); padding: 13px 22px; border-radius: var(--r2);
  font-size: 14px; font-weight: 500;
  transform: translateY(80px); opacity: 0; transition: all 0.3s ease;
  box-shadow: 0 12px 40px rgba(0,0,0,0.45);
  display: flex; align-items: center; gap: 8px;
}
.toast.show { transform: translateY(0); opacity: 1; }

/* ===========================
   RESPONSIVE
   =========================== */
@media (max-width: 900px) {
  .feed-layout, .dash-layout, .news-featured, .about-grid { grid-template-columns: 1fr; }
  .news-featured-thumb { height: 180px; }
  .dash-sidebar { position: static; display: flex; overflow-x: auto; gap: 4px; padding: 10px; }
  .dash-nav-item { white-space: nowrap; flex-shrink: 0; }
  .dash-nav-divider { display: none; }
  .profile-stats { grid-template-columns: repeat(2,1fr); }
  .stats-row { grid-template-columns: repeat(2,1fr); }
  .portfolio-grid { grid-template-columns: 1fr; }
}
@media (max-width: 640px) {
  #main-nav { padding: 0 16px; }
  .nav-links { display: none; }
  .hero-h1 { letter-spacing: -1.5px; }
  .hero-stats { flex-direction: column; align-items: center; }
  .stat { border-right: none; border-bottom: 1px solid var(--border); padding: 16px 0; width: 100%; }
  .stat:last-child { border-bottom: none; }
  .f-row { grid-template-columns: 1fr; }
  .market-grid { grid-template-columns: 1fr; }
}
</style>
</head>
<body>

<!-- ===== LOADING SCREEN ===== -->
<div id="loading-screen">
  <div class="load-logo">V</div>
  <div class="load-name">vouch.gg</div>
  <div class="load-bar-wrap"><div class="load-bar"></div></div>
  <div class="load-tagline">Your identity, fully vouched.</div>
</div>

<!-- ===== NAVIGATION ===== -->
<nav id="main-nav">
  <div class="nav-left">
    <div class="nav-brand" onclick="showPage('home')">
      <div class="nav-logomark">V</div>
      <span class="nav-wordmark">vouch.gg</span>
    </div>
    <div class="nav-links">
      <button class="nav-link active" onclick="showPage('home',this)">Home</button>
      <button class="nav-link" onclick="showPage('feed',this)">Feed</button>
      <button class="nav-link" onclick="showPage('market',this)">Market</button>
      <button class="nav-link" onclick="showPage('news',this)">News</button>
      <button class="nav-link" onclick="showPage('profile',this)">Profile</button>
      <button class="nav-link" onclick="showPage('dashboard',this)">Dashboard</button>
    </div>
  </div>
  <div class="nav-right">
    <button class="btn btn-ghost" onclick="openModal()">Create Profile</button>
    <button class="btn btn-primary" onclick="showPage('dashboard',null)">Dashboard</button>
  </div>
</nav>

<!-- ======================================================
     PAGE: HOME
     ====================================================== -->
<div id="page-home" class="page active">
  <div class="hero">
    <div class="hero-glow"></div>
    <h1 class="hero-h1">Your identity,<br><span class="grad">fully vouched.</span></h1>
    <p class="hero-sub">The ultimate profile platform for builders, creators and communities. Link Discord, showcase your work, build a reputation that means something.</p>
    <div class="hero-ctas">
      <button class="btn btn-primary btn-lg" onclick="openModal()">Create Your Profile</button>
      <button class="btn btn-ghost btn-lg" onclick="showPage('profile',null)">View Example Profile</button>
    </div>
    <div class="hero-stats">
      <div class="stat"><div class="stat-n">48K+</div><div class="stat-l">Active Profiles</div></div>
      <div class="stat"><div class="stat-n">1.2M</div><div class="stat-l">Profile Views</div></div>
      <div class="stat"><div class="stat-n">320K</div><div class="stat-l">Discord Linked</div></div>
      <div class="stat"><div class="stat-n">12K</div><div class="stat-l">Verified Members</div></div>
    </div>
  </div>
  <div class="wrap">
    <div class="claim-box">
      <h2>Get your vouch.gg link</h2>
      <p>Share your profile in Discord bios, Twitter, Reddit — anywhere you want to be found.</p>
      <div class="claim-row">
        <div class="claim-prefix">vouch.gg/</div>
        <input class="claim-input" id="claim-input" placeholder="yourname" type="text">
        <button class="btn btn-primary" onclick="claimUsername()">Claim →</button>
      </div>
    </div>
    <div class="section">
      <div class="section-title">Featured <span>Profiles</span></div>
      <div class="fp-row">
        <div class="fp-card" onclick="showPage('profile',null)">
          <div class="fp-av" style="background:linear-gradient(135deg,#7c5cfc,#5c8afc)">Z</div>
          <div class="fp-name">zeraph <span class="badge badge-verified" title="Verified">✓</span></div>
          <div class="fp-handle">#1234 · Developer</div>
          <div class="fp-badge"><span class="tag tag-purple">Top Creator</span></div>
        </div>
        <div class="fp-card">
          <div class="fp-av" style="background:linear-gradient(135deg,#fc5c8a,#ffc857)">N</div>
          <div class="fp-name">nxva <span class="badge badge-verified" title="Verified">✓</span></div>
          <div class="fp-handle">#5678 · Designer</div>
          <div class="fp-badge"><span class="tag tag-pink">Trending</span></div>
        </div>
        <div class="fp-card">
          <div class="fp-av" style="background:linear-gradient(135deg,#4ade80,#5c8afc)">K</div>
          <div class="fp-name">kxli</div>
          <div class="fp-handle">#9012 · Artist</div>
          <div class="fp-badge"><span class="tag tag-green">Rising</span></div>
        </div>
        <div class="fp-card">
          <div class="fp-av" style="background:linear-gradient(135deg,#ff73fa,#7c5cfc)">V</div>
          <div class="fp-name">vexed <span class="badge badge-verified" title="Verified">✓</span></div>
          <div class="fp-handle">#3456 · Music</div>
          <div class="fp-badge"><span class="tag tag-nitro">Featured</span></div>
        </div>
        <div class="fp-card">
          <div class="fp-av" style="background:linear-gradient(135deg,#ffc857,#fc5c8a)">R</div>
          <div class="fp-name">rxven</div>
          <div class="fp-handle">#7890 · Gamer</div>
          <div class="fp-badge"><span class="tag tag-gold">New</span></div>
        </div>
        <div class="fp-card">
          <div class="fp-av" style="background:linear-gradient(135deg,#5c8afc,#4ade80)">M</div>
          <div class="fp-name">mirel <span class="badge badge-verified" title="Verified">✓</span></div>
          <div class="fp-handle">#2211 · Writer</div>
          <div class="fp-badge"><span class="tag tag-blue">Popular</span></div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ======================================================
     PAGE: FEED
     ====================================================== -->
<div id="page-feed" class="page">
  <div class="wrap section">
    <div class="section-title">Community <span>Feed</span></div>
    <div class="feed-layout">
      <div class="feed-posts">

        <!-- New post input -->
        <div class="new-post-box">
          <div class="new-post-row">
            <div class="np-av">Y</div>
            <div class="np-inner">
              <textarea class="np-textarea" id="np-text" placeholder="Share something with the community..."></textarea>
              <div class="np-footer">
                <div class="np-emojis">
                  <span class="np-emoji" onclick="addEmoji('🔥')">🔥</span>
                  <span class="np-emoji" onclick="addEmoji('💜')">💜</span>
                  <span class="np-emoji" onclick="addEmoji('🎉')">🎉</span>
                  <span class="np-emoji" onclick="addEmoji('👏')">👏</span>
                  <span class="np-emoji" onclick="addEmoji('💯')">💯</span>
                </div>
                <button class="btn btn-primary btn-sm" onclick="submitPost()">Post</button>
              </div>
            </div>
          </div>
        </div>

        <!-- Official post -->
        <div class="post-card official">
          <div class="post-header">
            <div class="post-av" style="background:linear-gradient(135deg,var(--accent),var(--accent2));font-size:13px;font-weight:800">V</div>
            <div class="post-meta">
              <div class="post-name">
                vouch.gg
                <span class="badge badge-official" title="Official">★</span>
                <span class="tag tag-gold" style="font-size:10px;padding:2px 7px">Official</span>
              </div>
              <div class="post-time">2 hours ago</div>
            </div>
          </div>
          <div class="post-body">🚀 <strong>Big update dropping this week!</strong> We're launching Portfolio 2.0 with full drag-and-drop customization, new badge types in the Market, and enhanced Discord integration. Stay tuned for the changelog!</div>
          <div class="reactions">
            <div class="reaction active" onclick="toggleReaction(this)"><span class="emoji">🔥</span> <span class="rc">241</span></div>
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">💜</span> <span class="rc">189</span></div>
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">🎉</span> <span class="rc">97</span></div>
          </div>
        </div>

        <!-- User posts -->
        <div class="post-card">
          <div class="post-header">
            <div class="post-av" style="background:linear-gradient(135deg,#7c5cfc,#5c8afc)">Z</div>
            <div class="post-meta">
              <div class="post-name">zeraph <span class="badge badge-verified">✓</span></div>
              <div class="post-time">5 hours ago</div>
            </div>
          </div>
          <div class="post-body">Just redesigned my portfolio section completely. If you haven't set yours up yet — do it now. It genuinely gets you clients. My profile link is in my Discord bio 🔗</div>
          <div class="reactions">
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">👏</span> <span class="rc">56</span></div>
            <div class="reaction active" onclick="toggleReaction(this)"><span class="emoji">💯</span> <span class="rc">34</span></div>
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">🔥</span> <span class="rc">28</span></div>
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">❤️</span> <span class="rc">19</span></div>
          </div>
        </div>

        <div class="post-card">
          <div class="post-header">
            <div class="post-av" style="background:linear-gradient(135deg,#fc5c8a,#ffc857)">N</div>
            <div class="post-meta">
              <div class="post-name">nxva <span class="badge badge-verified">✓</span></div>
              <div class="post-time">8 hours ago</div>
            </div>
          </div>
          <div class="post-body">The new market items are insane. Just copped the animated banner effect and my profile looks completely different now. 100% worth it 👌</div>
          <div class="reactions">
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">🔥</span> <span class="rc">72</span></div>
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">😮</span> <span class="rc">45</span></div>
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">💜</span> <span class="rc">31</span></div>
          </div>
        </div>

        <div class="post-card">
          <div class="post-header">
            <div class="post-av" style="background:linear-gradient(135deg,#4ade80,#5c8afc)">K</div>
            <div class="post-meta">
              <div class="post-name">kxli</div>
              <div class="post-time">1 day ago</div>
            </div>
          </div>
          <div class="post-body">Just hit 1000 profile views this month 🎉 Started with vouch.gg 3 weeks ago. It's already bringing way more traffic than my old linktree. The Discord integration is the 🔑</div>
          <div class="reactions">
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">🎉</span> <span class="rc">103</span></div>
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">🔥</span> <span class="rc">88</span></div>
            <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">👏</span> <span class="rc">67</span></div>
          </div>
        </div>

        <div id="feed-dynamic"></div>

      </div>

      <!-- Feed sidebar -->
      <div class="feed-sidebar">
        <div class="sidebar-card">
          <div class="sidebar-title">What's New</div>
          <div class="update-item">
            <h4>Portfolio 2.0 Beta</h4>
            <p>Drag-and-drop portfolio builder now in beta testing.</p>
            <div class="date">Apr 18, 2026</div>
          </div>
          <div class="update-item">
            <h4>New Market Items</h4>
            <p>8 new badge types and 3 animated banners added.</p>
            <div class="date">Apr 15, 2026</div>
          </div>
          <div class="update-item">
            <h4>Discord Boost Display</h4>
            <p>Nitro & boost status now auto-syncs to your profile.</p>
            <div class="date">Apr 10, 2026</div>
          </div>
          <div class="update-item">
            <h4>Music Integration</h4>
            <p>Add Spotify tracks to play on your profile page.</p>
            <div class="date">Apr 5, 2026</div>
          </div>
        </div>
        <div class="sidebar-card">
          <div class="sidebar-title">Online Now</div>
          <div class="online-row">
            <div class="online-dot"></div>
            <div class="online-name">zeraph</div>
            <div class="online-tag">Developer</div>
          </div>
          <div class="online-row">
            <div class="online-dot"></div>
            <div class="online-name">nxva</div>
            <div class="online-tag">Designer</div>
          </div>
          <div class="online-row">
            <div class="online-dot" style="background:#ffc857;box-shadow:0 0 6px #ffc857"></div>
            <div class="online-name">vexed</div>
            <div class="online-tag">Away</div>
          </div>
          <div class="online-row">
            <div class="online-dot"></div>
            <div class="online-name">rxven</div>
            <div class="online-tag">Gamer</div>
          </div>
          <div class="online-row">
            <div class="online-dot"></div>
            <div class="online-name">mirel</div>
            <div class="online-tag">Writer</div>
          </div>
        </div>
        <div class="sidebar-card">
          <div class="sidebar-title">Trending Tags</div>
          <div style="display:flex;flex-wrap:wrap;gap:7px">
            <span class="tag tag-purple">#portfolio</span>
            <span class="tag tag-blue">#discord</span>
            <span class="tag tag-green">#dev</span>
            <span class="tag tag-pink">#design</span>
            <span class="tag tag-gold">#verified</span>
            <span class="tag tag-nitro">#nitro</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ======================================================
     PAGE: MARKET
     ====================================================== -->
<div id="page-market" class="page">
  <div class="wrap section">
    <div class="section-title">Profile <span>Market</span></div>
    <div class="market-filters">
      <button class="market-filter active" onclick="filterMarket(this,'all')">All Items</button>
      <button class="market-filter" onclick="filterMarket(this,'badges')">Badges</button>
      <button class="market-filter" onclick="filterMarket(this,'banners')">Banners</button>
      <button class="market-filter" onclick="filterMarket(this,'effects')">Effects</button>
      <button class="market-filter" onclick="filterMarket(this,'music')">Music</button>
    </div>
    <div class="market-grid">
      <div class="market-card" data-cat="badges">
        <div class="market-card-badge"><span class="tag tag-gold" style="font-size:10px;padding:2px 8px">Popular</span></div>
        <div class="market-icon mi-gold">✓</div>
        <div class="market-name">Verified Badge</div>
        <div class="market-desc">A gold checkmark displayed next to your username across all of vouch.gg.</div>
        <div class="market-footer">
          <div class="market-price">800 VC</div>
          <button class="market-buy" onclick="buyItem(this,'Verified Badge')">Buy</button>
        </div>
      </div>
      <div class="market-card" data-cat="banners">
        <div class="market-card-badge"><span class="tag tag-pink" style="font-size:10px;padding:2px 8px">New</span></div>
        <div class="market-icon mi-pink">🌊</div>
        <div class="market-name">Animated Banner</div>
        <div class="market-desc">A smooth animated gradient banner for your profile — 5 colour themes included.</div>
        <div class="market-footer">
          <div class="market-price">500 VC</div>
          <button class="market-buy" onclick="buyItem(this,'Animated Banner')">Buy</button>
        </div>
      </div>
      <div class="market-card" data-cat="effects">
        <div class="market-icon mi-purple">✨</div>
        <div class="market-name">Sparkle Effect</div>
        <div class="market-desc">Particle sparkles that float around your avatar on your public profile page.</div>
        <div class="market-footer">
          <div class="market-price">350 VC</div>
          <button class="market-buy" onclick="buyItem(this,'Sparkle Effect')">Buy</button>
        </div>
      </div>
      <div class="market-card" data-cat="badges">
        <div class="market-icon mi-blue">🛡️</div>
        <div class="market-name">Early Adopter Badge</div>
        <div class="market-desc">Show you were here from the start. Limited edition — only 5,000 available.</div>
        <div class="market-footer">
          <div class="market-price">1,200 VC</div>
          <button class="market-buy" onclick="buyItem(this,'Early Adopter Badge')">Buy</button>
        </div>
      </div>
      <div class="market-card" data-cat="music">
        <div class="market-card-badge"><span class="tag tag-green" style="font-size:10px;padding:2px 8px">Hot</span></div>
        <div class="market-icon mi-green">🎵</div>
        <div class="market-name">Music Widget Pro</div>
        <div class="market-desc">Display a custom music player with Spotify integration and full track controls.</div>
        <div class="market-footer">
          <div class="market-price">600 VC</div>
          <button class="market-buy" onclick="buyItem(this,'Music Widget Pro')">Buy</button>
        </div>
      </div>
      <div class="market-card" data-cat="effects">
        <div class="market-icon mi-purple">🌈</div>
        <div class="market-name">Gradient Username</div>
        <div class="market-desc">Your display name shows with a custom colour gradient across your entire profile.</div>
        <div class="market-footer">
          <div class="market-price">450 VC</div>
          <button class="market-buy" onclick="buyItem(this,'Gradient Username')">Buy</button>
        </div>
      </div>
      <div class="market-card" data-cat="banners">
        <div class="market-icon mi-blue">🌌</div>
        <div class="market-name">Galaxy Banner</div>
        <div class="market-desc">A deep space animated banner with twinkling stars and nebula effects.</div>
        <div class="market-footer">
          <div class="market-price">700 VC</div>
          <button class="market-buy" onclick="buyItem(this,'Galaxy Banner')">Buy</button>
        </div>
      </div>
      <div class="market-card" data-cat="badges">
        <div class="market-icon mi-gold">💎</div>
        <div class="market-name">Premium Badge</div>
        <div class="market-desc">A diamond-tier badge showing you're a premium vouch.gg member.</div>
        <div class="market-footer">
          <div class="market-price">2,500 VC</div>
          <button class="market-buy" onclick="buyItem(this,'Premium Badge')">Buy</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ======================================================
     PAGE: NEWS
     ====================================================== -->
<div id="page-news" class="page">
  <div class="wrap section">
    <div class="section-title">Latest <span>News</span></div>

    <!-- Featured news -->
    <div class="news-featured" onclick="">
      <div class="news-featured-thumb">🚀</div>
      <div class="news-featured-body">
        <div style="display:flex;align-items:center;gap:8px">
          <span class="news-label nl-announce">Announcement</span>
          <div class="official-news-author">
            <div class="official-av">V</div>
            vouch.gg Team
            <span class="badge badge-official" title="Official">★</span>
          </div>
        </div>
        <div class="news-featured-title">Portfolio 2.0: Build the Profile You Actually Deserve</div>
        <div class="news-featured-excerpt">We've rebuilt the portfolio system from scratch. Full drag-and-drop, custom sections, embedded media, and a completely new visual editor. Coming this week.</div>
        <div class="news-featured-meta">
          <span>Apr 18, 2026</span>
          <span>·</span>
          <span>3 min read</span>
        </div>
      </div>
    </div>

    <div class="news-grid">
      <div class="news-card">
        <div class="news-thumb">🛒</div>
        <div class="news-body">
          <div style="display:flex;align-items:center;gap:6px"><span class="news-label nl-feature">Feature</span><div class="official-news-author"><div class="official-av" style="width:16px;height:16px;font-size:7px">V</div>Official <span class="badge badge-official" style="width:13px;height:13px;font-size:7px">★</span></div></div>
          <div class="news-title">8 New Market Items Just Dropped</div>
          <div class="news-excerpt">From animated banners to exclusive badges — the biggest market update yet is here.</div>
          <div class="news-date">Apr 15, 2026</div>
        </div>
      </div>
      <div class="news-card">
        <div class="news-thumb">🎮</div>
        <div class="news-body">
          <span class="news-label nl-update">Update</span>
          <div class="news-title">Discord Boost Status Now Syncs to Profiles</div>
          <div class="news-excerpt">If you boost a server, it now automatically shows on your vouch profile.</div>
          <div class="news-date">Apr 10, 2026</div>
        </div>
      </div>
      <div class="news-card">
        <div class="news-thumb">🎵</div>
        <div class="news-body">
          <span class="news-label nl-feature">Feature</span>
          <div class="news-title">Add Music to Your Profile</div>
          <div class="news-excerpt">The new music widget lets visitors hear what you're listening to right on your page.</div>
          <div class="news-date">Apr 5, 2026</div>
        </div>
      </div>
      <div class="news-card">
        <div class="news-thumb">🔒</div>
        <div class="news-body">
          <span class="news-label nl-update">Update</span>
          <div class="news-title">Security & Privacy Controls Update</div>
          <div class="news-excerpt">New granular privacy settings for exactly what appears publicly on your profile.</div>
          <div class="news-date">Mar 28, 2026</div>
        </div>
      </div>
      <div class="news-card">
        <div class="news-thumb">📊</div>
        <div class="news-body">
          <span class="news-label nl-feature">Feature</span>
          <div class="news-title">Profile Analytics Dashboard</div>
          <div class="news-excerpt">See who's viewing your profile, where they're coming from, and what they click.</div>
          <div class="news-date">Mar 20, 2026</div>
        </div>
      </div>
      <div class="news-card">
        <div class="news-thumb">🌍</div>
        <div class="news-body">
          <span class="news-label nl-announce">Announcement</span>
          <div class="news-title">vouch.gg Hits 40,000 Profiles</div>
          <div class="news-excerpt">A huge thank you to every person who has vouched. We're just getting started.</div>
          <div class="news-date">Mar 15, 2026</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ======================================================
     PAGE: PROFILE (Example Public Profile)
     ====================================================== -->
<div id="page-profile" class="page">
  <div class="wrap section">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:16px">
      <div class="section-title" style="margin-bottom:0">Public <span>Profile</span></div>
      <div style="display:flex;gap:8px">
        <button class="btn btn-ghost btn-sm" onclick="copyProfileLink()">Copy Profile Link 🔗</button>
        <button class="btn btn-primary btn-sm" onclick="showPage('dashboard',null)">Edit Profile →</button>
      </div>
    </div>

    <div class="profile-outer">
      <div class="profile-banner">
        <div class="profile-banner-overlay"></div>
      </div>

      <div class="profile-info-wrap">
        <div class="profile-avatar-wrap">
          <div class="profile-avatar">Z</div>
        </div>
        <div class="profile-name-row">
          <div class="profile-name">zeraph</div>
          <span class="badge badge-verified" title="Verified">✓</span>
          <span class="tag tag-gold" style="font-size:10px;padding:2px 8px">Early Adopter</span>
          <span class="tag tag-purple" style="font-size:10px;padding:2px 8px">Top Creator</span>
        </div>
        <div class="profile-handle">@zeraph#1234 · Joined vouch.gg Feb 2026</div>
        <div class="profile-bio">Full-stack developer & open source enthusiast. Building things people actually use. TypeScript, Rust, Go. Open to freelance work — check my portfolio.</div>
        <div class="profile-tags-row">
          <span class="tag tag-purple">Developer</span>
          <span class="tag tag-blue">Open Source</span>
          <span class="tag tag-green">Freelance</span>
        </div>
        <div class="profile-discord-row">
          <div class="discord-link-badge">
            <div class="discord-icon">D</div>
            <span>zeraph#1234</span>
          </div>
          <span class="tag tag-nitro">✨ Nitro</span>
          <span class="tag tag-nitro">🚀 Server Booster</span>
        </div>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn btn-primary btn-sm">Message</button>
          <button class="btn btn-ghost btn-sm">Follow</button>
          <button class="btn btn-ghost btn-sm" onclick="showProfileTab('portfolio')">Portfolio →</button>
        </div>
      </div>

      <div class="profile-stats">
        <div class="pstat"><div class="pstat-val">1.2K</div><div class="pstat-lbl">Profile Views</div></div>
        <div class="pstat"><div class="pstat-val">342</div><div class="pstat-lbl">Followers</div></div>
        <div class="pstat"><div class="pstat-val">3</div><div class="pstat-lbl">Servers Owns</div></div>
        <div class="pstat"><div class="pstat-val">Aug '21</div><div class="pstat-lbl">On Discord</div></div>
      </div>

      <div class="profile-tabs">
        <button class="ptab active" onclick="showProfileTab('about',this)">About</button>
        <button class="ptab" onclick="showProfileTab('posts',this)">Posts</button>
        <button class="ptab" onclick="showProfileTab('portfolio',this)">Portfolio</button>
        <button class="ptab" onclick="showProfileTab('servers',this)">Servers</button>
      </div>

      <div class="profile-tab-content">

        <!-- ABOUT TAB -->
        <div class="tab-pane active" id="tab-about">
          <div class="music-player">
            <div class="music-thumb">🎵</div>
            <div class="music-info">
              <div class="music-title">Blinding Lights</div>
              <div class="music-artist">The Weeknd</div>
              <div class="music-bar-wrap"><div class="music-bar-fill"></div></div>
            </div>
            <div class="music-controls">
              <button class="mc-btn">⏮</button>
              <button class="mc-btn play">▶</button>
              <button class="mc-btn">⏭</button>
            </div>
          </div>
          <div class="about-grid">
            <div class="about-item"><h4>Discord Username</h4><p>zeraph#1234</p></div>
            <div class="about-item"><h4>Joined Discord</h4><p>August 2021</p></div>
            <div class="about-item"><h4>Joined vouch.gg</h4><p>February 2026</p></div>
            <div class="about-item"><h4>Discord Nitro</h4><p>✨ Active since Jan 2023</p></div>
            <div class="about-item"><h4>Servers Owns</h4><p>3 servers · 8,400 total members</p></div>
            <div class="about-item"><h4>Servers In</h4><p>24 servers</p></div>
          </div>
        </div>

        <!-- POSTS TAB -->
        <div class="tab-pane" id="tab-posts">
          <div style="display:flex;flex-direction:column;gap:12px">
            <div class="post-card" style="margin:0;border-color:var(--border)">
              <div class="post-body" style="margin-bottom:12px">Just redesigned my portfolio section completely. If you haven't set yours up yet — do it now. It genuinely gets you clients.</div>
              <div class="reactions">
                <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">👏</span> <span class="rc">56</span></div>
                <div class="reaction active" onclick="toggleReaction(this)"><span class="emoji">💯</span> <span class="rc">34</span></div>
              </div>
            </div>
            <div class="post-card" style="margin:0;border-color:var(--border)">
              <div class="post-body" style="margin-bottom:12px">Working on a new open source project — a Discord bot framework in Rust. Star it when it drops 🦀</div>
              <div class="reactions">
                <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">🔥</span> <span class="rc">88</span></div>
                <div class="reaction" onclick="toggleReaction(this)"><span class="emoji">❤️</span> <span class="rc">43</span></div>
              </div>
            </div>
          </div>
        </div>

        <!-- PORTFOLIO TAB -->
        <div class="tab-pane" id="tab-portfolio">
          <div class="portfolio-grid">
            <div class="portfolio-item">
              <div class="portfolio-thumb" style="background:linear-gradient(135deg,rgba(124,92,252,0.15),rgba(92,138,252,0.1))">💻</div>
              <div class="portfolio-info">
                <div class="portfolio-name">DevPanel SaaS</div>
                <div class="portfolio-type">Web App · TypeScript</div>
              </div>
            </div>
            <div class="portfolio-item">
              <div class="portfolio-thumb" style="background:linear-gradient(135deg,rgba(74,222,128,0.1),rgba(92,138,252,0.1))">🤖</div>
              <div class="portfolio-info">
                <div class="portfolio-name">Blade Discord Bot</div>
                <div class="portfolio-type">Open Source · Rust</div>
              </div>
            </div>
            <div class="portfolio-item">
              <div class="portfolio-thumb" style="background:linear-gradient(135deg,rgba(252,92,138,0.1),rgba(255,200,87,0.08))">📱</div>
              <div class="portfolio-info">
                <div class="portfolio-name">Notify Mobile App</div>
                <div class="portfolio-type">iOS / Android · React Native</div>
              </div>
            </div>
            <div class="portfolio-item">
              <div class="portfolio-thumb" style="background:linear-gradient(135deg,rgba(255,200,87,0.1),rgba(252,92,138,0.08))">🌐</div>
              <div class="portfolio-info">
                <div class="portfolio-name">Personal Website</div>
                <div class="portfolio-type">Website · Next.js</div>
              </div>
            </div>
          </div>
        </div>

        <!-- SERVERS TAB -->
        <div class="tab-pane" id="tab-servers">
          <div class="server-list">
            <div class="server-item">
              <div class="server-icon" style="background:rgba(124,92,252,0.15)">⚡</div>
              <div class="server-info">
                <div class="server-name">DevZone HQ</div>
                <div class="server-members">4,200 members</div>
              </div>
              <span class="server-owner-badge">Owner</span>
            </div>
            <div class="server-item">
              <div class="server-icon" style="background:rgba(74,222,128,0.12)">🌱</div>
              <div class="server-info">
                <div class="server-name">Open Source Builders</div>
                <div class="server-members">3,100 members</div>
              </div>
              <span class="server-owner-badge">Owner</span>
            </div>
            <div class="server-item">
              <div class="server-icon" style="background:rgba(92,138,252,0.15)">🛠️</div>
              <div class="server-info">
                <div class="server-name">Rust & Chill</div>
                <div class="server-members">1,100 members</div>
              </div>
              <span class="server-owner-badge">Owner</span>
            </div>
            <div class="server-item">
              <div class="server-icon" style="background:rgba(255,200,87,0.1)">🏆</div>
              <div class="server-info">
                <div class="server-name">TypeScript Alliance</div>
                <div class="server-members">22,000 members</div>
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</div>

<!-- ======================================================
     PAGE: DASHBOARD
     ====================================================== -->
<div id="page-dashboard" class="page">
  <div class="wrap section">
    <div class="section-title">Your <span>Dashboard</span></div>

    <!-- Stats row -->
    <div class="stats-row" style="margin-bottom:22px">
      <div class="stat-card"><div class="sc-val" style="color:var(--accent)">1,247</div><div class="sc-lbl">Profile Views</div><div class="sc-trend">↑ 18% this week</div></div>
      <div class="stat-card"><div class="sc-val" style="color:var(--green)">342</div><div class="sc-lbl">Followers</div><div class="sc-trend">↑ 12 today</div></div>
      <div class="stat-card"><div class="sc-val" style="color:var(--gold)">1,850</div><div class="sc-lbl">VC Balance</div><div class="sc-trend">Earned 200 this week</div></div>
      <div class="stat-card"><div class="sc-val" style="color:var(--accent2)">94</div><div class="sc-lbl">Link Clicks</div><div class="sc-trend">↑ 7% this week</div></div>
    </div>

    <div class="dash-layout">
      <!-- Dash sidebar nav -->
      <div class="dash-sidebar">
        <button class="dash-nav-item active" onclick="showDashPane('appearance',this)"><span class="dni">🎨</span> Appearance</button>
        <button class="dash-nav-item" onclick="showDashPane('profile',this)"><span class="dni">👤</span> Profile Info</button>
        <button class="dash-nav-item" onclick="showDashPane('discord',this)"><span class="dni">💬</span> Discord</button>
        <button class="dash-nav-item" onclick="showDashPane('music',this)"><span class="dni">🎵</span> Music</button>
        <button class="dash-nav-item" onclick="showDashPane('portfolio',this)"><span class="dni">💼</span> Portfolio</button>
        <div class="dash-nav-divider"></div>
        <button class="dash-nav-item" onclick="showDashPane('privacy',this)"><span class="dni">🔒</span> Privacy</button>
        <button class="dash-nav-item" onclick="showDashPane('link',this)"><span class="dni">🔗</span> Profile Link</button>
      </div>

      <!-- Dash content -->
      <div class="dash-content">

        <!-- APPEARANCE PANE -->
        <div class="dash-pane active" id="dpane-appearance">
          <div class="dcard">
            <div class="dcard-title"><span class="icon">🖼️</span> Banner</div>
            <div class="banner-prev" id="banner-preview" onclick="changeBanner()">
              <div class="banner-prev-overlay"></div>
            </div>
            <div class="f-label" style="margin-bottom:8px">Banner Colour Theme</div>
            <div class="swatches">
              <div class="swatch active" style="background:linear-gradient(135deg,#120a2e,#0a1535)" onclick="setBanner(this,'linear-gradient(135deg,#120a2e,#0a1535,#0e2518)')"></div>
              <div class="swatch" style="background:linear-gradient(135deg,#2a0a1a,#1a0a2a)" onclick="setBanner(this,'linear-gradient(135deg,#2a0a1a,#1a0a2a,#2a1a0a)')"></div>
              <div class="swatch" style="background:linear-gradient(135deg,#0a2a1a,#0a1a2a)" onclick="setBanner(this,'linear-gradient(135deg,#0a2a1a,#0a1a2a)')"></div>
              <div class="swatch" style="background:linear-gradient(135deg,#1a1a0a,#2a1a0a)" onclick="setBanner(this,'linear-gradient(135deg,#1a1a0a,#2a0a1a)')"></div>
              <div class="swatch" style="background:linear-gradient(135deg,#0a0a2a,#1a0a3a)" onclick="setBanner(this,'linear-gradient(135deg,#0a0a2a,#1a0a3a,#0a1a2a)')"></div>
              <div class="swatch" style="background:linear-gradient(135deg,#1a0a0a,#2a1a1a)" onclick="setBanner(this,'linear-gradient(135deg,#1a0a0a,#2a0a0a)')"></div>
            </div>
          </div>
          <div class="dcard">
            <div class="dcard-title"><span class="icon">🖼️</span> Avatar</div>
            <div style="display:flex;align-items:center;gap:16px">
              <div class="profile-avatar" style="width:72px;height:72px;font-size:24px;border:none">Z</div>
              <div class="av-upload" onclick="showToast('📸 Image upload coming soon!')">
                <span class="icon">📷</span>
                <span>Upload</span>
              </div>
              <div style="font-size:13px;color:var(--text3);line-height:1.5">PNG, JPG or GIF.<br>Max 4MB. Square recommended.</div>
            </div>
          </div>
        </div>

        <!-- PROFILE INFO PANE -->
        <div class="dash-pane" id="dpane-profile">
          <div class="dcard">
            <div class="dcard-title"><span class="icon">✏️</span> Profile Info</div>
            <div class="f-field">
              <label class="f-label">Username (from Discord — auto set)</label>
              <input class="f-input readonly" value="zeraph#1234" readonly>
              <div class="f-hint">Your username is your Discord username and cannot be changed here.</div>
            </div>
            <div class="f-row">
              <div class="f-field" style="margin:0">
                <label class="f-label">Display Name</label>
                <input class="f-input" value="zeraph" placeholder="How your name displays">
              </div>
              <div class="f-field" style="margin:0">
                <label class="f-label">Pronouns</label>
                <input class="f-input" value="he/him" placeholder="Optional">
              </div>
            </div>
            <div class="f-field">
              <label class="f-label">Bio</label>
              <textarea class="f-input">Full-stack developer & open source enthusiast. Building things people actually use. TypeScript, Rust, Go. Open to freelance work.</textarea>
            </div>
            <div class="f-field">
              <label class="f-label">Tags (comma separated)</label>
              <input class="f-input" value="Developer, Open Source, Freelance">
            </div>
            <div class="f-field">
              <label class="f-label">Location</label>
              <input class="f-input" value="London, UK" placeholder="Optional">
            </div>
            <div class="f-field" style="margin-bottom:0">
              <label class="f-label">Website</label>
              <input class="f-input" value="https://zeraph.dev" placeholder="https://...">
            </div>
          </div>
          <div style="display:flex;justify-content:flex-end">
            <button class="btn btn-primary" onclick="showToast('✅ Profile saved!')">Save Changes</button>
          </div>
        </div>

        <!-- DISCORD PANE -->
        <div class="dash-pane" id="dpane-discord">
          <div class="dcard">
            <div class="dcard-title"><span class="icon">💬</span> Discord Connection</div>
            <div class="discord-connected">
              <div class="dc-av">Z</div>
              <div class="dc-info">
                <div class="dc-name">zeraph</div>
                <div class="dc-handle">zeraph#1234</div>
                <div class="dc-badges">
                  <span class="tag tag-nitro" style="font-size:11px;padding:3px 9px">✨ Nitro</span>
                  <span class="tag tag-nitro" style="font-size:11px;padding:3px 9px">🚀 Server Booster</span>
                  <span class="tag tag-discord" style="font-size:11px;padding:3px 9px">In 24 servers</span>
                </div>
              </div>
              <button class="btn btn-ghost btn-sm">Disconnect</button>
            </div>
            <div style="margin-top:16px;padding:14px;background:var(--bg3);border-radius:var(--r2);font-size:13px;color:var(--text3);line-height:1.6">
              ✅ <strong style="color:var(--text2)">Auto-synced:</strong> Nitro status, server boosts, servers owned, member counts, and join date are all automatically pulled from Discord and displayed on your profile.
            </div>
          </div>
          <div class="dcard">
            <div class="dcard-title"><span class="icon">🔧</span> Display Settings</div>
            <div class="toggle-list">
              <div class="toggle-row">
                <div class="toggle-info"><h4>Show Nitro Status</h4><p>Display your Nitro badge publicly on your profile.</p></div>
                <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
              </div>
              <div class="toggle-row">
                <div class="toggle-info"><h4>Show Server Boosts</h4><p>Show which servers you're currently boosting.</p></div>
                <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
              </div>
              <div class="toggle-row">
                <div class="toggle-info"><h4>Show Servers Owned</h4><p>Display the servers you own with member counts.</p></div>
                <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
              </div>
              <div class="toggle-row">
                <div class="toggle-info"><h4>Show Discord Join Date</h4><p>Display when you first joined Discord.</p></div>
                <button class="toggle-switch" onclick="this.classList.toggle('on')"></button>
              </div>
            </div>
          </div>
        </div>

        <!-- MUSIC PANE -->
        <div class="dash-pane" id="dpane-music">
          <div class="dcard">
            <div class="dcard-title"><span class="icon">🎵</span> Profile Music</div>
            <div class="f-field">
              <label class="f-label">Track Title</label>
              <input class="f-input" value="Blinding Lights" placeholder="Track name">
            </div>
            <div class="f-field">
              <label class="f-label">Artist</label>
              <input class="f-input" value="The Weeknd" placeholder="Artist name">
            </div>
            <div class="f-field">
              <label class="f-label">Spotify Link (optional)</label>
              <input class="f-input" value="" placeholder="https://open.spotify.com/track/...">
            </div>
            <div class="toggle-row" style="border:none;padding:0;margin-top:8px">
              <div class="toggle-info"><h4>Show music player on profile</h4><p>Visitors will see the player at the top of your About tab.</p></div>
              <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
            </div>
          </div>
          <div style="display:flex;justify-content:flex-end">
            <button class="btn btn-primary" onclick="showToast('🎵 Music settings saved!')">Save Music</button>
          </div>
        </div>

        <!-- PORTFOLIO PANE -->
        <div class="dash-pane" id="dpane-portfolio">
          <div class="dcard">
            <div class="dcard-title"><span class="icon">💼</span> Portfolio Projects</div>
            <div class="portfolio-grid" style="margin-bottom:16px">
              <div class="portfolio-item">
                <div class="portfolio-thumb" style="background:linear-gradient(135deg,rgba(124,92,252,0.15),rgba(92,138,252,0.1))">💻</div>
                <div class="portfolio-info">
                  <div class="portfolio-name">DevPanel SaaS</div>
                  <div class="portfolio-type">Web App · TypeScript</div>
                </div>
              </div>
              <div class="portfolio-item" style="display:flex;flex-direction:column;align-items:center;justify-content:center;cursor:pointer;border-style:dashed;gap:6px" onclick="showToast('➕ Add project coming soon!')">
                <div style="font-size:28px;color:var(--text3)">+</div>
                <div style="font-size:13px;color:var(--text3)">Add Project</div>
              </div>
            </div>
            <div class="toggle-row" style="border:none;padding:0">
              <div class="toggle-info"><h4>Show Portfolio tab on profile</h4><p>Visitors can browse your portfolio from your public page.</p></div>
              <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
            </div>
          </div>
        </div>

        <!-- PRIVACY PANE -->
        <div class="dash-pane" id="dpane-privacy">
          <div class="dcard">
            <div class="dcard-title"><span class="icon">🔒</span> Privacy Settings</div>
            <div class="toggle-list">
              <div class="toggle-row">
                <div class="toggle-info"><h4>Public Profile</h4><p>Anyone with your link can view your profile.</p></div>
                <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
              </div>
              <div class="toggle-row">
                <div class="toggle-info"><h4>Show in Discover</h4><p>Allow your profile to appear in featured sections and searches.</p></div>
                <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
              </div>
              <div class="toggle-row">
                <div class="toggle-info"><h4>Allow Direct Messages</h4><p>Other vouch.gg users can message you via your profile.</p></div>
                <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
              </div>
              <div class="toggle-row">
                <div class="toggle-info"><h4>Show Profile View Count</h4><p>Display how many times your profile has been viewed.</p></div>
                <button class="toggle-switch" onclick="this.classList.toggle('on')"></button>
              </div>
              <div class="toggle-row">
                <div class="toggle-info"><h4>Show Follower Count</h4><p>Display your follower number on your public profile.</p></div>
                <button class="toggle-switch on" onclick="this.classList.toggle('on')"></button>
              </div>
            </div>
          </div>
        </div>

        <!-- LINK PANE -->
        <div class="dash-pane" id="dpane-link">
          <div class="dcard">
            <div class="dcard-title"><span class="icon">🔗</span> Your Profile Link</div>
            <p style="font-size:13px;color:var(--text3);margin-bottom:16px">Share this link in your Discord bio, Twitter, Reddit — anywhere you want to be found.</p>
            <div class="profile-link-box">
              <div class="plb-url">vouch.gg/zeraph</div>
              <button class="copy-btn" onclick="copyProfileLink()">Copy</button>
            </div>
            <div style="margin-top:16px;display:flex;gap:8px;flex-wrap:wrap">
              <button class="btn btn-ghost btn-sm" onclick="showToast('📤 Share options coming soon!')">Share</button>
              <button class="btn btn-ghost btn-sm" onclick="showPage('profile',null)">Preview Profile →</button>
            </div>
          </div>
        </div>

      </div><!-- /dash-content -->
    </div><!-- /dash-layout -->
  </div>
</div>

<!-- ======================================================
     CREATE PROFILE MODAL
     ====================================================== -->
<div class="modal-overlay hidden" id="create-modal" onclick="closeModalOutside(event)">
  <div class="modal">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <div class="modal-title">Create your profile</div>
    <div class="modal-sub">Connect Discord to get started. Your Discord username becomes your unique vouch.gg handle.</div>
    <div class="modal-steps">
      <div class="mstep done" id="mstep1"></div>
      <div class="mstep" id="mstep2"></div>
      <div class="mstep" id="mstep3"></div>
    </div>
    <div id="modal-step1">
      <div class="discord-connect" style="margin-bottom:20px">
        <h3>Connect Discord</h3>
        <p>We'll automatically pull your username, Nitro status, servers and more to power your profile.</p>
        <button class="btn btn-discord" onclick="connectDiscord()">Connect with Discord</button>
      </div>
    </div>
    <div id="modal-step2" style="display:none">
      <div class="f-field">
        <label class="f-label">Display Name</label>
        <input class="f-input" id="modal-displayname" placeholder="How your name appears on vouch.gg">
      </div>
      <div class="f-field">
        <label class="f-label">Bio</label>
        <textarea class="f-input" id="modal-bio" placeholder="Tell people who you are..."></textarea>
      </div>
      <div style="display:flex;justify-content:space-between;margin-top:8px">
        <button class="btn btn-ghost" onclick="modalBack()">Back</button>
        <button class="btn btn-primary" onclick="modalNext2()">Next →</button>
      </div>
    </div>
    <div id="modal-step3" style="display:none">
      <div style="text-align:center;padding:20px 0">
        <div style="font-size:52px;margin-bottom:16px">🎉</div>
        <h3 style="font-family:'Syne',sans-serif;font-size:20px;font-weight:700;margin-bottom:8px">You're all set!</h3>
        <p style="font-size:14px;color:var(--text3);margin-bottom:24px;line-height:1.6">Your vouch.gg profile is live at <strong style="color:var(--accent)">vouch.gg/you</strong>. Share it everywhere.</p>
        <button class="btn btn-primary" onclick="closeModal();showPage('dashboard',null)">Go to Dashboard →</button>
      </div>
    </div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<!-- ======================================================
     JAVASCRIPT
     ====================================================== -->
<script>
// ===== LOADING =====
window.addEventListener('load', function() {
  setTimeout(function() {
    document.getElementById('loading-screen').classList.add('fade-out');
  }, 2100);
});

// ===== NAVIGATION =====
function showPage(id, btn) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  if (btn) btn.classList.add('active');
}

// ===== PROFILE TABS =====
function showProfileTab(tab, btn) {
  document.querySelectorAll('.tab-pane').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.ptab').forEach(t => t.classList.remove('active'));
  document.getElementById('tab-' + tab).classList.add('active');
  if (btn) btn.classList.add('active');
  else {
    document.querySelectorAll('.ptab').forEach(function(t) {
      if (t.textContent.toLowerCase().indexOf(tab) >= 0) t.classList.add('active');
    });
  }
}

// ===== DASHBOARD PANES =====
function showDashPane(id, btn) {
  document.querySelectorAll('.dash-pane').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.dash-nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById('dpane-' + id).classList.add('active');
  if (btn) btn.classList.add('active');
}

// ===== REACTIONS =====
function toggleReaction(el) {
  var rc = el.querySelector('.rc');
  var n = parseInt(rc.textContent);
  if (el.classList.contains('active')) {
    el.classList.remove('active');
    rc.textContent = n - 1;
  } else {
    el.classList.add('active');
    rc.textContent = n + 1;
  }
}

// ===== MARKET =====
function filterMarket(btn, cat) {
  document.querySelectorAll('.market-filter').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  document.querySelectorAll('.market-card').forEach(function(card) {
    if (cat === 'all' || card.getAttribute('data-cat') === cat) {
      card.style.display = '';
    } else {
      card.style.display = 'none';
    }
  });
}

function buyItem(btn, name) {
  btn.textContent = 'Owned ✓';
  btn.classList.add('market-owned');
  showToast('🛒 ' + name + ' added to your profile!');
}

// ===== FEED =====
function addEmoji(e) {
  var ta = document.getElementById('np-text');
  ta.value += e;
  ta.focus();
}

function submitPost() {
  var text = document.getElementById('np-text').value.trim();
  if (!text) { showToast('⚠️ Write something first!'); return; }
  var el = document.createElement('div');
  el.className = 'post-card';
  el.style.animation = 'pageIn 0.3s ease';
  el.innerHTML = '<div class="post-header">'
    + '<div class="post-av" style="background:linear-gradient(135deg,var(--accent),var(--accent2))">Y</div>'
    + '<div class="post-meta"><div class="post-name">You</div><div class="post-time">Just now</div></div>'
    + '</div>'
    + '<div class="post-body">' + escapeHtml(text) + '</div>'
    + '<div class="reactions">'
    + '<div class="reaction" onclick="toggleReaction(this)"><span class="emoji">🔥</span> <span class="rc">0</span></div>'
    + '<div class="reaction" onclick="toggleReaction(this)"><span class="emoji">❤️</span> <span class="rc">0</span></div>'
    + '</div>';
  document.getElementById('feed-dynamic').prepend(el);
  document.getElementById('np-text').value = '';
  showToast('✅ Post shared!');
}

function escapeHtml(s) {
  return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}

// ===== CLAIM USERNAME =====
function claimUsername() {
  var val = document.getElementById('claim-input').value.trim();
  if (!val) { showToast('⚠️ Enter a username first!'); return; }
  showToast('🎉 vouch.gg/' + val + ' is yours!');
  openModal();
}

// ===== BANNER =====
function setBanner(swatch, grad) {
  document.querySelectorAll('.swatch').forEach(s => s.classList.remove('active'));
  swatch.classList.add('active');
  document.getElementById('banner-preview').style.background = grad;
  document.querySelector('.profile-banner').style.background = grad;
}
function changeBanner() { showToast('🖼️ Custom banner upload coming soon!'); }

// ===== COPY LINK =====
function copyProfileLink() {
  if (navigator.clipboard) {
    navigator.clipboard.writeText('https://vouch.gg/zeraph').catch(function() {});
  }
  showToast('🔗 Profile link copied!');
}

// ===== MODAL =====
var modalStep = 1;
function openModal() {
  document.getElementById('create-modal').classList.remove('hidden');
  modalStep = 1;
  showModalStep(1);
}
function closeModal() {
  document.getElementById('create-modal').classList.add('hidden');
}
function closeModalOutside(e) {
  if (e.target.id === 'create-modal') closeModal();
}
function showModalStep(n) {
  [1,2,3].forEach(function(i) {
    var el = document.getElementById('modal-step' + i);
    if (el) el.style.display = i === n ? '' : 'none';
    var ms = document.getElementById('mstep' + i);
    if (ms) ms.classList.toggle('done', i <= n);
  });
}
function connectDiscord() {
  showToast('💬 Connecting to Discord...');
  setTimeout(function() {
    modalStep = 2;
    showModalStep(2);
    showToast('✅ Discord connected: zeraph#1234');
  }, 1200);
}
function modalNext2() {
  modalStep = 3;
  showModalStep(3);
}
function modalBack() {
  modalStep = 1;
  showModalStep(1);
}

// ===== TOAST =====
var toastTimer;
function showToast(msg) {
  var t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(function() { t.classList.remove('show'); }, 2800);
}
</script>
</body>
</html>
