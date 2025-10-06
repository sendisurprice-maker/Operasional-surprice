<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Task Management Tracker Surprice</title>
<style>
  * { box-sizing: border-box; }
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 0;
    background: #f4f7fa;
    color: #2c3e50;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  header {
    background: #34495e;
    color: white;
    padding: 20px 15px;
    text-align: center;
    font-size: 24px;
    font-weight: 700;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  }
  .sidebar {
    width: 220px;
    background: #2c3e50;
    position: fixed;
    top: 70px;
    bottom: 0;
    left: 0;
    padding-top: 20px;
    overflow-y: auto;
    box-shadow: 2px 0 5px rgba(0,0,0,0.1);
    z-index: 100;
  }
  .sidebar a {
    display: block;
    color: #ecf0f1;
    padding: 14px 20px;
    text-decoration: none;
    font-weight: 600;
    border-left: 4px solid transparent;
    transition: background 0.3s;
    cursor: pointer;
  }
  .sidebar a:hover, .sidebar a.active {
    background: #1abc9c;
    border-left-color: #16a085;
    color: white;
  }
  .main {
    margin-left: 240px;
    padding: 30px 40px;
    flex-grow: 1;
    min-height: calc(100vh - 70px);
  }
  .section { display: none; }
  .section.active { display: block; }
  h3 {
    color: #34495e;
    margin-bottom: 20px;
    font-weight: 700;
    border-bottom: 2px solid #1abc9c;
    padding-bottom: 8px;
  }
  .form-input { margin-bottom: 20px; max-width: 500px; }
  input[type=text], select, input[type=file], textarea {
    width: 100%;
    padding: 10px 12px;
    border: 1.8px solid #bdc3c7;
    border-radius: 8px;
    font-size: 15px;
    transition: border-color 0.3s;
    margin-bottom: 10px;
  }
  input[type=text]:focus, select:focus, textarea:focus {
    border-color: #1abc9c;
    outline: none;
  }
  button {
    padding: 10px 18px;
    margin-top: 10px;
    background: #1abc9c;
    color: white;
    border: none;
    border-radius: 8px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.3s;
    box-shadow: 0 3px 6px rgba(26,188,156,0.4);
  }
  button:hover {
    background: #16a085;
    box-shadow: 0 4px 8px rgba(22,160,133,0.6);
  }
  .report-link {
    background: white;
    margin: 10px 0;
    padding: 15px 20px;
    border-radius: 10px;
    box-shadow: 0 1px 4px rgba(0,0,0,0.1);
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: box-shadow 0.3s;
  }
  .report-link:hover { box-shadow: 0 4px 12px rgba(26,188,156,0.3); }
  .report-link a {
    font-size: 16px;
    color: #2980b9;
    text-decoration: none;
    font-weight: 600;
    max-width: 80%;
    word-break: break-all;
  }
  .report-link a:hover {
    color: #1abc9c;
    text-decoration: underline;
  }
  .report-link button {
    background: #e74c3c;
    padding: 6px 12px;
    font-size: 13px;
    box-shadow: none;
    border-radius: 6px;
    margin: 0;
  }
  .report-link button:hover { background: #c0392b; }
  .info-box {
    background: #fff3cd;
    border: 2px solid #ffc107;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 20px;
  }
  .info-box h4 { margin: 0 0 10px 0; color: #856404; }
  .foto-item {
    margin: 20px 0;
    padding: 15px;
    background: white;
    border-radius: 10px;
    box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  }
  .foto-item img {
    border-radius: 10px;
    margin-top: 10px;
    max-width: 100%;
    height: auto;
    box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  }
  footer {
    margin-top: 30px;
    text-align: center;
    font-size: 13px;
    color: #7f8c8d;
    padding: 15px 0;
    background: #ecf0f1;
  }
  #motivasi {
    margin: 15px 0 30px 0;
    font-weight: 700;
    color: #16a085;
    text-align: center;
    font-size: 18px;
    height: 30px;
  }
  #chat-widget {
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 280px;
    font-size: 14px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    border-radius: 8px;
    background: white;
    z-index: 9999;
  }
  #chat-header {
    background: #1abc9c;
    color: white;
    padding: 10px 15px;
    cursor: pointer;
    border-radius: 8px 8px 0 0;
    font-weight: 700;
  }
  #chat-body {
    display: none;
    border: 1px solid #ccc;
    max-height: 320px;
    overflow-y: auto;
    border-radius: 0 0 8px 8px;
  }
  .chat-msg {
    background: #ecf0f1;
    margin: 8px 10px;
    padding: 8px 12px;
    border-radius: 6px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 14px;
    word-break: break-word;
  }
  .chat-msg button {
    background: none;
    border: none;
    color: #e74c3c;
    cursor: pointer;
    font-size: 14px;
    padding: 0 4px;
  }
  .chat-input {
    display: flex;
    gap: 8px;
    padding: 10px 12px;
    border-top: 1px solid #ddd;
  }
  .chat-input input {
    flex: 1;
    padding: 8px 12px;
    border: 1.5px solid #bdc3c7;
    border-radius: 6px;
    font-size: 14px;
  }
  .chat-input button {
    background: #1abc9c;
    color: white;
    border: none;
    border-radius: 6px;
    padding: 8px 14px;
    font-weight: 700;
    margin: 0;
  }
  @media (max-width: 768px) {
    .sidebar { position: relative; width: 100%; height: auto; }
    .main { margin-left: 0; padding: 20px 15px; }
  }
</style>
</head>
<body>

<header>🌟 Welcome Tim Surprice 🌟<br>📊 Task Management Tracker Operasional</header>

<!-- SIDEBAR -->
<div class="sidebar">
  <a href="#" onclick="showSection('setup'); setActiveLink(this);" class="active">⚙️ Setup Firebase</a>
  <a href="#" onclick="showSection('dashboard'); setActiveLink(this);">Dashboard</a>
  <a href="#" onclick="showSection('cs'); setActiveLink(this);">Customer Service</a>
  <a href="#" onclick="showSection('gudang'); setActiveLink(this);">Gudang</a>
  <a href="#" onclick="showSection('finance'); setActiveLink(this);">Finance</a>
  <a href="#" onclick="showSection('marketing'); setActiveLink(this);">Marketing</a>
  <a href="#" onclick="showSection('admin'); setActiveLink(this);">Admin</a>
  <a href="#" onclick="showSection('operasional'); setActiveLink(this);">Kepala Operasional</a>
  <a href="#" onclick="showSection('kebersihan'); setActiveLink(this);">Laporan Kebersihan</a>
</div>

<!-- MAIN CONTENT -->
<div class="main">
  <div id="motivasi"></div>

  <div id="setup" class="section active">
    <h3>⚙️ Setup Firebase</h3>
    <div class="info-box">
      <h4>📝 Panduan Setup Firebase:</h4>
      <ol>
        <li>Buka <a href="https://console.firebase.google.com" target="_blank">Firebase Console</a></li>
        <li>Buat Project baru → tambahkan aplikasi web → salin <strong>firebaseConfig</strong>.</li>
      </ol>
    </div>
    <textarea id="firebase-config" rows="10" placeholder="Paste config JSON di sini..."></textarea>
    <button onclick="saveFirebaseConfig()">💾 Simpan Config</button>
    <button onclick="testConnection()" style="background:#3498db;margin-left:10px;">🔌 Test Koneksi</button>
    <div id="setup-status"></div>
  </div>

  <div id="dashboard" class="section">
    <h3>📊 Dashboard Semua Divisi</h3>
    <div id="dashboard-list">Loading...</div>
  </div>

  <!-- contoh satu divisi -->
  <div id="cs" class="section">
    <h3>Divisi Customer Service</h3>
    <div class="form-input">
      <input id="cs-name" type="text" placeholder="Nama Laporan" />
      <input id="cs-url" type="text" placeholder="Link Google Spreadsheet" />
      <button onclick="addSpreadsheet('cs')">💾 Simpan</button>
    </div>
    <div id="cs-list">Loading...</div>
  </div>

  <div id="gudang" class="section"><h3>Divisi Gudang</h3><div class="form-input">
    <input id="gudang-name" type="text" placeholder="Nama Laporan" />
    <input id="gudang-url" type="text" placeholder="Link Google Spreadsheet" />
    <button onclick="addSpreadsheet('gudang')">💾 Simpan</button>
  </div><div id="gudang-list">Loading...</div></div>

  <div id="finance" class="section"><h3>Divisi Finance</h3>
    <div class="form-input"><input id="finance-name" type="text" placeholder="Nama Laporan" /><input id="finance-url" type="text" placeholder="Link Google Spreadsheet" /><button onclick="addSpreadsheet('finance')">💾 Simpan</button></div><div id="finance-list">Loading...</div>
  </div>

  <div id="marketing" class="section"><h3>Divisi Marketing</h3>
    <div class="form-input"><input id="marketing-name" type="text" placeholder="Nama Laporan" /><input id="marketing-url" type="text" placeholder="Link Google Spreadsheet" /><button onclick="addSpreadsheet('marketing')">💾 Simpan</button></div><div id="marketing-list">Loading...</div>
  </div>

  <div id="admin" class="section"><h3>Divisi Admin</h3>
    <div class="form-input"><input id="admin-name" type="text" placeholder="Nama Laporan" /><input id="admin-url" type="text" placeholder="Link Google Spreadsheet" /><button onclick="addSpreadsheet('admin')">💾 Simpan</button></div><div id="admin-list">Loading...</div>
  </div>

  <div id="operasional" class="section"><h3>Kepala Operasional</h3>
    <div class="form-input"><input id="operasional-name" type="text" placeholder="Nama Laporan" /><input id="operasional-url" type="text" placeholder="Link Google Spreadsheet" /><button onclick="addSpreadsheet('operasional')">💾 Simpan</button></div><div id="operasional-list">Loading...</div>
  </div>

  <div id="kebersihan" class="section">
    <h3>📷 Laporan Kebersihan</h3>
    <div class="form-input">
      <select id="area">
        <option>Admin</option><option>Gudang</option><option>Checker</option><option>Packer</option><option>Staging</option>
      </select>
      <input id="foto" type="file" accept="image/*" />
      <button onclick="uploadFoto()">📤 Upload</button>
    </div>
    <div id="galeri">Loading...</div>
  </div>

  <footer>© Sendi_Muchdianto</footer>
</div>

<!-- CHAT WIDGET -->
<div id="chat-widget">
  <div id="chat-header" onclick="toggleChat()">💬 Komentar</div>
  <div id="chat-body">
    <div id="chatBox">Loading...</div>
    <div class="chat-input">
      <input id="chatInput" type="text" placeholder="Tulis pesan..." />
      <button onclick="sendMessage()">➤</button>
    </div>
    <div style="text-align:right;padding:6px 10px;">
      <button onclick="clearAllMessages()" style="background:#e74c3c;padding:4px 8px;font-size:13px;">🗑️ Hapus Semua</button>
    </div>
  </div>
</div>

<script type="module">
  import { initializeApp } from 'https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js';
  import { getFirestore, collection, addDoc, getDocs, deleteDoc, doc, query, orderBy } from 'https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js';
  import { getStorage, ref, uploadBytes, getDownloadURL, deleteObject } from 'https://www.gstatic.com/firebasejs/10.7.1/firebase-storage.js';

  let db = null, storage = null, firebaseInitialized = false;

  const motivasiList = [
    "💡 Tetap semangat tim! Fokus hari ini = hasil besar esok 🌟",
    "🚀 Fokus Hari ini dan Masa Depan!",
    "🔥 Jangan menunda pekerjaan, sukses diraih bersama!",
    "🌱 Konsistensi kecil setiap hari membuahkan hasil besar!"
  ];

  document.getElementById("motivasi").innerHTML = `<marquee>${motivasiList[Math.floor(Math.random()*motivasiList.length)]}</marquee>`;

  document.addEventListener("DOMContentLoaded", initFirebase);

  function showSection(id) {
    document.querySelectorAll(".section").forEach(s => s.classList.remove("active"));
    document.getElementById(id).classList.add("active");
  }
  function setActiveLink(el) {
    document.querySelectorAll(".sidebar a").forEach(a => a.classList.remove("active"));
    el.classList.add("active");
  }

  function initFirebase() {
    const configStr = localStorage.getItem('firebaseConfig');
    if (!configStr) return showSetupReminder();
    try {
      const firebaseConfig = JSON.parse(configStr);
      const app = initializeApp(firebaseConfig);
      db = getFirestore(app);
      storage = getStorage(app);
      firebaseInitialized = true;
      loadAllData();
    } catch (e) {
      alert('Config Firebase error: ' + e.message);
    }
  }

  function showSetupReminder() {
    const ids = ['dashboard-list','cs-list','gudang-list','finance-list','marketing-list','admin-list','operasional-list','galeri','chatBox'];
    ids.forEach(id => {
      const el = document.getElementById(id);
      if (el) el.innerHTML = '<div class="info-box"><h4>⚠️ Setup Firebase Dulu!</h4></div>';
    });
  }

  window.saveFirebaseConfig = function(){
    const text = document.getElementById('firebase-config').value.trim();
    try {
      const cfg = JSON.parse(text);
      if (!cfg.apiKey || !cfg.projectId) throw Error("Config tidak lengkap");
      localStorage.setItem('firebaseConfig', text);
      document.getElementById('setup-status').innerHTML = '<div
```
