<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<title>Task Management Tracker Surprice</title>
<style>
  * {
    box-sizing: border-box;
  }
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
    letter-spacing: 1px;
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
    transition: background 0.3s, border-color 0.3s;
    cursor: pointer;
  }
  .sidebar a:hover,
  .sidebar a.active {
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
  h3 {
    color: #34495e;
    margin-bottom: 20px;
    font-weight: 700;
    border-bottom: 2px solid #1abc9c;
    padding-bottom: 8px;
  }
  .form-input {
    margin-bottom: 20px;
    max-width: 500px;
  }
  input[type=text], select, input[type=file] {
    width: 100%;
    padding: 10px 12px;
    border: 1.8px solid #bdc3c7;
    border-radius: 8px;
    font-size: 15px;
    transition: border-color 0.3s;
  }
  input[type=text]:focus, select:focus, input[type=file]:focus {
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
  .report-link:hover {
    box-shadow: 0 4px 12px rgba(26,188,156,0.3);
  }
  .report-link a {
    font-size: 16px;
    color: #2980b9;
    text-decoration: none;
    font-weight: 600;
    max-width: 90%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
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
    transition: background 0.3s;
    cursor: pointer;
  }
  .report-link button:hover {
    background: #c0392b;
  }
  img {
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
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.7);
  }
  #motivasi {
    margin: 15px 0 30px 0;
    font-weight: 700;
    color: #16a085;
    text-align: center;
    font-size: 18px;
    height: 30px;
    overflow: hidden;
  }
  /* Floating Chat */
  #chat-widget {
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 280px;
    font-size: 14px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    border-radius: 8px;
    background: white;
    user-select: none;
    z-index: 9999;
  }
  #chat-header {
    background: #1abc9c;
    color: white;
    padding: 10px 15px;
    cursor: pointer;
    border-radius: 8px 8px 0 0;
    font-weight: 700;
    letter-spacing: 0.5px;
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
    transition: color 0.3s;
  }
  .chat-msg button:hover {
    color: #c0392b;
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
    transition: border-color 0.3s;
  }
  .chat-input input:focus {
    border-color: #1abc9c;
    outline: none;
  }
  .chat-input button {
    background: #1abc9c;
    color: white;
    border: none;
    border-radius: 6px;
    padding: 8px 14px;
    font-weight: 700;
    cursor: pointer;
    transition: background 0.3s;
  }
  .chat-input button:hover {
    background: #16a085;
  }
  #chat-body > div:last-child {
    text-align: right;
    padding: 6px 10px;
  }
  #chat-body > div:last-child button {
    background: #e74c3c;
    color: white;
    padding: 4px 8px;
    font-size: 13px;
    border-radius: 6px;
    cursor: pointer;
    border: none;
    transition: background 0.3s;
  }
  #chat-body > div:last-child button:hover {
    background: #c0392b;
  }
  @media (max-width: 768px) {
    .sidebar {
      position: relative;
      width: 100%;
      height: auto;
      padding-top: 0;
      box-shadow: none;
    }
    .main {
      margin-left: 0;
      padding: 20px 15px;
    }
  }
</style>
</head>
<body>

<header>
  🌟 Welcome Tim Surprice 🌟 <br />
  📊 Task Management Tracker Operasional
</header>

<div class="sidebar">
  <a href="#" onclick="showSection('dashboard'); setActiveLink(this);" class="active">Dashboard</a>
  <a href="#" onclick="showSection('cs'); setActiveLink(this);">Customer Service</a>
  <a href="#" onclick="showSection('gudang'); setActiveLink(this);">Gudang</a>
  <a href="#" onclick="showSection('finance'); setActiveLink(this);">Finance</a>
  <a href="#" onclick="showSection('marketing'); setActiveLink(this);">Marketing</a>
  <a href="#" onclick="showSection('admin'); setActiveLink(this);">Admin</a>
  <a href="#" onclick="showSection('operasional'); setActiveLink(this);">Kepala Operasional</a>
  <a href="#" onclick="showSection('kebersihan'); setActiveLink(this);">Laporan Kebersihan</a>
</div>

<div class="main">
  <div id="motivasi"></div>

  <div id="dashboard" class="section active">
    <h3>📊 Dashboard Semua Divisi</h3>
    <div id="dashboard-list"></div>
  </div>

  <div id="cs" class="section">
    <h3>Divisi Customer Service</h3>
    <div class="form-input">
      <input type="text" id="cs-name" placeholder="Nama Laporan" />
      <input type="text" id="cs-url" placeholder="Link Google Spreadsheet" />
      <button onclick="addSpreadsheet('cs')">Simpan</button>
    </div>
    <div id="cs-list"></div>
  </div>

  <div id="gudang" class="section">
    <h3>Divisi Gudang</h3>
    <div class="form-input">
      <input type="text" id="gudang-name" placeholder="Nama Laporan" />
      <input type="text" id="gudang-url" placeholder="Link Google Spreadsheet" />
      <button onclick="addSpreadsheet('gudang')">Simpan</button>
    </div>
    <div id="gudang-list"></div>
  </div>

  <div id="finance" class="section">
    <h3>Divisi Finance</h3>
    <div class="form-input">
      <input type="text" id="finance-name" placeholder="Nama Laporan Keuangan" />
      <input type="text" id="finance-url" placeholder="Link Google Spreadsheet" />
      <button onclick="addSpreadsheet('finance')">Simpan</button>
    </div>
    <div id="finance-list"></div>
  </div>

  <div id="marketing" class="section">
    <h3>Divisi Marketing</h3>
    <div class="form-input">
      <input type="text" id="marketing-name" placeholder="Nama Laporan Marketing" />
      <input type="text" id="marketing-url" placeholder="Link Google Spreadsheet" />
      <button onclick="addSpreadsheet('marketing')">Simpan</button>
    </div>
    <div id="marketing-list"></div>
  </div>

  <div id="admin" class="section">
    <h3>Divisi Admin</h3>
    <div class="form-input">
      <input type="text" id="admin-name" placeholder="Nama Laporan Admin" />
      <input type="text" id="admin-url" placeholder="Link Google Spreadsheet" />
      <button onclick="addSpreadsheet('admin')">Simpan</button>
    </div>
    <div id="admin-list"></div>
  </div>

  <div id="operasional" class="section">
    <h3>Kepala Operasional</h3>
    <div class="form-input">
      <input type="text" id="operasional-name" placeholder="Nama Laporan Operasional" />
      <input type="text" id="operasional-url" placeholder="Link Google Spreadsheet" />
      <button onclick="addSpreadsheet('operasional')">Simpan</button>
    </div>
    <div id="operasional-list"></div>
  </div>

  <div id="kebersihan" class="section">
    <h3>📷 Laporan Kebersihan & Kerapian</h3>
    <div class="form-input">
      <select id="area">
        <option value="Admin">Admin</option>
        <option value="Gudang">Gudang</option>
        <option value="Checker">Checker</option>
        <option value="Packer">Packer</option>
        <option value="Staging">Staging</option>
      </select>
      <input type="file" id="foto" accept="image/*" />
      <button onclick="uploadFoto()">Upload</button>
    </div>
    <div id="galeri"></div>
  </div>

  <footer>© Sendi_Muchdianto</footer>
</div>

<div id="chat-widget">
  <div id="chat-header" onclick="toggleChat()">💬 Komentar</div>
  <div id="chat-body">
    <div id="chatBox"></div>
    <div class="chat-input">
      <input type="text" id="chatInput" placeholder="Tulis pesan..." />
      <button onclick="sendMessage()">➤</button>
    </div>
    <div>
      <button onclick="clearAllMessages()">🗑️ Hapus Semua</button>
    </div>
  </div>
</div>

<script>
  // Motivasi
  const motivasiList = [
    "💡 Tetap semangat tim! Fokus hari ini = hasil besar esok 🌟",
    "🚀 Fokus Hari ini dan Masa Depan!",
    "🔥 Jangan menunda pekerjaan, sukses diraih bersama!",
    "🌱 Konsistensi kecil setiap hari membuahkan hasil besar!"
  ];
  function tampilkanMotivasi() {
    const rand = motivasiList[Math.floor(Math.random() * motivasiList.length)];
    document.getElementById("motivasi").innerHTML = `<marquee behavior="scroll" direction="left">${rand}</marquee>`;
  }
  tampilkanMotivasi();

  // Data laporan per divisi
  let spreadsheets = JSON.parse(localStorage.getItem("spreadsheets")) || {
    cs: [],
    gudang: [],
    finance: [],
    marketing: [],
    admin: [],
    operasional: []
  };

  function isValidSpreadsheetUrl(url) {
    return url.includes("docs.google.com/spreadsheets");
  }

  function addSpreadsheet(divisi) {
    const nameInput = document.getElementById(divisi + "-name");
    const urlInput = document.getElementById(divisi + "-url");
    const name = nameInput.value.trim();
    const url = urlInput.value.trim();

    if (!name || !url) {
      alert("Nama & URL wajib diisi!");
      return;
    }
    if (!isValidSpreadsheetUrl(url)) {
      alert("Link Google Spreadsheet tidak valid!");
      return;
    }

    spreadsheets[divisi].push({ name, url });
    localStorage.setItem("spreadsheets", JSON.stringify(spreadsheets));
    nameInput.value = "";
    urlInput.value = "";
    renderSpreadsheets(divisi);
    renderDashboard();
  }

  function renderSpreadsheets(divisi) {
    const container = document.getElementById(divisi + "-list");
    if (!container) return;
    container.innerHTML = "";
    spreadsheets[divisi].forEach((r, i) => {
      container.innerHTML += `
        <div class="report-link">
          <a href="${r.url}" target="_blank" rel="noopener noreferrer" title="${r.url}">${r.name}</a>
          <button onclick="deleteSpreadsheet('${divisi}',${i})" aria-label="Hapus laporan ${r.name}">Hapus</button>
        </div>`;
    });
  }

  function deleteSpreadsheet(divisi, index) {
    if (confirm("Yakin ingin menghapus laporan ini?")) {
      spreadsheets[divisi].splice(index, 1);
      localStorage.setItem("spreadsheets", JSON.stringify(spreadsheets));
      renderSpreadsheets(divisi);
      renderDashboard();
    }
 
