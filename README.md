<html lang="tr"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
    <title>Mercan Tekstil | Mühendislik &amp; Arşiv</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&amp;display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #05060a;
            --panel: rgba(15,18,28,0.96);
            --acc: #00d2ff;
            --acc2: #3a7bd5;
            --txt: #f8fafc;
            --dim: #94a3b8;
            --border: rgba(255,255,255,0.08);
            --ok: #10b981;
            --err: #f43f5e;
            --sidebar-w: 320px;
        }
        * { margin:0; padding:0; box-sizing:border-box; font-family:'Inter',system-ui,sans-serif; -webkit-tap-highlight-color:transparent; }
        body {
            background-color: var(--bg);
            background-image:
                radial-gradient(at 0% 0%, rgba(0,210,255,.08) 0, transparent 50%),
                radial-gradient(at 100% 100%, rgba(58,123,213,.08) 0, transparent 50%);
            background-attachment: fixed;
            color: var(--txt);
            min-height:100vh;
            padding: 1rem;
            display: flex;
            justify-content: center;
        }

        /* Sidebar */
        #sidebar {
            position: fixed;
            left: calc(-1 * var(--sidebar-w));
            top: 0;
            width: var(--sidebar-w);
            height: 100%;
            background: var(--panel);
            backdrop-filter: blur(30px);
            border-right: 1px solid var(--border);
            z-index: 1000;
            transition: left 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            padding: 2rem 1.5rem;
            box-shadow: 15px 0 50px rgba(0,0,0,0.6);
        }
        #sidebar.open { left: 0; }
        .sidebar-hdr { display: flex; justify-content: space-between; align-items: center; margin-bottom: 2rem; border-bottom: 1px solid var(--border); padding-bottom: 1rem; }
        .save-item { background: rgba(255,255,255,0.02); border: 1px solid var(--border); border-radius: 14px; padding: 1rem; margin-bottom: 1rem; cursor: pointer; transition: all 0.2s; position: relative; }
        .save-item:hover { background: rgba(0,210,255,0.05); border-color: var(--acc); transform: translateX(5px); }
        .save-name { font-weight: 700; color: #fff; font-size: 0.95rem; display: block; }
        .save-date { font-size: 0.7rem; color: var(--dim); margin-top: 0.2rem; display: block; }
        .save-rm { position: absolute; top: 1rem; right: 1rem; color: var(--err); opacity: 0.4; font-size: 0.9rem; }
        .save-rm:hover { opacity: 1; transform: scale(1.2); }

        .app { width: 100%; max-width:1300px; position: relative; }
        header { margin-bottom:2rem; padding: 1rem 0; border-bottom:1px solid var(--border); display: flex; justify-content: space-between; align-items: center; }
        .nav-actions { display: flex; gap: 1rem; }
        
        h1 { font-size:clamp(1.5rem,5vw,2.4rem); font-weight:800; background:linear-gradient(to right,#fff,var(--acc)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; letter-spacing:-1px; text-transform:uppercase; }
        .sub { color:var(--dim); font-size:.8rem; letter-spacing:2px; text-transform:uppercase; font-weight: 500; }
        
        .grid { display:grid; grid-template-columns: 1.1fr 0.9fr; gap:1.5rem; align-items:start; }
        @media(max-width:1000px){ .grid{ grid-template-columns:1fr; } }
        
        .card { background:var(--panel); border:1px solid var(--border); border-radius:28px; padding:1.8rem; box-shadow:0 25px 50px rgba(0,0,0,.5); }
        .card-title { font-size:1rem; font-weight:700; margin-bottom:1.5rem; display:flex; align-items:center; gap:.7rem; color:var(--acc); text-transform: uppercase; letter-spacing: 1px; }
        
        .params { display:grid; grid-template-columns: 1fr 1fr; gap:1rem; }
        .ig { display:flex; flex-direction:column; gap:.4rem; }
        label { font-size:.65rem; color:var(--dim); font-weight:800; text-transform:uppercase; letter-spacing:1px; }
        input, select { background:rgba(0,0,0,.4); border:1px solid var(--border); border-radius:12px; padding:.8rem 1rem; color:#fff; font-size:.95rem; width:100%; transition:all 0.2s; }
        input:focus { outline:none; border-color:var(--acc); background: rgba(0,0,0,.6); }
        
        .yarn-section { margin-top: 2rem; padding-top: 1.5rem; border-top: 1px solid var(--border); }
        .item-row { background:rgba(255,255,255,.02); border:1px solid var(--border); border-radius:18px; padding:1.2rem; margin-bottom:1.2rem; }
        .row-hdr { display:flex; justify-content:space-between; align-items:center; margin-bottom:1rem; font-size:.85rem; font-weight:700; color:var(--acc); }
        .row-grid { display:grid; grid-template-columns: 1fr 1fr; gap:0.8rem; }
        
        .btn { cursor:pointer; border:none; border-radius:14px; padding:.9rem 1.4rem; font-weight:700; font-size:.85rem; text-transform:uppercase; display:flex; align-items:center; justify-content:center; gap:.6rem; transition:all 0.2s; }
        .btn-add { background:rgba(0,210,255,0.05); color:var(--acc); border:1px dashed var(--acc); width: 100%; margin-top: 0.5rem; }
        .btn-save { background: var(--ok); color: #fff; width: 100%; margin-top: 1.5rem; box-shadow: 0 10px 20px rgba(16,185,129,0.2); }
        .btn-ghost { background:rgba(255,255,255,.05); color:var(--txt); border:1px solid var(--border); }
        .btn:hover { transform: translateY(-2px); filter: brightness(1.2); }
        .rm { background:rgba(244,63,94,.15); color:var(--err); width:28px; height:28px; border-radius:50%; display:flex; align-items:center; justify-content:center; cursor:pointer; }
        
        .metrics { display:grid; grid-template-columns:repeat(3,1fr); gap:1.2rem; margin-bottom:1.8rem; }
        .mc { background:rgba(255,255,255,.03); padding:1.4rem; border-radius:22px; border:1px solid var(--border); text-align:center; }
        .mc.hi { border-color:var(--acc2); background: linear-gradient(135deg, rgba(58,123,213,0.1), transparent); }
        .mc-lbl { font-size:.65rem; color:var(--dim); text-transform:uppercase; font-weight:800; margin-bottom:.6rem; letter-spacing:1px; }
        .mc-val { font-size:1.7rem; font-weight:800; color:#fff; }
        
        .abox { background:rgba(0,210,255,.04); border:1px solid rgba(0,210,255,.15); border-radius:22px; padding:1.5rem; }
        .arow { display:flex; justify-content:space-between; align-items:center; padding:.7rem 0; border-bottom:1px solid rgba(255,255,255,.05); font-size:.85rem; }
        .arow:last-child { border:none; }
        .albl { color:var(--acc); font-weight:700; text-transform:uppercase; font-size:.7rem; letter-spacing:0.5px; }
        
        .badge { padding:.4rem .8rem; border-radius:10px; font-size:.75rem; font-weight:800; }
        .b-ok { background:rgba(16,185,129,.1); color:var(--ok); border:1px solid rgba(16,185,129,0.3); }
        .b-err { background:rgba(244,63,94,.1); color:var(--err); border:1px solid rgba(244,63,94,0.3); }
        
        footer { text-align:center; margin-top:3rem; color:var(--dim); font-size:.75rem; opacity:.4; }
    </style>
</head>
<body>

<div id="sidebar">
    <div class="sidebar-hdr">
        <h3 style="color:var(--acc); letter-spacing:1px;">KAYIT ARŞİVİ</h3>
        <button class="btn btn-ghost" onclick="toggleSidebar()" style="padding:0.5rem; min-height:auto;">✕</button>
    </div>
    <div id="saveList"><p style="color:var(--dim); font-size:0.85rem; text-align:center; margin-top:2rem;">Henüz kayıt yok.</p></div>
</div>

<div class="app">
    <header>
        <div>
            <h1>MERCAN TEKSTİL</h1>
            <p class="sub">Mühendislik &amp; Üretim Analiz</p>
        </div>
        <div class="nav-actions">
            <button class="btn btn-ghost" onclick="toggleSidebar()">📂 ARŞİVİ AÇ</button>
        </div>
    </header>

    <main class="grid">
        <section class="card">
            <div class="card-title">🏭 Üretim Parametreleri</div>
            <div class="params">
                <div class="ig"><label>Kumaş Eni (cm)</label><input type="number" id="fabricWidth" value="160"></div>
                <div class="ig"><label>Tezgah Eni (cm)</label><input type="number" id="loomWidth" value="340"></div>
                <div class="ig"><label>RPM (Makine Hızı)</label><input type="number" id="loomSpeed" value="600"></div>
                <div class="ig"><label>Randıman (%)</label><input type="number" id="efficiency" value="85"></div>
                <div class="ig"><label>Günlük Saat</label><input type="number" id="dailyHours" value="24"></div>
                <div class="ig"><label>Sipariş Hedefi (Adet)</label><input type="number" id="orderLength" value="1000"></div>
                <div class="ig"><label>Çözgü Sıklık</label><input type="number" id="warpDensity" value="40"></div>
                <div class="ig"><label>Atkı Sıklık</label><input type="number" id="weftDensity" value="24"></div>
                <div class="ig"><label>Ana Desen Boyu (cm)</label><input type="number" id="mainDesign" value="100"></div>
                <div class="ig"><label>Saçak Boyu (cm)</label><input type="number" id="fringeLength" value="10"></div>
            </div>

            <div class="yarn-section">
                <div class="card-title" style="font-size:0.85rem">🧵 Çözgü İplikleri</div>
                <div id="warpList"><div class="item-row" id="y17766306424662jip">
            <div class="row-hdr"><span>Bileşen</span><button class="rm" onclick="removeYarn('y17766306424662jip','warp')">✕</button></div>
            <div class="row-grid">
                <div class="ig" style="grid-column:span 2"><label>İplik Adı</label><input type="text" class="yn" value=""></div>
                <div class="ig"><label>Birim</label><select class="yu"><option value="denier">Denye</option><option value="ne">Ne</option><option value="nm">Nm</option></select></div>
                <div class="ig"><label>No</label><input type="number" class="yno" value=""></div>
                <div class="ig"><label>Oran (%)</label><input type="number" class="yr" value=""></div>
                <div class="ig"><label>Fiyat (TL/kg)</label><input type="number" class="yp" value=""></div>
                <div class="ig" style="grid-column:span 2"><label>Fire (%)</label><input type="number" class="yf" value="5"></div>
            </div></div></div>
                <button class="btn btn-add" onclick="addYarn('warp')">+ Çözgü Bileşeni Ekle</button>
            </div>

            <div class="yarn-section">
                <div class="card-title" style="font-size:0.85rem">🎞️ Atkı İplikleri</div>
                <div id="weftList"><div class="item-row" id="y1776630642466ymzo">
            <div class="row-hdr"><span>Bileşen</span><button class="rm" onclick="removeYarn('y1776630642466ymzo','weft')">✕</button></div>
            <div class="row-grid">
                <div class="ig" style="grid-column:span 2"><label>İplik Adı</label><input type="text" class="yn" value=""></div>
                <div class="ig"><label>Birim</label><select class="yu"><option value="denier">Denye</option><option value="ne">Ne</option><option value="nm">Nm</option></select></div>
                <div class="ig"><label>No</label><input type="number" class="yno" value=""></div>
                <div class="ig"><label>Oran (%)</label><input type="number" class="yr" value=""></div>
                <div class="ig"><label>Fiyat (TL/kg)</label><input type="number" class="yp" value=""></div>
                <div class="ig" style="grid-column:span 2"><label>Fire (%)</label><input type="number" class="yf" value="5"></div>
            </div></div></div>
                <button class="btn btn-add" onclick="addYarn('weft')">+ Atkı Bileşeni Ekle</button>
            </div>

            <button class="btn btn-save" onclick="saveCalculation()">💾 HESAPLAMAYI ARŞİVE KAYDET</button>
        </section>

        <section class="card" id="resultsSection" style="opacity: 1;">
            <div class="card-title">📊 Analiz Dashboard</div>
            <div class="metrics">
                <div class="mc"><div class="mc-lbl">Bant Sayısı</div><div class="mc-val" id="resBant">2</div></div>
                <div class="mc hi"><div class="mc-lbl">Rapor Gramaj</div><div class="mc-val" id="resRaporGram">0 g</div></div>
                <div class="mc hi"><div class="mc-lbl">Rapor Maliyet</div><div class="mc-val" id="resRaporMaliyet">0.00 TL</div></div>
            </div>
            
            <div id="validationBox" style="margin-bottom:1.5rem">
                <div style="display:flex;gap:0.8rem">
                    <span class="badge b-err">Çözgü: %0.0</span>
                    <span class="badge b-err">Atkı: %0.0</span>
                </div></div>
            
            <div class="abox" id="analysisBox" style="display: block;">
                <div id="analysisContent"><div class="arow"><span class="albl">Üretim Kapasitesi (Günde)</span><span style="color:#fff; font-weight:800;">510 Adet</span></div><div class="arow"><span class="albl">Toplam Kumaş Üretimi</span><span>612.0 m / Gün</span></div><div class="arow"><span class="albl">Makine İlerlemesi</span><span>306.0 m / Gün</span></div><div class="arow"><span class="albl">Ana Desen Gramajı</span><span>0.0 g/m²</span></div><div class="arow"><span class="albl" style="color:var(--dim)">── Çözgü İhtiyacı (1000 Adet) ──</span></div><div class="arow" style="padding-left:0.5rem"><span>İplik</span><span style="font-size:0.75rem">0.0g/Adet | <b>0 g</b></span></div><div class="arow"><span class="albl" style="color:var(--dim)">── Atkı İhtiyacı (1000 Adet) ──</span></div><div class="arow" style="padding-left:0.5rem"><span>İplik</span><span style="font-size:0.75rem">0.0g/Adet | <b>0 g</b></span></div></div>
            </div>
        </section>
    </main>
    <footer>© 2024 Mercan Tekstil - Profesyonel Üretim Sistemleri</footer>
</div>

<script>
    const neToDenier = ne => 5315 / ne;
    const nmToDenier = nm => 9000 / nm;
    const fmtW = g => g < 1000 ? Math.round(g) + ' g' : (g/1000).toFixed(2) + ' kg';

    function toggleSidebar() { document.getElementById('sidebar').classList.toggle('open'); }

    function addYarn(type, data = null) {
        const list = document.getElementById(type + 'List');
        const id = 'y' + Date.now() + Math.random().toString(36).substr(2, 4);
        const d = document.createElement('div');
        d.className = 'item-row';
        d.id = id;
        d.innerHTML = `
            <div class="row-hdr"><span>Bileşen</span><button class="rm" onclick="removeYarn('${id}','${type}')">✕</button></div>
            <div class="row-grid">
                <div class="ig" style="grid-column:span 2"><label>İplik Adı</label><input type="text" class="yn" value="${data?data.name:''}"></div>
                <div class="ig"><label>Birim</label><select class="yu"><option value="denier" ${data&&data.unit=='denier'?'selected':''}>Denye</option><option value="ne" ${data&&data.unit=='ne'?'selected':''}>Ne</option><option value="nm" ${data&&data.unit=='nm'?'selected':''}>Nm</option></select></div>
                <div class="ig"><label>No</label><input type="number" class="yno" value="${data?data.no:''}"></div>
                <div class="ig"><label>Oran (%)</label><input type="number" class="yr" value="${data?data.ratio:''}"></div>
                <div class="ig"><label>Fiyat (TL/kg)</label><input type="number" class="yp" value="${data?data.price:''}"></div>
                <div class="ig" style="grid-column:span 2"><label>Fire (%)</label><input type="number" class="yf" value="${data?data.waste:'5'}"></div>
            </div>`;
        list.appendChild(d);
        if(!data) calculate();
    }

    function removeYarn(id, type) { document.getElementById(id).remove(); calculate(); }

    function getInputs(listId) {
        return Array.from(document.querySelectorAll('#' + listId + ' .item-row')).map(r => ({
            name: r.querySelector('.yn').value,
            unit: r.querySelector('.yu').value,
            no: parseFloat(r.querySelector('.yno').value) || 0,
            ratio: parseFloat(r.querySelector('.yr').value) || 0,
            price: parseFloat(r.querySelector('.yp').value) || 0,
            waste: parseFloat(r.querySelector('.yf').value) || 0
        }));
    }

    function calculate() {
        try {
            const getV = id => parseFloat(document.getElementById(id).value) || 0;
            const fw=getV('fabricWidth'), lw=getV('loomWidth'), rpm=getV('loomSpeed'), eff=getV('efficiency')/100, dh=getV('dailyHours'), ord=getV('orderLength'), wd=getV('warpDensity'), fd=getV('weftDensity'), mdCm=getV('mainDesign'), frCm=getV('fringeLength');
            
            if(!fw || !lw || !fd) return;

            const mdM = mdCm/100, frM = frCm/100, totalM = mdM + (frM*2), loomCount = Math.floor(lw/fw);
            
            // Çözgü: (Sıklık * En * Denye * Oran) / 9000
            const warps = getInputs('warpList').map(y => {
                let den = y.no;
                if(y.unit==='ne') den=neToDenier(y.no); else if(y.unit==='nm') den=nmToDenier(y.no);
                const gpm = (wd * fw * den * (y.ratio/100)) / 9000;
                const gpmF = gpm * (1 + y.waste/100);
                return { name: y.name, gpmF, costM: gpmF * (y.price/1000), ratio: y.ratio };
            });

            // Atkı: (Sıklık * TezgahEni * Denye * Oran) / (9000 * Bant)
            const wefts = getInputs('weftList').map(y => {
                let den = y.no;
                if(y.unit==='ne') den=neToDenier(y.no); else if(y.unit==='nm') den=nmToDenier(y.no);
                const gpm = (fd * lw * den * (y.ratio/100)) / (9000 * loomCount);
                const gpmF = gpm * (1 + y.waste/100);
                return { name: y.name, gpmF, costM: gpmF * (y.price/1000), ratio: y.ratio };
            });

            const wSum=warps.reduce((s,x)=>s+x.ratio,0), fSum=wefts.reduce((s,x)=>s+x.ratio,0);
            const wOk=Math.abs(wSum-100)<0.5, fOk=Math.abs(fSum-100)<0.5;
            
            document.getElementById('validationBox').innerHTML = `
                <div style="display:flex;gap:0.8rem">
                    <span class="badge ${wOk?'b-ok':'b-err'}">Çözgü: %${wSum.toFixed(1)}</span>
                    <span class="badge ${fOk?'b-ok':'b-err'}">Atkı: %${fSum.toFixed(1)}</span>
                </div>`;

            const wG = warps.reduce((s,x)=>s+x.gpmF,0), wC = warps.reduce((s,x)=>s+x.costM,0);
            const fG = wefts.reduce((s,x)=>s+x.gpmF,0), fC = wefts.reduce((s,x)=>s+x.costM,0);

            // Bir raporun toplam gramaj ve maliyeti
            const unitGram = (wG * totalM) + (fG * mdM);
            const unitCost = (wC * totalM) + (fC * mdM);

            // Üretim Kapasitesi
            const machineMetersDay = (rpm * eff * 60 * dh) / (fd * 100);
            const totalFabricMetersDay = machineMetersDay * loomCount;
            const unitsDay = (machineMetersDay / totalM) * loomCount;

            document.getElementById('resBant').innerText = loomCount;
            document.getElementById('resRaporGram').innerText = Math.round(unitGram) + ' g';
            document.getElementById('resRaporMaliyet').innerText = unitCost.toFixed(2) + ' TL';

            let ac = `<div class="arow"><span class="albl">Üretim Kapasitesi (Günde)</span><span style="color:#fff; font-weight:800;">${unitsDay.toFixed(0)} Adet</span></div>`;
            ac += `<div class="arow"><span class="albl">Toplam Kumaş Üretimi</span><span>${totalFabricMetersDay.toFixed(1)} m / Gün</span></div>`;
            ac += `<div class="arow"><span class="albl">Makine İlerlemesi</span><span>${machineMetersDay.toFixed(1)} m / Gün</span></div>`;
            ac += `<div class="arow"><span class="albl">Ana Desen Gramajı</span><span>${((wG + fG) / (fw/100)).toFixed(1)} g/m²</span></div>`;
            
            const addNeeds = (title, list, len) => {
                if(list.length==0) return;
                ac += `<div class="arow"><span class="albl" style="color:var(--dim)">── ${title} (${ord} Adet) ──</span></div>`;
                list.forEach(y => { 
                    const uG = y.gpmF * len;
                    ac += `<div class="arow" style="padding-left:0.5rem"><span>${y.name||'İplik'}</span><span style="font-size:0.75rem">${uG.toFixed(1)}g/Adet | <b>${fmtW(uG * ord)}</b></span></div>`; 
                });
            };
            addNeeds('Çözgü İhtiyacı', warps, totalM);
            addNeeds('Atkı İhtiyacı', wefts, mdM);

            document.getElementById('analysisContent').innerHTML = ac;
            document.getElementById('analysisBox').style.display = 'block';
            document.getElementById('resultsSection').style.opacity = '1';
        } catch(e) {}
    }

    // Arşivleme
    function saveCalculation() {
        const name = prompt("Kayıt ismi girin (Örn: Mavi Havlu v1):");
        if(!name) return;
        const save = {
            id: Date.now(), name, date: new Date().toLocaleString('tr-TR'),
            p: { fw:document.getElementById('fabricWidth').value, lw:document.getElementById('loomWidth').value, rpm:document.getElementById('loomSpeed').value, eff:document.getElementById('efficiency').value, dh:document.getElementById('dailyHours').value, ord:document.getElementById('orderLength').value, wd:document.getElementById('warpDensity').value, fd:document.getElementById('weftDensity').value, md:document.getElementById('mainDesign').value, fl:document.getElementById('fringeLength').value },
            w: getInputs('warpList'), f: getInputs('weftList')
        };
        let s = JSON.parse(localStorage.getItem('mercan_eng_saves') || '[]');
        s.push(save);
        localStorage.setItem('mercan_eng_saves', JSON.stringify(s));
        renderSaves();
        alert("Hesaplama başarıyla arşivlendi!");
    }

    function renderSaves() {
        const list = document.getElementById('saveList');
        const s = JSON.parse(localStorage.getItem('mercan_eng_saves') || '[]');
        if(s.length == 0) { list.innerHTML = '<p style="color:var(--dim); font-size:0.85rem; text-align:center; margin-top:2rem;">Henüz kayıt yok.</p>'; return; }
        list.innerHTML = s.map(x => `
            <div class="save-item" onclick="loadSave(${x.id})">
                <span class="save-name">${x.name}</span>
                <span class="save-date">${x.date}</span>
                <span class="save-rm" onclick="event.stopPropagation(); deleteSave(${x.id})">✕</span>
            </div>
        `).join('');
    }

    function loadSave(id) {
        const s = JSON.parse(localStorage.getItem('mercan_eng_saves') || '[]').find(x => x.id === id);
        if(!s) return;
        document.getElementById('fabricWidth').value = s.p.fw;
        document.getElementById('loomWidth').value = s.p.lw;
        document.getElementById('loomSpeed').value = s.p.rpm;
        document.getElementById('efficiency').value = s.p.eff;
        document.getElementById('dailyHours').value = s.p.dh;
        document.getElementById('orderLength').value = s.p.ord;
        document.getElementById('warpDensity').value = s.p.wd;
        document.getElementById('weftDensity').value = s.p.fd;
        document.getElementById('mainDesign').value = s.p.md;
        document.getElementById('fringeLength').value = s.p.fl;
        document.getElementById('warpList').innerHTML = '';
        document.getElementById('weftList').innerHTML = '';
        s.w.forEach(y => addYarn('warp', y));
        s.f.forEach(y => addYarn('weft', y));
        calculate();
        toggleSidebar();
    }

    function deleteSave(id) {
        if(!confirm("Bu kaydı silmek istediğinize emin misiniz?")) return;
        let s = JSON.parse(localStorage.getItem('mercan_eng_saves') || '[]').filter(x => x.id !== id);
        localStorage.setItem('mercan_eng_saves', JSON.stringify(s));
        renderSaves();
    }

    document.addEventListener('input', calculate);
    window.onload = () => { renderSaves(); addYarn('warp'); addYarn('weft'); };
</script>


</body></html>