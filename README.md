<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rapzz Motion | Creative Hub</title>
    <style>
        :root {
            --bg-dark: #121212;
            --card-gray: #1e1e1e;
            --accent-green: #38ef7d;
            --text-main: #ffffff;
            --text-dim: #b0b0b0;
        }

        body {
            font-family: 'Segoe UI', sans-serif;
            margin: 0; padding-bottom: 80px;
            background-color: var(--bg-dark); color: var(--text-main);
            user-select: none;
            overflow-x: hidden;
        }

        header { padding: 15px 20px; display: flex; align-items: center; justify-content: space-between; position: sticky; top: 0; background: var(--bg-dark); z-index: 100; border-bottom: 1px solid #333; }
        .brand { font-weight: bold; font-size: 1.2rem; color: var(--accent-green); }
        .status-bar { text-align: center; font-size: 0.8rem; color: var(--text-dim); padding: 5px 0; background: #1a1a1a; }

        /* OVERLAY MENU (GARIS 3) */
        #menu-overlay {
            position: fixed; top: 0; left: -100%; width: 100%; height: 100%;
            background: rgba(18, 18, 18, 0.98); z-index: 200;
            transition: 0.3s; display: flex; flex-direction: column;
            justify-content: center; align-items: center; gap: 25px;
        }
        #menu-overlay.active { left: 0; }
        .menu-item-large { font-size: 1.5rem; color: white; text-decoration: none; font-weight: bold; cursor: pointer; }
        .menu-item-large:hover { color: var(--accent-green); }
        .close-menu { position: absolute; top: 20px; right: 25px; font-size: 2rem; cursor: pointer; }

        .container { display: none; padding: 0; animation: fadeIn 0.2s; }
        .container.active { display: block; }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* BERANDA & TREND STYLE */
        .section-header { padding: 20px 20px 10px; display: flex; justify-content: space-between; align-items: center; }
        .section-header h2 { font-size: 1rem; margin: 0; }
        .scroll-row { display: flex; overflow-x: auto; padding: 10px 20px; gap: 20px; scrollbar-width: none; }
        .category-item { display: flex; flex-direction: column; align-items: center; min-width: 65px; }
        .icon-circle { width: 55px; height: 55px; border-radius: 50%; background: var(--card-gray); border: 2px solid var(--accent-green); display: flex; align-items: center; justify-content: center; font-size: 1.5rem; margin-bottom: 8px; }
        
        .trend-info-card { background: var(--card-gray); margin: 0 20px 20px; padding: 15px; border-radius: 12px; border-left: 4px solid #ff0050; }
        .trend-info-card h3 { margin: 0 0 5px; font-size: 0.9rem; color: #00f2ea; }
        .trend-info-card p { margin: 0; font-size: 0.75rem; color: var(--text-dim); line-height: 1.4; }

        .item-card { background: var(--card-gray); border-radius: 12px; display: flex; padding: 12px; align-items: center; gap: 15px; margin: 0 20px 12px; border-left: 3px solid var(--accent-green); cursor: pointer; }
        .item-preview { width: 65px; height: 65px; background: #333; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-size: 1.2rem; color: var(--accent-green); }

        /* TUTORIAL GRID STYLE */
        .tutorial-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; padding: 0 20px 20px; }
        .tutorial-card { background: var(--card-gray); border-radius: 12px; overflow: hidden; cursor: pointer; }
        .tutorial-thumb { height: 100px; background: #2a2a2a; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; }
        .tutorial-info { padding: 10px; }
        .tutorial-info h4 { margin: 0; font-size: 0.8rem; }
        .tutorial-info p { font-size: 0.65rem; color: var(--text-dim); margin-top: 4px; }

        .banner-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; padding: 0 20px 20px; }
        .banner { height: 70px; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 0.85rem; color: white; }
        .banner.blue { background: linear-gradient(135deg, #004d4d, #008080); }
        .banner.purple { background: linear-gradient(135deg, #32004d, #660099); }

        /* EDIT FORM */
        .edit-form { padding: 20px; }
        .input-group { margin-bottom: 15px; }
        .input-group label { display: block; font-size: 0.8rem; color: var(--text-dim); margin-bottom: 5px; }
        .input-group input, .input-group select { width: 100%; background: var(--card-gray); border: 1px solid #444; padding: 12px; border-radius: 8px; color: white; box-sizing: border-box; }
        .submit-btn { background: var(--accent-green); color: black; width: 100%; padding: 15px; border-radius: 8px; font-weight: bold; border: none; cursor: pointer; }

        /* NAV */
        .bottom-bar { position: fixed; bottom: 0; width: 100%; background: #1a1a1a; display: flex; justify-content: space-around; align-items: center; padding: 10px 0 20px; border-top: 1px solid #333; }
        .nav-link { text-align: center; color: var(--text-dim); font-size: 0.65rem; text-decoration: none; flex: 1; cursor: pointer; }
        .nav-link.active { color: var(--accent-green); }
        .nav-main-btn { background: var(--accent-green); width: 50px; height: 50px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 2rem; color: #000; margin-top: -35px; box-shadow: 0 4px 15px rgba(0,0,0,0.4); cursor: pointer; }
    </style>
</head>
<body>

<div id="menu-overlay">
    <div class="close-menu" onclick="toggleMenu()">×</div>
    <div class="menu-item-large" onclick="quickNav('Beranda')">🏠 BERANDA</div>
    <div class="menu-item-large" onclick="quickNav('Tutorial')">🎓 TUTORIAL</div>
    <div class="menu-item-large" onclick="quickNav('Edit')">➕ MODE EDIT</div>
    <div class="menu-item-large" onclick="quickNav('Proyek')">📂 PROYEK</div>
    <div class="menu-item-large" onclick="quickNav('Templat')">🖼️ TEMPLAT</div>
</div>

<header>
    <div style="cursor: pointer; font-size: 1.5rem;" onclick="toggleMenu()">☰</div>
    <div class="brand">RAPZZ MOTION</div>
    <div>👤</div>
</header>

<div class="status-bar">
    <span id="live-clock">00:00:00</span> | <span id="local-tz">WIB</span>
</div>

<div id="page-Beranda" class="container active">
    <div class="section-header"><h2>Templat Baru</h2></div>
    <div class="scroll-row">
        <div class="category-item"><div class="icon-circle">⭐</div><span class="label">Untuk Anda</span></div>
        <div class="category-item"><div class="icon-circle">📸</div><span class="label">Cinematic</span></div>
        <div class="category-item"><div class="icon-circle">⚡</div><span class="label">Jedag Jedug</span></div>
        <div class="category-item"><div class="icon-circle">✨</div><span class="label">Preset</span></div>
    </div>

    <div class="section-header"><h2>Preset Trend TikTok </h2></div>
    <div class="trend-info-card"><h3>🔥 XML Preset Hard JJ</h3><p>Gunakan preset ini untuk hasil Jedag Jedug yang presisi mengikuti beat musik bass.</p></div>
    <div class="trend-info-card"><h3>✨ Link 5MB Aesthetic Blur</h3><p>Transisi blur yang lembut dengan color grading cinematic.</p></div>

    <div class="section-header"><h2>Daftar Harga Edit</h2></div>
    <div class="item-card" onclick="showPage('Edit')"><div class="item-preview">🎬</div><div class="item-info"><h4>Paket Simple (5k)</h4><p style="font-size:0.7rem; color:var(--text-dim);">HD | 15 Detik</p></div></div>
    <div class="item-card" onclick="showPage('Edit')"><div class="item-preview">💎</div><div class="item-info"><h4>Paket Pro (8k)</h4><p style="font-size:0.7rem; color:var(--text-dim);">60 FPS | Smooth</p></div></div>
    <div class="item-card" onclick="showPage('Edit')"><div class="item-preview">🔥</div><div class="item-info"><h4>Paket Premium (10k)</h4><p style="font-size:0.7rem; color:var(--text-dim);">4K | Full Request</p></div></div>

    <div class="section-header"><h2>Apa itu Alight Motion?</h2></div>
    <div class="trend-info-card" style="border-left-color: var(--accent-green);">
        <h3>🚀 Motion Graphics Profesional</h3>
        <p>Alight Motion adalah aplikasi pertama di mobile untuk motion graphics. Digunakan untuk membuat animasi berkualitas tinggi dengan sistem layer dan keyframe yang presisi.</p>
    </div>
</div>

<div id="page-Tutorial" class="container">
    <div class="section-header"><h2 style="font-size: 1.2rem;">Tutorial</h2></div>
    <div class="tutorial-grid">
        <div class="tutorial-card">
            <div class="tutorial-thumb">▶</div>
            <div class="tutorial-info"><h4>Getting Started - Part One</h4><p>Pelajari dasar penggunaan.</p></div>
        </div>
        <div class="tutorial-card">
            <div class="tutorial-thumb">▶</div>
            <div class="tutorial-info"><h4>Getting Started - Part Two</h4><p>Cara membuat animasi yang smooth.</p></div>
        </div>
    </div>
    <div class="banner-grid">
        <div class="banner blue">Memulai</div>
        <div class="banner purple">Langkah Berikutnya</div>
    </div>
    <div class="section-header"><h2 style="font-size: 0.9rem;">Pelajari selengkapnya</h2></div>
    <div class="tutorial-grid">
        <div class="tutorial-card"><div class="tutorial-thumb" style="background:#161b22;">🎮</div><div class="tutorial-info"><h4>Controlpad Guide</h4><p>Panduan menggunakan keyframe snapping.</p></div></div>
        <div class="tutorial-card"><div class="tutorial-thumb" style="background:#161b22;">🎨</div><div class="tutorial-info"><h4>Grouping Tips</h4><p>Cara mengelompokkan layer video.</p></div></div>
    </div>
</div>

<div id="page-Edit" class="container">
    <div class="section-header"><h2>Mode Edit (Order)</h2></div>
    <div class="edit-form">
        <div class="input-group"><label>Nama</label><input type="text" id="cust-name" placeholder="Nama Anda..."></div>
        <div class="input-group"><label>Paket</label>
            <select id="cust-paket">
                <option value="Simple (5k)">Simple (5k)</option>
                <option value="Pro (8k)">Pro (8k)</option>
                <option value="Premium (10k)">Premium (10k)</option>
            </select>
        </div>
        <button class="submit-btn" onclick="kirimOrder()">KIRIM KE WHATSAPP</button>
    </div>
</div>

<div id="page-Proyek" class="container">
    <div class="section-header"><h2>Katalog Proyek</h2></div>
    <div class="item-card"><div class="item-preview">📄</div><div class="item-info"><h4>XML Project Mentahan</h4><p style="font-size:0.7rem; color:var(--text-dim);">File mentahan proyek Alight Motion.</p></div></div>
    <div class="item-card"><div class="item-preview">🔗</div><div class="item-info"><h4>Link 5MB Preset</h4><p style="font-size:0.7rem; color:var(--text-dim);">Impor otomatis melalui tautan aplikasi.</p></div></div>
</div>

<div id="page-Templat" class="container">
    <div class="section-header"><h2>Trend Templat TikTok</h2></div>
    <div class="item-card"><div class="item-preview">🎙️</div><div class="item-info"><h4>JJ Sop Spoken</h4><p style="font-size:0.7rem; color:var(--text-dim);">JJ dubbing suara lembut.</p></div></div>
    <div class="item-card"><div class="item-preview">🖼️</div><div class="item-info"><h4>JJ 1 Foto Trend</h4><p style="font-size:0.7rem; color:var(--text-dim);">Animasi kreatif satu foto.</p></div></div>
    <div class="item-card"><div class="item-preview">🚀</div><div class="item-info"><h4>JJ Viral TikTok</h4><p style="font-size:0.7rem; color:var(--text-dim);">Gaya Jedag Jedug FYP.</p></div></div>
</div>

<nav class="bottom-bar">
    <div class="nav-link active" onclick="showPage('Beranda')">🏠<br>Beranda</div>
    <div class="nav-link" onclick="showPage('Tutorial')">🎓<br>Tutorial</div>
    <div class="nav-main-btn" onclick="showPage('Edit')">+</div>
    <div class="nav-link" onclick="showPage('Proyek')">📂<br>Proyek</div>
    <div class="nav-link" onclick="showPage('Templat')">🖼️<br>Templat</div>
</nav>

<script>
    function toggleMenu() { document.getElementById('menu-overlay').classList.toggle('active'); }
    function quickNav(pId) { toggleMenu(); showPage(pId); }
    function showPage(pId) {
        document.querySelectorAll('.container').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.nav-link').forEach(n => n.classList.remove('active'));
        document.getElementById('page-' + pId).classList.add('active');
        document.querySelectorAll('.nav-link').forEach(n => { if(n.innerText.includes(pId)) n.classList.add('active'); });
    }
    function kirimOrder() {
        const name = document.getElementById('cust-name').value || "Editor";
        const pkg = document.getElementById('cust-paket').value;
        window.location.href = `https://wa.me/62882007235276?text=Halo%20Rapzz%20Motion,%20saya%20${name}%20ingin%20order%20paket%20${pkg}`;
    }
    function startClock() { setInterval(() => { document.getElementById('live-clock').innerText = new Date().toLocaleTimeString('id-ID'); }, 1000); }
    window.onload = startClock;
</script>
</body>
</html>
