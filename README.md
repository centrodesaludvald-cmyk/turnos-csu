<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Turnos Equipo Clínico — CSU Valdivia</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@2.44.0/tabler-icons.min.css">
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; background: #f5f5f5; color: #1a1a1a; min-height: 100vh; }
  .container { padding: 1.5rem 1rem; max-width: 480px; margin: 0 auto; }
  .header { text-align: center; margin-bottom: 1.5rem; }
  .header h1 { font-size: 18px; font-weight: 600; color: #1a1a1a; }
  .header p { font-size: 13px; color: #666; margin-top: 4px; }
  .logo { font-size: 13px; color: #999; text-align: center; margin-bottom: 1rem; font-weight: 500; letter-spacing: 0.5px; }
  select, textarea, button, input { font-family: inherit; font-size: 14px; border-radius: 8px; border: 1px solid #ddd; padding: 10px 12px; width: 100%; background: #fff; color: #1a1a1a; }
  select:focus, textarea:focus, input:focus { outline: none; border-color: #888; }
  button { cursor: pointer; background: #fff; border: 1px solid #ddd; width: auto; padding: 8px 16px; transition: background 0.15s; }
  button:hover { background: #f0f0f0; }
  .select-wrap { margin-bottom: 1rem; }
  .day-card { background: #fff; border: 1px solid #e8e8e8; border-radius: 12px; padding: 1rem 1.25rem; margin-bottom: 10px; }
  .day-header { display: flex; align-items: center; gap: 8px; margin-bottom: 10px; }
  .day-name { font-size: 15px; font-weight: 600; color: #1a1a1a; }
  .day-date { font-size: 12px; color: #888; }
  .bloque-row { display: flex; align-items: flex-start; gap: 10px; padding: 7px 0; border-top: 1px solid #f0f0f0; }
  .bloque-area { font-size: 12px; color: #666; min-width: 95px; padding-top: 3px; }
  .bloque-right { display: flex; flex-direction: column; gap: 4px; }
  .badge { font-size: 11px; padding: 3px 9px; border-radius: 6px; background: #e8f1fc; color: #1a5ca8; display: inline-block; font-weight: 500; }
  .badge.colacion { background: #fef3e2; color: #8a5100; }
  .tarea-box { margin-top: 8px; padding: 8px 10px; background: #f0faf5; border-radius: 8px; border-left: 3px solid #1D9E75; font-size: 12px; color: #1a1a1a; }
  .tarea-label { font-size: 11px; color: #666; margin-bottom: 2px; }
  .no-result { text-align: center; padding: 2rem; color: #888; font-size: 14px; }
  .loading { text-align: center; padding: 1.5rem; color: #aaa; font-size: 13px; }
  .admin-toggle { text-align: center; margin-top: 2rem; margin-bottom: 0.5rem; }
  .admin-toggle button { font-size: 11px; color: #ddd; background: none; border: none; padding: 4px 8px; width: auto; }
  .admin-toggle button:hover { color: #aaa; background: none; }
  .admin-panel { display: none; border: 1px solid #e8e8e8; border-radius: 12px; padding: 1rem 1.25rem; margin-top: 0.5rem; background: #fff; }
  .admin-panel.open { display: block; }
  .admin-section { margin-bottom: 1.25rem; }
  .admin-section-title { font-size: 13px; font-weight: 600; color: #1a1a1a; margin-bottom: 10px; padding-bottom: 6px; border-bottom: 1px solid #f0f0f0; }
  .flex-row { display: flex; gap: 6px; margin-bottom: 6px; }
  .flex-row select, .flex-row input { flex: 1; font-size: 13px; padding: 8px 10px; }
  textarea.admin-txt { width: 100%; font-size: 13px; padding: 8px 10px; resize: vertical; min-height: 52px; border: 1px solid #ddd; border-radius: 8px; }
  .btn-add { width: 100%; padding: 9px; font-size: 13px; margin-top: 6px; background: #1a1a1a; color: #fff; border: none; border-radius: 8px; font-weight: 500; }
  .btn-add:hover { background: #333; }
  .btn-danger { width: 100%; padding: 9px; font-size: 13px; margin-top: 6px; background: #fff; color: #c0392b; border: 1px solid #e8e8e8; border-radius: 8px; }
  .btn-danger:hover { background: #fff5f5; }
  .items-list { margin-top: 10px; }
  .list-item { display: flex; align-items: flex-start; gap: 6px; padding: 7px 0; border-top: 1px solid #f0f0f0; font-size: 12px; }
  .list-item-info { flex: 1; color: #1a1a1a; }
  .list-item-sub { color: #888; font-size: 11px; margin-top: 1px; }
  .del-btn { background: none; border: none; cursor: pointer; color: #bbb; padding: 2px 4px; font-size: 14px; width: auto; flex-shrink: 0; }
  .del-btn:hover { color: #c0392b; background: none; }
  .empty-list { font-size: 12px; color: #aaa; text-align: center; padding: 8px 0; }
  .saved-ok { font-size: 11px; color: #1D9E75; text-align: center; margin-top: 4px; display: none; }
  .pin-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); display: flex; align-items: center; justify-content: center; z-index: 100; }
  .pin-box { background: #fff; border-radius: 12px; padding: 1.5rem; width: 280px; text-align: center; }
  .pin-box h3 { font-size: 15px; font-weight: 600; margin-bottom: 12px; }
  .pin-box input { text-align: center; font-size: 20px; letter-spacing: 8px; margin-bottom: 10px; }
  .pin-error { font-size: 12px; color: #c0392b; margin-top: 6px; display: none; }
  .bulk-table { width: 100%; border-collapse: collapse; font-size: 12px; margin-top: 8px; }
  .bulk-table th { background: #f5f5f5; padding: 6px 8px; text-align: left; font-weight: 600; border: 1px solid #e8e8e8; }
  .bulk-table td { padding: 4px 4px; border: 1px solid #f0f0f0; }
  .bulk-table select, .bulk-table input { font-size: 11px; padding: 4px 6px; border-radius: 4px; width: 100%; }
  .bulk-row-add { font-size: 12px; color: #1a5ca8; background: none; border: none; cursor: pointer; margin-top: 6px; width: auto; padding: 4px 0; }
  .bulk-row-add:hover { background: none; text-decoration: underline; }
</style>
</head>
<body>
<div class="container">
  <div class="logo">CSU VALDIVIA — USS</div>
  <div class="header">
    <h1><i class="ti ti-calendar-week" style="font-size:20px;vertical-align:-3px;margin-right:6px"></i>Turnos equipo clínico</h1>
    <p id="semanaLabel">Cargando...</p>
  </div>

  <div class="select-wrap">
    <select id="nameSelect">
      <option value="">— Selecciona tu nombre —</option>
      <option>Barbara</option><option>Camila</option><option>Cony</option><option>Diego</option>
      <option>Gisa</option><option>Jacqueline</option><option>Javiera</option><option>Marcia</option><option>Nathaly</option>
    </select>
  </div>

  <div id="results"></div>

  <div class="admin-toggle">
    <button id="adminBtn">···</button>
  </div>

  <div class="admin-panel" id="adminPanel">

    <div class="admin-section">
      <p class="admin-section-title"><i class="ti ti-calendar" style="font-size:13px;vertical-align:-1px;margin-right:5px"></i>Nombre de la semana</p>
      <input type="text" id="semanaTexto" placeholder="Ej: Semana 22 – 27 junio 2025" style="font-size:13px;padding:8px 10px;margin-bottom:4px">
      <button class="btn-add" id="saveSemanaBtn"><i class="ti ti-device-floppy" style="font-size:13px;vertical-align:-2px;margin-right:3px"></i>Guardar</button>
      <div class="saved-ok" id="semanaSaved">✓ Guardado</div>
    </div>

    <div class="admin-section">
      <p class="admin-section-title"><i class="ti ti-table-import" style="font-size:13px;vertical-align:-1px;margin-right:5px"></i>Carga masiva de turnos</p>
      <p style="font-size:12px;color:#888;margin-bottom:8px">Agrega todas las filas que necesites y guarda todo de una vez.</p>
      <table class="bulk-table">
        <thead>
          <tr>
            <th>Día</th><th>Persona</th><th>Área</th><th>Horario</th><th></th>
          </tr>
        </thead>
        <tbody id="bulkBody"></tbody>
      </table>
      <button class="bulk-row-add" id="addRowBtn"><i class="ti ti-plus" style="font-size:12px;vertical-align:-1px"></i> Agregar fila</button>
      <button class="btn-add" id="saveBulkBtn" style="margin-top:10px"><i class="ti ti-device-floppy" style="font-size:13px;vertical-align:-2px;margin-right:3px"></i>Guardar todos los turnos</button>
      <div class="saved-ok" id="bulkSaved">✓ Turnos guardados</div>
    </div>

    <div class="admin-section">
      <p class="admin-section-title"><i class="ti ti-clipboard-list" style="font-size:13px;vertical-align:-1px;margin-right:5px"></i>Asignar tarea</p>
      <div class="flex-row">
        <select id="tDia">
          <option value="">Día</option>
          <option>Lunes</option><option>Martes</option><option>Miércoles</option>
          <option>Jueves</option><option>Viernes</option><option>Sábado</option>
        </select>
        <select id="tNombre">
          <option value="">Persona</option>
          <option>Barbara</option><option>Camila</option><option>Cony</option><option>Diego</option>
          <option>Gisa</option><option>Jacqueline</option><option>Javiera</option><option>Marcia</option><option>Nathaly</option>
        </select>
      </div>
      <textarea class="admin-txt" id="tTexto" placeholder="Escribe la tarea o indicación..."></textarea>
      <button class="btn-add" id="addTareaBtn"><i class="ti ti-plus" style="font-size:13px;vertical-align:-2px;margin-right:3px"></i>Agregar tarea</button>
      <div class="saved-ok" id="tareaSaved">✓ Guardado</div>
      <div class="items-list" id="tareasList"></div>
    </div>

    <div class="admin-section">
      <p class="admin-section-title"><i class="ti ti-list" style="font-size:13px;vertical-align:-1px;margin-right:5px"></i>Bloques cargados</p>
      <div class="items-list" id="bloquesList"></div>
    </div>

    <div class="admin-section">
      <p class="admin-section-title" style="color:#c0392b"><i class="ti ti-trash" style="font-size:13px;vertical-align:-1px;margin-right:5px"></i>Limpiar semana</p>
      <p style="font-size:12px;color:#888;margin-bottom:8px">Borra todos los bloques y tareas para comenzar semana nueva.</p>
      <button class="btn-danger" id="clearBtn"><i class="ti ti-refresh" style="font-size:13px;vertical-align:-2px;margin-right:3px"></i>Limpiar todo</button>
    </div>

  </div>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getDatabase, ref, set, push, remove, onValue } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-database.js";

const firebaseConfig = {
  apiKey: "AIzaSyDrm0TlQ0fNK57xIFSVX82L1qdMbyBU8Ng",
  authDomain: "turnos-equipo-cl.firebaseapp.com",
  databaseURL: "https://turnos-equipo-cl-default-rtdb.firebaseio.com",
  projectId: "turnos-equipo-cl",
  storageBucket: "turnos-equipo-cl.firebasestorage.app",
  messagingSenderId: "313100676497",
  appId: "1:313100676497:web:5edc3746bc1be66758be30"
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);

const COLACION = { '07:45': '13:00–14:00', '09:00': '13:00–14:00', '10:00': '14:00–15:00', '11:00': '14:00–15:00' };
function getColacion(h) { return COLACION[h.split('–')[0]] || null; }
const dias = ['Lunes','Martes','Miércoles','Jueves','Viernes','Sábado'];
const horarios = ['07:45–13:00','07:45–17:00','09:00–14:00','10:00–14:00','10:00–20:00','11:00–14:00','11:00–20:00','13:00–14:00','14:00–15:00','14:00–16:00','14:00–17:00','14:00–20:00','15:00–16:00','15:00–17:00','16:00–20:00','17:00–20:00'];
const areas = ['Esterilización','Rayos','Pabellón','Dispensario 1','Dispensario 2'];
const nombres = ['Barbara','Camila','Cony','Diego','Gisa','Jacqueline','Javiera','Marcia','Nathaly'];

let bloques = {};
let tareas = {};
let currentNombre = '';
const PIN = '2715';

function makeSelect(opts, placeholder) {
  return `<select><option value="">${placeholder}</option>${opts.map(o=>`<option>${o}</option>`).join('')}</select>`;
}

function addBulkRow(dia='', nombre='', area='', horario='') {
  const tr = document.createElement('tr');
  tr.innerHTML = `
    <td>${makeSelect(dias,'Día')}</td>
    <td>${makeSelect(nombres,'Persona')}</td>
    <td>${makeSelect(areas,'Área')}</td>
    <td>${makeSelect(horarios,'Horario')}</td>
    <td><button class="del-btn" onclick="this.closest('tr').remove()"><i class="ti ti-x"></i></button></td>`;
  if (dia) tr.querySelectorAll('select')[0].value = dia;
  if (nombre) tr.querySelectorAll('select')[1].value = nombre;
  if (area) tr.querySelectorAll('select')[2].value = area;
  if (horario) tr.querySelectorAll('select')[3].value = horario;
  document.getElementById('bulkBody').appendChild(tr);
}

document.getElementById('addRowBtn').addEventListener('click', () => addBulkRow());
addBulkRow();

onValue(ref(db, 'semana'), snap => {
  const val = snap.val();
  document.getElementById('semanaLabel').textContent = val || 'Semana actual';
  const si = document.getElementById('semanaTexto');
  if (si && !si.value) si.value = val || '';
});

onValue(ref(db, 'bloques'), snap => {
  bloques = snap.val() || {};
  if (currentNombre) renderResults(currentNombre);
  renderBloquesList();
});

onValue(ref(db, 'tareas'), snap => {
  tareas = snap.val() || {};
  if (currentNombre) renderResults(currentNombre);
  renderTareasList();
});

function renderResults(nombre) {
  const div = document.getElementById('results');
  if (!nombre) { div.innerHTML = ''; return; }
  let html = ''; let found = false;
  dias.forEach(dia => {
    const propios = Object.values(bloques).filter(b => b.dia === dia && b.nombre === nombre);
    if (!propios.length) return;
    found = true;
    const cols = new Set();
    propios.forEach(b => { const c = getColacion(b.horario); if (c) cols.add(c); });
    const td = Object.values(tareas).filter(t => t.dia === dia && t.nombre === nombre);
    html += `<div class="day-card"><div class="day-header"><i class="ti ti-calendar-event" style="font-size:16px;color:#888"></i><span class="day-name">${dia}</span></div>`;
    propios.forEach(b => {
      html += `<div class="bloque-row"><span class="bloque-area"><i class="ti ti-building-hospital" style="font-size:12px;vertical-align:-1px;margin-right:3px"></i>${b.area}</span><div class="bloque-right"><span class="badge">${b.horario}</span></div></div>`;
    });
    cols.forEach(c => {
      html += `<div class="bloque-row"><span class="bloque-area" style="color:#8a5100"><i class="ti ti-tools-kitchen-2" style="font-size:12px;vertical-align:-1px;margin-right:3px"></i>Colación</span><div class="bloque-right"><span class="badge colacion">${c}</span></div></div>`;
    });
    td.forEach(t => {
      html += `<div class="tarea-box"><div class="tarea-label"><i class="ti ti-clipboard-text" style="font-size:11px;vertical-align:-1px;margin-right:3px"></i>Tarea asignada</div>${t.texto}</div>`;
    });
    html += `</div>`;
  });
  if (!found) html = `<div class="no-result"><i class="ti ti-user-x" style="font-size:32px;color:#bbb;display:block;margin-bottom:8px"></i><p>Sin turnos asignados esta semana.</p></div>`;
  div.innerHTML = html;
}

function showSaved(id) {
  const el = document.getElementById(id);
  el.style.display = 'block';
  setTimeout(() => el.style.display = 'none', 2000);
}

function renderBloquesList() {
  const div = document.getElementById('bloquesList');
  if (!div) return;
  const entries = Object.entries(bloques);
  if (!entries.length) { div.innerHTML = '<p class="empty-list">No hay bloques cargados.</p>'; return; }
  div.innerHTML = entries.map(([key, b]) => `
    <div class="list-item">
      <div class="list-item-info"><strong>${b.nombre}</strong> — ${b.dia}<div class="list-item-sub">${b.area} · ${b.horario}${getColacion(b.horario) ? ' · col. ' + getColacion(b.horario) : ''}</div></div>
      <button class="del-btn" onclick="window.deleteBloque('${key}')"><i class="ti ti-trash"></i></button>
    </div>`).join('');
}

function renderTareasList() {
  const div = document.getElementById('tareasList');
  if (!div) return;
  const entries = Object.entries(tareas);
  if (!entries.length) { div.innerHTML = '<p class="empty-list">No hay tareas asignadas.</p>'; return; }
  div.innerHTML = entries.map(([key, t]) => `
    <div class="list-item">
      <div class="list-item-info"><strong>${t.nombre}</strong> — ${t.dia}<div class="list-item-sub">${t.texto}</div></div>
      <button class="del-btn" onclick="window.deleteTarea('${key}')"><i class="ti ti-trash"></i></button>
    </div>`).join('');
}

window.deleteBloque = key => remove(ref(db, 'bloques/' + key));
window.deleteTarea = key => remove(ref(db, 'tareas/' + key));

document.getElementById('nameSelect').addEventListener('change', e => {
  currentNombre = e.target.value;
  renderResults(currentNombre);
});

document.getElementById('adminBtn').addEventListener('click', () => {
  const panel = document.getElementById('adminPanel');
  if (panel.classList.contains('open')) { panel.classList.remove('open'); return; }
  const overlay = document.createElement('div');
  overlay.className = 'pin-overlay';
  overlay.innerHTML = `<div class="pin-box"><h3><i class="ti ti-lock" style="font-size:16px;vertical-align:-2px;margin-right:6px"></i>Acceso admin</h3><input type="password" id="pinInput" placeholder="····" maxlength="4"><div style="display:flex;gap:8px;margin-top:8px"><button onclick="document.body.removeChild(this.closest('.pin-overlay'))" style="flex:1;padding:9px;font-size:13px">Cancelar</button><button id="pinOk" style="flex:1;padding:9px;font-size:13px;background:#1a1a1a;color:#fff;border:none;border-radius:8px">Entrar</button></div><div class="pin-error" id="pinError">Clave incorrecta</div></div>`;
  document.body.appendChild(overlay);
  setTimeout(() => overlay.querySelector('#pinInput').focus(), 100);
  overlay.querySelector('#pinOk').addEventListener('click', () => {
    const val = overlay.querySelector('#pinInput').value;
    if (val === PIN) {
      document.body.removeChild(overlay);
      panel.classList.add('open');
    } else {
      overlay.querySelector('#pinError').style.display = 'block';
      overlay.querySelector('#pinInput').value = '';
    }
  });
  overlay.querySelector('#pinInput').addEventListener('keydown', e => {
    if (e.key === 'Enter') overlay.querySelector('#pinOk').click();
  });
});

document.getElementById('saveSemanaBtn').addEventListener('click', () => {
  const val = document.getElementById('semanaTexto').value.trim();
  if (!val) return;
  set(ref(db, 'semana'), val).then(() => showSaved('semanaSaved'));
});

document.getElementById('saveBulkBtn').addEventListener('click', () => {
  const rows = document.querySelectorAll('#bulkBody tr');
  const nuevos = [];
  rows.forEach(row => {
    const sels = row.querySelectorAll('select');
    const dia = sels[0].value, nombre = sels[1].value, area = sels[2].value, horario = sels[3].value;
    if (dia && nombre && area && horario) nuevos.push({ dia, nombre, area, horario });
  });
  if (!nuevos.length) return;
  const promises = nuevos.map(b => push(ref(db, 'bloques'), b));
  Promise.all(promises).then(() => {
    document.getElementById('bulkBody').innerHTML = '';
    addBulkRow();
    showSaved('bulkSaved');
  });
});

document.getElementById('addTareaBtn').addEventListener('click', () => {
  const dia = document.getElementById('tDia').value;
  const nombre = document.getElementById('tNombre').value;
  const texto = document.getElementById('tTexto').value.trim();
  if (!dia || !nombre || !texto) return;
  push(ref(db, 'tareas'), { dia, nombre, texto }).then(() => {
    ['tDia','tNombre'].forEach(id => document.getElementById(id).value = '');
    document.getElementById('tTexto').value = '';
    showSaved('tareaSaved');
  });
});

document.getElementById('clearBtn').addEventListener('click', () => {
  if (!confirm('¿Seguro que quieres borrar todos los bloques y tareas?')) return;
  remove(ref(db, 'bloques'));
  remove(ref(db, 'tareas'));
});
</script>
</body>
</html>
