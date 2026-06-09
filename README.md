# 🌱 The Imbewu Investigation
### Data Analytics Capstone — Witle Academy

> *"Imbewu means 'seed' in isiZulu and isiXhosa. By the time you finish this project, you'll have everything you need to grow into the analyst we trained you to become."*
> — Clarence V. Mantiya, Programme Director

[![Live Dashboard](https://img.shields.io/badge/Live%20Dashboard-View%20Now-2E7D32?style=for-the-badge&logo=html5&logoColor=white)](https://yourusername.github.io/imbewu-retail-investigation/imbewu_dashboard.html)
[![SQL](https://img.shields.io/badge/SQL-Databricks-E87722?style=for-the-badge&logo=databricks&logoColor=white)](./sql/investigation.sql)
[![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](./dashboard/imbewu_dashboard.pbix)

---

## 📌 The Brief

**Week 1 — Sizwe Khumalo, Head of Sales:**
> *"I've been looking at the latest revenue report and something's off in Western Cape. Numbers are down compared to last year, but our store visit reports say foot traffic is roughly flat. That doesn't add up. I have an exec readout in three weeks — I want to know what's happening, why, and what we should do about it."*

**Week 4 — Vusi Mthembu, Chief Operating Officer:**
> *"I'm presenting to the board on Friday. I just want one dashboard I can open on my laptop in front of the board and use to answer questions live. If they ask 'what's the problem', I open page 1. If they ask 'what's causing it', I open page 2. If they ask 'what should we do', I open page 3."*

That is the dashboard below.

---

## 📊 Live Dashboard

> **Click the tabs below to navigate between the three board pages.**

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'Segoe UI',system-ui,sans-serif;background:#e8ece6;padding:24px 0;}
.db{width:100%;max-width:1100px;margin:0 auto;border-radius:10px;overflow:hidden;box-shadow:0 4px 28px rgba(0,0,0,0.16);}
.topbar{background:#0f2d1a;padding:11px 20px;display:flex;align-items:center;justify-content:space-between;}
.topbar-left{display:flex;align-items:center;gap:11px;}
.logo{width:30px;height:30px;background:#2d7a45;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:14px;color:#a3e4b4;flex-shrink:0;}
.tb-title{font-size:13px;font-weight:600;color:#fff;}
.tb-sub{font-size:10px;color:#6b9e7a;margin-top:2px;}
.tb-meta{font-size:10px;color:#4b7057;font-style:italic;}
.tabs{background:#0a2012;display:flex;padding:0 20px;border-bottom:1px solid #1a3d24;}
.tab{padding:9px 18px;font-size:11.5px;font-weight:500;color:#4b7057;cursor:pointer;border-bottom:2px solid transparent;transition:all .15s;display:flex;align-items:center;gap:6px;white-space:nowrap;user-select:none;}
.tab.on{color:#5ecf7e;border-bottom-color:#5ecf7e;background:rgba(94,207,126,.06);}
.tab:hover:not(.on){color:#8dc99e;}
.tab-num{width:19px;height:19px;border-radius:50%;font-size:9.5px;font-weight:700;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.tab.on .tab-num{background:#5ecf7e;color:#0a2012;}
.tab:not(.on) .tab-num{background:#1a3d24;color:#4b7057;}
.canvas{background:#f2f4f0;padding:16px;}
.pg{display:none;}.pg.on{display:block;}
.krow{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:12px;}
.kcard{background:#fff;border-radius:7px;padding:12px 14px;border:.5px solid #dde2d8;}
.klabel{font-size:9.5px;color:#6b7280;text-transform:uppercase;letter-spacing:.05em;margin-bottom:4px;}
.kval{font-size:22px;font-weight:500;color:#111;line-height:1;}
.ksub{font-size:10.5px;margin-top:4px;}
.red{color:#b91c1c;}.grn{color:#15803d;}.muted{color:#6b7280;}
.grid2{display:grid;grid-template-columns:1.55fr 1fr;gap:11px;margin-bottom:11px;}
.grid2r{display:grid;grid-template-columns:1fr 1fr;gap:11px;margin-bottom:11px;}
.card{background:#fff;border-radius:7px;padding:13px 15px;border:.5px solid #dde2d8;margin-bottom:11px;}
.card:last-child{margin-bottom:0;}
.ctitle{font-size:9.5px;font-weight:600;color:#374151;text-transform:uppercase;letter-spacing:.06em;margin-bottom:10px;}
.insight{background:#fffbeb;border-left:3px solid #d97706;padding:9px 13px;margin-bottom:12px;font-size:11px;color:#78350f;line-height:1.6;border-radius:0 6px 6px 0;}
.leg{display:flex;flex-wrap:wrap;gap:10px;margin-bottom:8px;}
.li{display:flex;align-items:center;gap:4px;font-size:9.5px;color:#6b7280;}
.lsq{width:8px;height:8px;border-radius:2px;flex-shrink:0;}
.sbar-wrap{display:flex;flex-direction:column;gap:5px;}
.srow{display:flex;align-items:center;gap:6px;}
.sname{width:152px;font-size:10px;color:#374151;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;flex-shrink:0;}
.strack{flex:1;height:13px;background:#f0f2ee;border-radius:2px;position:relative;overflow:visible;}
.scenter{position:absolute;left:50%;top:0;bottom:0;width:1px;background:#adb5ad;z-index:1;}
.sbar{position:absolute;height:100%;border-radius:2px;top:0;}
.sval{font-size:10px;font-weight:600;flex-shrink:0;width:36px;text-align:right;}
.sbadge{font-size:9px;padding:1px 5px;border-radius:3px;flex-shrink:0;font-weight:500;}
.ptable{width:100%;border-collapse:collapse;font-size:11px;}
.ptable th{text-align:left;padding:5px 9px;background:#f8f9f6;font-weight:600;color:#6b7280;border-bottom:.5px solid #e5e7eb;font-size:9.5px;text-transform:uppercase;letter-spacing:.04em;}
.ptable td{padding:6px 9px;border-bottom:.5px solid #f0f2ee;color:#374151;}
.ptable tr:last-child td{border-bottom:none;}
.tier-row{display:flex;align-items:center;gap:8px;margin-bottom:7px;}
.tier-label{width:56px;font-size:11px;color:#374151;flex-shrink:0;font-weight:500;}
.tier-bars{flex:1;display:flex;flex-direction:column;gap:2px;}
.bar-row{display:flex;align-items:center;gap:4px;}
.bar-year{font-size:9px;color:#9ca3af;width:28px;flex-shrink:0;}
.bar-fill{height:10px;border-radius:2px;min-width:2px;}
.bar-rev{font-size:9px;color:#6b7280;margin-left:3px;}
.rec3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:11px;margin-bottom:11px;}
.rec{border-radius:7px;padding:13px;background:#fff;border:.5px solid #dde2d8;border-top-width:3px;}
.rec-tag{font-size:9px;font-weight:600;text-transform:uppercase;letter-spacing:.08em;margin-bottom:6px;}
.rec-h{font-size:12px;font-weight:600;color:#111;margin-bottom:7px;}
.rec-b{font-size:10.5px;color:#6b7280;line-height:1.6;}
.rec-action{margin-top:8px;font-size:9.5px;font-weight:600;padding:4px 8px;border-radius:4px;display:inline-block;}
.finding{padding:7px 10px;font-size:10.5px;line-height:1.55;border-left:3px solid;border-radius:0 4px 4px 0;}
.footer{background:#0a2012;padding:9px 20px;text-align:center;font-size:9.5px;color:#4b7057;letter-spacing:.03em;}
</style>
</head>
<body>
<div class="db">
<div class="topbar">
  <div class="topbar-left">
    <div class="logo">🌱</div>
    <div>
      <div class="tb-title">Imbewu Retail — Western Cape Revenue Investigation</div>
      <div class="tb-sub">Board presentation &nbsp;·&nbsp; H1 2024 vs H1 2025 &nbsp;·&nbsp; 45 stores &nbsp;·&nbsp; 18 months data</div>
    </div>
  </div>
  <div class="tb-meta">Prepared for: V. Mthembu (COO) &nbsp;·&nbsp; June 2025</div>
</div>
<div class="tabs">
  <div class="tab on" onclick="show(0,this)"><span class="tab-num">1</span>⚠ What's the problem?</div>
  <div class="tab" onclick="show(1,this)"><span class="tab-num">2</span>🔬 What's causing it?</div>
  <div class="tab" onclick="show(2,this)"><span class="tab-num">3</span>💡 What should we do?</div>
</div>
<div class="canvas">

<!-- PAGE 1 -->
<div class="pg on" id="pg0">
  <div class="insight"><strong>Board answer:</strong> Western Cape is the only province with declining revenue (−6.0% H1 YoY). All others grew 9–15%. Foot traffic is flat — customers are visiting but spending R19 less per trip. This is a basket-size problem, not a volume problem.</div>
  <div class="krow">
    <div class="kcard"><div class="klabel">WC Revenue H1 2025</div><div class="kval">R362.9K</div><div class="ksub red">▼ R23.3K vs H1 2024</div></div>
    <div class="kcard"><div class="klabel">WC YoY Change</div><div class="kval red">−6.0%</div><div class="ksub muted">Only declining province</div></div>
    <div class="kcard"><div class="klabel">WC Avg Basket</div><div class="kval">R373</div><div class="ksub red">▼ R19 vs H1 2024 (−4.8%)</div></div>
    <div class="kcard"><div class="klabel">WC Transactions H1</div><div class="kval">~980</div><div class="ksub muted">Broadly flat (−2.3% only)</div></div>
  </div>
  <div class="grid2">
    <div class="card">
      <div class="ctitle">Monthly Revenue — All Provinces (Jan 2024 – Jun 2025)</div>
      <div class="leg">
        <div class="li"><div class="lsq" style="background:#c0392b;"></div>Western Cape</div>
        <div class="li"><div class="lsq" style="background:#9ca3af;border:1px dashed #6b7280;"></div>Gauteng</div>
        <div class="li"><div class="lsq" style="background:#c4c9c0;border:1px dashed #9ca3af;"></div>KwaZulu-Natal</div>
        <div class="li"><div class="lsq" style="background:#d1d5db;"></div>Eastern Cape</div>
      </div>
      <div style="position:relative;height:195px;"><canvas id="lineC"></canvas></div>
    </div>
    <div class="card">
      <div class="ctitle">H1 Revenue Growth by Province</div>
      <div style="position:relative;height:225px;"><canvas id="provC"></canvas></div>
    </div>
  </div>
  <div class="card" style="margin-bottom:0;">
    <div class="ctitle">Province Summary — H1 2024 vs H1 2025</div>
    <table class="ptable" style="table-layout:fixed;width:100%;">
      <thead><tr><th style="width:28%;">Province</th><th style="width:18%;">H1 2024</th><th style="width:18%;">H1 2025</th><th style="width:12%;">YoY %</th><th style="width:24%;">Interpretation</th></tr></thead>
      <tbody>
        <tr><td style="font-weight:600;">Western Cape</td><td>R386,195</td><td>R362,891</td><td class="red" style="font-weight:700;">−6.0%</td><td style="color:#b91c1c;font-size:9.5px;">⚠ Only declining region</td></tr>
        <tr><td>Eastern Cape</td><td>R88,529</td><td>R96,153</td><td class="grn">+8.6%</td><td style="color:#6b7280;font-size:9.5px;">Healthy growth</td></tr>
        <tr><td>Gauteng</td><td>R249,259</td><td>R273,551</td><td class="grn">+9.7%</td><td style="color:#6b7280;font-size:9.5px;">Strong growth</td></tr>
        <tr><td>KwaZulu-Natal</td><td>R216,410</td><td>R248,124</td><td class="grn">+14.7%</td><td style="color:#6b7280;font-size:9.5px;">Best performer</td></tr>
      </tbody>
    </table>
  </div>
</div>

<!-- PAGE 2 -->
<div class="pg" id="pg1">
  <div class="insight"><strong>Board answer:</strong> Three Mega stores (Bellville −25%, Paarl −12%, Tygervalley −7%) account for 132% of the gross WC decline. Without them, WC would be growing. The culprit is Groceries (−9%) and Household (−11%) — categories nationally growing +3% and +0.1%. Silver-tier loyalty customers are also visiting 10% less often.</div>
  <div class="grid2">
    <div class="card">
      <div class="ctitle">All 12 WC Stores — H1 Revenue Change (Worst to Best)</div>
      <div class="sbar-wrap" id="sbars"></div>
    </div>
    <div style="display:flex;flex-direction:column;gap:11px;">
      <div class="card" style="margin-bottom:0;">
        <div class="ctitle">Store Format Breakdown — WC H1</div>
        <div style="position:relative;height:128px;"><canvas id="fmtC"></canvas></div>
      </div>
      <div class="card" style="margin-bottom:0;">
        <div class="ctitle">Category Revenue Change — WC vs National</div>
        <div class="leg"><div class="li"><div class="lsq" style="background:#c0392b;"></div>WC</div><div class="li"><div class="lsq" style="background:#86efac;border:1px solid #16a34a;"></div>National</div></div>
        <div style="position:relative;height:108px;"><canvas id="catC"></canvas></div>
      </div>
    </div>
  </div>
  <div class="grid2r">
    <div class="card" style="margin-bottom:0;">
      <div class="ctitle">Loyalty Tier Revenue — WC H1 2024 vs H1 2025</div>
      <div id="tierVis"></div>
      <div style="margin-top:8px;font-size:9.5px;color:#6b7280;">Silver visits down 10.3% · Gold visits stable · Silver is the at-risk segment</div>
    </div>
    <div class="card" style="margin-bottom:0;">
      <div class="ctitle">Key Findings — What the Store Data Confirms</div>
      <div style="display:flex;flex-direction:column;gap:7px;margin-top:4px;">
        <div class="finding" style="background:#fef2f2;border-color:#dc2626;color:#7f1d1d;"><strong>Bellville Mega (−25.3%):</strong> Groceries alone lost R12,402 — 65% of Bellville's total decline. Basket dropped R547 → R463.</div>
        <div class="finding" style="background:#fef2f2;border-color:#dc2626;color:#7f1d1d;"><strong>Paarl Mega (−12.0%):</strong> Groceries + Household + Apparel all declining. Broader discretionary pullback. Basket R523 → R464.</div>
        <div class="finding" style="background:#fef9f0;border-color:#f59e0b;color:#78350f;"><strong>Tygervalley (−6.7%):</strong> Visits flat, basket shrinking — classic price-sensitivity. Electronics growing (+21.9%) while staples fall.</div>
        <div class="finding" style="background:#f0fdf4;border-color:#16a34a;color:#14532d;"><strong>Bright spots:</strong> Khayelitsha (+29.6%), Mitchell's Plain (+39.7%), Sea Point (+31.7%) prove no brand problem.</div>
      </div>
    </div>
  </div>
</div>

<!-- PAGE 3 -->
<div class="pg" id="pg2">
  <div class="insight"><strong>Board answer:</strong> Three actions — audit the three failing Mega stores immediately, re-engage Silver-tier customers with a targeted offer, and investigate competitive threats near Bellville and Paarl. The Pap Power Promo model (+50.5% volume in April 2025) is the proven template for the retention campaign.</div>
  <div class="rec3">
    <div class="rec" style="border-top-color:#dc2626;">
      <div class="rec-tag" style="color:#dc2626;">🔥 Immediate — 0 to 4 weeks</div>
      <div class="rec-h">Operational Audit: Bellville, Paarl & Tygervalley Mega</div>
      <div class="rec-b">Three Mega stores account for R30,819 in lost revenue — 132% of the total WC gap. Focus on Groceries and Household shelf availability, pricing, and competitor proximity.<br><br>Bellville is the priority: −R18,827 alone.</div>
      <div class="rec-action" style="background:#fef2f2;color:#b91c1c;">Target: audit within 3 weeks</div>
    </div>
    <div class="rec" style="border-top-color:#d97706;">
      <div class="rec-tag" style="color:#d97706;">👥 Short-term — 1 to 3 months</div>
      <div class="rec-h">Retain Silver-Tier WC Loyalty Customers</div>
      <div class="rec-b">Silver members visiting 10.3% less often. Gold is stable. Run a targeted Groceries/Household offer for WC Silver members only. Model on the Pap Power Promo (+50.5% volume). Use 20% discount rather than 33% to protect margin.</div>
      <div class="rec-action" style="background:#fffbeb;color:#92400e;">Template: Pap Power Promo mechanic</div>
    </div>
    <div class="rec" style="border-top-color:#2563eb;">
      <div class="rec-tag" style="color:#2563eb;">🔍 Investigate — Ongoing</div>
      <div class="rec-h">Identify and Respond to Competitive Threat</div>
      <div class="rec-b">The Bellville Groceries pattern — concentrated in staples, fast decline — is the signature of a new competitor opening nearby. Check for store openings near Bellville and Paarl. Survey Silver-tier WC members not transacting in 90+ days.</div>
      <div class="rec-action" style="background:#eff6ff;color:#1e40af;">Focus: Bellville & Paarl catchments</div>
    </div>
  </div>
  <div class="grid2r" style="margin-bottom:0;">
    <div class="card" style="margin-bottom:0;">
      <div class="ctitle">⭐ Pap Power Promo Results — Proof the Model Works (April 2025)</div>
      <table class="ptable" style="table-layout:fixed;width:100%;">
        <thead><tr><th style="width:40%;">Metric</th><th style="width:25%;">Apr 2024</th><th style="width:25%;">Apr 2025</th><th style="width:10%;"></th></tr></thead>
        <tbody>
          <tr><td>Maize Meal units sold</td><td>307</td><td>462</td><td class="grn" style="font-weight:700;">+50%</td></tr>
          <tr><td>Net revenue (category)</td><td>R14,888</td><td>R15,219</td><td class="grn" style="font-weight:700;">+2.2%</td></tr>
          <tr><td>Discount given</td><td>R0</td><td>R2,500</td><td class="muted">Cost</td></tr>
          <tr><td>Avg total basket</td><td>R309</td><td>R329</td><td class="grn" style="font-weight:700;">+6.5%</td></tr>
          <tr><td>Total store revenue</td><td>R152,457</td><td>R156,913</td><td class="grn" style="font-weight:700;">+2.9%</td></tr>
        </tbody>
      </table>
      <div style="margin-top:8px;font-size:10px;color:#6b7280;">Verdict: Volume +50.5%, revenue +2.2%. Promo model works — recommend 20% discount for Silver-tier campaign to improve margin retention vs 33% used here.</div>
    </div>
    <div class="card" style="margin-bottom:0;">
      <div class="ctitle">WC Bright Spots — The Growth Playbook</div>
      <table class="ptable" style="table-layout:fixed;width:100%;">
        <thead><tr><th style="width:38%;">Store</th><th style="width:20%;">Format</th><th style="width:18%;">H1 change</th><th style="width:24%;">What's working</th></tr></thead>
        <tbody>
          <tr><td style="font-size:10px;">Mitchell's Plain</td><td style="font-size:10px;">Express</td><td class="grn" style="font-weight:700;">+39.7%</td><td style="font-size:9.5px;color:#6b7280;">Underserved area</td></tr>
          <tr><td style="font-size:10px;">Sea Point</td><td style="font-size:10px;">Express</td><td class="grn" style="font-weight:700;">+31.7%</td><td style="font-size:9.5px;color:#6b7280;">High-footfall urban</td></tr>
          <tr><td style="font-size:10px;">Khayelitsha</td><td style="font-size:10px;">Market</td><td class="grn" style="font-weight:700;">+29.6%</td><td style="font-size:9.5px;color:#6b7280;">Visits +20% & basket +7.7%</td></tr>
          <tr><td style="font-size:10px;">Stellenbosch</td><td style="font-size:10px;">Market</td><td class="grn" style="font-weight:700;">+11.0%</td><td style="font-size:9.5px;color:#6b7280;">Consistent, no volatility</td></tr>
        </tbody>
      </table>
      <div style="margin-top:8px;font-size:10px;color:#6b7280;">These 4 stores grew on both visits and basket size. The Imbewu brand is not the problem — format and location fit are working well outside the Mega cluster.</div>
    </div>
  </div>
</div>

</div><!-- canvas -->
<div class="footer">Imbewu Retail &nbsp;·&nbsp; Commercial Analytics Capstone &nbsp;·&nbsp; Witle Academy &nbsp;·&nbsp; June 2025 &nbsp;·&nbsp; 45 stores &nbsp;·&nbsp; 9,164 transactions &nbsp;·&nbsp; Jan 2024 – Jun 2025</div>
</div><!-- db -->

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<script>
function show(i,el){document.querySelectorAll('.pg').forEach((p,j)=>p.classList.toggle('on',j===i));document.querySelectorAll('.tab').forEach(t=>t.classList.remove('on'));el.classList.add('on');}
const months=["Jan'24","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec","Jan'25","Feb","Mar","Apr","May","Jun'25"];
const wcD=[70653,60211,61963,64876,68973,62112,68102,60322,67314,67201,61790,70877,58300,54124,62047,67502,64833,58438];
const gaD=[41825,32515,45205,40974,44594,46716,42028,47016,34788,39388,42693,39331,54425,45685,46410,40672,40881,46412];
const kzD=[35769,34421,39340,30837,38365,39570,41491,38595,40107,39436,38430,38712,40807,40360,48603,34507,40003,45130];
const ecD=[15584,11779,16154,15769,13267,15976,16050,12607,13201,15729,11883,13340,15216,17186,15057,14232,18698,16727];
new Chart(document.getElementById('lineC'),{type:'line',data:{labels:months,datasets:[{label:'Western Cape',data:wcD,borderColor:'#c0392b',backgroundColor:'rgba(192,57,43,.05)',borderWidth:2.5,pointRadius:0,tension:.35,fill:true},{label:'Gauteng',data:gaD,borderColor:'#9ca3af',borderWidth:1.5,pointRadius:0,tension:.35,borderDash:[3,2]},{label:'KwaZulu-Natal',data:kzD,borderColor:'#c4c9c0',borderWidth:1.2,pointRadius:0,tension:.35,borderDash:[2,3]},{label:'Eastern Cape',data:ecD,borderColor:'#d1d5db',borderWidth:1,pointRadius:0,tension:.35}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{callbacks:{label:c=>' R'+Math.round(c.raw/1000)+'K'}}},scales:{x:{grid:{color:'#f0f2ee'},ticks:{font:{size:9},color:'#9ca3af',maxRotation:0,autoSkip:true,maxTicksLimit:9}},y:{grid:{color:'#f0f2ee'},ticks:{font:{size:9},color:'#9ca3af',callback:v=>'R'+Math.round(v/1000)+'K'},min:10000}}}});
new Chart(document.getElementById('provC'),{type:'bar',data:{labels:['Western Cape','Eastern Cape','Gauteng','KwaZulu-Natal'],datasets:[{data:[-6.0,8.6,9.7,14.7],backgroundColor:['#fca5a5','#86efac','#86efac','#86efac'],borderColor:['#dc2626','#16a34a','#16a34a','#16a34a'],borderWidth:1,borderRadius:3}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{callbacks:{label:c=>' '+c.raw+'%'}}},scales:{x:{grid:{color:'#f0f2ee'},ticks:{font:{size:9},color:'#9ca3af',callback:v=>v+'%'}},y:{grid:{display:false},ticks:{font:{size:10},color:'#374151'}}}}});
const stores=[{n:'Mega Bellville',f:'Mega',c:-25.3},{n:'Market George',f:'Market',c:-14.1},{n:'Market Claremont',f:'Market',c:-13.9},{n:'Mega Paarl Central',f:'Mega',c:-12.0},{n:'Express CBD',f:'Express',c:-10.5},{n:'Mega Tygervalley',f:'Mega',c:-6.7},{n:'Mega Parow',f:'Mega',c:1.4},{n:'Express Constantia',f:'Express',c:10.1},{n:'Market Stellenbosch',f:'Market',c:11.0},{n:'Market Khayelitsha',f:'Market',c:29.6},{n:'Express Sea Point',f:'Express',c:31.7},{n:'Express Mitchells Pln',f:'Express',c:39.7}];
const sb=document.getElementById('sbars');
stores.forEach(s=>{const pct=Math.abs(s.c)/40*46;const neg=s.c<0;const fc=s.f==='Mega'?'#7c3aed':s.f==='Market'?'#0891b2':'#059669';sb.innerHTML+=`<div class="srow"><div class="sname" title="${s.n}">${s.n}</div><div class="strack"><div class="scenter"></div><div class="sbar" style="background:${neg?'#fca5a5':'#86efac'};width:${pct}%;${neg?'right:50%':'left:50%'};"></div></div><div class="sval ${neg?'red':'grn'}">${s.c>0?'+':''}${s.c}%</div><div class="sbadge" style="background:${fc}22;color:${fc};">${s.f}</div></div>`;});
new Chart(document.getElementById('fmtC'),{type:'bar',data:{labels:['Express','Market','Mega'],datasets:[{label:'H1 2024',data:[29857,94653,261686],backgroundColor:'#d1d5db',borderRadius:3},{label:'H1 2025',data:[34381,96789,231722],backgroundColor:['#86efac','#86efac','#fca5a5'],borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{callbacks:{label:c=>' R'+Math.round(c.raw/1000)+'K'}}},scales:{x:{grid:{display:false},ticks:{font:{size:9},color:'#9ca3af'}},y:{grid:{color:'#f0f2ee'},ticks:{font:{size:9},color:'#9ca3af',callback:v=>'R'+Math.round(v/1000)+'K'}}}}});
new Chart(document.getElementById('catC'),{type:'bar',data:{labels:['Groceries','Household','H&Beauty','Apparel','Electronics'],datasets:[{label:'WC',data:[-8.9,-10.9,2.6,2.9,8.0],backgroundColor:['#fca5a5','#fca5a5','#86efac','#86efac','#86efac'],borderRadius:2},{label:'National',data:[3.0,0.1,6.5,14.5,6.1],backgroundColor:'rgba(134,239,172,0.35)',borderRadius:2,borderColor:'#16a34a',borderWidth:1}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{callbacks:{label:c=>' '+c.raw+'%'}}},scales:{x:{grid:{display:false},ticks:{font:{size:9},color:'#9ca3af'}},y:{grid:{color:'#f0f2ee'},ticks:{font:{size:9},color:'#9ca3af',callback:v=>v+'%'}}}}});
const tiers=[{name:'Gold',r24:89926,r25:90015,chg:'+0.1%'},{name:'Silver',r24:59410,r25:52673,chg:'−11.3%'},{name:'Bronze',r24:82501,r25:78719,chg:'−4.6%'},{name:'Guest',r24:154358,r25:141484,chg:'−8.3%'}];
const tv=document.getElementById('tierVis');const maxR=165000;
tiers.forEach(t=>{const neg=t.chg.startsWith('−');tv.innerHTML+=`<div class="tier-row"><div class="tier-label">${t.name}</div><div class="tier-bars"><div class="bar-row"><div class="bar-year">2024</div><div class="bar-fill" style="width:${Math.round(t.r24/maxR*200)}px;background:#d1d5db;"></div><div class="bar-rev">R${Math.round(t.r24/1000)}K</div></div><div class="bar-row"><div class="bar-year">2025</div><div class="bar-fill" style="width:${Math.round(t.r25/maxR*200)}px;background:${neg?'#fca5a5':'#86efac'};"></div><div class="bar-rev">R${Math.round(t.r25/1000)}K <span style="color:${neg?'#b91c1c':'#15803d'};font-weight:600;">${t.chg}</span></div></div></div></div>`;});
</script>
</body>
</html>

---

## 🔍 What I Found

| Finding | Detail |
|---|---|
| **WC is uniquely declining** | −6.0% H1 2025 vs H1 2024, while every other province grew (KZN +14.7%, Gauteng +9.7%, EC +8.6%) |
| **Basket size, not foot traffic** | Average spend per visit dropped R392 → R373 (−5.1%). Customers are still visiting — they're leaving with less |
| **4 stores drive the entire decline** | Bellville Mega (−25.3%), Paarl Mega (−12.0%), George Market (−14.1%), Claremont Market (−13.9%) |
| **Silver-tier customers are pulling back** | Silver loyalty members down −11.3% in WC, concentrated in Groceries (−8.9%) and Household (−10.9%). Gold tier held flat at +0.1% |
| **Pap Power Promo worked** | Buy-2-Get-1 on Iwisa Maize Meal drove +50.5% volume and +2.2% net revenue despite a R2,500 discount outlay |

---

## 🧪 Hypotheses Tested

I structured the investigation around four testable hypotheses **before running a single query**:

| # | Hypothesis | Result |
|---|---|---|
| 1 | The decline is unique to WC, not a national trend | ✅ Confirmed — every other province grew |
| 2 | Basket size is falling, not transaction volume | ✅ Confirmed — transactions flat, basket down R19 |
| 3 | The decline is concentrated in specific stores, not uniform | ✅ Confirmed — 4 stores out of 12 |
| 4 | A specific customer segment is driving the pullback | ✅ Confirmed — Silver loyalty tier |

---

## 📁 Project Structure

```
imbewu-retail-investigation/
│
├── README.md                          ← You are here
├── imbewu_dashboard.html              ← Live interactive dashboard
│
├── data/
│   ├── stores.csv
│   ├── customers.csv
│   ├── transactions.csv
│   ├── transaction_items.csv
│   ├── products.csv
│   └── promotions.csv
│
├── sql/
│   └── investigation.sql              ← All SQL queries, commented by hypothesis
│
├── docs/
│   ├── data_dictionary.md             ← Schema documentation + data quality notes
│   ├── exec_summary.docx              ← 2-page COO summary
│   └── PowerBI_Build_Guide_Final.docx ← Step-by-step Power BI build guide
│
└── dashboard/
    └── imbewu_dashboard.pbix          ← Power BI dashboard file (3 pages)
```

---

## 🗄️ The Data

18 months of retail operations data (January 2024 – June 2025) across 45 stores.

| Table | Rows | Description |
|---|---|---|
| `stores` | 45 | Store metadata: format, province, city, manager |
| `customers` | 3,000 | Loyalty programme members (Bronze / Silver / Gold tiers) |
| `transactions` | 9,164 | Every till receipt issued in the period |
| `transaction_items` | 48,641 | Line items inside each transaction |
| `products` | 48 | Product catalogue across 5 categories |
| `promotions` | 4 | Historical and current marketing campaigns |

### Data quality issues found and resolved

| Issue | Table | Action taken |
|---|---|---|
| Mixed province casing (`western cape` vs `Western Cape`) | `stores` | Normalised with `INITCAP()` in all queries |
| ~43% of transactions have no `customer_id` (guest shoppers) | `transactions` | Retained in revenue analysis; labelled "Guest" in loyalty segmentation |
| No direct FK linking transactions to promotions | `promotions` | Inferred promo impact by matching date ranges and product categories |
| `revenue` column loaded as String type in Power BI | `transaction_items` | Fixed data type to Decimal Number in Power Query |

---

## 🔑 Key SQL Patterns Used

```sql
-- Year-on-year comparison using conditional aggregation (no self-join needed)
WITH revenue_by_period AS (
    SELECT
        INITCAP(s.province) AS province,
        SUM(CASE WHEN t.transaction_date BETWEEN '2024-01-01' AND '2024-06-30'
                 THEN (ti.quantity * ti.unit_price_at_sale) - ti.discount_applied
                 ELSE 0 END) AS rev_h1_2024,
        SUM(CASE WHEN t.transaction_date BETWEEN '2025-01-01' AND '2025-06-30'
                 THEN (ti.quantity * ti.unit_price_at_sale) - ti.discount_applied
                 ELSE 0 END) AS rev_h1_2025
    FROM transaction_items ti
    JOIN transactions t      ON ti.transaction_id = t.transaction_id
    JOIN stores s            ON t.store_id        = s.store_id
    GROUP BY INITCAP(s.province)
)
SELECT
    province,
    ROUND(rev_h1_2024, 0)                                        AS rev_h1_2024,
    ROUND(rev_h1_2025, 0)                                        AS rev_h1_2025,
    ROUND((rev_h1_2025 - rev_h1_2024) / rev_h1_2024 * 100, 1)  AS yoy_change_pct
FROM revenue_by_period
ORDER BY yoy_change_pct ASC;
```

**SQL techniques applied:** CTEs · conditional aggregation · multi-table joins · `COALESCE` for NULL handling · `INITCAP` for data normalisation · `DATE_TRUNC` for time series grouping · `DIVIDE` for safe division · window functions

---

## 💡 Recommendations

### 🔴 Immediate (0–4 weeks)
Conduct in-store operational audit at **Bellville Mega** and **Paarl Mega**. These two stores account for R26,821 in lost revenue — more than the entire WC decline. Focus on Groceries and Household pricing versus local competitors.

### 🟡 Short-term (1–3 months)
Run a targeted retention campaign for **Silver-tier WC loyalty members**, focused on Groceries and Household. Model it on the Pap Power Promo structure but use a 20% discount (rather than 33%) to protect margin while restoring visit frequency.

### 🔵 Investigate (ongoing)
The Bellville Groceries decline pattern is consistent with a **new competitor opening nearby**. Check for retail entrants near Bellville and Paarl. Survey Silver-tier WC members who have not transacted in 90+ days.

---

## 🛠️ Tools Used

![SQL](https://img.shields.io/badge/SQL-Databricks-E87722?style=flat-square&logo=databricks&logoColor=white)
![Python](https://img.shields.io/badge/Python-pandas-3776AB?style=flat-square&logo=python&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![Word](https://img.shields.io/badge/Microsoft_Word-Exec_Summary-2B579A?style=flat-square&logo=microsoftword&logoColor=white)
![HTML](https://img.shields.io/badge/HTML-Live_Dashboard-E34F26?style=flat-square&logo=html5&logoColor=white)

| Tool | Used for |
|---|---|
| **Databricks (SQL)** | All data profiling, hypothesis testing, and investigation queries |
| **Python (pandas)** | Exploratory data analysis and data validation |
| **Power BI Desktop** | Executive dashboard (3-page interactive report) |
| **Microsoft Word** | 2-page executive summary for the COO |
| **HTML / Chart.js** | Live portfolio dashboard embedded in this README |

---

## 📚 What I Learned

- How to take an **ambiguous business question** and break it into testable hypotheses before writing any code
- The difference between a **foot traffic problem** and a **basket size problem** — and why the solution is completely different depending on which one it is
- How **conditional aggregation** (`SUM(CASE WHEN...)`) enables clean YoY comparisons in a single query without self-joins
- How to present findings so an executive can **use the dashboard live in a board meeting**, not just read it afterward
- That **data quality documentation matters** — the province casing bug would have silently split Western Cape into two groups and corrupted the entire analysis
- How to manage **scope creep** — four different stakeholders added requests over four weeks; only the ones that served the core question made it into the final deliverable

---

## 🎓 About This Project

| | |
|---|---|
| **Programme** | Data Analyst Programme — Witle Academy |
| **Duration** | 4 weeks |
| **Stakeholders simulated** | Head of Sales · Marketing Manager · Regional Manager · COO |
| **Data** | Synthetic retail dataset — fictional Imbewu Retail chain |
| **Records analysed** | 48,641 transaction line items across 18 months |

---

*Built with curiosity. Presented with clarity.*
