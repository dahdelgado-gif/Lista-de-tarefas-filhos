[quadro-de-tarefas.html](https://github.com/user-attachments/files/31386705/quadro-de-tarefas.html)
# Lista-de-tarefas-filhos<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quadro de Tarefas</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root{
    --board: #2f4a3e;
    --board-dark: #24392f;
    --paper: #fbf3e1;
    --paper-line: #e3d6b8;
    --ink: #2a2620;
    --tape-yellow: #e8a33d;
    --tape-coral: #e85d4e;
    --gui: #3e7cb1;
    --gui-soft: #dceaf4;
    --man: #c6467d;
    --man-soft: #f8dfea;
    --done: #4a8a5f;
    --missed: #c0392b;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    min-height:100vh;
    background:
      radial-gradient(circle at 20% 10%, rgba(255,255,255,0.05), transparent 40%),
      repeating-linear-gradient(45deg, rgba(0,0,0,0.015) 0 2px, transparent 2px 4px),
      var(--board);
    font-family:'Nunito', sans-serif;
    color: var(--ink);
    padding: 28px 16px 60px;
  }
  .wrap{ max-width: 980px; margin: 0 auto; }
  header.top{
    text-align:center;
    margin-bottom: 28px;
  }
  header.top h1{
    font-family:'Caveat', cursive;
    font-size: 3.2rem;
    color: var(--paper);
    margin: 0 0 4px;
    transform: rotate(-1deg);
  }
  header.top p{
    color: rgba(251,243,225,0.75);
    margin:0;
    font-weight:600;
    letter-spacing: 0.02em;
  }
  .week-nav{
    display:flex;
    align-items:center;
    justify-content:center;
    gap: 14px;
    margin: 18px 0 30px;
  }
  .week-nav button{
    background: rgba(251,243,225,0.12);
    border: 1px solid rgba(251,243,225,0.3);
    color: var(--paper);
    width: 36px; height:36px;
    border-radius: 50%;
    cursor:pointer;
    font-size: 1.1rem;
    line-height:1;
    transition: background 0.15s ease;
  }
  .week-nav button:hover{ background: rgba(251,243,225,0.24); }
  .week-label{
    color: var(--paper);
    font-weight: 700;
    background: rgba(0,0,0,0.18);
    padding: 8px 18px;
    border-radius: 999px;
    font-size: 0.95rem;
    min-width: 210px;
    text-align:center;
  }
  .card{
    background: var(--paper);
    border-radius: 6px;
    padding: 22px 20px 24px;
    margin-bottom: 26px;
    position: relative;
    box-shadow: 0 14px 30px rgba(0,0,0,0.28), 0 2px 0 rgba(0,0,0,0.05);
    transform: rotate(var(--tilt, -0.4deg));
  }
  .card::before{
    content:"";
    position:absolute;
    top:-14px; left:50%;
    transform: translateX(-50%) rotate(-3deg);
    width: 64px; height: 26px;
    background: var(--tape-yellow);
    opacity:0.85;
    box-shadow: 0 2px 4px rgba(0,0,0,0.2);
  }
  .card.man::before{ background: var(--tape-coral); transform: translateX(-50%) rotate(3deg); }
  .card-head{
    display:flex;
    align-items:center;
    gap: 14px;
    margin-bottom: 18px;
    flex-wrap: wrap;
  }
  .avatar{
    width: 52px; height:52px;
    border-radius: 50%;
    display:flex; align-items:center; justify-content:center;
    font-family:'Caveat', cursive;
    font-size: 1.7rem;
    font-weight:700;
    color:#fff;
    flex-shrink:0;
  }
  .card.gui .avatar{ background: var(--gui); }
  .card.man .avatar{ background: var(--man); }
  .card-head h2{
    font-family:'Caveat', cursive;
    font-size: 2rem;
    margin:0;
    line-height:1;
  }
  .card-head .age{
    font-size:0.8rem;
    color:#6b6354;
    font-weight:700;
    text-transform:uppercase;
    letter-spacing:0.04em;
  }
  .totals{
    margin-left:auto;
    display:flex;
    gap:10px;
    flex-wrap:wrap;
  }
  .pill{
    font-weight:800;
    font-size:0.85rem;
    padding:7px 12px;
    border-radius:999px;
    white-space:nowrap;
  }
  .pill.ganho{ background: #e2f2e6; color: var(--done); }
  .pill.perda{ background: #fbe4e1; color: var(--missed); }
  .pill.total{ color:#fff; }
  .card.gui .pill.total{ background: var(--gui); }
  .card.man .pill.total{ background: var(--man); }

  .grid-scroll{ overflow-x:auto; -webkit-overflow-scrolling: touch; }
  table.tasks{
    width:100%;
    border-collapse:collapse;
    font-size:0.85rem;
    min-width: 640px;
  }
  table.tasks th, table.tasks td{
    padding: 8px 6px;
    text-align:center;
    border-bottom: 1px solid var(--paper-line);
  }
  table.tasks th{
    font-size:0.72rem;
    text-transform:uppercase;
    letter-spacing:0.03em;
    color:#8a7f68;
    font-weight:800;
  }
  table.tasks td.task-name{
    text-align:left;
    font-weight:700;
    color:var(--ink);
    padding-right: 10px;
  }
  .task-remove{
    background:none;border:none;color:#b8ab8c;cursor:pointer;
    font-size:0.75rem; margin-left:6px; padding:0;
  }
  .task-remove:hover{ color: var(--missed); }
  .cell{
    width: 34px; height: 34px;
    border-radius: 8px;
    border: 1px solid var(--paper-line);
    background: #fff;
    cursor:pointer;
    display:inline-flex;
    align-items:center;
    justify-content:center;
    font-size: 1rem;
    user-select:none;
    transition: transform 0.08s ease;
  }
  .cell:active{ transform: scale(0.9); }
  .cell.done{ background: var(--done); border-color: var(--done); color:#fff; }
  .cell.missed{ background: var(--missed); border-color: var(--missed); color:#fff; }
  .cell.livre{
    cursor:default;
    background: repeating-linear-gradient(45deg, #f1ebd9, #f1ebd9 4px, #e7dfc7 4px, #e7dfc7 8px);
    color:#b8ab8c;
    font-size:0.6rem;
    font-weight:800;
  }
  .cell.locked{ cursor:not-allowed; opacity:0.85; }
  td.total-col{ font-weight:800; color:#6b6354; }

  .add-task{
    margin-top: 14px;
    display:flex;
    gap:8px;
    flex-wrap:wrap;
    align-items:center;
  }
  .add-task input[type=text]{
    flex:1;
    min-width: 160px;
    padding: 8px 10px;
    border-radius: 8px;
    border: 1px solid var(--paper-line);
    font-family:'Nunito', sans-serif;
    font-size:0.85rem;
    background:#fff;
  }
  .add-task button{
    padding: 8px 16px;
    border-radius: 8px;
    border:none;
    font-weight:700;
    cursor:pointer;
    color:#fff;
    font-size:0.85rem;
  }
  .card.gui .add-task button{ background: var(--gui); }
  .card.man .add-task button{ background: var(--man); }

  .day-picker{
    display:flex;
    gap:4px;
    flex-wrap:wrap;
  }
  .day-picker label{
    font-size:0.65rem;
    font-weight:700;
    color:#8a7f68;
    background:#f1ebd9;
    padding:4px 6px;
    border-radius:5px;
    cursor:pointer;
    display:flex;
    align-items:center;
    gap:3px;
  }
  .day-picker input{ accent-color: var(--gui); }
  .card.man .day-picker input{ accent-color: var(--man); }

  .summary-bar{
    max-width: 980px;
    margin: 0 auto 20px;
    background: rgba(0,0,0,0.2);
    border-radius: 10px;
    padding: 14px 20px;
    color: var(--paper);
    display:flex;
    justify-content: space-between;
    flex-wrap:wrap;
    gap:10px;
    font-weight:700;
  }
  .summary-bar .grand-total{ font-family:'Caveat', cursive; font-size:1.6rem; }
  footer.legend{
    text-align:center;
    color: rgba(251,243,225,0.6);
    font-size:0.78rem;
    margin-top: 10px;
  }
  .legend span{ margin: 0 8px; }
  .modal-overlay{
    display:none;
    position:fixed; inset:0;
    background:rgba(0,0,0,0.55);
    align-items:center; justify-content:center;
    z-index:1000;
    padding: 16px;
  }
  .modal-overlay.open{ display:flex; }
  .modal-box{
    background: var(--paper);
    border-radius: 10px;
    padding: 22px 20px;
    max-width: 340px;
    width: 100%;
    box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    text-align:center;
  }
  .modal-box h3{
    font-family:'Caveat', cursive;
    font-size: 1.7rem;
    margin: 0 0 6px;
  }
  .modal-box p{
    margin: 0 0 16px;
    font-size: 0.9rem;
    color:#6b6354;
  }
  .modal-box input[type=password], .modal-box input[type=text]{
    width:100%;
    padding: 10px 12px;
    border-radius: 8px;
    border: 1px solid var(--paper-line);
    font-family:'Nunito', sans-serif;
    font-size: 1rem;
    text-align:center;
    margin-bottom: 14px;
    letter-spacing: 0.15em;
  }
  .modal-box .modal-error{
    color: var(--missed);
    font-size: 0.8rem;
    font-weight:700;
    margin: -8px 0 12px;
    min-height: 1em;
  }
  .modal-actions{
    display:flex;
    gap:10px;
    justify-content:center;
  }
  .modal-actions button{
    flex:1;
    padding: 9px 14px;
    border-radius: 8px;
    border:none;
    font-weight:700;
    cursor:pointer;
    font-size:0.85rem;
  }
  .modal-actions .btn-primary{ background: var(--gui); color:#fff; }
  .modal-actions .btn-secondary{ background:#e7dfc7; color:var(--ink); }
  @media (max-width: 560px){
    header.top h1{ font-size: 2.4rem; }
    .totals{ margin-left:0; width:100%; justify-content:flex-start; }
  }
</style>
</head>
<body>
<div class="wrap">
  <header class="top">
    <h1>Quadro de Tarefas</h1>
    <p>Guilherme &amp; Manuella</p>
  </header>

  <div class="week-nav">
    <button id="prevWeek" aria-label="Semana anterior">‹</button>
    <div class="week-label" id="weekLabel">carregando...</div>
    <button id="nextWeek" aria-label="Pr&oacute;xima semana">›</button>
  </div>

  <div style="max-width:980px; margin:0 auto 18px; display:flex; gap:10px; justify-content:center; flex-wrap:wrap;">
    <button id="modeBtn" style="background:rgba(251,243,225,0.14); border:1px solid rgba(251,243,225,0.35); color:#fbf3e1; padding:8px 16px; border-radius:8px; font-weight:800; cursor:pointer; font-size:0.85rem;">🔒 Modo visualiza&ccedil;&atilde;o</button>
    <button id="monthBtn" style="background:rgba(251,243,225,0.14); border:1px solid rgba(251,243,225,0.35); color:#fbf3e1; padding:8px 16px; border-radius:8px; font-weight:700; cursor:pointer; font-size:0.85rem;">📅 Resumo mensal</button>
    <button id="changePinBtn" style="display:none; background:rgba(251,243,225,0.14); border:1px solid rgba(251,243,225,0.35); color:#fbf3e1; padding:8px 16px; border-radius:8px; font-weight:700; cursor:pointer; font-size:0.85rem;">🔑 Trocar PIN</button>
  </div>

  <div id="monthPanel" style="display:none; max-width:980px; margin:0 auto 26px; background:var(--paper); border-radius:6px; padding:20px; box-shadow:0 14px 30px rgba(0,0,0,0.28);">
    <div style="display:flex; align-items:center; justify-content:center; gap:14px; margin-bottom:16px;">
      <button id="prevMonth" style="width:32px;height:32px;border-radius:50%;border:1px solid var(--paper-line);background:#fff;cursor:pointer;">‹</button>
      <div id="monthLabel" style="font-family:'Caveat',cursive; font-size:1.6rem; min-width:180px; text-align:center;"></div>
      <button id="nextMonth" style="width:32px;height:32px;border-radius:50%;border:1px solid var(--paper-line);background:#fff;cursor:pointer;">›</button>
    </div>
    <div id="monthContent"></div>
  </div>

  <div id="weekView"></div>


  <div id="saveBanner" style="display:none; max-width:980px; margin:16px auto; background:rgba(192,57,43,0.18); border:1px solid rgba(192,57,43,0.4); color:#fbf3e1; padding:10px 16px; border-radius:8px; font-size:0.85rem; font-weight:700; text-align:center;">
    ⚠ Salvamento autom&aacute;tico falhou agora. Seus dados continuam aqui na tela, mas use "Baixar backup" antes de fechar pra n&atilde;o perder nada.
  </div>
  <div style="max-width:980px; margin:0 auto 20px; display:flex; gap:10px; justify-content:center; flex-wrap:wrap;">
    <button id="exportBtn" style="background:rgba(251,243,225,0.14); border:1px solid rgba(251,243,225,0.35); color:#fbf3e1; padding:8px 16px; border-radius:8px; font-weight:700; cursor:pointer; font-size:0.85rem;">⬇ Baixar backup</button>
    <button id="importBtn" style="background:rgba(251,243,225,0.14); border:1px solid rgba(251,243,225,0.35); color:#fbf3e1; padding:8px 16px; border-radius:8px; font-weight:700; cursor:pointer; font-size:0.85rem;">⬆ Importar backup</button>
    <input type="file" id="importFile" accept="application/json" style="display:none;">
  </div>

  <footer class="legend">
    <span>⭐ feito (+R$0,50)</span>
    <span>✕ n&atilde;o feito (−R$1,00)</span>
    <span>listrado = dia livre</span>
  </footer>
</div>

<div class="modal-overlay" id="modalOverlay">
  <div class="modal-box">
    <h3 id="modalTitle">Título</h3>
    <p id="modalMsg"></p>
    <input type="password" id="modalInput" inputmode="numeric" style="display:none;">
    <div class="modal-error" id="modalError"></div>
    <div class="modal-actions" id="modalActions"></div>
  </div>
</div>

<script>
const DAY_LABELS = ['Dom','Seg','Ter','Qua','Qui','Sex','Sáb'];
const KID_DEFS = [
  { id:'guilherme', name:'Guilherme', age:8, cls:'gui',
    tasks:[
      {id:'t1', name:'Escovar os dentes', days:[0,1,2,3,4,5,6]},
      {id:'t2', name:'Tomar banho', days:[0,1,2,3,4,5,6]},
      {id:'t3', name:'Arrumar a cama', days:[0,1,2,3,4,5,6]},
      {id:'t4', name:'Organizar pertences', days:[0,1,2,3,4,5,6]},
      {id:'t5', name:'Lavar a louça', days:[2,4,6]},
      {id:'t6', name:'Secar a louça', days:[1,3,5]},
      {id:'t7', name:'Cuidar da Jully', days:[2,4,6]},
    ]
  },
  { id:'manuella', name:'Manuella', age:10, cls:'man',
    tasks:[
      {id:'t1', name:'Escovar os dentes', days:[0,1,2,3,4,5,6]},
      {id:'t2', name:'Tomar banho', days:[0,1,2,3,4,5,6]},
      {id:'t3', name:'Arrumar a cama', days:[0,1,2,3,4,5,6]},
      {id:'t4', name:'Organizar pertences', days:[0,1,2,3,4,5,6]},
      {id:'t5', name:'Secar a louça', days:[2,4,6]},
      {id:'t6', name:'Lavar a louça', days:[1,3,5]},
      {id:'t7', name:'Cuidar da Jully', days:[1,3,5]},
    ]
  }
];
const GANHO = 0.5;
const PERDA = 1.0;
const STORAGE_KEY = 'quadro-tarefas:state';

function sundayOf(date){
  const d = new Date(date);
  d.setHours(0,0,0,0);
  d.setDate(d.getDate() - d.getDay());
  return d;
}
function isoDate(d){ return d.toISOString().slice(0,10); }
function fmtShort(d){ return d.toLocaleDateString('pt-BR', {day:'2-digit', month:'2-digit'}); }
function fmtMoney(v){ return 'R$ ' + v.toFixed(2).replace('.',','); }

// ---- Modal genérico (substitui prompt/alert/confirm, bloqueados em iframe sandboxado) ----
const modalOverlay = document.getElementById('modalOverlay');
const modalTitle = document.getElementById('modalTitle');
const modalMsg = document.getElementById('modalMsg');
const modalInput = document.getElementById('modalInput');
const modalError = document.getElementById('modalError');
const modalActions = document.getElementById('modalActions');

function closeModal(){
  modalOverlay.classList.remove('open');
  modalInput.style.display = 'none';
  modalInput.value = '';
  modalError.textContent = '';
}

function showAskModal({title, message, placeholder='', onSubmit}){
  modalTitle.textContent = title;
  modalMsg.textContent = message;
  modalError.textContent = '';
  modalInput.style.display = 'block';
  modalInput.type = 'password';
  modalInput.value = '';
  modalInput.placeholder = placeholder;
  modalActions.innerHTML = `
    <button class="btn-secondary" id="modalCancel">Cancelar</button>
    <button class="btn-primary" id="modalOk">Confirmar</button>`;
  modalOverlay.classList.add('open');
  setTimeout(() => modalInput.focus(), 50);

  const submit = () => onSubmit(modalInput.value);
  document.getElementById('modalOk').onclick = submit;
  document.getElementById('modalCancel').onclick = closeModal;
  modalInput.onkeydown = (e) => { if(e.key === 'Enter') submit(); };
}

function showConfirmModal({title, message, onConfirm}){
  modalTitle.textContent = title;
  modalMsg.textContent = message;
  modalError.textContent = '';
  modalInput.style.display = 'none';
  modalActions.innerHTML = `
    <button class="btn-secondary" id="modalCancel">Cancelar</button>
    <button class="btn-primary" id="modalOk" style="background:var(--missed);">Remover</button>`;
  modalOverlay.classList.add('open');
  document.getElementById('modalOk').onclick = () => { closeModal(); onConfirm(); };
  document.getElementById('modalCancel').onclick = closeModal;
}

function showInfoModal({title, message}){
  modalTitle.textContent = title;
  modalMsg.textContent = message;
  modalError.textContent = '';
  modalInput.style.display = 'none';
  modalActions.innerHTML = `<button class="btn-primary" id="modalOk">OK</button>`;
  modalOverlay.classList.add('open');
  document.getElementById('modalOk').onclick = closeModal;
}

let state = { tasksByKid:{}, weeks:{}, pin:'1234' };
let currentWeekStart = sundayOf(new Date());
let manageMode = false;
let viewMode = 'week'; // 'week' or 'month'
let currentMonth = new Date(new Date().getFullYear(), new Date().getMonth(), 1);
// Guarda se o armazenamento compartilhado (entre dispositivos) está funcionando.
// Se não estiver, cai automaticamente para armazenamento local (só neste navegador),
// pra nunca perder dados mesmo se o modo compartilhado falhar no ambiente de preview.
let storageShared = true;

function defaultTasksByKid(){
  const obj = {};
  KID_DEFS.forEach(k => { obj[k.id] = k.tasks.map(t => ({...t})); });
  return obj;
}

async function loadState(){
  let loaded = false;
  try{
    const res = await window.storage.get(STORAGE_KEY, true);
    if(res && res.value){
      state = JSON.parse(res.value);
      loaded = true;
    }
    storageShared = true;
  }catch(e){
    // Ainda tenta o modo local antes de desistir
    try{
      const res2 = await window.storage.get(STORAGE_KEY, false);
      if(res2 && res2.value){
        state = JSON.parse(res2.value);
        loaded = true;
      }
      storageShared = false;
      console.log('armazenamento compartilhado indispon\u00edvel, usando local neste navegador');
    }catch(e2){
      console.log('sem dados salvos ainda, come\u00e7ando do zero');
    }
  }
  if(!state.tasksByKid || Object.keys(state.tasksByKid).length === 0){
    state.tasksByKid = defaultTasksByKid();
  }
  if(!state.weeks) state.weeks = {};
  if(!state.pin) state.pin = '1234';
}

async function saveState(){
  const banner = document.getElementById('saveBanner');
  const payload = JSON.stringify(state);
  try{
    let result;
    try{
      result = await window.storage.set(STORAGE_KEY, payload, storageShared);
    }catch(e){
      if(storageShared){
        // Armazenamento compartilhado falhou: tenta local como reserva
        storageShared = false;
        result = await window.storage.set(STORAGE_KEY, payload, false);
      }else{
        throw e;
      }
    }
    if(!result) throw new Error('sem confirma\u00e7\u00e3o do servidor');
    if(banner) banner.style.display = 'none';
  }catch(e){
    console.error('erro ao salvar', e);
    if(banner) banner.style.display = 'block';
  }
}

function downloadBackup(){
  const blob = new Blob([JSON.stringify(state, null, 2)], {type:'application/json'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  const stamp = new Date().toISOString().slice(0,10);
  a.href = url;
  a.download = `backup-quadro-tarefas-${stamp}.json`;
  document.body.appendChild(a);
  a.click();
  a.remove();
  URL.revokeObjectURL(url);
}

function importBackup(file){
  const reader = new FileReader();
  reader.onload = async () => {
    try{
      const parsed = JSON.parse(reader.result);
      if(!parsed.tasksByKid || !parsed.weeks) throw new Error('arquivo inv\u00e1lido');
      state = parsed;
      await saveState();
      render();
      showInfoModal({ title: 'Pronto!', message: 'Backup importado com sucesso.' });
    }catch(e){
      showInfoModal({ title: 'Ops', message: 'Não consegui ler esse arquivo de backup. Confira se é o arquivo certo.' });
    }
  };
  reader.readAsText(file);
}

function getWeekMarks(){
  const key = isoDate(currentWeekStart);
  if(!state.weeks[key]) state.weeks[key] = {};
  KID_DEFS.forEach(k => { if(!state.weeks[key][k.id]) state.weeks[key][k.id] = {}; });
  return state.weeks[key];
}

function cycleState(cur){
  if(cur === 'done') return 'missed';
  if(cur === 'missed') return null;
  return 'done';
}

function computeKidTotal(kidId, marks){
  const tasks = state.tasksByKid[kidId];
  let ganho = 0, perda = 0;
  tasks.forEach(t => {
    const rowMarks = marks[kidId][t.id] || {};
    t.days.forEach(day => {
      const v = rowMarks[day];
      if(v === 'done') ganho += GANHO;
      else if(v === 'missed') perda += PERDA;
    });
  });
  return { ganho, perda, total: ganho - perda };
}

function render(){
  const weekEnd = new Date(currentWeekStart);
  weekEnd.setDate(weekEnd.getDate() + 6);
  document.getElementById('weekLabel').textContent = fmtShort(currentWeekStart) + ' a ' + fmtShort(weekEnd);

  const marks = getWeekMarks();
  const weekViewEl = document.getElementById('weekView');

  let grandGanho = 0, grandPerda = 0;
  let cardsHtml = '';

  KID_DEFS.forEach((kidDef, idx) => {
    const tasks = state.tasksByKid[kidDef.id];
    const { ganho, perda, total } = computeKidTotal(kidDef.id, marks);
    grandGanho += ganho; grandPerda += perda;

    cardsHtml += `
      <div class="card ${kidDef.cls}" style="--tilt:${idx % 2 === 0 ? '-0.4deg' : '0.4deg'}">
        <div class="card-head">
          <div class="avatar">${kidDef.name[0]}</div>
          <div>
            <h2>${kidDef.name}</h2>
            <div class="age">${kidDef.age} anos</div>
          </div>
          <div class="totals">
            <span class="pill ganho">+ ${fmtMoney(ganho)}</span>
            <span class="pill perda">− ${fmtMoney(perda)}</span>
            <span class="pill total">= ${fmtMoney(total)}</span>
          </div>
        </div>
        <div class="grid-scroll">
          <table class="tasks">
            <thead>
              <tr>
                <th style="text-align:left;">Tarefa</th>
                ${DAY_LABELS.map(d => `<th>${d}</th>`).join('')}
                <th>Feitas</th>
              </tr>
            </thead>
            <tbody>
              ${tasks.map(t => renderTaskRow(kidDef.id, t, marks)).join('')}
            </tbody>
          </table>
        </div>
        ${manageMode ? `
        <div class="add-task">
          <input type="text" placeholder="Nova tarefa..." data-newtask="${kidDef.id}">
          <div class="day-picker" data-newdays="${kidDef.id}">
            ${DAY_LABELS.map((d,i) => `<label><input type="checkbox" value="${i}" checked>${d}</label>`).join('')}
          </div>
          <button data-addbtn="${kidDef.id}">Adicionar</button>
        </div>` : ''}
      </div>`;
  });

  weekViewEl.innerHTML = cardsHtml + `
    <div class="summary-bar">
      <div>Ganhos da semana: ${fmtMoney(grandGanho)}</div>
      <div>Perdas da semana: ${fmtMoney(grandPerda)}</div>
      <div class="grand-total">Total: ${fmtMoney(grandGanho - grandPerda)}</div>
    </div>`;

  updateModeUI();
  attachHandlers();
}

function updateModeUI(){
  const btn = document.getElementById('modeBtn');
  const pinBtn = document.getElementById('changePinBtn');
  if(manageMode){
    btn.textContent = '🔓 Modo gerenciamento (ativo)';
    pinBtn.style.display = 'inline-block';
  }else{
    btn.textContent = '🔒 Modo visualização';
    pinBtn.style.display = 'none';
  }
}

function renderMonthPanel(){
  document.getElementById('monthLabel').textContent = currentMonth.toLocaleDateString('pt-BR', {month:'long', year:'numeric'});
  const totals = computeMonthTotals(currentMonth.getFullYear(), currentMonth.getMonth());
  let html = '';
  let grandGanho = 0, grandPerda = 0;
  KID_DEFS.forEach(kidDef => {
    const t = totals[kidDef.id];
    grandGanho += t.ganho; grandPerda += t.perda;
    html += `
      <div style="display:flex; align-items:center; justify-content:space-between; padding:12px 4px; border-bottom:1px solid var(--paper-line);">
        <div style="display:flex; align-items:center; gap:10px;">
          <div class="avatar" style="width:36px;height:36px;font-size:1.1rem;background:${kidDef.cls === 'gui' ? 'var(--gui)' : 'var(--man)'};">${kidDef.name[0]}</div>
          <strong>${kidDef.name}</strong>
        </div>
        <div style="display:flex; gap:8px; flex-wrap:wrap;">
          <span class="pill ganho">+ ${fmtMoney(t.ganho)}</span>
          <span class="pill perda">− ${fmtMoney(t.perda)}</span>
          <span class="pill total" style="background:${kidDef.cls === 'gui' ? 'var(--gui)' : 'var(--man)'};">= ${fmtMoney(t.ganho - t.perda)}</span>
        </div>
      </div>`;
  });
  html += `
    <div style="display:flex; justify-content:flex-end; gap:8px; margin-top:14px; font-weight:800;">
      Total do m&ecirc;s: <span>${fmtMoney(grandGanho - grandPerda)}</span>
    </div>`;
  document.getElementById('monthContent').innerHTML = html;
}

function computeMonthTotals(year, month){
  const totals = {};
  KID_DEFS.forEach(k => { totals[k.id] = { ganho:0, perda:0 }; });
  Object.keys(state.weeks).forEach(weekKey => {
    const weekStart = new Date(weekKey + 'T00:00:00');
    const weekData = state.weeks[weekKey];
    KID_DEFS.forEach(kidDef => {
      const tasks = state.tasksByKid[kidDef.id];
      const kidMarks = weekData[kidDef.id] || {};
      tasks.forEach(t => {
        const rowMarks = kidMarks[t.id] || {};
        Object.keys(rowMarks).forEach(dayStr => {
          const day = Number(dayStr);
          const actualDate = new Date(weekStart);
          actualDate.setDate(actualDate.getDate() + day);
          if(actualDate.getFullYear() === year && actualDate.getMonth() === month){
            if(rowMarks[day] === 'done') totals[kidDef.id].ganho += GANHO;
            else if(rowMarks[day] === 'missed') totals[kidDef.id].perda += PERDA;
          }
        });
      });
    });
  });
  return totals;
}

function renderTaskRow(kidId, t, marks){
  const rowMarks = marks[kidId][t.id] || {};
  let feitas = 0;
  const cells = DAY_LABELS.map((_, day) => {
    if(!t.days.includes(day)){
      return `<td><div class="cell livre">LIVRE</div></td>`;
    }
    const v = rowMarks[day];
    if(v === 'done') feitas++;
    const symbol = v === 'done' ? '⭐' : (v === 'missed' ? '✕' : '');
    const cls = v === 'done' ? 'done' : (v === 'missed' ? 'missed' : '');
    const lockCls = manageMode ? '' : ' locked';
    return `<td><div class="cell ${cls}${lockCls}" data-kid="${kidId}" data-task="${t.id}" data-day="${day}">${symbol}</div></td>`;
  }).join('');
  return `<tr>
    <td class="task-name">${t.name}${manageMode ? `<button class="task-remove" data-removekid="${kidId}" data-removetask="${t.id}">remover</button>` : ''}</td>
    ${cells}
    <td class="total-col">${feitas}</td>
  </tr>`;
}

function attachHandlers(){
  document.querySelectorAll('.cell:not(.livre)').forEach(cell => {
    cell.addEventListener('click', async () => {
      if(!manageMode){
        flashLockHint();
        return;
      }
      const kidId = cell.dataset.kid, taskId = cell.dataset.task, day = Number(cell.dataset.day);
      const marks = getWeekMarks();
      if(!marks[kidId][taskId]) marks[kidId][taskId] = {};
      const cur = marks[kidId][taskId][day] || null;
      const next = cycleState(cur);
      if(next === null) delete marks[kidId][taskId][day];
      else marks[kidId][taskId][day] = next;
      await saveState();
      render();
    });
  });

  document.querySelectorAll('[data-removekid]').forEach(btn => {
    btn.addEventListener('click', async () => {
      const kidId = btn.dataset.removekid, taskId = btn.dataset.removetask;
      showConfirmModal({
        title: 'Remover tarefa',
        message: 'Tem certeza que quer remover essa tarefa da lista?',
        onConfirm: async () => {
          state.tasksByKid[kidId] = state.tasksByKid[kidId].filter(t => t.id !== taskId);
          await saveState();
          render();
        }
      });
    });
  });

  document.querySelectorAll('[data-addbtn]').forEach(btn => {
    btn.addEventListener('click', async () => {
      const kidId = btn.dataset.addbtn;
      const input = document.querySelector(`[data-newtask="${kidId}"]`);
      const dayBoxes = document.querySelectorAll(`[data-newdays="${kidId}"] input`);
      const name = input.value.trim();
      if(!name) return;
      const days = Array.from(dayBoxes).filter(b => b.checked).map(b => Number(b.value));
      if(days.length === 0) return;
      const newId = 't' + Date.now();
      state.tasksByKid[kidId].push({ id:newId, name, days });
      input.value = '';
      await saveState();
      render();
    });
  });
}

let lockHintTimer = null;
function flashLockHint(){
  const banner = document.getElementById('saveBanner');
  banner.style.background = 'rgba(0,0,0,0.25)';
  banner.style.borderColor = 'rgba(251,243,225,0.4)';
  banner.textContent = '🔒 Entre no modo gerenciamento (bot\u00e3o acima) pra marcar tarefas.';
  banner.style.display = 'block';
  clearTimeout(lockHintTimer);
  lockHintTimer = setTimeout(() => { banner.style.display = 'none'; }, 2500);
}

document.getElementById('prevWeek').addEventListener('click', () => {
  currentWeekStart.setDate(currentWeekStart.getDate() - 7);
  render();
});
document.getElementById('nextWeek').addEventListener('click', () => {
  currentWeekStart.setDate(currentWeekStart.getDate() + 7);
  render();
});

document.getElementById('modeBtn').addEventListener('click', () => {
  if(manageMode){
    manageMode = false;
    render();
    return;
  }
  showAskModal({
    title: 'Modo gerenciamento',
    message: 'Digite o PIN para editar as tarefas:',
    placeholder: 'PIN',
    onSubmit: (entered) => {
      if(entered === state.pin){
        manageMode = true;
        closeModal();
        render();
      }else{
        modalError.textContent = 'PIN incorreto. Tente de novo.';
        modalInput.value = '';
        modalInput.focus();
      }
    }
  });
});

document.getElementById('monthBtn').addEventListener('click', () => {
  const panel = document.getElementById('monthPanel');
  const weekViewEl = document.getElementById('weekView');
  const weekNav = document.querySelector('.week-nav');
  if(viewMode === 'week'){
    viewMode = 'month';
    panel.style.display = 'block';
    weekViewEl.style.display = 'none';
    weekNav.style.display = 'none';
    document.getElementById('monthBtn').textContent = '📋 Voltar pra semana';
    renderMonthPanel();
  }else{
    viewMode = 'week';
    panel.style.display = 'none';
    weekViewEl.style.display = 'block';
    weekNav.style.display = 'flex';
    document.getElementById('monthBtn').textContent = '📅 Resumo mensal';
  }
});

document.getElementById('prevMonth').addEventListener('click', () => {
  currentMonth.setMonth(currentMonth.getMonth() - 1);
  renderMonthPanel();
});
document.getElementById('nextMonth').addEventListener('click', () => {
  currentMonth.setMonth(currentMonth.getMonth() + 1);
  renderMonthPanel();
});

document.getElementById('changePinBtn').addEventListener('click', () => {
  showAskModal({
    title: 'Trocar PIN',
    message: 'Digite o novo PIN de gerenciamento:',
    placeholder: 'Novo PIN',
    onSubmit: async (novo) => {
      const trimmed = (novo || '').trim();
      if(!trimmed){
        modalError.textContent = 'Digite um PIN válido.';
        return;
      }
      state.pin = trimmed;
      await saveState();
      closeModal();
      showInfoModal({ title: 'Pronto!', message: 'PIN atualizado com sucesso.' });
    }
  });
});

document.getElementById('exportBtn').addEventListener('click', downloadBackup);
document.getElementById('importBtn').addEventListener('click', () => {
  document.getElementById('importFile').click();
});
document.getElementById('importFile').addEventListener('change', (e) => {
  const file = e.target.files[0];
  if(file) importBackup(file);
  e.target.value = '';
});

modalOverlay.addEventListener('click', (e) => {
  if(e.target === modalOverlay) closeModal();
});

(async function init(){
  await loadState();
  render();
})();
</script>
</body>
</html>
