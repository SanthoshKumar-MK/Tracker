<!-- filename: monthly-expense-tracker-mobile-category-actions.html --><!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title>Monthly Expense Tracker</title>
  <link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;600;700;800&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    :root{--dl-green:#86BC25;--dl-green-dark:#6B9A1E;--dl-blue:#00A3E0;--dl-blue-dark:#005587;--dl-charcoal:#282728;--dl-gray-100:#F5F5F5;--dl-gray-200:#E6E6E6;--warn:#E8A317;--error:#DA291C}
    *{box-sizing:border-box}body{margin:0;font-family:'Open Sans',sans-serif;background:var(--dl-gray-100);color:var(--dl-charcoal)}
    header{background:var(--dl-charcoal);padding:16px 24px;display:flex;justify-content:space-between;align-items:center;gap:16px;flex-wrap:wrap}
    h1{margin:0;color:#fff;font-size:2rem;font-weight:800}h1 span{color:var(--dl-green)}
    .header-right,.month-nav,.rec-actions,.cat-actions,.form-row,.chart-legend,.legend-item,.balance-actions{display:flex;align-items:center}
    .header-right{gap:8px;flex-wrap:wrap}.month-nav{gap:8px;background:rgba(255,255,255,.08);padding:4px 8px;border-radius:24px}
    .month-label{color:#fff;font-size:.9rem;font-weight:700;min-width:136px;text-align:center}.current-badge{display:none;background:var(--dl-green);color:#fff;padding:4px 8px;border-radius:12px;font-size:.72rem;font-weight:700}
    .container{max-width:1120px;margin:0 auto;padding:24px 16px}.summary-bar,.rec-grid,.cat-grid{display:grid;gap:16px}.summary-bar{grid-template-columns:repeat(5,1fr);margin-bottom:32px}
    .s-card,.rec-card,.cat-card,.chart-box,.modal{background:#fff;border:1px solid var(--dl-gray-200);box-shadow:0 1px 3px rgba(0,0,0,.05)}.s-card,.rec-card,.cat-card,.chart-box{border-radius:10px}
    .s-card{padding:16px}.s-card .lbl{font-size:.72rem;font-weight:700;color:#777;text-transform:uppercase;letter-spacing:.04em}.s-card .val{margin-top:8px;font-size:1.5rem;font-weight:800}.s-card .sub{margin-top:8px;font-size:.74rem;color:#777;font-weight:600}
    .green .val{color:var(--dl-green)}.blue .val{color:var(--dl-blue)}.warn .val{color:var(--warn)}.gray .val{color:#888}.clickable{cursor:pointer;transition:160ms}
    .clickable:hover,.rec-card:hover,.cat-card:hover,.dash-card:hover{box-shadow:0 4px 12px rgba(0,0,0,.08);border-color:var(--dl-green)}
    .section{margin-bottom:32px}.sec-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:16px}.sec-head h2{margin:0;font-size:1rem;font-weight:700;display:flex;gap:8px;align-items:center}.sec-head h2::before{content:'';width:4px;height:18px;background:var(--dl-green);border-radius:2px}
    .rec-grid{grid-template-columns:repeat(auto-fill,minmax(230px,1fr))}.cat-grid{grid-template-columns:repeat(auto-fill,minmax(220px,1fr))}
    .rec-card,.cat-card{padding:16px;transition:160ms}.rec-card.paid{background:#F6FFE8;border-color:var(--dl-green)}
    .rec-top,.cat-top{display:flex;justify-content:space-between;gap:8px}.rec-name,.cat-name{font-weight:700}.rec-day,.cat-count,.rec-amt-sub{font-size:.72rem;color:#888}
    .rec-amt,.cat-total{font-size:1.2rem;font-weight:800;margin:12px 0 4px}.cat-total{color:var(--dl-green)}.cat-icon{font-size:1.4rem}
    .rec-actions,.cat-actions{gap:8px;margin-top:12px;flex-wrap:nowrap}.rec-actions .btn:first-child,.cat-actions .btn:first-child{flex:1 1 auto}.rec-actions .icon-btn,.cat-actions .icon-btn{flex:0 0 34px}
    .dash-card{border:2px dashed var(--dl-gray-200);border-radius:10px;display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:120px;background:#fff;cursor:pointer;transition:160ms}.dash-card .plus{font-size:2rem;color:#aaa}.dash-card p{margin:4px 0 0;color:#888;font-weight:600;font-size:.82rem}
    .due-badge{padding:10px 8px;border-radius:12px;font-size:.68rem;font-weight:700;white-space:nowrap}.paid-b{background:var(--dl-green);color:#fff}.soon-b{background:var(--warn);color:#fff}.overdue-b{background:var(--error);color:#fff}.future-b{background:var(--dl-gray-200);color:#555}
    .chart-box{padding:24px}.chart-box canvas{max-height:300px}.chart-legend{gap:16px;margin-top:16px;flex-wrap:wrap}.legend-item{gap:8px;font-size:.78rem;font-weight:600;color:#555}.legend-dot{width:12px;height:12px;border-radius:3px}
    .btn{border:none;border-radius:8px;padding:8px 12px;font:600 .82rem 'Open Sans',sans-serif;cursor:pointer;transition:160ms;white-space:nowrap}.btn-green{background:var(--dl-green);color:#fff}.btn-green:hover{background:var(--dl-green-dark)}.btn-blue{background:var(--dl-blue);color:#fff}.btn-blue:hover{background:var(--dl-blue-dark)}.btn-outline{background:#fff;color:var(--dl-charcoal);border:1px solid var(--dl-gray-200)}.btn-outline:hover{background:var(--dl-gray-100)}.btn-danger{background:var(--error);color:#fff}.btn-sm{padding:6px 10px;font-size:.76rem}.btn-full{width:100%}
    .icon-btn{width:34px;min-width:34px;padding:6px 0;font-size:.95rem;line-height:1;text-align:center}
    .overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.45);align-items:center;justify-content:center;padding:16px;z-index:100}.overlay.open{display:flex}.modal{width:100%;max-width:450px;border-radius:12px;padding:24px}
    .modal-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:16px}.modal-head h3{margin:0;font-size:1.05rem;font-weight:800}.modal-close{background:none;border:none;font-size:1.2rem;cursor:pointer;color:#888}
    .form-group{margin-bottom:16px}.form-group label{display:block;margin-bottom:8px;font-size:.78rem;font-weight:700;color:#555}.form-group input{width:100%;padding:10px 12px;border:1px solid var(--dl-gray-200);border-radius:8px;font:400 .92rem 'Open Sans',sans-serif;outline:none}.form-group input:focus{border-color:var(--dl-green)}
    .input-hint{margin-top:6px;font-size:.72rem;color:#999}.entry-list{max-height:180px;overflow:auto;border:1px solid var(--dl-gray-200);border-radius:8px;padding:8px 12px;margin-bottom:16px}.entry-empty{padding:8px 0;text-align:center;color:#aaa;font-size:.82rem}
    .entry-row{display:flex;align-items:center;gap:8px;padding:8px 0;border-bottom:1px solid var(--dl-gray-200)}.entry-row:last-child{border-bottom:none}.edesc{flex:1}.eamt{font-weight:700;color:var(--dl-green)}
    .balance-actions{gap:8px;width:100%;flex-wrap:nowrap}.balance-btn{flex:1 1 0;min-width:0;display:flex;justify-content:center;align-items:center}
    .toast{position:fixed;right:24px;bottom:24px;background:var(--dl-charcoal);color:#fff;padding:12px 16px;border-radius:8px;font-size:.82rem;font-weight:600;opacity:0;transform:translateY(8px);transition:180ms;pointer-events:none;z-index:200}.toast.show{opacity:1;transform:translateY(0)}.toast.success{background:var(--dl-green)}.toast.warn{background:var(--warn)}
    @media(max-width:980px){.summary-bar{grid-template-columns:repeat(3,1fr)}}
    @media(max-width:768px){header{padding:16px}.header-right{width:100%;justify-content:space-between}.month-nav{width:100%;justify-content:space-between}.month-label{min-width:0;flex:1}.rec-grid,.cat-grid{grid-template-columns:repeat(auto-fill,minmax(200px,1fr))}}
    @media(max-width:560px){.summary-bar{grid-template-columns:repeat(2,1fr)}.rec-grid,.cat-grid{grid-template-columns:1fr}.rec-actions,.cat-actions,.balance-actions,.form-row{flex-wrap:wrap}.rec-actions .btn:first-child,.cat-actions .btn:first-child,.balance-btn,.form-row .btn{width:100%;flex:1 1 100%}.icon-btn{width:48%;min-width:48%}.modal{padding:18px}.chart-box{padding:16px}}
    @media(max-width:420px){.summary-bar{grid-template-columns:1fr}h1{font-size:1.6rem}.btn{padding:10px 12px}.entry-row{flex-wrap:wrap}.entry-row .btn{width:100%}}
  </style>
</head>
<body>
  <header>
    <h1>Expense <span>Tracker</span></h1>
    <div class="header-right">
      <div class="month-nav">
        <button class="btn btn-outline btn-sm" id="prevBtn">‹</button>
        <span class="month-label" id="monthLabel"></span>
        <button class="btn btn-outline btn-sm" id="nextBtn">›</button>
      </div>
      <span class="current-badge" id="currentBadge">Current</span>
      <button class="btn btn-blue" id="exportBtn">Export CSV</button>
      <button class="btn btn-danger" id="resetBtn">Reset Data</button>
    </div>
  </header>

  <div class="container">
    <div class="summary-bar">
      <div class="s-card green"><div class="lbl">Total Spent</div><div class="val" id="totalSpent">₹0</div></div>
      <div class="s-card blue"><div class="lbl">Recurring Total</div><div class="val" id="recurringTotal">₹0</div></div>
      <div class="s-card warn"><div class="lbl">Categories Total</div><div class="val" id="catTotal">₹0</div></div>
      <div class="s-card gray"><div class="lbl">Recurring Paid</div><div class="val" id="recurringPaid">0/0</div></div>
      <div class="s-card clickable" id="balanceCard">
        <div class="lbl">Available Balance</div>
        <div class="val" id="availableBalance">₹0</div>
        <div class="sub" id="balanceBase">Monthly budget: ₹0</div>
      </div>
    </div>

    <div class="section"><div class="sec-head"><h2>Recurring Expenses</h2></div><div class="rec-grid" id="recurringGrid"></div></div>
    <div class="section"><div class="sec-head"><h2>Expense Categories</h2></div><div class="cat-grid" id="categoryGrid"></div></div>
    <div class="section">
      <div class="sec-head"><h2>Month-over-Month Spend</h2></div>
      <div class="chart-box">
        <canvas id="spendChart"></canvas>
        <div class="chart-legend">
          <div class="legend-item"><span class="legend-dot" style="background:#86BC25"></span>Recurring</div>
          <div class="legend-item"><span class="legend-dot" style="background:#00A3E0"></span>Categories</div>
          <div class="legend-item"><span class="legend-dot" style="background:#282728"></span>Total</div>
        </div>
      </div>
    </div>
  </div>

  <div class="overlay" id="recModal">
    <div class="modal">
      <div class="modal-head"><h3 id="recModalTitle">Add Recurring Expense</h3><button class="modal-close" data-close="recModal">✕</button></div>
      <div class="form-group"><label>Expense Name</label><input id="recName" placeholder="e.g. Netflix, Insurance"></div>
      <div class="form-group"><label>Due Day of Month</label><input id="recDay" type="number" min="1" max="31" placeholder="1-31"></div>
      <div class="form-group"><label>Default Amount (₹)</label><input id="recAmt" type="number" min="0" placeholder="e.g. 5000"></div>
      <div class="form-row"><button class="btn btn-green btn-full" id="recSaveBtn">Save</button><button class="btn btn-outline" data-close="recModal">Cancel</button></div>
    </div>
  </div>

  <div class="overlay" id="expenseModal">
    <div class="modal">
      <div class="modal-head"><h3 id="expModalTitle">Add Expense</h3><button class="modal-close" data-close="expenseModal">✕</button></div>
      <div class="form-group"><label>Description</label><input id="expDesc" placeholder="e.g. Weekly groceries"></div>
      <div class="form-group"><label>Amount (₹)</label><input id="expAmount" type="number" min="0" placeholder="0"></div>
      <div class="entry-list" id="entryList"></div>
      <div class="form-row"><button class="btn btn-green" id="addExpenseBtn">Add</button><button class="btn btn-outline" data-close="expenseModal">Close</button></div>
    </div>
  </div>

  <div class="overlay" id="catModal">
    <div class="modal">
      <div class="modal-head"><h3 id="catModalTitle">Add Custom Category</h3><button class="modal-close" data-close="catModal">✕</button></div>
      <div class="form-group"><label>Category Name</label><input id="catName" placeholder="e.g. Travel, Utilities"></div>
      <div class="form-group"><label>Icon</label><input id="catIcon" placeholder="e.g. ✈️" maxlength="4"></div>
      <div class="form-row"><button class="btn btn-green btn-full" id="catSaveBtn">Create Category</button><button class="btn btn-outline" data-close="catModal">Cancel</button></div>
    </div>
  </div>

  <div class="overlay" id="balanceModal">
    <div class="modal">
      <div class="modal-head"><h3>Monthly Balance</h3><button class="modal-close" data-close="balanceModal">✕</button></div>
      <div class="form-group">
        <label>Amount (₹)</label>
        <input id="balanceInput" type="number" min="0" placeholder="Use for manual or rollover addition">
        <div class="input-hint" id="balanceHint"></div>
      </div>
      <div class="form-row balance-actions">
        <button class="btn btn-green balance-btn" id="saveBalanceBtn">Save Manual</button>
        <button class="btn btn-blue balance-btn" id="addRolloverBtn">Add to Rollover</button>
        <button class="btn btn-outline balance-btn" id="rolloverBtn">Use Rollover</button>
      </div>
    </div>
  </div>

  <div class="toast" id="toast"></div>

  <script>
    // Code Generated by Sidekick is for learning and experimentation purposes only.
    const fmt=n=>'₹'+Number(n||0).toLocaleString('en-IN');
    const ord=n=>{const s=['th','st','nd','rd'],v=n%100;return n+(s[(v-20)%10]||s[v]||s[0]);};
    const monthKey=(y,m)=>`${y}-${String(m+1).padStart(2,'0')}`, prevMonth=(y,m)=>m?{y,m:m-1}:{y:y-1,m:11};
    const monthNames=['January','February','March','April','May','June','July','August','September','October','November','December'], monthShort=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
    const today=new Date(), DB_NAME='ExpenseTrackerDB', DB_VERSION=1, STORE='appState', APP_KEY='main';
    const blankMonth=()=>({recurring:{},categories:{},balanceOverride:null,balanceAddition:0});
    const defaultState=()=>({recurringDefs:[{id:1,name:'Rent',day:1,defaultAmount:25000},{id:2,name:'EMI',day:2,defaultAmount:25000},{id:3,name:'Mutual Fund',day:4,defaultAmount:2200}],categoryDefs:[{id:1,name:'Groceries',icon:'🛒'},{id:2,name:'Investment',icon:'📈'},{id:3,name:'Food',icon:'🍔'},{id:4,name:'Misc',icon:'📦'}],monthData:{}});
    let state=defaultState(), viewYear=today.getFullYear(), viewMonth=today.getMonth(), editingRecId=null, editingCatId=null, activeCatId=null, chart=null, db=null;

    const $=id=>document.getElementById(id);
    function showToast(msg,type=''){const t=$('toast');t.textContent=msg;t.className=`toast show ${type}`;clearTimeout(t._tid);t._tid=setTimeout(()=>t.className='toast',3000);}
    function monthTotalFrom(md){const rec=state.recurringDefs.filter(d=>md.recurring[d.id]?.paid).reduce((s,d)=>s+Number(md.recurring[d.id]?.amount||0),0);const cat=state.categoryDefs.reduce((s,d)=>s+(md.categories[d.id]||[]).reduce((a,e)=>a+Number(e.amount||0),0),0);return{recSpent:rec,catSpent:cat,totalSpent:rec+cat};}
    function normalizeMonth(md){md.recurring=md.recurring||{};md.categories=md.categories||{};if(md.balanceOverride===undefined) md.balanceOverride=typeof md.availableBalance==='number'?md.availableBalance:null;if(md.balanceAddition===undefined) md.balanceAddition=0;delete md.availableBalance;state.recurringDefs.forEach(d=>{if(!md.recurring[d.id]) md.recurring[d.id]={paid:false,amount:d.defaultAmount};});state.categoryDefs.forEach(d=>{if(!md.categories[d.id]) md.categories[d.id]=[];});return md;}
    function peekMonth(y,m){const md=state.monthData[monthKey(y,m)];return md?normalizeMonth(md):null;}
    function getMonth(y,m){const k=monthKey(y,m);if(!state.monthData[k]) state.monthData[k]=blankMonth();return normalizeMonth(state.monthData[k]);}
    function snapshot(y,m,depth=0){const md=peekMonth(y,m)||blankMonth(), spent=monthTotalFrom(normalizeMonth(md)).totalSpent, manual=md.balanceOverride, add=Number(md.balanceAddition||0);let budget,source;if(manual!==null&&manual!==''&&manual!==undefined){budget=Number(manual)||0;source='Manual';}else if(depth>120){budget=add;source=add?'Rollover + Added':'Rolled over';}else{const p=prevMonth(y,m), prev=snapshot(p.y,p.m,depth+1);budget=prev.remaining+add;source=add?`Rollover + ${fmt(add)}`:'Rolled over';}return{budget,spent,remaining:budget-spent,source};}
    function isCurrentMonth(){return viewYear===today.getFullYear()&&viewMonth===today.getMonth();}
    function openModal(id){$(id).classList.add('open')} function closeModal(id){$(id).classList.remove('open')} function nextId(arr){return arr.length?Math.max(...arr.map(x=>x.id))+1:Date.now()}
    function dueStatus(day,paid){if(paid) return ['paid-b','Paid ✓'];if(!isCurrentMonth()) return ['future-b',`Due ${ord(day)}`];const diff=day-today.getDate();if(diff<0) return ['overdue-b',`${ord(day)} — Overdue`];if(diff===0) return ['soon-b','Due Today'];if(diff<=3) return ['soon-b',`Due in ${diff}d`];return ['future-b',`Due ${ord(day)}`];}

    function openDB(){return new Promise((resolve,reject)=>{const req=indexedDB.open(DB_NAME,DB_VERSION);req.onupgradeneeded=e=>{const d=e.target.result;if(!d.objectStoreNames.contains(STORE)) d.createObjectStore(STORE,{keyPath:'key'});};req.onsuccess=()=>resolve(req.result);req.onerror=()=>reject(req.error);});}
    function readState(){return new Promise((resolve,reject)=>{const tx=db.transaction(STORE,'readonly'), req=tx.objectStore(STORE).get(APP_KEY);req.onsuccess=()=>resolve(req.result?.data||null);req.onerror=()=>reject(req.error);});}
    function writeState(){return new Promise((resolve,reject)=>{const tx=db.transaction(STORE,'readwrite');tx.objectStore(STORE).put({key:APP_KEY,data:state});tx.oncomplete=resolve;tx.onerror=()=>reject(tx.error);});}
    function deleteState(){return new Promise((resolve,reject)=>{const tx=db.transaction(STORE,'readwrite'), req=tx.objectStore(STORE).delete(APP_KEY);req.onsuccess=resolve;req.onerror=()=>reject(req.error);});}
    async function persist(){try{if(db) await writeState();}catch(e){console.error(e);showToast('Save failed','warn');}}
    async function initDB(){try{db=await openDB();const saved=await readState();if(saved){state={recurringDefs:Array.isArray(saved.recurringDefs)?saved.recurringDefs:defaultState().recurringDefs,categoryDefs:Array.isArray(saved.categoryDefs)?saved.categoryDefs:defaultState().categoryDefs,monthData:saved.monthData&&typeof saved.monthData==='object'?saved.monthData:{}};Object.values(state.monthData).forEach(normalizeMonth);await persist();}else await persist();}catch(e){console.error(e);showToast('IndexedDB unavailable; using temporary memory','warn');}render();}

    function renderSummary(md){const totals=monthTotalFrom(md), snap=snapshot(viewYear,viewMonth), rem=snap.remaining;$('totalSpent').textContent=fmt(totals.totalSpent);$('recurringTotal').textContent=fmt(totals.recSpent);$('catTotal').textContent=fmt(totals.catSpent);$('recurringPaid').textContent=`${state.recurringDefs.filter(d=>md.recurring[d.id]?.paid).length}/${state.recurringDefs.length}`;const bal=$('availableBalance');bal.textContent=fmt(rem);bal.style.color=rem<0?'var(--error)':rem===0?'var(--dl-charcoal)':'var(--dl-green)';$('balanceBase').textContent=`Monthly budget: ${fmt(snap.budget)} • ${snap.source}`;}
    function renderRecurring(md){$('recurringGrid').innerHTML=state.recurringDefs.map(d=>{const e=md.recurring[d.id], [bc,bl]=dueStatus(d.day,e.paid), sub=Number(e.amount)===Number(d.defaultAmount)?'Default amount':`Default: ${fmt(d.defaultAmount)}`;return `<div class="rec-card ${e.paid?'paid':''}"><div class="rec-top"><div><div class="rec-name">${d.name}</div><div class="rec-day">Due ${ord(d.day)} every month</div></div><span class="due-badge ${bc}">${bl}</span></div><div class="rec-amt">${fmt(e.amount)}</div><div class="rec-amt-sub">${sub}</div><div class="rec-actions"><button class="btn ${e.paid?'btn-outline':'btn-green'} btn-sm" data-action="toggle-paid" data-id="${d.id}">${e.paid?'Unmark':'Mark Paid'}</button><button class="btn btn-blue btn-sm icon-btn" data-action="edit-rec" data-id="${d.id}" title="Edit" aria-label="Edit">✎</button><button class="btn btn-danger btn-sm icon-btn" data-action="delete-rec" data-id="${d.id}" title="Delete" aria-label="Delete">🗑</button></div></div>`}).join('')+`<div class="dash-card" data-action="open-add-rec"><div class="plus">＋</div><p>Add Recurring</p></div>`;}
    function renderCategories(md){$('categoryGrid').innerHTML=state.categoryDefs.map(d=>{const entries=md.categories[d.id]||[], total=entries.reduce((s,e)=>s+Number(e.amount||0),0);return `<div class="cat-card"><div class="cat-top"><div class="cat-icon">${d.icon}</div><div class="cat-count">${entries.length} entr${entries.length===1?'y':'ies'}</div></div><div class="cat-name">${d.name}</div><div class="cat-total">${fmt(total)}</div><div class="cat-actions"><button class="btn btn-green btn-sm" data-action="open-expense" data-id="${d.id}">Open</button><button class="btn btn-blue btn-sm icon-btn" data-action="edit-cat" data-id="${d.id}" title="Edit" aria-label="Edit">✎</button><button class="btn btn-danger btn-sm icon-btn" data-action="delete-cat" data-id="${d.id}" title="Delete" aria-label="Delete">🗑</button></div></div>`}).join('')+`<div class="dash-card" data-action="open-cat-modal"><div class="plus">＋</div><p>Add Category</p></div>`;}
    function renderChart(){const labels=[], recData=[], catData=[];for(let i=5;i>=0;i--){let y=viewYear,m=viewMonth-i;while(m<0){m+=12;y--}const md=peekMonth(y,m)||blankMonth();normalizeMonth(md);labels.push(`${monthShort[m]} ${y}`);const t=monthTotalFrom(md);recData.push(t.recSpent);catData.push(t.catSpent)}const totalData=recData.map((v,i)=>v+catData[i]), ctx=$('spendChart').getContext('2d');if(chart) chart.destroy();chart=new Chart(ctx,{type:'bar',data:{labels,datasets:[{label:'Recurring',data:recData,backgroundColor:'#86BC25',borderRadius:5},{label:'Categories',data:catData,backgroundColor:'#00A3E0',borderRadius:5},{label:'Total',data:totalData,type:'line',borderColor:'#282728',backgroundColor:'rgba(40,39,40,.08)',pointBackgroundColor:'#282728',pointRadius:4,borderWidth:2,tension:.35,fill:true}]},options:{responsive:true,maintainAspectRatio:true,plugins:{legend:{display:false},tooltip:{callbacks:{label:c=>` ${c.dataset.label}: ${fmt(c.parsed.y)}`}}},scales:{x:{stacked:true,grid:{display:false}},y:{stacked:true,ticks:{callback:v=>'₹'+(v>=1000?(v/1000).toFixed(0)+'k':v)},grid:{color:'#f0f0f0'}}}}});}
    function renderMonthNav(){$('monthLabel').textContent=`${monthNames[viewMonth]} ${viewYear}`;$('currentBadge').style.display=isCurrentMonth()?'inline-block':'none';$('nextBtn').disabled=isCurrentMonth();}
    function render(){const md=getMonth(viewYear,viewMonth);renderMonthNav();renderSummary(md);renderRecurring(md);renderCategories(md);renderChart();}
    function shiftMonth(dir){if(dir===1&&isCurrentMonth()) return;viewMonth+=dir;if(viewMonth>11){viewMonth=0;viewYear++}if(viewMonth<0){viewMonth=11;viewYear--}render()}

    function openAddRec(){editingRecId=null;$('recModalTitle').textContent='Add Recurring Expense';$('recSaveBtn').textContent='Save';['recName','recDay','recAmt'].forEach(id=>$(id).value='');openModal('recModal');setTimeout(()=>$('recName').focus(),60)}
    function openEditRec(id){const d=state.recurringDefs.find(x=>x.id===id);if(!d) return;editingRecId=id;$('recModalTitle').textContent=`Edit — ${d.name}`;$('recName').value=d.name;$('recDay').value=d.day;$('recAmt').value=d.defaultAmount;openModal('recModal');setTimeout(()=>$('recName').focus(),60)}
    async function saveRecurring(){const name=$('recName').value.trim(), day=parseInt($('recDay').value,10), amt=parseFloat($('recAmt').value);if(!name) return showToast('Please enter an expense name','warn');if(!day||day<1||day>31) return showToast('Enter a valid due day','warn');if(isNaN(amt)||amt<0) return showToast('Enter a valid amount','warn');if(editingRecId!==null){const d=state.recurringDefs.find(x=>x.id===editingRecId), old=d.defaultAmount;d.name=name;d.day=day;d.defaultAmount=amt;const md=getMonth(viewYear,viewMonth);if(!md.recurring[d.id].paid||old===md.recurring[d.id].amount) md.recurring[d.id].amount=amt;showToast(`Updated "${name}"`,'success')}else{const id=nextId(state.recurringDefs);state.recurringDefs.push({id,name,day,defaultAmount:amt});Object.values(state.monthData).forEach(md=>normalizeMonth(md).recurring[id]={paid:false,amount:amt});showToast(`Added "${name}"`,'success')}await persist();closeModal('recModal');render();}
    async function deleteRecurring(id){const d=state.recurringDefs.find(x=>x.id===id);if(!d||!confirm(`Delete recurring expense "${d.name}"?`)) return;state.recurringDefs=state.recurringDefs.filter(x=>x.id!==id);Object.values(state.monthData).forEach(md=>delete normalizeMonth(md).recurring[id]);await persist();showToast(`Deleted "${d.name}"`,'warn');render()}
    async function togglePaid(id){const md=getMonth(viewYear,viewMonth), d=state.recurringDefs.find(x=>x.id===id);md.recurring[id].paid=!md.recurring[id].paid;await persist();showToast(md.recurring[id].paid?`${d.name} marked paid`:`${d.name} unmarked`,md.recurring[id].paid?'success':'');render()}

    function openExpenseModal(catId){activeCatId=catId;const def=state.categoryDefs.find(c=>c.id===catId), md=getMonth(viewYear,viewMonth);$('expModalTitle').textContent=`${def.icon} ${def.name}`;$('expDesc').value='';$('expAmount').value='';renderEntryList(def,md.categories[catId]||[]);openModal('expenseModal');setTimeout(()=>$('expDesc').focus(),60)}
    function renderEntryList(def,entries){$('entryList').innerHTML=entries.length?entries.map((e,i)=>`<div class="entry-row"><span class="edesc">${e.desc}</span><span class="eamt">${fmt(e.amount)}</span><button class="btn btn-danger btn-sm" data-action="delete-entry" data-id="${def.id}" data-index="${i}">Delete</button></div>`).join(''):'<div class="entry-empty">No entries yet — add one above.</div>'}
    async function addExpenseEntry(){const desc=$('expDesc').value.trim()||'Expense', amount=parseFloat($('expAmount').value);if(isNaN(amount)||amount<=0) return showToast('Enter a valid amount','warn');const md=getMonth(viewYear,viewMonth), def=state.categoryDefs.find(c=>c.id===activeCatId);md.categories[activeCatId].push({desc,amount});await persist();$('expDesc').value='';$('expAmount').value='';renderEntryList(def,md.categories[activeCatId]);render();showToast(`Added ${fmt(amount)} to ${def.name}`,'success');$('expDesc').focus()}

    function openAddCategory(){editingCatId=null;$('catModalTitle').textContent='Add Custom Category';$('catSaveBtn').textContent='Create Category';$('catName').value='';$('catIcon').value='';openModal('catModal');setTimeout(()=>$('catName').focus(),60)}
    function openEditCategory(id){const d=state.categoryDefs.find(x=>x.id===id);if(!d) return;editingCatId=id;$('catModalTitle').textContent=`Edit — ${d.name}`;$('catSaveBtn').textContent='Save Changes';$('catName').value=d.name;$('catIcon').value=d.icon;openModal('catModal');setTimeout(()=>$('catName').focus(),60)}
    async function saveCategory(){const name=$('catName').value.trim(), icon=$('catIcon').value.trim()||'📌';if(!name) return showToast('Category name is required','warn');if(editingCatId!==null){const d=state.categoryDefs.find(x=>x.id===editingCatId);d.name=name;d.icon=icon;showToast(`Updated "${name}" category`,'success')}else{const id=nextId(state.categoryDefs);state.categoryDefs.push({id,name,icon});Object.values(state.monthData).forEach(md=>normalizeMonth(md).categories[id]=[]);showToast(`Added "${name}" category`,'success')}await persist();closeModal('catModal');render()}
    async function deleteCategory(id){const d=state.categoryDefs.find(x=>x.id===id);if(!d||!confirm(`Delete category "${d.name}" and all its entries?`)) return;state.categoryDefs=state.categoryDefs.filter(x=>x.id!==id);Object.values(state.monthData).forEach(md=>delete normalizeMonth(md).categories[id]);if(activeCatId===id) closeModal('expenseModal');await persist();showToast(`Deleted "${d.name}" category`,'warn');render()}
    async function deleteEntry(catId,index){const md=getMonth(viewYear,viewMonth), def=state.categoryDefs.find(c=>c.id===catId);md.categories[catId].splice(index,1);await persist();renderEntryList(def,md.categories[catId]);render();showToast('Entry deleted','warn')}

    function openBalanceModal(){const md=getMonth(viewYear,viewMonth), snap=snapshot(viewYear,viewMonth);$('balanceInput').value=md.balanceOverride??(md.balanceAddition||'');$('balanceHint').textContent=md.balanceOverride!==null?`Manual budget active: ${fmt(md.balanceOverride)}`:md.balanceAddition?`Using rollover plus addition: ${fmt(md.balanceAddition)}`:`Using rollover: ${fmt(snap.budget)} from prior month ending balance`;openModal('balanceModal');setTimeout(()=>$('balanceInput').focus(),60)}
    async function saveMonthlyBalance(){const value=parseFloat($('balanceInput').value);if(isNaN(value)||value<0) return showToast('Enter a valid manual budget','warn');const md=getMonth(viewYear,viewMonth);md.balanceOverride=value;md.balanceAddition=0;await persist();closeModal('balanceModal');render();showToast('Manual monthly budget updated','success')}
    async function addToRollover(){const value=parseFloat($('balanceInput').value);if(isNaN(value)||value<0) return showToast('Enter a valid addition amount','warn');const md=getMonth(viewYear,viewMonth);md.balanceOverride=null;md.balanceAddition=value;await persist();closeModal('balanceModal');render();showToast('Rollover addition saved','success')}
    async function useRollover(){const md=getMonth(viewYear,viewMonth);md.balanceOverride=null;md.balanceAddition=0;await persist();closeModal('balanceModal');render();showToast('This month now uses rollover','success')}

    async function resetAppData(){if(!confirm('This will delete all saved expense data and restore defaults. Continue?')) return;try{if(db) await deleteState();state=defaultState();viewYear=today.getFullYear();viewMonth=today.getMonth();editingRecId=null;editingCatId=null;activeCatId=null;document.querySelectorAll('.overlay.open').forEach(o=>o.classList.remove('open'));await persist();render();showToast('All saved data has been reset','warn')}catch(e){console.error(e);showToast('Reset failed','warn')}}
    function exportCSV(){const md=getMonth(viewYear,viewMonth), totals=monthTotalFrom(md), snap=snapshot(viewYear,viewMonth);let csv=`Monthly Expense Tracker — ${monthNames[viewMonth]} ${viewYear}\n\n`;csv+='RECURRING EXPENSES\nName,Due Day,Default Amount,This Month Amount,Status\n';state.recurringDefs.forEach(d=>{const e=md.recurring[d.id];csv+=`"${d.name}",${ord(d.day)},${d.defaultAmount},${e.amount},${e.paid?'Paid':'Unpaid'}\n`});csv+='\nCATEGORY EXPENSES\nCategory,Description,Amount\n';state.categoryDefs.forEach(d=>(md.categories[d.id]||[]).forEach(e=>csv+=`"${d.name}","${e.desc}",${e.amount}\n`));csv+=`\nSUMMARY\nBudget Source,${snap.source}\nMonthly Budget,${snap.budget}\nRemaining Balance,${snap.remaining}\nRecurring Paid Total,${totals.recSpent}\nCategories Total,${totals.catSpent}\nGrand Total,${totals.totalSpent}\n`;const blob=new Blob([csv],{type:'text/csv'}), url=URL.createObjectURL(blob), a=document.createElement('a');a.href=url;a.download=`expenses-${monthKey(viewYear,viewMonth)}.csv`;a.click();URL.revokeObjectURL(url);showToast('CSV exported','success')}

    $('prevBtn').addEventListener('click',()=>shiftMonth(-1));$('nextBtn').addEventListener('click',()=>shiftMonth(1));$('exportBtn').addEventListener('click',exportCSV);$('resetBtn').addEventListener('click',resetAppData);$('balanceCard').addEventListener('click',openBalanceModal);$('recSaveBtn').addEventListener('click',saveRecurring);$('addExpenseBtn').addEventListener('click',addExpenseEntry);$('catSaveBtn').addEventListener('click',saveCategory);$('saveBalanceBtn').addEventListener('click',saveMonthlyBalance);$('addRolloverBtn').addEventListener('click',addToRollover);$('rolloverBtn').addEventListener('click',useRollover);

    document.addEventListener('click',e=>{const close=e.target.closest('[data-close]');if(close) closeModal(close.dataset.close);const a=e.target.closest('[data-action]');if(!a) return;const id=Number(a.dataset.id), index=Number(a.dataset.index);switch(a.dataset.action){case'toggle-paid':togglePaid(id);break;case'edit-rec':openEditRec(id);break;case'delete-rec':deleteRecurring(id);break;case'open-add-rec':openAddRec();break;case'open-expense':openExpenseModal(id);break;case'open-cat-modal':openAddCategory();break;case'edit-cat':openEditCategory(id);break;case'delete-cat':deleteCategory(id);break;case'delete-entry':deleteEntry(id,index);break;}});
    document.querySelectorAll('.overlay').forEach(o=>o.addEventListener('click',e=>{if(e.target===o) o.classList.remove('open')}));
    document.addEventListener('keydown',e=>{if(e.key==='Escape'){document.querySelectorAll('.overlay.open').forEach(o=>o.classList.remove('open'));return}if(e.key!=='Enter') return;if($('recModal').classList.contains('open')) return saveRecurring();if($('expenseModal').classList.contains('open')) return addExpenseEntry();if($('catModal').classList.contains('open')) return saveCategory();if($('balanceModal').classList.contains('open')) return saveMonthlyBalance()});

    initDB();
  </script>
</body>
</html>
