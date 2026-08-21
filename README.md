<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0"/>
<title>Partes y Mantenimiento - Transporte Liquido</title>
<link rel="icon" href="data:,">
<style>
  :root{
    --bg:#EEF1F4;
    --ink:#1A2233;
    --ink-soft:#5B6472;
    --primary:#16233F;
    --primary-2:#233A63;
    --accent:#FFB020;
    --urgent:#D64545;
    --urgent-bg:#FDECEC;
    --medium:#E8A33D;
    --medium-bg:#FDF3E3;
    --low:#3F7CAC;
    --low-bg:#E9F1F7;
    --success:#2E8B57;
    --success-bg:#E7F4EC;
    --card:#FFFFFF;
    --line:#DCE1E8;
    --radius:14px;
    --font-display:'Archivo Black', 'Arial Black', sans-serif;
    --font-body:'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  }
  @import url('https://fonts.googleapis.com/css2?family=Archivo+Black&family=Inter:wght@400;500;600;700;800&display=swap');

  *{box-sizing:border-box;}
  body{margin:0;font-family:var(--font-body);background:var(--bg);color:var(--ink);}
  #root{max-width:560px;margin:0 auto;min-height:100vh;background:var(--bg);position:relative;padding-bottom:40px;}

  .topbar{background:var(--primary);color:#fff;padding:18px 18px 60px;position:relative;overflow:hidden;}
  .topbar::after{
    content:"";position:absolute;right:-30px;top:-30px;width:160px;height:160px;
    background:radial-gradient(circle, rgba(255,176,32,0.18) 0%, transparent 70%);
  }
  .topbar-inner{position:relative;z-index:1;display:flex;align-items:center;gap:12px;}
  .logo-tank{width:38px;height:38px;flex-shrink:0;}
  .logo-company{height:40px;width:auto;flex-shrink:0;display:block;}
  .brand{display:flex;flex-direction:column;line-height:1.1;}
  .brand-title{font-family:var(--font-display);font-size:15px;letter-spacing:0.5px;}
  .brand-sub{font-size:11px;color:#B9C2D6;letter-spacing:0.5px;margin-top:2px;}

  .role-switch{
    display:flex;background:var(--card);border-radius:999px;padding:4px;
    margin:-42px 18px 0;position:relative;z-index:2;box-shadow:0 6px 20px rgba(20,30,55,0.18);
  }
  .role-btn{
    flex:1;border:none;background:transparent;padding:12px 8px;border-radius:999px;
    font-family:var(--font-body);font-weight:700;font-size:13.5px;cursor:pointer;
    color:var(--ink-soft);transition:all .18s ease;display:flex;align-items:center;justify-content:center;gap:6px;
  }
  .role-btn.active{background:var(--primary);color:#fff;}
  .role-btn .badge{
    background:var(--urgent);color:#fff;font-size:10px;font-weight:800;
    border-radius:999px;padding:1px 6px;min-width:16px;text-align:center;
  }

  .content{padding:22px 18px 10px;}

  .field{margin-bottom:18px;}
  .field label{
    display:block;font-size:12.5px;font-weight:800;color:var(--ink-soft);
    text-transform:uppercase;letter-spacing:0.6px;margin-bottom:8px;
  }
  .field label .req{color:var(--urgent);}
  input[type="text"], input[type="number"], input[type="date"], textarea, select{
    width:100%;border:2px solid var(--line);border-radius:10px;padding:13px 14px;
    font-size:15px;font-family:var(--font-body);background:var(--card);color:var(--ink);
  }
  input:focus, textarea:focus, select:focus{outline:none;border-color:var(--primary-2);}
  textarea{resize:vertical;min-height:90px;}

  .chip-row{display:flex;flex-wrap:wrap;gap:8px;}
  .chip{
    border:2px solid var(--line);background:var(--card);border-radius:10px;
    padding:11px 14px;font-weight:700;font-size:13.5px;cursor:pointer;color:var(--ink);
    display:flex;align-items:center;gap:7px;transition:all .15s ease;
  }
  .chip.selected{border-color:var(--primary);background:var(--primary);color:#fff;}

  .urg-row{display:flex;flex-direction:column;gap:9px;}
  .urg-opt{
    border:2px solid var(--line);border-radius:10px;padding:12px 14px;
    display:flex;align-items:center;gap:11px;cursor:pointer;background:var(--card);
  }
  .urg-dot{width:14px;height:14px;border-radius:50%;flex-shrink:0;}
  .urg-opt .urg-text{font-weight:700;font-size:14px;}
  .urg-opt .urg-desc{font-size:12px;color:var(--ink-soft);margin-top:1px;}
  .urg-opt.selected[data-level="urgente"]{border-color:var(--urgent);background:var(--urgent-bg);}
  .urg-opt.selected[data-level="cuando_se_pueda"]{border-color:var(--medium);background:var(--medium-bg);}
  .urg-opt.selected[data-level="tener_en_cuenta"]{border-color:var(--low);background:var(--low-bg);}

  .photo-zone{
    border:2px dashed var(--line);border-radius:12px;padding:18px;text-align:center;
    background:var(--card);cursor:pointer;
  }
  .photo-zone p{margin:8px 0 0;font-size:13px;color:var(--ink-soft);font-weight:600;}
  .thumbs{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px;}
  .thumb{position:relative;width:72px;height:72px;border-radius:9px;overflow:hidden;border:1px solid var(--line);}
  .thumb img{width:100%;height:100%;object-fit:cover;}
  .thumb .rm{
    position:absolute;top:2px;right:2px;background:rgba(20,20,20,0.7);color:#fff;
    border:none;border-radius:50%;width:20px;height:20px;font-size:12px;cursor:pointer;line-height:1;
  }

  .submit-btn{
    width:100%;background:var(--accent);color:var(--primary);border:none;border-radius:12px;
    padding:16px;font-family:var(--font-display);font-size:14px;letter-spacing:0.4px;
    cursor:pointer;margin-top:6px;box-shadow:0 6px 16px rgba(255,176,32,0.35);
  }
  .submit-btn:disabled{opacity:0.5;box-shadow:none;cursor:not-allowed;}
  .btn-secondary{
    background:var(--primary);color:#fff;border:none;border-radius:10px;padding:12px 16px;
    font-weight:800;font-size:13px;cursor:pointer;
  }
  .btn-ghost{
    background:transparent;color:var(--primary);border:2px solid var(--primary);border-radius:10px;
    padding:10px 14px;font-weight:800;font-size:12.5px;cursor:pointer;
  }
  .btn-danger-ghost{
    background:transparent;color:var(--urgent);border:2px solid var(--urgent);border-radius:10px;
    padding:8px 12px;font-weight:800;font-size:12px;cursor:pointer;
  }

  .toast{
    position:fixed;bottom:24px;left:50%;transform:translateX(-50%);
    background:var(--success);color:#fff;padding:13px 20px;border-radius:10px;
    font-weight:700;font-size:13.5px;box-shadow:0 8px 20px rgba(0,0,0,0.2);
    display:flex;align-items:center;gap:8px;z-index:50;animation:toastin .2s ease;
  }
  @keyframes toastin{from{opacity:0;transform:translate(-50%,10px);}to{opacity:1;transform:translate(-50%,0);}}

  .filters{display:flex;gap:7px;overflow-x:auto;padding-bottom:4px;margin-bottom:16px;}
  .filter-chip{
    flex-shrink:0;border:2px solid var(--line);background:var(--card);border-radius:999px;
    padding:8px 13px;font-size:12.5px;font-weight:700;cursor:pointer;color:var(--ink-soft);white-space:nowrap;
  }
  .filter-chip.active{border-color:var(--primary);background:var(--primary);color:#fff;}

  .report-card{
    background:var(--card);border-radius:var(--radius);padding:15px;margin-bottom:12px;
    border-left:6px solid var(--low);box-shadow:0 2px 8px rgba(20,30,55,0.06);
  }
  .report-card[data-urg="urgente"]{border-left-color:var(--urgent);}
  .report-card[data-urg="cuando_se_pueda"]{border-left-color:var(--medium);}
  .report-card[data-urg="tener_en_cuenta"]{border-left-color:var(--low);}

  .rc-top{display:flex;justify-content:space-between;align-items:flex-start;gap:8px;}
  .rc-vehicle{font-family:var(--font-display);font-size:15px;color:var(--primary);}
  .rc-time{font-size:11px;color:var(--ink-soft);white-space:nowrap;margin-top:3px;}
  .rc-tags{display:flex;gap:6px;flex-wrap:wrap;margin:9px 0;}
  .tag{border-radius:7px;padding:4px 9px;font-size:11px;font-weight:800;letter-spacing:0.3px;}
  .tag.urg-urgente{background:var(--urgent-bg);color:var(--urgent);}
  .tag.urg-cuando_se_pueda{background:var(--medium-bg);color:#96631F;}
  .tag.urg-tener_en_cuenta{background:var(--low-bg);color:var(--low);}
  .tag.tipo{background:#EEF1F4;color:var(--ink-soft);}
  .rc-desc{font-size:13.5px;color:var(--ink);margin:8px 0;line-height:1.45;}
  .rc-meta{font-size:12px;color:var(--ink-soft);margin-bottom:8px;}
  .rc-meta b{color:var(--ink);}
  .rc-photos{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:10px;}
  .rc-photos img{width:58px;height:58px;object-fit:cover;border-radius:7px;cursor:pointer;border:1px solid var(--line);}
  .status-row{display:flex;gap:6px;flex-wrap:wrap;}
  .status-btn{
    border:1.5px solid var(--line);background:#fff;border-radius:8px;padding:7px 10px;
    font-size:11.5px;font-weight:700;cursor:pointer;color:var(--ink-soft);
  }
  .status-btn.active-pendiente{border-color:var(--urgent);color:var(--urgent);background:var(--urgent-bg);}
  .status-btn.active-revision{border-color:var(--medium);color:#96631F;background:var(--medium-bg);}
  .status-btn.active-resuelto{border-color:var(--success);color:var(--success);background:var(--success-bg);}

  .empty-state{text-align:center;padding:60px 20px;color:var(--ink-soft);}
  .empty-state svg{opacity:0.35;margin-bottom:10px;}
  .empty-state p{font-size:14px;font-weight:600;}

  .lightbox{
    position:fixed;inset:0;background:rgba(10,14,24,0.9);z-index:100;
    display:flex;align-items:center;justify-content:center;padding:20px;
  }
  .lightbox img{max-width:100%;max-height:90vh;border-radius:8px;}
  .lightbox-close{position:absolute;top:18px;right:18px;background:rgba(255,255,255,0.15);border:none;color:#fff;width:38px;height:38px;border-radius:50%;font-size:18px;cursor:pointer;}

  /* --- sub navegacion mantenimiento --- */
  .subnav{display:flex;gap:8px;margin-bottom:16px;overflow-x:auto;}
  .subnav-btn{
    flex-shrink:0;padding:9px 14px;border-radius:10px;border:2px solid var(--line);
    background:var(--card);font-weight:700;font-size:12.5px;cursor:pointer;color:var(--ink-soft);white-space:nowrap;
  }
  .subnav-btn.active{background:var(--primary);color:#fff;border-color:var(--primary);}
  .subnav-btn .mini-badge{background:var(--urgent);color:#fff;border-radius:999px;padding:1px 6px;font-size:9.5px;margin-left:5px;}

  .section-title{font-family:var(--font-display);font-size:13px;color:var(--primary);margin:4px 0 12px;letter-spacing:0.3px;}
  .summary-strip{
    display:flex;gap:10px;margin-bottom:16px;
  }
  .summary-box{
    flex:1;background:var(--card);border-radius:12px;padding:13px;text-align:center;box-shadow:0 2px 8px rgba(20,30,55,0.06);
  }
  .summary-box .num{font-family:var(--font-display);font-size:17px;color:var(--primary);}
  .summary-box .lbl{font-size:10.5px;color:var(--ink-soft);font-weight:700;text-transform:uppercase;margin-top:3px;}

  .list-card{
    background:var(--card);border-radius:12px;padding:14px;margin-bottom:10px;box-shadow:0 2px 8px rgba(20,30,55,0.06);
  }
  .list-card-top{display:flex;justify-content:space-between;align-items:flex-start;gap:8px;}
  .list-card-title{font-weight:800;font-size:14px;color:var(--ink);}
  .list-card-sub{font-size:12px;color:var(--ink-soft);margin-top:2px;}
  .cost-pill{background:var(--success-bg);color:var(--success);font-weight:800;font-size:13px;padding:4px 10px;border-radius:8px;white-space:nowrap;}

  .form-card{background:var(--card);border-radius:12px;padding:16px;margin-bottom:16px;border:2px dashed var(--line);}
  .form-row{display:flex;gap:10px;}
  .form-row .field{flex:1;}
  .add-toggle{
    display:flex;align-items:center;justify-content:center;gap:6px;width:100%;
    border:2px dashed var(--line);background:transparent;border-radius:12px;padding:13px;
    font-weight:800;font-size:13px;color:var(--primary);cursor:pointer;margin-bottom:16px;
  }

  .pend-pill{background:var(--medium-bg);color:#96631F;font-weight:800;font-size:11.5px;padding:3px 8px;border-radius:7px;}

  .toggle-row{display:flex;align-items:center;gap:8px;margin:8px 0;}
  .toggle-row input[type="checkbox"]{width:18px;height:18px;}
  .toggle-row label{font-size:13px;font-weight:700;color:var(--ink);text-transform:none;letter-spacing:0;margin:0;}

  .mount-banner{
    background:var(--primary);color:#fff;border-radius:12px;padding:12px 14px;margin-bottom:14px;
    display:flex;justify-content:space-between;align-items:center;gap:10px;font-size:12.5px;font-weight:700;
  }
  .mount-banner button{background:var(--accent);color:var(--primary);border:none;border-radius:8px;padding:6px 10px;font-weight:800;font-size:11.5px;cursor:pointer;}

  .vehicle-card{
    background:var(--card);border-radius:12px;padding:13px 14px;margin-bottom:9px;
    display:flex;justify-content:space-between;align-items:center;cursor:pointer;
    border:2px solid var(--line);box-shadow:0 2px 8px rgba(20,30,55,0.05);
  }
  .vehicle-card.selected{border-color:var(--primary);}
  .vehicle-card .vc-plate{font-family:var(--font-display);font-size:14px;color:var(--primary);}
  .vehicle-card .vc-meta{font-size:11.5px;color:var(--ink-soft);margin-top:2px;}
  .vehicle-card .vc-alert{background:var(--urgent);color:#fff;font-size:10px;font-weight:800;border-radius:999px;padding:2px 7px;}

  .axle-diagram{background:var(--card);border-radius:12px;padding:18px 12px;margin-bottom:14px;}
  .axle-row{display:flex;flex-direction:column;align-items:center;margin-bottom:22px;}
  .axle-row:last-child{margin-bottom:4px;}
  .axle-label{font-size:10.5px;font-weight:800;color:var(--ink-soft);text-transform:uppercase;margin-bottom:10px;letter-spacing:0.4px;}
  .axle-bar{display:flex;align-items:center;gap:16px;position:relative;}
  .axle-bar::before{
    content:"";position:absolute;left:0;right:0;top:50%;height:4px;background:var(--line);
    border-radius:2px;z-index:0;
  }
  .wheel-group{display:flex;gap:4px;position:relative;z-index:1;}
  .wheel-slot{
    width:36px;height:36px;border-radius:9px;border:2px solid var(--line);background:#F5F6F8;
    display:flex;align-items:center;justify-content:center;font-size:9.5px;font-weight:800;
    cursor:pointer;color:var(--ink-soft);
  }
  .wheel-slot.filled{background:var(--primary);color:#fff;border-color:var(--primary);}
  .wheel-slot.alert{background:var(--urgent);border-color:var(--urgent);color:#fff;}
  .wheel-slot.picking{border-color:var(--accent);box-shadow:0 0 0 3px rgba(255,176,32,0.35);}

  .slot-panel{
    background:var(--low-bg);border-radius:12px;padding:14px;margin-top:6px;border:2px solid var(--low);
  }
  .slot-panel.filled-panel{background:var(--card);border-color:var(--primary);}
  .slot-panel .sp-title{font-weight:800;font-size:13px;color:var(--primary);margin-bottom:8px;}
  .pick-tire{
    background:var(--card);border:2px solid var(--line);border-radius:9px;padding:10px 12px;
    margin-bottom:7px;cursor:pointer;display:flex;justify-content:space-between;align-items:center;
  }
  .pick-tire b{font-size:13px;}
  .pick-tire span{font-size:11px;color:var(--ink-soft);}

  .km-row{display:flex;gap:8px;align-items:flex-end;margin-bottom:16px;}
  .km-row .field{flex:1;margin-bottom:0;}

  table.simple-table{width:100%;border-collapse:collapse;font-size:12.5px;}
  table.simple-table th{text-align:left;color:var(--ink-soft);font-size:10.5px;text-transform:uppercase;padding:6px 4px;border-bottom:2px solid var(--line);}
  table.simple-table td{padding:7px 4px;border-bottom:1px solid var(--line);}
</style>
</head>
<body>
<div id="root"></div>

<!-- Firebase (guarda y sincroniza los datos entre todos los moviles) -->
<script src="https://www.gstatic.com/firebasejs/10.13.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.13.0/firebase-firestore-compat.js"></script>

<script>
const KEY_AVERIAS = 'partes:list';
const KEY_REPARACIONES = 'reparaciones:list';
const KEY_NEUMATICOS = 'neumaticos:data';

let reports = [];
let repairs = [];
let tireData = { proveedores: [], compras: [], stock: [], vehiculos: [], rotationThreshold: 10000 };

let currentRole = 'chofer';
const MANT_PIN = '7412';
let mantAuthenticated = false;
let showPinPrompt = false;
let pinError = false;
let activeFilter = 'todos';
let selectedTipo = null;
let selectedUrgencia = null;
let selectedPhotos = [];
let loading = true;

let mantSubTab = 'averias';
let selectedReportId = null;
let newCommentText = '';
let neumSubTab = 'compras';
let showAddCompra = false;
let showAddVehiculo = false;
let showAddReparacion = false;
let mountingTireId = null;
let selectedVehiculoId = null;
let activeSlotKey = null;

const TIPOS = [
  {id:'cisterna', label:'Cisterna', icon:'🛢️'},
  {id:'ruedas', label:'Ruedas', icon:'🛞'},
  {id:'mecanica', label:'Mecánica', icon:'🔧'},
  {id:'taller', label:'Taller', icon:'🏭'},
];
const URGENCIAS = [
  {id:'urgente', label:'Urgente', desc:'No puede seguir circulando', color:'var(--urgent)'},
  {id:'cuando_se_pueda', label:'Cuando se pueda', desc:'Necesita revisión próximamente', color:'var(--medium)'},
  {id:'tener_en_cuenta', label:'Hay que tenerlo en cuenta', desc:'No urgente, pero anotarlo', color:'var(--low)'},
];
const URG_LABELS = {urgente:'Urgente', cuando_se_pueda:'Cuando se pueda', tener_en_cuenta:'Tener en cuenta'};
const TIPO_LABELS = {cisterna:'Cisterna', ruedas:'Ruedas', mecanica:'Mecánica', taller:'Taller'};

/* ---------------- STORAGE (Firebase Firestore) ---------------- */
/* Estos datos los rellena Firebase con lo que copies de tu proyecto. Ver guia paso a paso. */
const firebaseConfig = {
  apiKey: "AIzaSyCwuoDAVWer1irBrGvDDhWNhD6ddUMhr1s",
  authDomain: "mantenimiento-flota-63980.firebaseapp.com",
  projectId: "mantenimiento-flota-63980",
  storageBucket: "mantenimiento-flota-63980.firebasestorage.app",
  messagingSenderId: "1033220715622",
  appId: "1:1033220715622:web:0babc9cf91cd506d93a9a7"
};

firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();
const COL = 'partes_liquidos';
let firstLoadDone = { averias:false, reparaciones:false, neumaticos:false };

function checkAllLoaded(){
  if(firstLoadDone.averias && firstLoadDone.reparaciones && firstLoadDone.neumaticos){
    loading = false;
    render();
  }
}

function loadAll(){
  db.collection(COL).doc('averias').onSnapshot(doc=>{
    reports = (doc.exists && doc.data().list) ? doc.data().list : [];
    firstLoadDone.averias = true;
    if(loading) checkAllLoaded(); else render();
  }, err=>{ console.error('Error averias', err); firstLoadDone.averias = true; checkAllLoaded(); });

  db.collection(COL).doc('reparaciones').onSnapshot(doc=>{
    repairs = (doc.exists && doc.data().list) ? doc.data().list : [];
    firstLoadDone.reparaciones = true;
    if(loading) checkAllLoaded(); else render();
  }, err=>{ console.error('Error reparaciones', err); firstLoadDone.reparaciones = true; checkAllLoaded(); });

  db.collection(COL).doc('neumaticos').onSnapshot(doc=>{
    tireData = doc.exists ? doc.data() : { proveedores: [], compras: [], stock: [], vehiculos: [], rotationThreshold: 10000 };
    if(!tireData.proveedores) tireData.proveedores = [];
    if(!tireData.compras) tireData.compras = [];
    if(!tireData.stock) tireData.stock = [];
    if(!tireData.vehiculos) tireData.vehiculos = [];
    if(!tireData.rotationThreshold) tireData.rotationThreshold = 10000;
    firstLoadDone.neumaticos = true;
    if(loading) checkAllLoaded(); else render();
  }, err=>{ console.error('Error neumaticos', err); firstLoadDone.neumaticos = true; checkAllLoaded(); });
}

async function saveReports(){ try{ await db.collection(COL).doc('averias').set({list: reports}); }catch(e){ console.error(e); showToast('⚠ Error guardando (revisa conexión)'); } }
async function saveRepairs(){ try{ await db.collection(COL).doc('reparaciones').set({list: repairs}); }catch(e){ console.error(e); showToast('⚠ Error guardando (revisa conexión)'); } }
async function saveTireData(){ try{ await db.collection(COL).doc('neumaticos').set(tireData); }catch(e){ console.error(e); showToast('⚠ Error guardando (revisa conexión)'); } }

/* ---------------- UTIL ---------------- */

function compressImage(file){
  return new Promise((resolve,reject)=>{
    const reader = new FileReader();
    reader.onload = (e)=>{
      const img = new Image();
      img.onload = ()=>{
        const maxDim = 900;
        let w = img.width, h = img.height;
        if(w > h && w > maxDim){ h = h*(maxDim/w); w = maxDim; }
        else if(h > maxDim){ w = w*(maxDim/h); h = maxDim; }
        const canvas = document.createElement('canvas');
        canvas.width = w; canvas.height = h;
        const ctx = canvas.getContext('2d');
        ctx.drawImage(img,0,0,w,h);
        resolve(canvas.toDataURL('image/jpeg', 0.55));
      };
      img.onerror = reject;
      img.src = e.target.result;
    };
    reader.onerror = reject;
    reader.readAsDataURL(file);
  });
}
function showToast(msg){
  const t = document.createElement('div');
  t.className = 'toast';
  t.innerHTML = '<span>✓</span><span>'+msg+'</span>';
  document.getElementById('root').appendChild(t);
  setTimeout(()=>t.remove(), 2600);
}
const LOGO_BASE64 = "iVBORw0KGgoAAAANSUhEUgAAAPYAAABMCAYAAABeQ0rbAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAA+hpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMTM4IDc5LjE1OTgyNCwgMjAxNi8wOS8xNC0wMTowOTowMSAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczpkYz0iaHR0cDovL3B1cmwub3JnL2RjL2VsZW1lbnRzLzEuMS8iIHhtbG5zOnhtcE1NPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvbW0vIiB4bWxuczpzdFJlZj0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL3NUeXBlL1Jlc291cmNlUmVmIyIgeG1wOkNyZWF0b3JUb29sPSJDb3JlbERSQVcgWDciIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6QzlFMkEyNkY0NjE5MTFFOEE2MzhGQkE4NkMyQzRCOTkiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6QzlFMkEyNzA0NjE5MTFFOEE2MzhGQkE4NkMyQzRCOTkiPiA8ZGM6Y3JlYXRvcj4gPHJkZjpTZXE+IDxyZGY6bGk+QWxlamFuZHJvPC9yZGY6bGk+IDwvcmRmOlNlcT4gPC9kYzpjcmVhdG9yPiA8ZGM6dGl0bGU+IDxyZGY6QWx0PiA8cmRmOmxpIHhtbDpsYW5nPSJ4LWRlZmF1bHQiPlNpbiB0w610dWxvLTE8L3JkZjpsaT4gPC9yZGY6QWx0PiA8L2RjOnRpdGxlPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6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";
function tankIconSvg(){
  return '<img class="logo-company" src="data:image/png;base64,'+LOGO_BASE64+'" alt="Transvimon"/>';
}
function pendingUrgentCount(){ return reports.filter(r=>r.urgencia==='urgente' && r.estado!=='resuelto').length; }
function formatDate(iso){
  const d = new Date(iso);
  const now = new Date();
  const sameDay = d.toDateString()===now.toDateString();
  const time = d.toLocaleTimeString('es-ES',{hour:'2-digit',minute:'2-digit'});
  if(sameDay) return 'Hoy ' + time;
  return d.toLocaleDateString('es-ES',{day:'2-digit',month:'2-digit'}) + ' ' + time;
}
function formatDateOnly(iso){
  if(!iso) return '-';
  const d = new Date(iso);
  return d.toLocaleDateString('es-ES',{day:'2-digit',month:'2-digit',year:'numeric'});
}
function escapeHtml(str){
  const div = document.createElement('div');
  div.textContent = str==null?'':str;
  return div.innerHTML;
}
function uid(){ return Date.now() + '-' + Math.random().toString(36).slice(2,7); }
function euros(n){ return (Number(n)||0).toLocaleString('es-ES',{minimumFractionDigits:2, maximumFractionDigits:2}) + ' €'; }

/* ---------------- ROOT RENDER ---------------- */

function render(){
  const root = document.getElementById('root');
  const badge = pendingUrgentCount();
  root.innerHTML =
    '<div class="topbar">'+
      '<div class="topbar-inner">'+ tankIconSvg() +
        '<div class="brand">'+
          '<div class="brand-title">PARTES Y MANTENIMIENTO</div>'+
          '<div class="brand-sub">CISTERNAS · TRANSPORTE LÍQUIDO</div>'+
        '</div>'+
      '</div>'+
    '</div>'+
    '<div class="role-switch">'+
      '<button class="role-btn '+(currentRole==='chofer' && !showPinPrompt?'active':'')+'" data-role="chofer">🚚 Chofer</button>'+
      '<button class="role-btn '+(currentRole==='mantenimiento' || showPinPrompt?'active':'')+'" data-role="mantenimiento">'+
        '🔒 Mantenimiento '+(badge>0?'<span class="badge">'+badge+'</span>':'')+
      '</button>'+
    '</div>'+
    '<div class="content" id="content"></div>';

  document.querySelectorAll('.role-btn').forEach(b=>{
    b.onclick = ()=>{
      if(b.dataset.role==='mantenimiento' && !mantAuthenticated){
        showPinPrompt = true; pinError = false; render(); return;
      }
      showPinPrompt = false;
      currentRole = b.dataset.role;
      render();
    };
  });

  const content = document.getElementById('content');
  if(loading){
    content.innerHTML = '<div class="empty-state"><p>Cargando…</p></div>';
    return;
  }
  if(showPinPrompt) renderPinPrompt(content);
  else if(currentRole === 'chofer') renderChoferForm(content);
  else renderMantenimiento(content);
}

function renderPinPrompt(content){
  content.innerHTML =
    '<div style="text-align:center;padding:30px 10px 10px;">'+
      '<div style="font-size:38px;">🔒</div>'+
      '<div class="section-title" style="margin-top:10px;">ACCESO MANTENIMIENTO</div>'+
      '<p style="font-size:13px;color:var(--ink-soft);margin-bottom:20px;">Introduce el código para entrar</p>'+
    '</div>'+
    '<div class="field"><input type="text" inputmode="numeric" maxlength="4" id="pin-input" placeholder="••••" style="text-align:center;font-size:24px;letter-spacing:8px;font-weight:800;"/></div>'+
    (pinError ? '<p style="color:var(--urgent);font-size:12.5px;font-weight:700;text-align:center;margin-top:-8px;">Código incorrecto</p>' : '')+
    '<button class="submit-btn" id="pin-submit">ENTRAR</button>'+
    '<button class="btn-ghost" id="pin-cancel" style="width:100%;margin-top:10px;">Cancelar</button>';

  const input = document.getElementById('pin-input');
  input.focus();
  const tryPin = ()=>{
    if(input.value === MANT_PIN){
      mantAuthenticated = true; showPinPrompt = false; pinError = false; currentRole = 'mantenimiento';
      render();
    } else {
      pinError = true; renderPinPrompt(content);
    }
  };
  document.getElementById('pin-submit').onclick = tryPin;
  input.onkeydown = (e)=>{ if(e.key==='Enter') tryPin(); };
  document.getElementById('pin-cancel').onclick = ()=>{ showPinPrompt=false; currentRole='chofer'; render(); };
}

/* ---------------- CHOFER ---------------- */

function renderChoferForm(content){
  content.innerHTML =
    '<div class="field"><label>Tu nombre <span class="req">*</span></label>'+
    '<input type="text" id="f-nombre" placeholder="Nombre y apellido" value="'+((window.__draft&&window.__draft.nombre)||'')+'"/></div>'+
    '<div class="field"><label>Vehículo / matrícula <span class="req">*</span></label>'+
    '<input type="text" id="f-vehiculo" placeholder="Ej. 4521-BXK" value="'+((window.__draft&&window.__draft.vehiculo)||'')+'"/></div>'+
    '<div class="field"><label>Tipo de avería <span class="req">*</span></label>'+
    '<div class="chip-row" id="tipo-row">'+
      TIPOS.map(t=>'<div class="chip '+(selectedTipo===t.id?'selected':'')+'" data-tipo="'+t.id+'">'+t.icon+' '+t.label+'</div>').join('')+
    '</div></div>'+
    '<div class="field"><label>Urgencia <span class="req">*</span></label>'+
    '<div class="urg-row" id="urg-row">'+
      URGENCIAS.map(u=>'<div class="urg-opt '+(selectedUrgencia===u.id?'selected':'')+'" data-level="'+u.id+'" data-urg="'+u.id+'">'+
        '<div class="urg-dot" style="background:'+u.color+'"></div>'+
        '<div><div class="urg-text">'+u.label+'</div><div class="urg-desc">'+u.desc+'</div></div></div>').join('')+
    '</div></div>'+
    '<div class="field"><label>Descripción <span class="req">*</span></label>'+
    '<textarea id="f-desc" placeholder="Describe el problema con el máximo detalle posible…">'+((window.__draft&&window.__draft.desc)||'')+'</textarea></div>'+
    '<div class="field"><label>Fotos</label>'+
    '<div class="photo-zone" id="photo-zone"><div style="font-size:26px;">📷</div><p>Toca para añadir fotos (máx. 4)</p></div>'+
    '<input type="file" id="f-photos" accept="image/*" capture="environment" multiple style="display:none"/>'+
    '<div class="thumbs" id="thumbs"></div></div>'+
    '<button class="submit-btn" id="submit-btn">ENVIAR PARTE</button>';

  document.querySelectorAll('#tipo-row .chip').forEach(c=>{
    c.onclick = ()=>{ selectedTipo = c.dataset.tipo; renderChoferForm(content); };
  });
  document.querySelectorAll('#urg-row .urg-opt').forEach(u=>{
    u.onclick = ()=>{ selectedUrgencia = u.dataset.urg; renderChoferForm(content); };
  });

  const photoZone = document.getElementById('photo-zone');
  const photoInput = document.getElementById('f-photos');
  photoZone.onclick = ()=> photoInput.click();
  photoInput.onchange = async (e)=>{
    const files = Array.from(e.target.files).slice(0, 4 - selectedPhotos.length);
    for(const f of files){
      try{ selectedPhotos.push(await compressImage(f)); }catch(err){}
    }
    renderThumbs();
  };
  renderThumbs();

  ['f-nombre','f-vehiculo','f-desc'].forEach(id=>{
    document.getElementById(id).oninput = (e)=>{
      window.__draft = window.__draft || {};
      const map = {'f-nombre':'nombre','f-vehiculo':'vehiculo','f-desc':'desc'};
      window.__draft[map[id]] = e.target.value;
    };
  });

  document.getElementById('submit-btn').onclick = submitReport;
}

function renderThumbs(){
  const t = document.getElementById('thumbs');
  if(!t) return;
  t.innerHTML = selectedPhotos.map((p,i)=>'<div class="thumb"><img src="'+p+'"/><button class="rm" data-i="'+i+'">×</button></div>').join('');
  t.querySelectorAll('.rm').forEach(btn=>{
    btn.onclick = ()=>{ selectedPhotos.splice(parseInt(btn.dataset.i),1); renderThumbs(); };
  });
}

async function submitReport(){
  const nombre = document.getElementById('f-nombre').value.trim();
  const vehiculo = document.getElementById('f-vehiculo').value.trim();
  const desc = document.getElementById('f-desc').value.trim();

  if(!nombre || !vehiculo || !desc || !selectedTipo || !selectedUrgencia){
    showToast('⚠ Faltan campos obligatorios');
    return;
  }
  const btn = document.getElementById('submit-btn');
  btn.disabled = true; btn.textContent = 'ENVIANDO…';

  reports.unshift({
    id: uid(), nombre, vehiculo, tipo: selectedTipo, urgencia: selectedUrgencia,
    descripcion: desc, fotos: selectedPhotos.slice(), estado: 'pendiente', timestamp: new Date().toISOString(),
  });
  await saveReports();

  selectedTipo = null; selectedUrgencia = null; selectedPhotos = [];
  window.__draft = {};
  render();
  showToast('Parte enviado a mantenimiento');
}

/* ---------------- MANTENIMIENTO: NAV ---------------- */

function renderMantenimiento(content){
  const rotAlerts = countRotationAlerts();
  content.innerHTML =
    '<div class="subnav">'+
      '<div class="subnav-btn '+(mantSubTab==='averias'?'active':'')+'" data-tab="averias">Averías</div>'+
      '<div class="subnav-btn '+(mantSubTab==='reparaciones'?'active':'')+'" data-tab="reparaciones">Reparaciones</div>'+
      '<div class="subnav-btn '+(mantSubTab==='neumaticos'?'active':'')+'" data-tab="neumaticos">Neumáticos'+(rotAlerts>0?'<span class="mini-badge">'+rotAlerts+'</span>':'')+'</div>'+
      '<div class="subnav-btn" id="logout-mant" style="margin-left:auto;">🔒 Salir</div>'+
    '</div>'+
    '<div id="mant-body"></div>';

  document.querySelectorAll('.subnav-btn[data-tab]').forEach(b=>{
    b.onclick = ()=>{ mantSubTab = b.dataset.tab; renderMantenimiento(content); };
  });
  document.getElementById('logout-mant').onclick = ()=>{
    mantAuthenticated = false; currentRole = 'chofer'; render();
  };

  const body = document.getElementById('mant-body');
  if(mantSubTab==='averias') renderAverias(body);
  else if(mantSubTab==='reparaciones') renderReparaciones(body);
  else renderNeumaticos(body);
}

/* ---------------- AVERIAS (mantenimiento) ---------------- */

function renderAverias(content){
  const selected = reports.find(r=>r.id===selectedReportId);
  if(selected){ renderAveriaDetail(content, selected); return; }

  const filters = [
    {id:'todos', label:'Todos'},
    {id:'urgente', label:'🔴 Urgente'},
    {id:'cuando_se_pueda', label:'🟠 Cuando se pueda'},
    {id:'tener_en_cuenta', label:'🔵 Tenerlo en cuenta'},
    {id:'pendiente', label:'Pendientes'},
    {id:'revision', label:'En reparación'},
    {id:'resuelto', label:'Resueltos'},
  ];
  let filtered = reports.slice();
  if(['urgente','cuando_se_pueda','tener_en_cuenta'].includes(activeFilter)) filtered = filtered.filter(r=>r.urgencia===activeFilter);
  else if(activeFilter==='pendiente') filtered = filtered.filter(r=>r.estado==='pendiente');
  else if(activeFilter==='revision') filtered = filtered.filter(r=>r.estado==='revision');
  else if(activeFilter==='resuelto') filtered = filtered.filter(r=>r.estado==='resuelto');

  filtered.sort((a,b)=>{
    const order = {urgente:0, cuando_se_pueda:1, tener_en_cuenta:2};
    if(order[a.urgencia]!==order[b.urgencia]) return order[a.urgencia]-order[b.urgencia];
    return new Date(b.timestamp) - new Date(a.timestamp);
  });

  content.innerHTML =
    '<div class="filters" id="filters">'+
      filters.map(f=>'<div class="filter-chip '+(activeFilter===f.id?'active':'')+'" data-f="'+f.id+'">'+f.label+'</div>').join('')+
    '</div>'+
    '<div id="report-list"></div>';

  document.querySelectorAll('.filter-chip').forEach(c=>{
    c.onclick = ()=>{ activeFilter = c.dataset.f; renderAverias(content); };
  });

  const list = document.getElementById('report-list');
  if(filtered.length === 0){
    list.innerHTML = '<div class="empty-state"><p>No hay partes en esta categoría</p></div>';
    return;
  }
  const ESTADO_TAG = {
    pendiente: '<span class="tag" style="background:var(--urgent-bg);color:var(--urgent);">● Pendiente</span>',
    revision: '<span class="tag" style="background:var(--medium-bg);color:#96631F;">● En reparación</span>',
    resuelto: '<span class="tag" style="background:var(--success-bg);color:var(--success);">✔ Resuelto</span>',
  };
  list.innerHTML = filtered.map(r=>
    '<div class="report-card" data-urg="'+r.urgencia+'" data-id="'+r.id+'">'+
      '<div class="rc-top"><div class="rc-vehicle">'+escapeHtml(r.vehiculo)+'</div><div class="rc-time">'+formatDate(r.timestamp)+'</div></div>'+
      '<div class="rc-tags"><span class="tag urg-'+r.urgencia+'">'+URG_LABELS[r.urgencia]+'</span><span class="tag tipo">'+TIPO_LABELS[r.tipo]+'</span>'+(ESTADO_TAG[r.estado]||'')+'</div>'+
      '<div class="rc-desc">'+escapeHtml(r.descripcion)+'</div>'+
      '<div class="rc-meta">Chofer: <b>'+escapeHtml(r.nombre)+'</b></div>'+
      (r.fotos && r.fotos.length ? '<div class="rc-photos">'+r.fotos.map(p=>'<img src="'+p+'"/>').join('')+'</div>' : '')+
      '<button class="btn-secondary" data-open="'+r.id+'" style="width:100%;margin-top:6px;">'+(r.estado==='pendiente'?'Abrir parte →':(r.estado==='revision'?'Continuar reparación →':'Ver detalle →'))+'</button>'+
    '</div>'
  ).join('');

  list.querySelectorAll('.rc-photos img').forEach(img=>{
    img.onclick = (e)=>{ e.stopPropagation(); openLightbox(img.src); };
  });
  list.querySelectorAll('[data-open]').forEach(btn=>{
    btn.onclick = ()=>{ selectedReportId = btn.dataset.open; newCommentText=''; renderAverias(content); };
  });
}

function formatDuration(ms){
  if(!ms || ms<0) return '0 min';
  const mins = Math.floor(ms/60000);
  const days = Math.floor(mins/1440);
  const hours = Math.floor((mins%1440)/60);
  const remMins = mins%60;
  let parts = [];
  if(days>0) parts.push(days+' d');
  if(hours>0) parts.push(hours+' h');
  if(remMins>0 || parts.length===0) parts.push(remMins+' min');
  return parts.join(' ');
}

function renderAveriaDetail(content, r){
  const ESTADO_LABEL = {pendiente:'Pendiente', revision:'En reparación', resuelto:'Resuelto'};
  content.innerHTML =
    '<button class="btn-ghost" id="back-to-list" style="margin-bottom:14px;">← Volver a la lista</button>'+
    '<div class="report-card" data-urg="'+r.urgencia+'">'+
      '<div class="rc-top"><div class="rc-vehicle">'+escapeHtml(r.vehiculo)+'</div><div class="rc-time">'+formatDate(r.timestamp)+'</div></div>'+
      '<div class="rc-tags"><span class="tag urg-'+r.urgencia+'">'+URG_LABELS[r.urgencia]+'</span><span class="tag tipo">'+TIPO_LABELS[r.tipo]+'</span></div>'+
      '<div class="rc-desc">'+escapeHtml(r.descripcion)+'</div>'+
      '<div class="rc-meta">Chofer: <b>'+escapeHtml(r.nombre)+'</b> · Estado: <b>'+ESTADO_LABEL[r.estado]+'</b></div>'+
      (r.fotos && r.fotos.length ? '<div class="rc-photos">'+r.fotos.map(p=>'<img src="'+p+'"/>').join('')+'</div>' : '')+
    '</div>'+
    '<div id="averia-workzone"></div>';

  document.getElementById('back-to-list').onclick = ()=>{ selectedReportId = null; renderAverias(content); };
  content.querySelectorAll('.rc-photos img').forEach(img=>{ img.onclick = ()=> openLightbox(img.src); });

  const zone = document.getElementById('averia-workzone');

  if(r.estado === 'pendiente'){
    zone.innerHTML =
      '<div class="form-card">'+
        '<p style="font-size:13px;color:var(--ink-soft);margin-top:0;">Al iniciar, empieza a contar el tiempo de reparación hasta que cierres el parte.</p>'+
        '<button class="submit-btn" id="btn-iniciar">▶ INICIAR REPARACIÓN</button>'+
      '</div>';
    document.getElementById('btn-iniciar').onclick = async ()=>{
      r.estado = 'revision';
      r.inicioReparacion = new Date().toISOString();
      r.comentarios = r.comentarios || [];
      r.costeMaterial = r.costeMaterial || 0;
      await saveReports();
      renderAveriaDetail(content, r);
      showToast('Reparación iniciada');
    };
    return;
  }

  if(r.estado === 'revision'){
    const elapsed = formatDuration(new Date() - new Date(r.inicioReparacion));
    const comentarios = r.comentarios || [];
    zone.innerHTML =
      '<div class="summary-strip">'+
        '<div class="summary-box"><div class="num">'+elapsed+'</div><div class="lbl">Tiempo en reparación</div></div>'+
      '</div>'+
      '<div class="form-card">'+
        '<div class="field"><label>Coste de material (€)</label><input type="number" id="coste-material" step="0.01" value="'+(r.costeMaterial||0)+'"/></div>'+
        '<div class="field"><label>Añadir comentario (pieza cambiada, qué se hace…)</label>'+
          '<textarea id="nuevo-comentario" placeholder="Ej. Cambiado retén de rueda delantera izquierda…">'+newCommentText+'</textarea>'+
        '</div>'+
        '<button class="btn-secondary" id="add-comment" style="width:100%;">+ Añadir comentario</button>'+
      '</div>'+
      (comentarios.length ?
        '<div class="section-title">HISTORIAL</div>'+
        comentarios.slice().reverse().map(c=>
          '<div class="list-card"><div class="list-card-sub">'+formatDate(c.timestamp)+'</div><div class="rc-desc">'+escapeHtml(c.texto)+'</div></div>'
        ).join('')
        : '')+
      '<button class="submit-btn" id="btn-cerrar" style="background:var(--success);color:#fff;box-shadow:0 6px 16px rgba(46,139,87,0.35);">✔ CERRAR PARTE Y FINALIZAR</button>';

    document.getElementById('coste-material').onchange = async (e)=>{
      r.costeMaterial = Number(e.target.value)||0;
      await saveReports();
    };
    document.getElementById('nuevo-comentario').oninput = (e)=>{ newCommentText = e.target.value; };
    document.getElementById('add-comment').onclick = async ()=>{
      const texto = document.getElementById('nuevo-comentario').value.trim();
      if(!texto){ showToast('⚠ Escribe algo primero'); return; }
      r.comentarios = r.comentarios || [];
      r.comentarios.push({texto, timestamp:new Date().toISOString()});
      newCommentText = '';
      await saveReports();
      renderAveriaDetail(content, r);
      showToast('Comentario añadido');
    };
    document.getElementById('btn-cerrar').onclick = async ()=>{
      const fin = new Date().toISOString();
      r.finReparacion = fin;
      r.duracionMs = new Date(fin) - new Date(r.inicioReparacion);
      r.estado = 'resuelto';
      await saveReports();

      const resumen = (r.comentarios||[]).map(c=>'- '+c.texto).join('\n') || 'Sin comentarios registrados.';
      repairs.unshift({
        id: uid(), vehiculo: r.vehiculo, fecha: fin.slice(0,10),
        coste: r.costeMaterial||0, descripcion: resumen,
        duracionMs: r.duracionMs, origenAveriaId: r.id,
      });
      await saveRepairs();

      selectedReportId = null;
      render();
      showToast('Parte cerrado — reparación registrada');
    };
    return;
  }

  // resuelto
  const comentarios = r.comentarios || [];
  zone.innerHTML =
    '<div class="summary-strip">'+
      '<div class="summary-box"><div class="num">'+formatDuration(r.duracionMs)+'</div><div class="lbl">Duración reparación</div></div>'+
      '<div class="summary-box"><div class="num">'+euros(r.costeMaterial)+'</div><div class="lbl">Coste material</div></div>'+
    '</div>'+
    '<div class="list-card"><div class="list-card-sub">Iniciado: '+formatDate(r.inicioReparacion)+' · Cerrado: '+formatDate(r.finReparacion)+'</div></div>'+
    (comentarios.length ?
      '<div class="section-title">COMENTARIOS</div>'+
      comentarios.map(c=>
        '<div class="list-card"><div class="list-card-sub">'+formatDate(c.timestamp)+'</div><div class="rc-desc">'+escapeHtml(c.texto)+'</div></div>'
      ).join('')
      : '<div class="empty-state"><p>Sin comentarios registrados</p></div>');
}

function openLightbox(src){
  const lb = document.createElement('div');
  lb.className = 'lightbox';
  lb.innerHTML = '<button class="lightbox-close">×</button><img src="'+src+'"/>';
  lb.onclick = (e)=>{ if(e.target===lb || e.target.className==='lightbox-close') lb.remove(); };
  document.body.appendChild(lb);
}

/* ---------------- REPARACIONES ---------------- */

function renderReparaciones(content){
  const total = repairs.reduce((s,r)=>s+(Number(r.coste)||0),0);
  const sorted = repairs.slice().sort((a,b)=> new Date(b.fecha)-new Date(a.fecha));

  content.innerHTML =
    '<div class="summary-strip">'+
      '<div class="summary-box"><div class="num">'+repairs.length+'</div><div class="lbl">Reparaciones</div></div>'+
      '<div class="summary-box"><div class="num">'+euros(total)+'</div><div class="lbl">Gasto total</div></div>'+
    '</div>'+
    '<button class="add-toggle" id="toggle-add-rep">'+(showAddReparacion?'✕ Cancelar':'+ Registrar reparación')+'</button>'+
    '<div id="rep-form-wrap"></div>'+
    '<div id="rep-list"></div>';

  document.getElementById('toggle-add-rep').onclick = ()=>{ showAddReparacion = !showAddReparacion; renderReparaciones(content); };

  if(showAddReparacion){
    const wrap = document.getElementById('rep-form-wrap');
    wrap.innerHTML =
      '<div class="form-card">'+
        '<div class="field"><label>Vehículo / matrícula</label><input type="text" id="rep-vehiculo" placeholder="Ej. 4521-BXK"/></div>'+
        '<div class="form-row">'+
          '<div class="field"><label>Fecha</label><input type="date" id="rep-fecha" value="'+new Date().toISOString().slice(0,10)+'"/></div>'+
          '<div class="field"><label>Coste (€)</label><input type="number" id="rep-coste" placeholder="0.00" step="0.01"/></div>'+
        '</div>'+
        '<div class="field"><label>Descripción de la reparación</label><textarea id="rep-desc" placeholder="Qué se ha reparado…"></textarea></div>'+
        '<button class="submit-btn" id="rep-save">GUARDAR REPARACIÓN</button>'+
      '</div>';
    document.getElementById('rep-save').onclick = async ()=>{
      const vehiculo = document.getElementById('rep-vehiculo').value.trim();
      const fecha = document.getElementById('rep-fecha').value;
      const coste = document.getElementById('rep-coste').value;
      const desc = document.getElementById('rep-desc').value.trim();
      if(!vehiculo || !fecha || !desc){ showToast('⚠ Faltan campos'); return; }
      repairs.unshift({id:uid(), vehiculo, fecha, coste: Number(coste)||0, descripcion:desc});
      await saveRepairs();
      showAddReparacion = false;
      renderReparaciones(content);
      showToast('Reparación registrada');
    };
  }

  const list = document.getElementById('rep-list');
  if(sorted.length===0){
    list.innerHTML = '<div class="empty-state"><p>Todavía no hay reparaciones registradas</p></div>';
    return;
  }
  list.innerHTML = sorted.map(r=>
    '<div class="list-card">'+
      '<div class="list-card-top">'+
        '<div><div class="list-card-title">'+escapeHtml(r.vehiculo)+'</div>'+
        '<div class="list-card-sub">'+formatDateOnly(r.fecha)+(r.duracionMs?' · ⏱ '+formatDuration(r.duracionMs):'')+(r.origenAveriaId?' · 🔗 desde parte de avería':'')+'</div></div>'+
        '<div class="cost-pill">'+euros(r.coste)+'</div>'+
      '</div>'+
      '<div class="rc-desc" style="white-space:pre-line;">'+escapeHtml(r.descripcion)+'</div>'+
    '</div>'
  ).join('');
}

/* ---------------- NEUMATICOS ---------------- */

function renderNeumaticos(content){
  const rotAlerts = countRotationAlerts();
  content.innerHTML =
    '<div class="subnav">'+
      '<div class="subnav-btn '+(neumSubTab==='compras'?'active':'')+'" data-ntab="compras">Compras</div>'+
      '<div class="subnav-btn '+(neumSubTab==='almacen'?'active':'')+'" data-ntab="almacen">Almacén</div>'+
      '<div class="subnav-btn '+(neumSubTab==='vehiculos'?'active':'')+'" data-ntab="vehiculos">Vehículos'+(rotAlerts>0?'<span class="mini-badge">'+rotAlerts+'</span>':'')+'</div>'+
    '</div>'+
    '<div id="neum-body"></div>';

  document.querySelectorAll('.subnav-btn[data-ntab]').forEach(b=>{
    b.onclick = ()=>{ neumSubTab = b.dataset.ntab; renderNeumaticos(content); };
  });

  const body = document.getElementById('neum-body');
  if(neumSubTab==='compras') renderCompras(body);
  else if(neumSubTab==='almacen') renderAlmacen(body);
  else renderVehiculos(body);
}

/* --- Compras / stock inicial --- */

function renderCompras(content){
  const pendientesTotal = tireData.compras.reduce((s,c)=>s + (c.cantidad - c.cantidadDadaDeAlta), 0);
  content.innerHTML =
    '<div class="summary-strip">'+
      '<div class="summary-box"><div class="num">'+tireData.compras.length+'</div><div class="lbl">Pedidos</div></div>'+
      '<div class="summary-box"><div class="num">'+pendientesTotal+'</div><div class="lbl">Und. pendientes</div></div>'+
    '</div>'+
    '<button class="add-toggle" id="toggle-add-compra">'+(showAddCompra?'✕ Cancelar':'+ Nueva compra')+'</button>'+
    '<div id="compra-form-wrap"></div>'+
    '<div id="compra-list"></div>';

  document.getElementById('toggle-add-compra').onclick = ()=>{ showAddCompra = !showAddCompra; renderCompras(content); };

  if(showAddCompra){
    const wrap = document.getElementById('compra-form-wrap');
    const proveedoresOpts = tireData.proveedores.map(p=>'<option value="'+escapeHtml(p)+'">'+escapeHtml(p)+'</option>').join('');
    wrap.innerHTML =
      '<div class="form-card">'+
        '<div class="field"><label>Proveedor</label>'+
          '<select id="compra-proveedor-sel"><option value="">— elegir —</option>'+proveedoresOpts+'<option value="__nuevo__">+ Añadir nuevo proveedor</option></select>'+
        '</div>'+
        '<div class="field" id="nuevo-proveedor-wrap" style="display:none;"><label>Nombre del proveedor</label><input type="text" id="compra-proveedor-nuevo" placeholder="Nombre del proveedor"/></div>'+
        '<div class="form-row">'+
          '<div class="field"><label>Fecha</label><input type="date" id="compra-fecha" value="'+new Date().toISOString().slice(0,10)+'"/></div>'+
          '<div class="field"><label>Cantidad</label><input type="number" id="compra-cantidad" placeholder="Ej. 20"/></div>'+
        '</div>'+
        '<div class="form-row">'+
          '<div class="field"><label>Medida</label><input type="text" id="compra-medida" placeholder="Ej. 315/80 R22.5"/></div>'+
          '<div class="field"><label>Coste / unidad (€)</label><input type="number" id="compra-coste" placeholder="0.00" step="0.01"/></div>'+
        '</div>'+
        '<button class="submit-btn" id="compra-save">GUARDAR COMPRA</button>'+
      '</div>';

    document.getElementById('compra-proveedor-sel').onchange = (e)=>{
      document.getElementById('nuevo-proveedor-wrap').style.display = e.target.value==='__nuevo__' ? 'block' : 'none';
    };
    document.getElementById('compra-save').onclick = async ()=>{
      let proveedor = document.getElementById('compra-proveedor-sel').value;
      if(proveedor==='__nuevo__'){
        proveedor = document.getElementById('compra-proveedor-nuevo').value.trim();
        if(proveedor && !tireData.proveedores.includes(proveedor)) tireData.proveedores.push(proveedor);
      }
      const fecha = document.getElementById('compra-fecha').value;
      const cantidad = parseInt(document.getElementById('compra-cantidad').value);
      const medida = document.getElementById('compra-medida').value.trim();
      const coste = Number(document.getElementById('compra-coste').value)||0;
      if(!proveedor || !fecha || !cantidad || cantidad<=0){ showToast('⚠ Faltan campos'); return; }
      tireData.compras.unshift({id:uid(), proveedor, fecha, cantidad, cantidadDadaDeAlta:0, medida, costeUnidad:coste});
      await saveTireData();
      showAddCompra = false;
      renderCompras(content);
      showToast('Compra registrada');
    };
  }

  const list = document.getElementById('compra-list');
  if(tireData.compras.length===0){
    list.innerHTML = '<div class="empty-state"><p>Todavía no hay compras registradas</p></div>';
    return;
  }
  list.innerHTML = tireData.compras.map(c=>{
    const pendiente = c.cantidad - c.cantidadDadaDeAlta;
    return '<div class="list-card">'+
      '<div class="list-card-top">'+
        '<div><div class="list-card-title">'+escapeHtml(c.proveedor)+'</div>'+
        '<div class="list-card-sub">'+formatDateOnly(c.fecha)+' · '+escapeHtml(c.medida||'sin medida')+' · '+euros(c.costeUnidad)+'/ud</div></div>'+
        '<div class="cost-pill">'+c.cantidad+' ud</div>'+
      '</div>'+
      (pendiente>0 ?
        '<div style="margin-top:10px;display:flex;align-items:center;gap:8px;flex-wrap:wrap;">'+
          '<span class="pend-pill">'+pendiente+' pendientes de recibir</span>'+
          '<input type="number" id="alta-cant-'+c.id+'" value="'+pendiente+'" min="1" max="'+pendiente+'" style="width:70px;padding:8px;font-size:13px;"/>'+
          '<button class="btn-secondary" data-id="'+c.id+'" data-action="alta">Dar de alta en almacén</button>'+
        '</div>'
        : '<div style="margin-top:8px;"><span class="tag" style="background:var(--success-bg);color:var(--success);">Todo recibido</span></div>'
      )+
    '</div>';
  }).join('');

  list.querySelectorAll('[data-action="alta"]').forEach(btn=>{
    btn.onclick = async ()=>{
      const compra = tireData.compras.find(x=>x.id===btn.dataset.id);
      const input = document.getElementById('alta-cant-'+btn.dataset.id);
      let n = parseInt(input.value);
      const pendiente = compra.cantidad - compra.cantidadDadaDeAlta;
      if(!n || n<=0) return;
      if(n>pendiente) n = pendiente;
      for(let i=0;i<n;i++){
        tireData.stock.push({
          id: uid(), proveedor: compra.proveedor, medida: compra.medida, compraId: compra.id,
          fecha: new Date().toISOString().slice(0,10), estado:'almacen',
          montadaEnLlanta:false, tipoLlanta:null,
          vehiculoId:null, posicionKey:null, posicionLabel:null, kmInstalacion:null, fechaMontaje:null,
        });
      }
      compra.cantidadDadaDeAlta += n;
      await saveTireData();
      renderCompras(content);
      showToast(n+' neumático(s) dado(s) de alta en almacén');
    };
  });
}

/* --- Almacén --- */

function renderAlmacen(content){
  const enAlmacen = tireData.stock.filter(t=>t.estado==='almacen');
  content.innerHTML =
    '<div class="summary-strip">'+
      '<div class="summary-box"><div class="num">'+enAlmacen.length+'</div><div class="lbl">En almacén</div></div>'+
      '<div class="summary-box"><div class="num">'+tireData.stock.filter(t=>t.estado==='montado').length+'</div><div class="lbl">Montados</div></div>'+
    '</div>'+
    '<div id="almacen-list"></div>';

  const list = document.getElementById('almacen-list');
  if(enAlmacen.length===0){
    list.innerHTML = '<div class="empty-state"><p>No hay neumáticos en almacén ahora mismo</p></div>';
    return;
  }
  list.innerHTML = enAlmacen.map(t=>
    '<div class="list-card">'+
      '<div class="list-card-top">'+
        '<div><div class="list-card-title">'+escapeHtml(t.medida||'Sin medida')+'</div>'+
        '<div class="list-card-sub">'+escapeHtml(t.proveedor)+' · recibido '+formatDateOnly(t.fecha)+'</div></div>'+
      '</div>'+
      '<div class="toggle-row"><input type="checkbox" id="mont-'+t.id+'" '+(t.montadaEnLlanta?'checked':'')+'/><label for="mont-'+t.id+'">Ya está montada en una llanta</label></div>'+
      '<div class="field" style="margin-bottom:10px;"><input type="text" id="llanta-'+t.id+'" placeholder="Tipo de llanta (ej. acero, aluminio)" value="'+(t.tipoLlanta||'')+'"/></div>'+
      '<button class="btn-secondary" data-id="'+t.id+'" data-action="montar-vehiculo">Montar en vehículo →</button>'+
    '</div>'
  ).join('');

  enAlmacen.forEach(t=>{
    document.getElementById('mont-'+t.id).onchange = async (e)=>{ t.montadaEnLlanta = e.target.checked; await saveTireData(); };
    document.getElementById('llanta-'+t.id).oninput = async (e)=>{ t.tipoLlanta = e.target.value; await saveTireData(); };
  });
  list.querySelectorAll('[data-action="montar-vehiculo"]').forEach(btn=>{
    btn.onclick = ()=>{
      mountingTireId = btn.dataset.id;
      neumSubTab = 'vehiculos';
      render();
      showToast('Elige la posición en el diagrama del vehículo');
    };
  });
}

/* --- Vehiculos + diagrama de ejes --- */

function buildPositions(vehiculo){
  const pos = [];
  if(vehiculo.tipo==='camion'){
    pos.push({key:'dir-izq', label:'Dirección Izq', group:'Dirección'});
    pos.push({key:'dir-der', label:'Dirección Der', group:'Dirección'});
    const nTrac = vehiculo.ejesTraccion || 1;
    for(let e=1;e<=nTrac;e++){
      ['izq-ext','izq-int','der-int','der-ext'].forEach(side=>{
        pos.push({key:'trac'+e+'-'+side, label:'Tracción '+e+' '+side.replace('-',' '), group:'Tracción '+e});
      });
    }
  } else {
    const nEjes = vehiculo.ejesCisterna || 2;
    for(let e=1;e<=nEjes;e++){
      ['izq-ext','izq-int','der-int','der-ext'].forEach(side=>{
        pos.push({key:'eje'+e+'-'+side, label:'Eje '+e+' '+side.replace('-',' '), group:'Eje '+e});
      });
    }
  }
  return pos;
}

function tireKmRodados(tire, vehiculo){
  if(!vehiculo || tire.kmInstalacion==null) return 0;
  return Math.max(0, (vehiculo.km||0) - tire.kmInstalacion);
}
function countRotationAlerts(){
  let n = 0;
  tireData.stock.filter(t=>t.estado==='montado').forEach(t=>{
    const v = tireData.vehiculos.find(x=>x.id===t.vehiculoId);
    if(v && tireKmRodados(t,v) >= tireData.rotationThreshold) n++;
  });
  return n;
}

function renderVehiculos(content){
  content.innerHTML =
    '<div class="field" style="margin-bottom:14px;"><label>Avisar de girar neumáticos cada (km)</label>'+
      '<input type="number" id="rot-threshold" value="'+tireData.rotationThreshold+'"/></div>'+
    (mountingTireId ? '<div class="mount-banner" id="mount-banner"><span>🛞 Neumático seleccionado — toca una posición vacía en el diagrama para montarlo</span><button id="cancel-mount">Cancelar</button></div>' : '')+
    '<button class="add-toggle" id="toggle-add-veh">'+(showAddVehiculo?'✕ Cancelar':'+ Nuevo vehículo')+'</button>'+
    '<div id="veh-form-wrap"></div>'+
    '<div id="veh-list"></div>'+
    '<div id="veh-detail"></div>';

  document.getElementById('rot-threshold').onchange = async (e)=>{
    tireData.rotationThreshold = parseInt(e.target.value)||10000;
    await saveTireData();
    render();
  };

  if(mountingTireId){
    document.getElementById('cancel-mount').onclick = ()=>{ mountingTireId = null; render(); };
  }

  document.getElementById('toggle-add-veh').onclick = ()=>{ showAddVehiculo = !showAddVehiculo; renderVehiculos(content); };

  if(showAddVehiculo){
    const wrap = document.getElementById('veh-form-wrap');
    wrap.innerHTML =
      '<div class="form-card">'+
        '<div class="field"><label>Matrícula</label><input type="text" id="veh-matricula" placeholder="Ej. 4521-BXK"/></div>'+
        '<div class="field"><label>Tipo</label>'+
          '<div class="chip-row"><div class="chip selected" data-tipo="camion" id="chip-camion">🚛 Camión</div><div class="chip" data-tipo="cisterna" id="chip-cisterna">🛢️ Cisterna</div></div>'+
        '</div>'+
        '<div class="field" id="ejes-camion-wrap"><label>Ejes de tracción</label>'+
          '<select id="veh-ejes-trac"><option value="1">1 eje</option><option value="2">2 ejes</option></select></div>'+
        '<div class="field" id="ejes-cisterna-wrap" style="display:none;"><label>Nº de ejes de la cisterna</label>'+
          '<select id="veh-ejes-cist"><option value="2">2 ejes</option><option value="3">3 ejes</option><option value="4">4 ejes</option></select></div>'+
        '<div class="field"><label>Km actuales</label><input type="number" id="veh-km" placeholder="Ej. 185000"/></div>'+
        '<button class="submit-btn" id="veh-save">GUARDAR VEHÍCULO</button>'+
      '</div>';

    let tipoSel = 'camion';
    document.getElementById('chip-camion').onclick = ()=>{
      tipoSel='camion';
      document.getElementById('chip-camion').classList.add('selected');
      document.getElementById('chip-cisterna').classList.remove('selected');
      document.getElementById('ejes-camion-wrap').style.display='block';
      document.getElementById('ejes-cisterna-wrap').style.display='none';
    };
    document.getElementById('chip-cisterna').onclick = ()=>{
      tipoSel='cisterna';
      document.getElementById('chip-cisterna').classList.add('selected');
      document.getElementById('chip-camion').classList.remove('selected');
      document.getElementById('ejes-cisterna-wrap').style.display='block';
      document.getElementById('ejes-camion-wrap').style.display='none';
    };

    document.getElementById('veh-save').onclick = async ()=>{
      const matricula = document.getElementById('veh-matricula').value.trim();
      const km = parseInt(document.getElementById('veh-km').value)||0;
      if(!matricula){ showToast('⚠ Falta la matrícula'); return; }
      const vehiculo = {
        id: uid(), matricula, tipo: tipoSel, km,
        ejesTraccion: parseInt(document.getElementById('veh-ejes-trac').value)||1,
        ejesCisterna: parseInt(document.getElementById('veh-ejes-cist').value)||2,
        kmHistory: [{fecha: new Date().toISOString().slice(0,10), km}],
      };
      tireData.vehiculos.push(vehiculo);
      await saveTireData();
      showAddVehiculo = false;
      selectedVehiculoId = vehiculo.id;
      renderVehiculos(content);
      showToast('Vehículo añadido');
    };
  }

  const vehList = document.getElementById('veh-list');
  if(tireData.vehiculos.length===0){
    vehList.innerHTML = '<div class="empty-state"><p>Añade tu primer camión o cisterna</p></div>';
  } else {
    vehList.innerHTML = tireData.vehiculos.map(v=>{
      const positions = buildPositions(v);
      const mounted = tireData.stock.filter(t=>t.estado==='montado' && t.vehiculoId===v.id);
      const alerts = mounted.filter(t=>tireKmRodados(t,v) >= tireData.rotationThreshold).length;
      return '<div class="vehicle-card '+(selectedVehiculoId===v.id?'selected':'')+'" data-id="'+v.id+'">'+
        '<div><div class="vc-plate">'+escapeHtml(v.matricula)+'</div><div class="vc-meta">'+(v.tipo==='camion'?'Camión':'Cisterna')+' · '+(v.km||0).toLocaleString('es-ES')+' km · '+mounted.length+'/'+positions.length+' ruedas</div></div>'+
        (alerts>0 ? '<span class="vc-alert">'+alerts+' a girar</span>' : '')+
      '</div>';
    }).join('');
    vehList.querySelectorAll('.vehicle-card').forEach(card=>{
      card.onclick = ()=>{ selectedVehiculoId = card.dataset.id; activeSlotKey = null; renderVehiculos(content); };
    });
  }

  const detail = document.getElementById('veh-detail');
  const vehiculo = tireData.vehiculos.find(v=>v.id===selectedVehiculoId);
  if(!vehiculo){ detail.innerHTML=''; return; }
  renderVehicleDetail(detail, vehiculo);
}

function renderVehicleDetail(detail, vehiculo){
  const positions = buildPositions(vehiculo);
  const groups = [...new Set(positions.map(p=>p.group))];

  let diagramHtml = '<div class="axle-diagram">';
  groups.forEach(g=>{
    const groupPos = positions.filter(p=>p.group===g);
    diagramHtml += '<div class="axle-row"><div class="axle-label">'+g+'</div><div class="axle-bar"><div class="wheel-group">';
    groupPos.forEach(p=>{
      const tire = tireData.stock.find(t=>t.estado==='montado' && t.vehiculoId===vehiculo.id && t.posicionKey===p.key);
      let cls = 'wheel-slot';
      if(tire){
        cls += ' filled';
        if(tireKmRodados(tire,vehiculo) >= tireData.rotationThreshold) cls += ' alert';
      }
      if(activeSlotKey===p.key) cls += ' picking';
      diagramHtml += '<div class="'+cls+'" data-pos="'+p.key+'" title="'+p.label+'">'+(tire ? '🛞' : '+')+'</div>';
    });
    diagramHtml += '</div></div></div>';
  });
  diagramHtml += '</div>';

  detail.innerHTML =
    '<div class="km-row">'+
      '<div class="field"><label>Actualizar km de '+escapeHtml(vehiculo.matricula)+'</label><input type="number" id="veh-km-update" value="'+(vehiculo.km||0)+'"/></div>'+
      '<button class="btn-secondary" id="veh-km-save">Guardar km</button>'+
    '</div>'+
    diagramHtml+
    '<div id="slot-panel-wrap"></div>';

  document.getElementById('veh-km-save').onclick = async ()=>{
    const nuevoKm = parseInt(document.getElementById('veh-km-update').value)||0;
    vehiculo.km = nuevoKm;
    vehiculo.kmHistory = vehiculo.kmHistory || [];
    vehiculo.kmHistory.push({fecha:new Date().toISOString().slice(0,10), km:nuevoKm});
    await saveTireData();
    renderVehicleDetail(detail, vehiculo);
    showToast('Km actualizados');
  };

  detail.querySelectorAll('.wheel-slot').forEach(slot=>{
    slot.onclick = ()=>{
      activeSlotKey = activeSlotKey === slot.dataset.pos ? null : slot.dataset.pos;
      renderSlotPanel(detail, vehiculo, positions);
    };
  });

  renderSlotPanel(detail, vehiculo, positions);
}

function renderSlotPanel(detail, vehiculo, positions){
  const wrap = document.getElementById('slot-panel-wrap');
  if(!activeSlotKey){ wrap.innerHTML=''; return; }
  const posInfo = positions.find(p=>p.key===activeSlotKey);
  const tire = tireData.stock.find(t=>t.estado==='montado' && t.vehiculoId===vehiculo.id && t.posicionKey===activeSlotKey);

  if(tire){
    const km = tireKmRodados(tire, vehiculo);
    const alert = km >= tireData.rotationThreshold;
    wrap.innerHTML =
      '<div class="slot-panel filled-panel">'+
        '<div class="sp-title">'+posInfo.label+'</div>'+
        '<div style="font-size:12.5px;color:var(--ink-soft);line-height:1.7;">'+
          'Proveedor: <b style="color:var(--ink);">'+escapeHtml(tire.proveedor)+'</b><br/>'+
          'Medida: <b style="color:var(--ink);">'+escapeHtml(tire.medida||'-')+'</b><br/>'+
          'Llanta: <b style="color:var(--ink);">'+escapeHtml(tire.tipoLlanta||'-')+'</b><br/>'+
          'Montado: <b style="color:var(--ink);">'+formatDateOnly(tire.fechaMontaje)+'</b><br/>'+
          'Km rodados: <b style="color:'+(alert?'var(--urgent)':'var(--ink)')+';">'+km.toLocaleString('es-ES')+' km'+(alert?' — ¡TOCA GIRAR!':'')+'</b>'+
        '</div>'+
        '<button class="btn-danger-ghost" id="desmontar-btn" style="margin-top:10px;">Desmontar</button>'+
      '</div>';
    document.getElementById('desmontar-btn').onclick = async ()=>{
      tire.estado='almacen'; tire.vehiculoId=null; tire.posicionKey=null; tire.posicionLabel=null;
      tire.kmInstalacion=null; tire.fechaMontaje=null;
      await saveTireData();
      activeSlotKey = null;
      render();
      showToast('Neumático desmontado, ahora está en almacén');
    };
  } else {
    let candidatos = tireData.stock.filter(t=>t.estado==='almacen');
    if(mountingTireId) candidatos = candidatos.filter(t=>t.id===mountingTireId);
    wrap.innerHTML =
      '<div class="slot-panel">'+
        '<div class="sp-title">'+posInfo.label+' — elige neumático</div>'+
        (candidatos.length===0 ? '<div style="font-size:12.5px;color:var(--ink-soft);">No hay neumáticos disponibles en almacén</div>' :
          candidatos.map(t=>'<div class="pick-tire" data-id="'+t.id+'"><div><b>'+escapeHtml(t.medida||'Sin medida')+'</b><br/><span>'+escapeHtml(t.proveedor)+'</span></div><span>Montar →</span></div>').join('')
        )+
      '</div>';
    wrap.querySelectorAll('.pick-tire').forEach(el=>{
      el.onclick = async ()=>{
        const t = tireData.stock.find(x=>x.id===el.dataset.id);
        t.estado='montado'; t.vehiculoId=vehiculo.id; t.posicionKey=activeSlotKey; t.posicionLabel=posInfo.label;
        t.kmInstalacion = vehiculo.km||0; t.fechaMontaje = new Date().toISOString().slice(0,10);
        await saveTireData();
        mountingTireId = null;
        activeSlotKey = null;
        render();
        showToast('Neumático montado en '+posInfo.label);
      };
    });
  }
}

loadAll();
</script>
</body>
</html>
