# Operasional-surprice
Website untuk Laporan Task Management Operasional
[task04.html](https://github.com/user-attachments/files/22691315/task04.html)
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Task Management Tracker Surprice</title>
  <style>
    body { font-family: Arial, sans-serif; margin:0; background:#f8f9fa; }
    header { background:#2c3e50; color:white; padding:15px; text-align:center; font-size:22px; }
    .sidebar { width:220px; background:#34495e; position:fixed; top:0; bottom:0; left:0; padding-top:60px; }
    .sidebar a { display:block; color:white; padding:12px; text-decoration:none; font-weight:bold; }
    .sidebar a:hover { background:#1abc9c; }
    .main { margin-left:240px; padding:20px; }
    .section { display:none; }
    .section.active { display:block; }
    .report-link { background:#ecf0f1; margin:8px 0; padding:10px; border-radius:6px; }
    .form-input { margin:10px 0; }
    input[type=text], select, input[type=file] { width:100%; padding:8px; border:1px solid #ccc; border-radius:6px; margin-top:5px; }
    button { padding:6px 10px; margin-top:5px; background:#1abc9c; color:white; border:none; border-radius:6px; cursor:pointer; }
    button:hover { background:#16a085; }
    img { border-radius:6px; margin-top:5px; }
    h3 { margin-top:20px; color:#2c3e50; }
    footer { margin-top:30px; text-align:center; font-size:12px; color:gray; }
    #motivasi { margin:15px 0; font-weight:bold; color:#16a085; text-align:center; }
    /* Floating Chat */
    #chat-widget { position:fixed; bottom:20px; right:20px; width:250px; font-size:14px; }
    #chat-header { background:#1abc9c; color:white; padding:8px; cursor:pointer; border-radius:6px 6px 0 0; }
    #chat-body { display:none; border:1px solid #ccc; background:white; border-radius:0 0 6px 6px; max-height:300px; overflow-y:auto; }
    .chat-msg { background:#ecf0f1; margin:5px; padding:6px; border-radius:4px; display:flex; justify-content:space-between; }
    .chat-input { display:flex; gap:5px; padding:5px; }
    .chat-input input { flex:1; padding:5px; border:1px solid #ccc; border-radius:4px; }
  </style>
</head>
<body>

<header>
  🌟 Welcome Tim Surprice 🌟 <br>
  📊 Task Management Tracker Operasional
</header>

<!-- Sidebar -->
<div class="sidebar">
  <a href="#" onclick="showSection('dashboard')">Dashboard</a>
  <a href="#" onclick="showSection('cs')">Customer Service</a>
  <a href="#" onclick="showSection('gudang')">Gudang</a>
  <a href="#" onclick="showSection('finance')">Finance</a>
  <a href="#" onclick="showSection('marketing')">Marketing</a>
  <a href="#" onclick="showSection('admin')">Admin</a>
  <a href="#" onclick="showSection('operasional')">Kepala Operasional</a>
  <a href="#" onclick="showSection('kebersihan')">Laporan Kebersihan</a>
</div>

<div class="main">
  <div id="motivasi"></div>

  <!-- Dashboard -->
  <div id="dashboard" class="section active">
    <h3>📊 Dashboard Semua Divisi</h3>
    <div id="dashboard-list"></div>
  </div>

  <!-- Customer Service -->
  <div id="cs" class="section">
    <h3>Divisi Customer Service</h3>
    <div class="form-input">
      <input type="text" id="cs-name" placeholder="Nama Laporan">
      <input type="text" id="cs-url" placeholder="Link Google Spreadsheet">
      <button onclick="addSpreadsheet('cs')">Simpan</button>
    </div>
    <div id="cs-list"></div>
  </div>

  <!-- Gudang -->
  <div id="gudang" class="section">
    <h3>Divisi Gudang</h3>
    <div class="form-input">
      <input type="text" id="gudang-name" placeholder="Nama Laporan">
      <input type="text" id="gudang-url" placeholder="Link Google Spreadsheet">
      <button onclick="addSpreadsheet('gudang')">Simpan</button>
    </div>
    <div id="gudang-list"></div>
  </div>

  <!-- Finance -->
  <div id="finance" class="section">
    <h3>Divisi Finance</h3>
    <div class="form-input">
      <input type="text" id="finance-name" placeholder="Nama Laporan Keuangan">
      <input type="text" id="finance-url" placeholder="Link Google Spreadsheet">
      <button onclick="addSpreadsheet('finance')">Simpan</button>
    </div>
    <div id="finance-list"></div>
  </div>

  <!-- Marketing -->
  <div id="marketing" class="section">
    <h3>Divisi Marketing</h3>
    <div class="form-input">
      <input type="text" id="marketing-name" placeholder="Nama Laporan Marketing">
      <input type="text" id="marketing-url" placeholder="Link Google Spreadsheet">
      <button onclick="addSpreadsheet('marketing')">Simpan</button>
    </div>
    <div id="marketing-list"></div>
  </div>

  <!-- Admin -->
  <div id="admin" class="section">
    <h3>Divisi Admin</h3>
    <div class="form-input">
      <input type="text" id="admin-name" placeholder="Nama Laporan Admin">
      <input type="text" id="admin-url" placeholder="Link Google Spreadsheet">
      <button onclick="addSpreadsheet('admin')">Simpan</button>
    </div>
    <div id="admin-list"></div>
  </div>

  <!-- Kepala Operasional -->
  <div id="operasional" class="section">
    <h3>Kepala Operasional</h3>
    <div class="form-input">
      <input type="text" id="operasional-name" placeholder="Nama Laporan Operasional">
      <input type="text" id="operasional-url" placeholder="Link Google Spreadsheet">
      <button onclick="addSpreadsheet('operasional')">Simpan</button>
    </div>
    <div id="operasional-list"></div>
  </div>

  <!-- Laporan Kebersihan -->
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
      <input type="file" id="foto" accept="image/*">
      <button onclick="uploadFoto()">Upload</button>
    </div>
    <div id="galeri"></div>
  </div>

  <footer>© Sendi_Muchdianto</footer>
</div>

<!-- Floating Chat -->
<div id="chat-widget">
  <div id="chat-header" onclick="toggleChat()">💬 Komentar</div>
  <div id="chat-body">
    <div id="chatBox"></div>
    <div class="chat-input">
      <input type="text" id="chatInput" placeholder="Tulis pesan...">
      <button onclick="sendMessage()">➤</button>
    </div>
    <div style="text-align:right;padding:5px;">
      <button onclick="clearAllMessages()" style="background:red;color:white;border:none;padding:3px 6px;border-radius:4px;cursor:pointer;">🗑️ Hapus Semua</button>
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
  function tampilkanMotivasi(){
    const rand = motivasiList[Math.floor(Math.random() * motivasiList.length)];
    document.getElementById("motivasi").innerHTML = `<marquee>${rand}</marquee>`;
  }
  tampilkanMotivasi();

  // Data laporan per divisi
  let spreadsheets = JSON.parse(localStorage.getItem("spreadsheets")) || {
    cs: [], gudang: [], finance: [], marketing: [], admin: [], operasional: []
  };

  function addSpreadsheet(divisi){
    const name = document.getElementById(divisi+"-name").value.trim();
    const url = document.getElementById(divisi+"-url").value.trim();
    if(!name || !url){ alert("Nama & URL wajib diisi!"); return; }
    spreadsheets[divisi].push({name, url});
    localStorage.setItem("spreadsheets", JSON.stringify(spreadsheets));
    document.getElementById(divisi+"-name").value="";
    document.getElementById(divisi+"-url").value="";
    renderSpreadsheets(divisi);
    renderDashboard();
  }

  function renderSpreadsheets(divisi){
    const container = document.getElementById(divisi+"-list");
    if(!container) return;
    container.innerHTML = "";
    spreadsheets[divisi].forEach((r,i)=>{
      container.innerHTML += `
        <div class="report-link">
          <b>${r.name}</b><br>
          <a href="${r.url}" target="_blank">${r.url}</a>
          <button style="background:red" onclick="deleteSpreadsheet('${divisi}',${i})">Hapus</button>
        </div>`;
    });
  }

  function deleteSpreadsheet(divisi,index){
    spreadsheets[divisi].splice(index,1);
    localStorage.setItem("spreadsheets", JSON.stringify(spreadsheets));
    renderSpreadsheets(divisi);
    renderDashboard();
  }

  function showSection(id){
    document.querySelectorAll(".section").forEach(s=>s.classList.remove("active"));
    document.getElementById(id).classList.add("active");
  }

  function renderDashboard(){
    const dash = document.getElementById("dashboard-list");
    dash.innerHTML = "";
    Object.keys(spreadsheets).forEach(div=>{
      if(spreadsheets[div].length>0){
        dash.innerHTML += `<h4>${div.toUpperCase()}</h4>`;
        spreadsheets[div].forEach(r=>{
          dash.innerHTML += `<div class="report-link"><b>${r.name}</b> - <a href="${r.url}" target="_blank">Buka</a></div>`;
        });
      }
    });
  }

  // Chat
  let chatMessages = JSON.parse(localStorage.getItem("chatMessages")) || [];
  function renderChat(){
    const chatBox = document.getElementById("chatBox");
    chatBox.innerHTML = "";
    chatMessages.forEach((msg,index)=>{
      let div = document.createElement("div");
      div.className="chat-msg";
      div.innerHTML = `<span>${msg}</span>
        <button onclick="deleteMessage(${index})" style="background:none;border:none;color:red;cursor:pointer;font-size:12px;">❌</button>`;
      chatBox.appendChild(div);
    });
    chatBox.scrollTop = chatBox.scrollHeight;
  }
  function sendMessage(){
    const input=document.getElementById("chatInput");
    const text=input.value.trim();
    if(text){
      chatMessages.push(text);
      localStorage.setItem("chatMessages", JSON.stringify(chatMessages));
      input.value="";
      renderChat();
    }
  }
  function deleteMessage(index){
    chatMessages.splice(index,1);
    localStorage.setItem("chatMessages", JSON.stringify(chatMessages));
    renderChat();
  }
  function clearAllMessages(){
    if(confirm("Hapus semua komentar?")){
      chatMessages=[];
      localStorage.setItem("chatMessages", JSON.stringify(chatMessages));
      renderChat();
    }
  }
  function toggleChat(){
    const body=document.getElementById("chat-body");
    body.style.display = body.style.display==="none"?"block":"none";
  }

  // Kebersihan
  let galeri = JSON.parse(localStorage.getItem("galeri")) || [];
  function uploadFoto(){
    const area = document.getElementById("area").value;
    const file = document.getElementById("foto").files[0];
    if(!file){ alert("Pilih foto dulu!"); return; }
    const reader = new FileReader();
    reader.onload = function(e){
      galeri.push({area, src:e.target.result, date:new Date().toLocaleString()});
      localStorage.setItem("galeri", JSON.stringify(galeri));
      renderGaleri();
    }
    reader.readAsDataURL(file);
  }
  function renderGaleri(){
    const div = document.getElementById("galeri");
    div.innerHTML = "";
    galeri.forEach((g,i)=>{
      div.innerHTML += `
        <div class="report-link">
          <b>${g.area}</b> (${g.date})<br>
          <img src="${g.src}" width="150"><br>
          <button style="background:red" onclick="hapusFoto(${i})">Hapus</button>
        </div>`;
    });
  }
  function hapusFoto(i){
    galeri.splice(i,1);
    localStorage.setItem("galeri", JSON.stringify(galeri));
    renderGaleri();
  }

  // Init
  Object.keys(spreadsheets).forEach(renderSpreadsheets);
  renderDashboard();
  renderChat();
  renderGaleri();
</script>

</body>
</html>
