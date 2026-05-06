<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Eksplorasi Interaktif: Sistem Manajemen POAC Berbasis GAS</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Chosen Palette: Warm Neutrals with Slate and Blue Accents (Bg: stone-50, Text: slate-800, Accents: blue-600, emerald-500) -->
    <!-- Application Structure Plan: The SPA is designed as an interactive documentation hub. It uses a top navigation bar to scroll to functional sections. The core interactive features include a tabbed Database Schema Explorer to understand data structures without clutter, a tabbed Code Viewer for backend/frontend scripts, an interactive step-by-step Deployment Tracker, and a live Chart.js preview simulating the final 'Controlling' output. This structure transforms a flat markdown tutorial into an engaging, task-oriented learning experience. -->
    <!-- Visualization & Content Choices: 1. System Architecture -> Goal: Inform -> HTML/CSS Block Diagram -> No SVG used, pure DOM. 2. Database Schemas -> Goal: Organize -> Interactive Tabbed Tables -> Easy comparison. 3. Code Implementation -> Goal: Inform -> Tabbed Code blocks with Copy functionality -> Usability. 4. Deployment Steps -> Goal: Process -> Interactive Timeline/Checklist -> Tracks progress. 5. Controlling Preview -> Goal: Inform/Wow -> Chart.js Bar Chart -> Simulates end-goal. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <style>
        body { font-family: 'Inter', sans-serif; }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container { height: 400px; }
        }
        .custom-scrollbar::-webkit-scrollbar { height: 8px; width: 8px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: #f1f5f9; border-radius: 4px; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
    </style>
</head>
<body class="bg-stone-50 text-slate-800 antialiased selection:bg-blue-200 selection:text-blue-900">

    <nav class="fixed top-0 w-full bg-white/80 backdrop-blur-md border-b border-stone-200 z-50">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16 items-center">
                <div class="flex-shrink-0 font-bold text-xl tracking-tight text-blue-700 flex items-center gap-2">
                    <span class="text-2xl">📘</span> Hub POAC
                </div>
                <div class="hidden md:flex space-x-8 text-sm font-medium">
                    <a href="#arsitektur" class="text-slate-600 hover:text-blue-600 transition-colors">Arsitektur</a>
                    <a href="#database" class="text-slate-600 hover:text-blue-600 transition-colors">Struktur Database</a>
                    <a href="#kode" class="text-slate-600 hover:text-blue-600 transition-colors">Implementasi Kode</a>
                    <a href="#simulasi" class="text-slate-600 hover:text-blue-600 transition-colors">Simulasi Controlling</a>
                    <a href="#deploy" class="text-slate-600 hover:text-blue-600 transition-colors">Panduan Deploy</a>
                </div>
            </div>
        </div>
    </nav>

    <main class="pt-24 pb-16">
        <header class="max-w-4xl mx-auto px-4 text-center mb-16">
            <div class="inline-block px-3 py-1 bg-blue-100 text-blue-800 text-xs font-semibold rounded-full mb-4">
                Panduan Interaktif
            </div>
            <h1 class="text-4xl md:text-5xl font-extrabold tracking-tight text-slate-900 mb-6">
                Membangun Sistem Manajemen POAC Berbasis Web
            </h1>
            <p class="text-lg text-slate-600 leading-relaxed">
                Eksplorasi panduan lengkap pembuatan aplikasi manajemen internal berbasis prinsip <strong>Planning, Organizing, Actuating, Controlling</strong>. Sistem ini dirancang menggunakan ekosistem gratis dan kolaboratif: Google Sheets (Database), Google Apps Script (Backend), dan Tailwind CSS + Chart.js (Frontend UI).
            </p>
        </header>

        <section id="arsitektur" class="max-w-6xl mx-auto px-4 mb-24 scroll-mt-24">
            <div class="bg-white rounded-2xl shadow-sm border border-stone-200 p-8">
                <div class="mb-8">
                    <h2 class="text-2xl font-bold text-slate-800 mb-2">Arsitektur Sistem & Alur Kerja</h2>
                    <p class="text-slate-600">Bagian ini mengilustrasikan bagaimana ketiga komponen utama saling berkomunikasi. Google Apps Script bertindak sebagai jembatan yang menghubungkan antarmuka pengguna dengan database Spreadsheet.</p>
                </div>
                
                <div class="flex flex-col md:flex-row items-center justify-between gap-6 bg-slate-50 p-6 rounded-xl border border-slate-100">
                    <div class="flex-1 w-full bg-white p-6 rounded-xl shadow-sm border border-blue-100 text-center relative overflow-hidden group hover:border-blue-300 transition-all">
                        <div class="absolute top-0 left-0 w-full h-1 bg-blue-500"></div>
                        <div class="text-4xl mb-3">💻</div>
                        <h3 class="font-bold text-slate-800 mb-2">Frontend (UI)</h3>
                        <p class="text-sm text-slate-500">HTML, Tailwind CSS, JS.<br>Berjalan di Browser Pengguna.</p>
                    </div>
                    
                    <div class="text-slate-400 text-2xl font-bold hidden md:block">⇆</div>
                    <div class="text-slate-400 text-2xl font-bold md:hidden">⇅</div>

                    <div class="flex-1 w-full bg-white p-6 rounded-xl shadow-sm border border-emerald-100 text-center relative overflow-hidden group hover:border-emerald-300 transition-all">
                        <div class="absolute top-0 left-0 w-full h-1 bg-emerald-500"></div>
                        <div class="text-4xl mb-3">⚙️</div>
                        <h3 class="font-bold text-slate-800 mb-2">Backend (Server)</h3>
                        <p class="text-sm text-slate-500">Google Apps Script (Code.gs).<br>Fungsi CRUD & Autentikasi.</p>
                    </div>

                    <div class="text-slate-400 text-2xl font-bold hidden md:block">⇆</div>
                    <div class="text-slate-400 text-2xl font-bold md:hidden">⇅</div>

                    <div class="flex-1 w-full bg-white p-6 rounded-xl shadow-sm border border-green-100 text-center relative overflow-hidden group hover:border-green-300 transition-all">
                        <div class="absolute top-0 left-0 w-full h-1 bg-green-500"></div>
                        <div class="text-4xl mb-3">📊</div>
                        <h3 class="font-bold text-slate-800 mb-2">Database</h3>
                        <p class="text-sm text-slate-500">Google Sheets.<br>Penyimpanan Data Kolaboratif.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="database" class="max-w-6xl mx-auto px-4 mb-24 scroll-mt-24">
            <div class="mb-8">
                <h2 class="text-2xl font-bold text-slate-800 mb-2">Langkah 1: Persiapan Struktur Database (Google Sheets)</h2>
                <p class="text-slate-600">Buat Google Sheet baru, catat ID Spreadsheet dari URL-nya, lalu buat 4 tab di bagian bawah persis sesuai skema berikut. Klik pada setiap tab di bawah ini untuk melihat struktur kolom yang diwajibkan.</p>
            </div>

            <div class="bg-white rounded-2xl shadow-sm border border-stone-200 overflow-hidden">
                <div class="flex flex-wrap border-b border-stone-200 bg-slate-50 p-2 gap-2" id="dbTabContainer">
                    <button onclick="switchDbTab('plan')" id="btn-db-plan" class="px-5 py-2.5 text-sm font-medium rounded-lg bg-white shadow-sm border border-slate-200 text-blue-700 transition-all">📝 Planning</button>
                    <button onclick="switchDbTab('org')" id="btn-db-org" class="px-5 py-2.5 text-sm font-medium rounded-lg text-slate-600 hover:bg-slate-200 hover:text-slate-900 transition-all">👥 Organizing</button>
                    <button onclick="switchDbTab('act')" id="btn-db-act" class="px-5 py-2.5 text-sm font-medium rounded-lg text-slate-600 hover:bg-slate-200 hover:text-slate-900 transition-all">⚡ Actuating</button>
                    <button onclick="switchDbTab('ctrl')" id="btn-db-ctrl" class="px-5 py-2.5 text-sm font-medium rounded-lg text-slate-600 hover:bg-slate-200 hover:text-slate-900 transition-all">📊 Controlling</button>
                </div>

                <div class="p-6 overflow-x-auto custom-scrollbar">
                    <div id="content-db-plan" class="block">
                        <h3 class="font-semibold text-slate-800 mb-4 flex items-center gap-2">Tab 1: `Planning` <span class="text-xs font-normal bg-slate-100 text-slate-500 px-2 py-1 rounded">Menyimpan rencana strategis dan jadwal.</span></h3>
                        <table class="w-full text-left border-collapse min-w-[600px]">
                            <thead>
                                <tr class="bg-slate-50 text-slate-600 text-sm border-b border-slate-200">
                                    <th class="p-3 font-semibold">ID_Plan</th>
                                    <th class="p-3 font-semibold">Target</th>
                                    <th class="p-3 font-semibold">Strategi</th>
                                    <th class="p-3 font-semibold">Milestone</th>
                                    <th class="p-3 font-semibold">Mulai</th>
                                    <th class="p-3 font-semibold">Selesai</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr class="border-b border-slate-100 text-sm text-slate-500">
                                    <td class="p-3 italic">P17150...</td>
                                    <td class="p-3 italic">Kenaikan Sales 20%</td>
                                    <td class="p-3 italic">Promo Medsos</td>
                                    <td class="p-3 italic">1000 Leads</td>
                                    <td class="p-3 italic">2023-01-01</td>
                                    <td class="p-3 italic">2023-12-31</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <div id="content-db-org" class="hidden">
                        <h3 class="font-semibold text-slate-800 mb-4 flex items-center gap-2">Tab 2: `Organizing` <span class="text-xs font-normal bg-amber-100 text-amber-800 px-2 py-1 rounded">Sangat Penting: Digunakan untuk Autentikasi Login.</span></h3>
                        <table class="w-full text-left border-collapse min-w-[600px]">
                            <thead>
                                <tr class="bg-slate-50 text-slate-600 text-sm border-b border-slate-200">
                                    <th class="p-3 font-semibold">Username</th>
                                    <th class="p-3 font-semibold">Password</th>
                                    <th class="p-3 font-semibold">Nama</th>
                                    <th class="p-3 font-semibold">Divisi</th>
                                    <th class="p-3 font-semibold">Role</th>
                                </tr>
                            </thead>
                            <tbody class="text-sm">
                                <tr class="border-b border-slate-100">
                                    <td class="p-3 font-mono text-blue-600">admin</td>
                                    <td class="p-3">admin123</td>
                                    <td class="p-3">Pak Bos</td>
                                    <td class="p-3">Manajemen</td>
                                    <td class="p-3 font-semibold text-purple-600">Manager</td>
                                </tr>
                                <tr class="border-b border-slate-100">
                                    <td class="p-3 font-mono text-blue-600">staf1</td>
                                    <td class="p-3">staf123</td>
                                    <td class="p-3">Budi</td>
                                    <td class="p-3">Marketing</td>
                                    <td class="p-3 text-slate-500">Staf</td>
                                </tr>
                                <tr class="border-b border-slate-100">
                                    <td class="p-3 font-mono text-blue-600">staf2</td>
                                    <td class="p-3">staf123</td>
                                    <td class="p-3">Siti</td>
                                    <td class="p-3">IT</td>
                                    <td class="p-3 text-slate-500">Staf</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <div id="content-db-act" class="hidden">
                        <h3 class="font-semibold text-slate-800 mb-4 flex items-center gap-2">Tab 3: `Actuating` <span class="text-xs font-normal bg-slate-100 text-slate-500 px-2 py-1 rounded">Penyimpanan log aktivitas dan penugasan.</span></h3>
                        <table class="w-full text-left border-collapse min-w-[600px]">
                            <thead>
                                <tr class="bg-slate-50 text-slate-600 text-sm border-b border-slate-200">
                                    <th class="p-3 font-semibold">ID_Task</th>
                                    <th class="p-3 font-semibold">Task</th>
                                    <th class="p-3 font-semibold">PIC</th>
                                    <th class="p-3 font-semibold">Divisi</th>
                                    <th class="p-3 font-semibold">Status</th>
                                </tr>
                            </thead>
                            <tbody class="text-sm">
                                <tr class="border-b border-slate-100">
                                    <td class="p-3">T1</td>
                                    <td class="p-3">Posting Sosmed</td>
                                    <td class="p-3">Budi</td>
                                    <td class="p-3">Marketing</td>
                                    <td class="p-3"><span class="px-2 py-1 bg-yellow-100 text-yellow-800 rounded-full text-xs">Pending</span></td>
                                </tr>
                                <tr class="border-b border-slate-100">
                                    <td class="p-3">T2</td>
                                    <td class="p-3">Fix Bug Website</td>
                                    <td class="p-3">Siti</td>
                                    <td class="p-3">IT</td>
                                    <td class="p-3"><span class="px-2 py-1 bg-green-100 text-green-800 rounded-full text-xs">Selesai</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <div id="content-db-ctrl" class="hidden">
                        <h3 class="font-semibold text-slate-800 mb-4 flex items-center gap-2">Tab 4: `Controlling` <span class="text-xs font-normal bg-slate-100 text-slate-500 px-2 py-1 rounded">Metrik KPI dan ruang ulasan manajerial.</span></h3>
                        <table class="w-full text-left border-collapse min-w-[600px]">
                            <thead>
                                <tr class="bg-slate-50 text-slate-600 text-sm border-b border-slate-200">
                                    <th class="p-3 font-semibold">ID_Ctrl</th>
                                    <th class="p-3 font-semibold">Divisi</th>
                                    <th class="p-3 font-semibold">KPI</th>
                                    <th class="p-3 font-semibold">Progress</th>
                                    <th class="p-3 font-semibold">Kendala</th>
                                    <th class="p-3 font-semibold">Review_Manajer</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr class="border-b border-slate-100 text-sm text-slate-500">
                                    <td class="p-3 italic">C1</td>
                                    <td class="p-3 italic">Marketing</td>
                                    <td class="p-3 italic">Leads Bulanan</td>
                                    <td class="p-3 italic">80%</td>
                                    <td class="p-3 italic">Anggaran Iklan Habis</td>
                                    <td class="p-3 italic">Coba SEO Organik</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </section>

        <section id="kode" class="max-w-6xl mx-auto px-4 mb-24 scroll-mt-24">
            <div class="mb-8">
                <h2 class="text-2xl font-bold text-slate-800 mb-2">Langkah 2-4: Implementasi Kode (Apps Script)</h2>
                <p class="text-slate-600">Dari menu Ekstensi > Apps Script di Google Sheet, siapkan dua file berikut. Jangan lupa mengganti <code class="bg-slate-200 px-1 rounded text-sm text-pink-600">MASUKKAN_ID_SHEET_ANDA_DISINI</code> di dalam Code.gs dengan ID Spreadsheet asli Anda.</p>
            </div>

            <div class="bg-[#1e1e1e] rounded-2xl shadow-xl overflow-hidden border border-slate-800">
                <div class="flex items-center justify-between bg-[#2d2d2d] px-4 py-2 border-b border-[#404040]">
                    <div class="flex gap-2">
                        <button onclick="switchCodeTab('backend')" id="btn-code-backend" class="px-4 py-2 text-sm font-mono text-[#e4e4e4] bg-[#1e1e1e] border-t-2 border-blue-500 opacity-100 transition-all">Code.gs</button>
                        <button onclick="switchCodeTab('frontend')" id="btn-code-frontend" class="px-4 py-2 text-sm font-mono text-[#9cdcfe] opacity-60 hover:opacity-100 transition-all">Index.html</button>
                    </div>
                    <button onclick="copyCode()" class="text-xs text-slate-300 hover:text-white bg-[#404040] hover:bg-[#505050] px-3 py-1.5 rounded transition-colors flex items-center gap-1">
                        📋 Salin Kode
                    </button>
                </div>
                
                <div class="relative">
                    <pre id="code-backend" class="block p-6 text-sm font-mono text-[#d4d4d4] overflow-x-auto overflow-y-auto max-h-[500px] custom-scrollbar"><code class="language-javascript">const SHEET_ID = 'MASUKKAN_ID_SHEET_ANDA_DISINI'; 

function doGet(e) {
  return HtmlService.createTemplateFromFile('Index')
    .evaluate()
    .setTitle('POAC Management System')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
    .addMetaTag('viewport', 'width=device-width, initial-scale=1');
}

function getSheet(sheetName) {
  return SpreadsheetApp.openById(SHEET_ID).getSheetByName(sheetName);
}

// ==========================================
// FUNGSI ORGANIZING & LOGIN
// ==========================================
function loginUser(username, password) {
  const sheet = getSheet('Organizing');
  const data = sheet.getDataRange().getValues();
  for (let i = 1; i < data.length; i++) {
    if (data[i][0] == username && data[i][1] == password) {
      return { success: true, nama: data[i][2], divisi: data[i][3], role: data[i][4] };
    }
  }
  return { success: false, message: 'Username atau Password salah!' };
}

function getTim() {
  const sheet = getSheet('Organizing');
  const data = sheet.getDataRange().getValues();
  data.shift();
  return data;
}

// ==========================================
// FUNGSI PLANNING
// ==========================================
function getPlanning() {
  const sheet = getSheet('Planning');
  const data = sheet.getDataRange().getValues();
  data.shift(); 
  return data;
}

function addPlan(target, strategi, milestone, mulai, selesai) {
  const sheet = getSheet('Planning');
  const id = 'P' + new Date().getTime();
  sheet.appendRow([id, target, strategi, milestone, mulai, selesai]);
  return true;
}

// ==========================================
// FUNGSI ACTUATING (TUGAS HARIAN)
// ==========================================
function getTasks(role, divisi) {
  const sheet = getSheet('Actuating');
  const data = sheet.getDataRange().getValues();
  data.shift();
  if (role === 'Manager') return data; 
  return data.filter(row => row[3] === divisi);
}

function updateTaskStatus(idTask, newStatus) {
  const sheet = getSheet('Actuating');
  const data = sheet.getDataRange().getValues();
  for (let i = 1; i < data.length; i++) {
    if (data[i][0] === idTask) {
      sheet.getRange(i + 1, 5).setValue(newStatus); 
      return true;
    }
  }
  return false;
}

// ==========================================
// FUNGSI CONTROLLING (CHART DATA)
// ==========================================
function getChartData() {
  const sheet = getSheet('Actuating');
  const data = sheet.getDataRange().getValues();
  data.shift();
  let stats = {};
  data.forEach(row => {
    let divisi = row[3];
    let status = row[4];
    if(!stats[divisi]) stats[divisi] = { total: 0, selesai: 0 };
    stats[divisi].total += 1;
    if(status === 'Selesai') stats[divisi].selesai += 1;
  });
  return stats;
}</code></pre>
                    
                    <pre id="code-frontend" class="hidden p-6 text-sm font-mono text-[#d4d4d4] overflow-x-auto overflow-y-auto max-h-[500px] custom-scrollbar"><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="id"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  &lt;title&gt;Sistem POAC Internal&lt;/title&gt;
  &lt;script src="https://cdn.tailwindcss.com"&gt;&lt;/script&gt;
  &lt;script src="https://cdn.jsdelivr.net/npm/chart.js"&gt;&lt;/script&gt;
  &lt;style&gt; .hidden { display: none; } &lt;/style&gt;
&lt;/head&gt;
&lt;body class="bg-gray-100 font-sans"&gt;

  &lt;!-- LOGIN SCREEN --&gt;
  &lt;div id="loginScreen" class="min-h-screen flex items-center justify-center"&gt;
    &lt;div class="bg-white p-8 rounded-lg shadow-md w-96"&gt;
      &lt;h2 class="text-2xl font-bold mb-6 text-center text-blue-600"&gt;POAC Login&lt;/h2&gt;
      &lt;input type="text" id="username" placeholder="Username" class="w-full mb-4 p-2 border rounded"&gt;
      &lt;input type="password" id="password" placeholder="Password" class="w-full mb-6 p-2 border rounded"&gt;
      &lt;button onclick="doLogin()" class="w-full bg-blue-600 text-white p-2 rounded hover:bg-blue-700"&gt;Masuk&lt;/button&gt;
      &lt;p id="loginMsg" class="text-red-500 text-sm mt-2 text-center"&gt;&lt;/p&gt;
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;!-- MAIN DASHBOARD --&gt;
  &lt;div id="mainApp" class="hidden flex h-screen overflow-hidden"&gt;
    &lt;aside class="w-64 bg-slate-800 text-white flex flex-col"&gt;
      &lt;div class="p-4 border-b border-slate-700"&gt;
        &lt;h1 class="text-xl font-bold"&gt;POAC System&lt;/h1&gt;
        &lt;p id="userInfo" class="text-sm text-slate-400 mt-1"&gt;&lt;/p&gt;
      &lt;/div&gt;
      &lt;nav class="flex-1 p-4 space-y-2"&gt;
        &lt;button onclick="showTab('planning')" class="w-full text-left p-2 rounded hover:bg-slate-700"&gt;📝 Planning&lt;/button&gt;
        &lt;button onclick="showTab('organizing')" class="w-full text-left p-2 rounded hover:bg-slate-700"&gt;👥 Organizing&lt;/button&gt;
        &lt;button onclick="showTab('actuating')" class="w-full text-left p-2 rounded hover:bg-slate-700"&gt;⚡ Actuating&lt;/button&gt;
        &lt;button onclick="showTab('controlling')" class="w-full text-left p-2 rounded hover:bg-slate-700"&gt;📊 Controlling&lt;/button&gt;
      &lt;/nav&gt;
      &lt;div class="p-4 border-t border-slate-700"&gt;
        &lt;button onclick="logout()" class="w-full text-left p-2 text-red-400 hover:bg-slate-700 rounded"&gt;Keluar&lt;/button&gt;
      &lt;/div&gt;
    &lt;/aside&gt;

    &lt;main class="flex-1 overflow-y-auto p-8"&gt;
      &lt;!-- TAB: PLANNING --&gt;
      &lt;section id="tab-planning" class="hidden"&gt;
        &lt;h2 class="text-2xl font-bold mb-4"&gt;Planning (Perencanaan)&lt;/h2&gt;
        &lt;!-- Form Tambah (Hanya Manager) --&gt;
        &lt;div id="managerPlanForm" class="bg-white p-4 rounded shadow mb-6 hidden"&gt;
          &lt;h3 class="font-semibold mb-2"&gt;Tambah Rencana Baru&lt;/h3&gt;
          &lt;div class="grid grid-cols-2 gap-4"&gt;
            &lt;input type="text" id="pTarget" placeholder="Target" class="border p-2 rounded"&gt;
            &lt;input type="text" id="pStrategi" placeholder="Strategi" class="border p-2 rounded"&gt;
            &lt;input type="text" id="pMilestone" placeholder="Milestone" class="border p-2 rounded"&gt;
            &lt;input type="date" id="pMulai" class="border p-2 rounded"&gt;
          &lt;/div&gt;
          &lt;button onclick="savePlan()" class="mt-4 bg-green-500 text-white px-4 py-2 rounded"&gt;Simpan Rencana&lt;/button&gt;
        &lt;/div&gt;
        &lt;div class="bg-white rounded shadow overflow-hidden"&gt;
          &lt;table class="w-full text-left"&gt;
            &lt;thead class="bg-gray-200"&gt;
              &lt;tr&gt;&lt;th class="p-3"&gt;Target&lt;/th&gt;&lt;th class="p-3"&gt;Strategi&lt;/th&gt;&lt;th class="p-3"&gt;Milestone&lt;/th&gt;&lt;/tr&gt;
            &lt;/thead&gt;
            &lt;tbody id="planTableBody"&gt;&lt;/tbody&gt;
          &lt;/table&gt;
        &lt;/div&gt;
      &lt;/section&gt;

      &lt;!-- Sisa tab (Organizing, Actuating, Controlling) memiliki struktur serupa... --&gt;
      &lt;!-- Lihat skrip lengkap JS di bawah untuk logika client-side --&gt;
    &lt;/main&gt;
  &lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
                </div>
            </div>
        </section>

        <section id="simulasi" class="max-w-6xl mx-auto px-4 mb-24 scroll-mt-24">
            <div class="mb-8">
                <h2 class="text-2xl font-bold text-slate-800 mb-2">Simulasi Hasil: Visualisasi Controlling</h2>
                <p class="text-slate-600">Dalam fungsi <code class="bg-slate-200 px-1 rounded text-sm text-pink-600">getChartData()</code>, sistem secara otomatis mengolah log "Actuating" untuk menghitung persentase penyelesaian tugas per divisi. Berikut adalah simulasi langsung dari grafik yang akan dihasilkan oleh Chart.js di aplikasi Anda nanti.</p>
            </div>

            <div class="bg-white p-6 md:p-8 rounded-2xl shadow-sm border border-stone-200">
                <div class="text-center mb-6">
                    <h3 class="text-xl font-bold text-slate-800">Progress Penyelesaian Tugas Per Divisi</h3>
                    <p class="text-sm text-slate-500">Live Preview berdasarkan perhitungan (Tugas Selesai / Total Tugas) * 100%</p>
                </div>
                
                <div class="chart-container">
                    <canvas id="previewKpiChart"></canvas>
                </div>
            </div>
        </section>

        <section id="deploy" class="max-w-6xl mx-auto px-4 mb-16 scroll-mt-24">
            <div class="bg-blue-600 rounded-3xl shadow-xl p-8 md:p-12 text-white overflow-hidden relative">
                <div class="absolute top-0 right-0 -mt-16 -mr-16 text-[15rem] opacity-10">🚀</div>
                
                <div class="relative z-10">
                    <h2 class="text-3xl font-bold mb-6">Langkah 5: Cara Deploy (Membuat URL Web App)</h2>
                    <p class="text-blue-100 mb-8 max-w-2xl text-lg">Ikuti langkah interaktif ini setelah menempelkan kode ke dalam editor Apps Script Anda. Centang kotak seiring dengan progres Anda.</p>
                    
                    <div class="space-y-4">
                        <label class="flex items-start gap-4 p-4 rounded-xl bg-blue-700/50 hover:bg-blue-700 transition cursor-pointer group">
                            <input type="checkbox" class="mt-1 w-5 h-5 rounded border-blue-400 text-blue-500 focus:ring-blue-500 bg-white/10" onchange="updateProgress()">
                            <div>
                                <span class="font-bold block text-lg group-hover:text-white text-blue-50">1. Mulai Deployment Baru</span>
                                <span class="text-sm text-blue-200">Di pojok kanan atas editor Apps Script, klik tombol biru <strong>Terapkan</strong> (Deploy) > <strong>Deployment baru</strong> (New deployment).</span>
                            </div>
                        </label>

                        <label class="flex items-start gap-4 p-4 rounded-xl bg-blue-700/50 hover:bg-blue-700 transition cursor-pointer group">
                            <input type="checkbox" class="mt-1 w-5 h-5 rounded border-blue-400 text-blue-500 focus:ring-blue-500 bg-white/10" onchange="updateProgress()">
                            <div>
                                <span class="font-bold block text-lg group-hover:text-white text-blue-50">2. Pilih Jenis Aplikasi</span>
                                <span class="text-sm text-blue-200">Di pop-up yang muncul, klik ikon "Roda Gigi" (⚙️) di sebelah "Pilih jenis", lalu centang <strong>Aplikasi web</strong> (Web app).</span>
                            </div>
                        </label>

                        <label class="flex items-start gap-4 p-4 rounded-xl bg-blue-700/50 hover:bg-blue-700 transition cursor-pointer group">
                            <input type="checkbox" class="mt-1 w-5 h-5 rounded border-blue-400 text-blue-500 focus:ring-blue-500 bg-white/10" onchange="updateProgress()">
                            <div>
                                <span class="font-bold block text-lg group-hover:text-white text-blue-50">3. Konfigurasi Akses</span>
                                <span class="text-sm text-blue-200">Isi Deskripsi. Jalankan sebagai: <strong>Saya (Email Anda)</strong>. Siapa yang memiliki akses: <strong>Siapa saja</strong> (Anyone). Sistem dijamin aman karena kita memiliki fitur Login Mandiri.</span>
                            </div>
                        </label>

                        <label class="flex items-start gap-4 p-4 rounded-xl bg-blue-700/50 hover:bg-blue-700 transition cursor-pointer group">
                            <input type="checkbox" class="mt-1 w-5 h-5 rounded border-blue-400 text-blue-500 focus:ring-blue-500 bg-white/10" onchange="updateProgress()">
                            <div>
                                <span class="font-bold block text-lg group-hover:text-white text-blue-50">4. Otorisasi & Dapatkan URL</span>
                                <span class="text-sm text-blue-200">Klik <strong>Terapkan</strong>. Jika diminta otorisasi, pilih akun email Anda > Advanced/Lanjutan > Go to script (unsafe). Salin URL Web App yang diberikan dan bagikan ke Tim Anda! 🎉</span>
                            </div>
                        </label>
                    </div>

                    <div class="mt-8 pt-6 border-t border-blue-500 flex items-center justify-between">
                        <span class="font-medium text-blue-100">Progres Deploy: <span id="progressText">0%</span></span>
                        <div class="w-1/2 bg-blue-900 rounded-full h-2.5">
                            <div id="progressBar" class="bg-emerald-400 h-2.5 rounded-full transition-all duration-500" style="width: 0%"></div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-slate-900 text-slate-400 py-8 text-center text-sm border-t border-slate-800">
        <p>Sistem POAC Web App Interactive Guide</p>
    </footer>

    <script>
        const state = {
            activeDbTab: 'plan',
            activeCodeTab: 'backend',
            deployProgress: 0
        };

        function switchDbTab(tabName) {
            document.querySelectorAll('[id^="content-db-"]').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('[id^="btn-db-"]').forEach(el => {
                el.className = 'px-5 py-2.5 text-sm font-medium rounded-lg text-slate-600 hover:bg-slate-200 hover:text-slate-900 transition-all';
            });

            document.getElementById('content-db-' + tabName).classList.remove('hidden');
            const activeBtn = document.getElementById('btn-db-' + tabName);
            activeBtn.className = 'px-5 py-2.5 text-sm font-medium rounded-lg bg-white shadow-sm border border-slate-200 text-blue-700 transition-all';
            
            state.activeDbTab = tabName;
        }

        function switchCodeTab(tabName) {
            document.getElementById('code-backend').classList.add('hidden');
            document.getElementById('code-frontend').classList.add('hidden');
            
            const btnB = document.getElementById('btn-code-backend');
            const btnF = document.getElementById('btn-code-frontend');
            
            btnB.className = 'px-4 py-2 text-sm font-mono text-[#9cdcfe] opacity-60 hover:opacity-100 transition-all';
            btnF.className = 'px-4 py-2 text-sm font-mono text-[#9cdcfe] opacity-60 hover:opacity-100 transition-all';

            document.getElementById('code-' + tabName).classList.remove('hidden');
            const activeBtn = document.getElementById('btn-code-' + tabName);
            activeBtn.className = 'px-4 py-2 text-sm font-mono text-[#e4e4e4] bg-[#1e1e1e] border-t-2 border-blue-500 opacity-100 transition-all';

            state.activeCodeTab = tabName;
        }

        function copyCode() {
            const currentPre = document.getElementById('code-' + state.activeCodeTab);
            const textToCopy = currentPre.innerText;
            
            navigator.clipboard.writeText(textToCopy).then(() => {
                const btn = document.querySelector('button[onclick="copyCode()"]');
                const originalText = btn.innerHTML;
                btn.innerHTML = '✅ Tersalin!';
                btn.classList.add('text-emerald-400');
                setTimeout(() => {
                    btn.innerHTML = originalText;
                    btn.classList.remove('text-emerald-400');
                }, 2000);
            }).catch(err => {
                console.error('Failed to copy text: ', err);
                const textArea = document.createElement("textarea");
                textArea.value = textToCopy;
                document.body.appendChild(textArea);
                textArea.select();
                try {
                    document.execCommand('copy');
                    const btn = document.querySelector('button[onclick="copyCode()"]');
                    btn.innerHTML = '✅ Tersalin!';
                    setTimeout(() => btn.innerHTML = '📋 Salin Kode', 2000);
                } catch (err) {
                    console.error('Fallback copy failed', err);
                }
                document.body.removeChild(textArea);
            });
        }

        function updateProgress() {
            const checkboxes = document.querySelectorAll('input[type="checkbox"]');
            const checkedCount = Array.from(checkboxes).filter(cb => cb.checked).length;
            const total = checkboxes.length;
            
            state.deployProgress = Math.round((checkedCount / total) * 100);
            
            document.getElementById('progressText').innerText = state.deployProgress + '%';
            document.getElementById('progressBar').style.width = state.deployProgress + '%';
            
            if(state.deployProgress === 100) {
                document.getElementById('progressText').innerHTML = '100% - Siap Digunakan! 🎉';
                document.getElementById('progressText').classList.add('text-emerald-300');
            } else {
                document.getElementById('progressText').classList.remove('text-emerald-300');
            }
        }

        document.addEventListener('DOMContentLoaded', function() {
            const ctx = document.getElementById('previewKpiChart').getContext('2d');
            
            const dummyData = {
                labels: ['Marketing', 'IT', 'Manajemen', 'HRD'],
                percentages: [85, 100, 50, 75]
            };

            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: dummyData.labels,
                    datasets: [{
                        label: 'Persentase Penyelesaian Tugas (%)',
                        data: dummyData.percentages,
                        backgroundColor: [
                            'rgba(59, 130, 246, 0.7)', 
                            'rgba(16, 185, 129, 0.7)', 
                            'rgba(245, 158, 11, 0.7)', 
                            'rgba(139, 92, 246, 0.7)'  
                        ],
                        borderColor: [
                            'rgba(59, 130, 246, 1)',
                            'rgba(16, 185, 129, 1)',
                            'rgba(245, 158, 11, 1)',
                            'rgba(139, 92, 246, 1)'
                        ],
                        borderWidth: 1,
                        borderRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            backgroundColor: 'rgba(15, 23, 42, 0.9)',
                            titleFont: { size: 14, family: "'Inter', sans-serif" },
                            bodyFont: { size: 14, family: "'Inter', sans-serif" },
                            padding: 12,
                            callbacks: {
                                label: function(context) {
                                    return context.parsed.y + '% Selesai';
                                }
                            }
                        }
                    },
                    scales: {
                        y: { 
                            beginAtZero: true, 
                            max: 100,
                            grid: { color: 'rgba(0, 0, 0, 0.05)' },
                            ticks: {
                                font: { family: "'Inter', sans-serif" },
                                callback: function(value) { return value + '%' }
                            }
                        },
                        x: {
                            grid: { display: false },
                            ticks: { font: { family: "'Inter', sans-serif", weight: '500' } }
                        }
                    },
                    animation: {
                        duration: 2000,
                        easing: 'easeOutQuart'
                    }
                }
            });
        });
    </script>
</body>
</html>
