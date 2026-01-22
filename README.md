<!doctype html>
<html lang="id" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Presensi Magang KPKNL Serang</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&amp;display=swap" rel="stylesheet">
  <style>
    body {
      box-sizing: border-box;
      font-family: 'Plus Jakarta Sans', sans-serif;
    }
    * {
      box-sizing: border-box;
    }
    .glass {
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(20px);
    }
    .gradient-primary {
      background: linear-gradient(135deg, #0ea5e9 0%, #0284c7 50%, #0369a1 100%);
    }
    .gradient-success {
      background: linear-gradient(135deg, #10b981 0%, #059669 100%);
    }
    .gradient-warning {
      background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
    }
    .gradient-danger {
      background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
    }
    .card-hover {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .card-hover:hover {
      transform: translateY(-4px);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
    }
    .sidebar-item {
      transition: all 0.2s ease;
    }
    .sidebar-item:hover, .sidebar-item.active {
      background: rgba(14, 165, 233, 0.1);
      color: #0ea5e9;
    }
    .pulse-dot {
      animation: pulse 2s infinite;
    }
    @keyframes pulse {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.5; transform: scale(1.1); }
    }
    .fade-in {
      animation: fadeIn 0.3s ease-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .tab-indicator {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    input[type="file"] {
      display: none;
    }
    .file-label {
      cursor: pointer;
    }
    .status-badge {
      font-size: 0.7rem;
      padding: 0.25rem 0.5rem;
    }
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #f1f5f9;
      border-radius: 3px;
    }
    ::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 3px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #94a3b8;
    }
    .camera-preview {
      transform: scaleX(-1);
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
 </head>
 <body class="h-full bg-gradient-to-br from-slate-50 via-sky-50 to-cyan-50">
  <div id="app" class="h-full overflow-auto"><!-- Login Screen -->
   <div id="loginScreen" class="min-h-full flex items-center justify-center p-4">
    <div class="w-full max-w-md">
     <div class="glass rounded-3xl shadow-2xl p-8 fade-in">
      <div class="text-center mb-8">
       <div class="w-20 h-20 gradient-primary rounded-2xl flex items-center justify-center mx-auto mb-4 shadow-lg">
        <svg class="w-10 h-10 text-white" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
        </svg>
       </div>
       <h1 id="appTitleLogin" class="text-2xl font-bold text-slate-800">Presensi Magang</h1>
       <p id="officeNameLogin" class="text-slate-500 mt-1">KPKNL Serang</p>
      </div>
      <div class="space-y-4">
       <div><label class="block text-sm font-medium text-slate-700 mb-2">Nama Lengkap</label> <input type="text" id="loginName" placeholder="Masukkan nama lengkap" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
       </div>
       <div><label class="block text-sm font-medium text-slate-700 mb-2">Role</label> <select id="loginRole" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none"> <option value="mahasiswa">Mahasiswa/Siswa</option> <option value="pembimbing">Pembimbing</option> <option value="admin">Admin Instansi</option> </select>
       </div><button onclick="handleLogin()" class="w-full gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200"> Masuk </button>
      </div>
      <p class="text-center text-slate-400 text-sm mt-6">Sistem Presensi Magang Digital</p>
     </div>
    </div>
   </div><!-- Main App -->
   <div id="mainApp" class="hidden h-full"><!-- Mobile Header -->
    <div class="lg:hidden gradient-primary text-white p-4 flex items-center justify-between sticky top-0 z-40"><button onclick="toggleMobileSidebar()" class="p-2 hover:bg-white/20 rounded-lg transition-colors">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
      </svg></button>
     <h1 id="appTitleMobile" class="font-bold">Presensi Magang</h1><button onclick="handleLogout()" class="p-2 hover:bg-white/20 rounded-lg transition-colors">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
      </svg></button>
    </div>
    <div class="flex h-full lg:h-full"><!-- Sidebar -->
     <div id="sidebar" class="fixed lg:static inset-0 z-50 lg:z-auto transform -translate-x-full lg:translate-x-0 transition-transform duration-300">
      <div class="absolute inset-0 bg-black/50 lg:hidden" onclick="toggleMobileSidebar()"></div>
      <div class="relative w-72 h-full glass border-r border-slate-200 flex flex-col">
       <div class="p-6 border-b border-slate-100">
        <div class="flex items-center gap-3">
         <div class="w-12 h-12 gradient-primary rounded-xl flex items-center justify-center shadow-lg">
          <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
          </svg>
         </div>
         <div>
          <h1 id="appTitleSidebar" class="font-bold text-slate-800">Presensi Magang</h1>
          <p id="officeNameSidebar" class="text-xs text-slate-500">KPKNL Serang</p>
         </div>
        </div>
       </div>
       <div class="p-4 border-b border-slate-100">
        <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl">
         <div class="w-10 h-10 bg-gradient-to-br from-sky-400 to-cyan-500 rounded-full flex items-center justify-center text-white font-bold" id="userAvatar">
          M
         </div>
         <div class="flex-1 min-w-0">
          <p class="font-semibold text-slate-800 truncate" id="userName">User</p>
          <p class="text-xs text-slate-500 capitalize" id="userRole">Mahasiswa</p>
         </div>
        </div>
       </div>
       <nav class="flex-1 p-4 space-y-1 overflow-y-auto" id="sidebarNav"><!-- Navigation items will be populated by JS -->
       </nav>
       <div class="p-4 border-t border-slate-100"><button onclick="handleLogout()" class="w-full flex items-center gap-3 px-4 py-3 text-slate-600 hover:text-red-500 hover:bg-red-50 rounded-xl transition-all">
         <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
         </svg><span class="font-medium">Keluar</span> </button>
       </div>
      </div>
     </div><!-- Main Content -->
     <div class="flex-1 overflow-y-auto p-4 lg:p-6" id="mainContent"><!-- Content will be populated by JS -->
     </div>
    </div>
   </div><!-- Camera Modal -->
   <div id="cameraModal" class="fixed inset-0 z-[100] hidden items-center justify-center p-4 bg-black/70">
    <div class="bg-white rounded-2xl w-full max-w-lg overflow-hidden">
     <div class="p-4 border-b border-slate-100 flex items-center justify-between">
      <h3 class="font-semibold text-slate-800">Ambil Foto</h3><button onclick="closeCameraModal()" class="p-2 hover:bg-slate-100 rounded-lg transition-colors">
       <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
       </svg></button>
     </div>
     <div class="relative aspect-[4/3] bg-slate-900">
      <video id="cameraVideo" class="w-full h-full object-cover camera-preview" autoplay playsinline></video>
      <canvas id="cameraCanvas" class="hidden"></canvas><img id="capturedPhoto" class="hidden w-full h-full object-cover">
      <div id="cameraOverlay" class="absolute inset-0 flex items-center justify-center">
       <div class="w-48 h-48 border-4 border-white/50 rounded-full"></div>
      </div>
     </div>
     <div class="p-4 flex gap-3"><button id="captureBtn" onclick="capturePhoto()" class="flex-1 gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all"> 📸 Ambil Foto </button> <button id="retakeBtn" onclick="retakePhoto()" class="hidden flex-1 bg-slate-200 text-slate-700 py-3 rounded-xl font-semibold hover:bg-slate-300 transition-all"> 🔄 Ulangi </button> <button id="usePhotoBtn" onclick="usePhoto()" class="hidden flex-1 gradient-success text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all"> ✓ Gunakan </button>
     </div>
    </div>
   </div><!-- Toast Container -->
   <div id="toastContainer" class="fixed bottom-4 right-4 z-[200] space-y-2"></div>
  </div>
  <script>
    // ====== APP STATE ======
    let currentUser = null;
    let currentPage = 'dashboard';
    let allData = [];
    let cameraStream = null;
    let capturedPhotoData = null;
    let photoCallback = null;

    // Location config for KPKNL Serang
    const OFFICE_LOCATION = {
      lat: -6.1168,
      lng: 106.1542,
      radius: 1000, // meters
      name: 'KPKNL Serang'
    };

    // Default config
    const defaultConfig = {
      app_title: 'Presensi Magang',
      office_name: 'KPKNL Serang',
      primary_color: '#0ea5e9',
      secondary_color: '#f8fafc',
      text_color: '#1e293b',
      accent_color: '#10b981',
      border_color: '#e2e8f0'
    };

    let config = { ...defaultConfig };

    // ====== SDK INITIALIZATION ======
    async function initApp() {
      // Initialize Element SDK
      if (window.elementSdk) {
        window.elementSdk.init({
          defaultConfig,
          onConfigChange: async (newConfig) => {
            config = { ...defaultConfig, ...newConfig };
            applyConfig();
          },
          mapToCapabilities: (cfg) => ({
            recolorables: [
              {
                get: () => cfg.primary_color || defaultConfig.primary_color,
                set: (v) => window.elementSdk.setConfig({ primary_color: v })
              },
              {
                get: () => cfg.secondary_color || defaultConfig.secondary_color,
                set: (v) => window.elementSdk.setConfig({ secondary_color: v })
              },
              {
                get: () => cfg.text_color || defaultConfig.text_color,
                set: (v) => window.elementSdk.setConfig({ text_color: v })
              },
              {
                get: () => cfg.accent_color || defaultConfig.accent_color,
                set: (v) => window.elementSdk.setConfig({ accent_color: v })
              },
              {
                get: () => cfg.border_color || defaultConfig.border_color,
                set: (v) => window.elementSdk.setConfig({ border_color: v })
              }
            ],
            borderables: [],
            fontEditable: undefined,
            fontSizeable: undefined
          }),
          mapToEditPanelValues: (cfg) => new Map([
            ['app_title', cfg.app_title || defaultConfig.app_title],
            ['office_name', cfg.office_name || defaultConfig.office_name]
          ])
        });
      }

      // Initialize Data SDK
      if (window.dataSdk) {
        const result = await window.dataSdk.init({
          onDataChanged: (data) => {
            allData = data;
            if (currentUser) {
              renderCurrentPage();
            }
          }
        });
        if (!result.isOk) {
          showToast('Gagal menginisialisasi data', 'error');
        }
      }
    }

    function applyConfig() {
      const appTitle = config.app_title || defaultConfig.app_title;
      const officeName = config.office_name || defaultConfig.office_name;
      
      const titleEls = ['appTitleLogin', 'appTitleMobile', 'appTitleSidebar'];
      titleEls.forEach(id => {
        const el = document.getElementById(id);
        if (el) el.textContent = appTitle;
      });

      const officeEls = ['officeNameLogin', 'officeNameSidebar'];
      officeEls.forEach(id => {
        const el = document.getElementById(id);
        if (el) el.textContent = officeName;
      });

      document.title = `${appTitle} - ${officeName}`;
    }

    // ====== AUTH ======
    function handleLogin() {
      const name = document.getElementById('loginName').value.trim();
      const role = document.getElementById('loginRole').value;

      if (!name) {
        showToast('Masukkan nama lengkap', 'error');
        return;
      }

      currentUser = {
        id: 'user_' + Date.now(),
        name: name,
        role: role
      };

      localStorage.setItem('currentUser', JSON.stringify(currentUser));
      showMainApp();
    }

    function handleLogout() {
      currentUser = null;
      localStorage.removeItem('currentUser');
      document.getElementById('loginScreen').classList.remove('hidden');
      document.getElementById('mainApp').classList.add('hidden');
      document.getElementById('loginName').value = '';
    }

    function showMainApp() {
      document.getElementById('loginScreen').classList.add('hidden');
      document.getElementById('mainApp').classList.remove('hidden');
      
      document.getElementById('userName').textContent = currentUser.name;
      document.getElementById('userRole').textContent = getRoleName(currentUser.role);
      document.getElementById('userAvatar').textContent = currentUser.name.charAt(0).toUpperCase();
      
      renderSidebar();
      renderCurrentPage();
    }

    function getRoleName(role) {
      const names = {
        mahasiswa: 'Mahasiswa/Siswa',
        pembimbing: 'Pembimbing',
        admin: 'Admin Instansi'
      };
      return names[role] || role;
    }

    // ====== SIDEBAR ======
    function renderSidebar() {
      const nav = document.getElementById('sidebarNav');
      const menuItems = getMenuItems();
      
      nav.innerHTML = menuItems.map(item => `
        <button onclick="navigateTo('${item.id}')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 rounded-xl ${currentPage === item.id ? 'active bg-sky-50 text-sky-600' : 'text-slate-600'}">
          ${item.icon}
          <span class="font-medium">${item.label}</span>
          ${item.badge ? `<span class="ml-auto bg-red-500 text-white text-xs px-2 py-0.5 rounded-full">${item.badge}</span>` : ''}
        </button>
      `).join('');
    }

    function getMenuItems() {
      const baseMenu = [
        { id: 'dashboard', label: 'Dashboard', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 5a1 1 0 011-1h14a1 1 0 011 1v2a1 1 0 01-1 1H5a1 1 0 01-1-1V5zM4 13a1 1 0 011-1h6a1 1 0 011 1v6a1 1 0 01-1 1H5a1 1 0 01-1-1v-6zM16 13a1 1 0 011-1h2a1 1 0 011 1v6a1 1 0 01-1 1h-2a1 1 0 01-1-1v-6z"/></svg>' }
      ];

      if (currentUser.role === 'mahasiswa') {
        return [
          ...baseMenu,
          { id: 'presensi', label: 'Presensi', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>' },
          { id: 'aktivitas', label: 'Log Aktivitas', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"/></svg>' },
          { id: 'izin', label: 'Izin/Cuti', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/></svg>' },
          { id: 'pesan', label: 'Pesan', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z"/></svg>', badge: getUnreadCount() }
        ];
      } else if (currentUser.role === 'pembimbing') {
        return [
          ...baseMenu,
          { id: 'validasi', label: 'Validasi Aktivitas', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>', badge: getPendingCount() },
          { id: 'evaluasi', label: 'Evaluasi', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/></svg>' },
          { id: 'pengumuman', label: 'Pengumuman', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5.882V19.24a1.76 1.76 0 01-3.417.592l-2.147-6.15M18 13a3 3 0 100-6M5.436 13.683A4.001 4.001 0 017 6h1.832c4.1 0 7.625-1.234 9.168-3v14c-1.543-1.766-5.067-3-9.168-3H7a3.988 3.988 0 01-1.564-.317z"/></svg>' },
          { id: 'laporan', label: 'Laporan', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/></svg>' },
          { id: 'pesan', label: 'Pesan', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z"/></svg>', badge: getUnreadCount() }
        ];
      } else {
        return [
          ...baseMenu,
          { id: 'monitoring', label: 'Monitoring', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"/></svg>' },
          { id: 'users', label: 'Kelola Akun', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"/></svg>' },
          { id: 'laporan', label: 'Laporan', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/></svg>' },
          { id: 'pengumuman', label: 'Pengumuman', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5.882V19.24a1.76 1.76 0 01-3.417.592l-2.147-6.15M18 13a3 3 0 100-6M5.436 13.683A4.001 4.001 0 017 6h1.832c4.1 0 7.625-1.234 9.168-3v14c-1.543-1.766-5.067-3-9.168-3H7a3.988 3.988 0 01-1.564-.317z"/></svg>' }
        ];
      }
    }

    function getUnreadCount() {
      const messages = allData.filter(d => d.type === 'message' && d.messageTo === currentUser?.id && !d.read);
      return messages.length || null;
    }

    function getPendingCount() {
      const pending = allData.filter(d => d.type === 'activity' && d.activityStatus === 'pending');
      return pending.length || null;
    }

    function toggleMobileSidebar() {
      const sidebar = document.getElementById('sidebar');
      sidebar.classList.toggle('-translate-x-full');
    }

    function navigateTo(page) {
      currentPage = page;
      renderSidebar();
      renderCurrentPage();
      // Close mobile sidebar
      document.getElementById('sidebar').classList.add('-translate-x-full');
    }

    // ====== PAGE RENDERING ======
    function renderCurrentPage() {
      const content = document.getElementById('mainContent');
      
      switch(currentPage) {
        case 'dashboard':
          renderDashboard(content);
          break;
        case 'presensi':
          renderPresensi(content);
          break;
        case 'aktivitas':
          renderAktivitas(content);
          break;
        case 'izin':
          renderIzin(content);
          break;
        case 'validasi':
          renderValidasi(content);
          break;
        case 'evaluasi':
          renderEvaluasi(content);
          break;
        case 'monitoring':
          renderMonitoring(content);
          break;
        case 'users':
          renderUsers(content);
          break;
        case 'laporan':
          renderLaporan(content);
          break;
        case 'pengumuman':
          renderPengumuman(content);
          break;
        case 'pesan':
          renderPesan(content);
          break;
        default:
          renderDashboard(content);
      }
    }

    // ====== DASHBOARD ======
    function renderDashboard(content) {
      const today = new Date().toISOString().split('T')[0];
      const myAttendance = allData.filter(d => d.type === 'attendance' && d.userId === currentUser.id);
      const todayAttendance = myAttendance.find(a => a.date === today);
      const totalPresent = myAttendance.length;
      const totalLate = myAttendance.filter(a => a.isLate).length;
      const myActivities = allData.filter(d => d.type === 'activity' && d.userId === currentUser.id);
      const announcements = allData.filter(d => d.type === 'announcement').slice(-3);

      if (currentUser.role === 'mahasiswa') {
        content.innerHTML = `
          <div class="space-y-6 fade-in">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
              <div>
                <h2 class="text-2xl font-bold text-slate-800">Selamat Datang! 👋</h2>
                <p class="text-slate-500">${currentUser.name} - ${formatDate(new Date())}</p>
              </div>
              <div class="flex items-center gap-2 px-4 py-2 bg-white rounded-xl shadow-sm">
                <div class="w-2 h-2 rounded-full ${todayAttendance?.checkInTime ? 'bg-green-500' : 'bg-amber-500'} pulse-dot"></div>
                <span class="text-sm font-medium text-slate-600">${todayAttendance?.checkInTime ? 'Sudah Absen Masuk' : 'Belum Absen'}</span>
              </div>
            </div>

            <!-- Quick Actions -->
            <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
              <button onclick="navigateTo('presensi')" class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100 text-left">
                <div class="w-12 h-12 gradient-primary rounded-xl flex items-center justify-center mb-3">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>
                  </svg>
                </div>
                <p class="font-semibold text-slate-800">Presensi</p>
                <p class="text-xs text-slate-500 mt-1">${todayAttendance?.checkInTime ? 'Sudah masuk' : 'Tap untuk absen'}</p>
              </button>
              
              <button onclick="navigateTo('aktivitas')" class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100 text-left">
                <div class="w-12 h-12 gradient-success rounded-xl flex items-center justify-center mb-3">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"/>
                  </svg>
                </div>
                <p class="font-semibold text-slate-800">Log Aktivitas</p>
                <p class="text-xs text-slate-500 mt-1">${myActivities.length} kegiatan</p>
              </button>

              <button onclick="navigateTo('izin')" class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100 text-left">
                <div class="w-12 h-12 gradient-warning rounded-xl flex items-center justify-center mb-3">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/>
                  </svg>
                </div>
                <p class="font-semibold text-slate-800">Izin/Cuti</p>
                <p class="text-xs text-slate-500 mt-1">Ajukan izin</p>
              </button>

              <button onclick="navigateTo('pesan')" class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100 text-left">
                <div class="w-12 h-12 bg-gradient-to-br from-purple-500 to-indigo-600 rounded-xl flex items-center justify-center mb-3">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z"/>
                  </svg>
                </div>
                <p class="font-semibold text-slate-800">Pesan</p>
                <p class="text-xs text-slate-500 mt-1">${getUnreadCount() || 0} belum dibaca</p>
              </button>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
              <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <p class="text-sm text-slate-500">Total Hadir</p>
                <p class="text-2xl font-bold text-slate-800 mt-1">${totalPresent}</p>
              </div>
              <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <p class="text-sm text-slate-500">Keterlambatan</p>
                <p class="text-2xl font-bold text-amber-500 mt-1">${totalLate}</p>
              </div>
              <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <p class="text-sm text-slate-500">Aktivitas</p>
                <p class="text-2xl font-bold text-green-500 mt-1">${myActivities.filter(a => a.activityStatus === 'approved').length}</p>
              </div>
              <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <p class="text-sm text-slate-500">Pending</p>
                <p class="text-2xl font-bold text-sky-500 mt-1">${myActivities.filter(a => a.activityStatus === 'pending').length}</p>
              </div>
            </div>

            <!-- Announcements -->
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <h3 class="font-semibold text-slate-800 mb-4 flex items-center gap-2">
                <svg class="w-5 h-5 text-sky-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5.882V19.24a1.76 1.76 0 01-3.417.592l-2.147-6.15M18 13a3 3 0 100-6M5.436 13.683A4.001 4.001 0 017 6h1.832c4.1 0 7.625-1.234 9.168-3v14c-1.543-1.766-5.067-3-9.168-3H7a3.988 3.988 0 01-1.564-.317z"/>
                </svg>
                Pengumuman Terbaru
              </h3>
              ${announcements.length > 0 ? `
                <div class="space-y-3">
                  ${announcements.map(a => `
                    <div class="p-3 bg-slate-50 rounded-xl">
                      <p class="font-medium text-slate-800">${a.announcementTitle}</p>
                      <p class="text-sm text-slate-500 mt-1">${a.announcementContent}</p>
                      <p class="text-xs text-slate-400 mt-2">${formatDate(new Date(a.createdAt))}</p>
                    </div>
                  `).join('')}
                </div>
              ` : '<p class="text-slate-500 text-center py-4">Belum ada pengumuman</p>'}
            </div>
          </div>
        `;
      } else if (currentUser.role === 'pembimbing') {
        const allActivities = allData.filter(d => d.type === 'activity');
        const pendingActivities = allActivities.filter(a => a.activityStatus === 'pending');
        const allAttendance = allData.filter(d => d.type === 'attendance');
        const todayAllAttendance = allAttendance.filter(a => a.date === today);

        content.innerHTML = `
          <div class="space-y-6 fade-in">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
              <div>
                <h2 class="text-2xl font-bold text-slate-800">Dashboard Pembimbing ����</h2>
                <p class="text-slate-500">${currentUser.name} - ${formatDate(new Date())}</p>
              </div>
            </div>

            <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
              <div class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <div class="flex items-center justify-between">
                  <div class="w-12 h-12 gradient-primary rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"/>
                    </svg>
                  </div>
                  <span class="text-2xl font-bold text-slate-800">${todayAllAttendance.length}</span>
                </div>
                <p class="text-sm text-slate-500 mt-2">Hadir Hari Ini</p>
              </div>

              <button onclick="navigateTo('validasi')" class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100 text-left">
                <div class="flex items-center justify-between">
                  <div class="w-12 h-12 gradient-warning rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/>
                    </svg>
                  </div>
                  <span class="text-2xl font-bold text-amber-500">${pendingActivities.length}</span>
                </div>
                <p class="text-sm text-slate-500 mt-2">Menunggu Validasi</p>
              </button>

              <div class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <div class="flex items-center justify-between">
                  <div class="w-12 h-12 gradient-success rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>
                    </svg>
                  </div>
                  <span class="text-2xl font-bold text-green-500">${allActivities.filter(a => a.activityStatus === 'approved').length}</span>
                </div>
                <p class="text-sm text-slate-500 mt-2">Aktivitas Disetujui</p>
              </div>

              <div class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <div class="flex items-center justify-between">
                  <div class="w-12 h-12 gradient-danger rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
                    </svg>
                  </div>
                  <span class="text-2xl font-bold text-red-500">${allAttendance.filter(a => a.isLate).length}</span>
                </div>
                <p class="text-sm text-slate-500 mt-2">Total Keterlambatan</p>
              </div>
            </div>

            <!-- Pending Activities Preview -->
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <div class="flex items-center justify-between mb-4">
                <h3 class="font-semibold text-slate-800">Aktivitas Menunggu Validasi</h3>
                <button onclick="navigateTo('validasi')" class="text-sm text-sky-500 hover:text-sky-600 font-medium">Lihat Semua →</button>
              </div>
              ${pendingActivities.length > 0 ? `
                <div class="space-y-3">
                  ${pendingActivities.slice(0, 5).map(a => `
                    <div class="flex items-center gap-4 p-3 bg-slate-50 rounded-xl">
                      <div class="w-10 h-10 bg-gradient-to-br from-sky-400 to-cyan-500 rounded-full flex items-center justify-center text-white font-bold text-sm">
                        ${a.userName?.charAt(0) || 'U'}
                      </div>
                      <div class="flex-1 min-w-0">
                        <p class="font-medium text-slate-800 truncate">${a.userName || 'Unknown'}</p>
                        <p class="text-sm text-slate-500 truncate">${a.activity}</p>
                      </div>
                      <span class="text-xs text-slate-400">${formatDate(new Date(a.createdAt))}</span>
                    </div>
                  `).join('')}
                </div>
              ` : '<p class="text-slate-500 text-center py-4">Tidak ada aktivitas yang menunggu validasi</p>'}
            </div>
          </div>
        `;
      } else {
        // Admin Dashboard
        const allAttendance = allData.filter(d => d.type === 'attendance');
        const allActivities = allData.filter(d => d.type === 'activity');
        const allLeaves = allData.filter(d => d.type === 'leave');
        const todayAllAttendance = allAttendance.filter(a => a.date === today);
        const uniqueUsers = [...new Set(allAttendance.map(a => a.userId))];

        content.innerHTML = `
          <div class="space-y-6 fade-in">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
              <div>
                <h2 class="text-2xl font-bold text-slate-800">Dashboard Admin 🏢</h2>
                <p class="text-slate-500">${currentUser.name} - ${formatDate(new Date())}</p>
              </div>
            </div>

            <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
              <div class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <div class="flex items-center justify-between">
                  <div class="w-12 h-12 gradient-primary rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"/>
                    </svg>
                  </div>
                  <span class="text-2xl font-bold text-slate-800">${uniqueUsers.length}</span>
                </div>
                <p class="text-sm text-slate-500 mt-2">Total Peserta Magang</p>
              </div>

              <div class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <div class="flex items-center justify-between">
                  <div class="w-12 h-12 gradient-success rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>
                    </svg>
                  </div>
                  <span class="text-2xl font-bold text-green-500">${todayAllAttendance.length}</span>
                </div>
                <p class="text-sm text-slate-500 mt-2">Hadir Hari Ini</p>
              </div>

              <div class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <div class="flex items-center justify-between">
                  <div class="w-12 h-12 gradient-warning rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/>
                    </svg>
                  </div>
                  <span class="text-2xl font-bold text-amber-500">${allAttendance.filter(a => a.isLate).length}</span>
                </div>
                <p class="text-sm text-slate-500 mt-2">Total Keterlambatan</p>
              </div>

              <div class="card-hover bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
                <div class="flex items-center justify-between">
                  <div class="w-12 h-12 bg-gradient-to-br from-purple-500 to-indigo-600 rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"/>
                    </svg>
                  </div>
                  <span class="text-2xl font-bold text-purple-500">${allActivities.length}</span>
                </div>
                <p class="text-sm text-slate-500 mt-2">Total Aktivitas</p>
              </div>
            </div>

            <!-- Recent Attendance -->
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <h3 class="font-semibold text-slate-800 mb-4">Presensi Hari Ini</h3>
              ${todayAllAttendance.length > 0 ? `
                <div class="overflow-x-auto">
                  <table class="w-full">
                    <thead>
                      <tr class="text-left text-sm text-slate-500 border-b border-slate-100">
                        <th class="pb-3">Nama</th>
                        <th class="pb-3">Masuk</th>
                        <th class="pb-3">Pulang</th>
                        <th class="pb-3">Status</th>
                      </tr>
                    </thead>
                    <tbody>
                      ${todayAllAttendance.map(a => `
                        <tr class="border-b border-slate-50">
                          <td class="py-3">
                            <div class="flex items-center gap-2">
                              <div class="w-8 h-8 bg-gradient-to-br from-sky-400 to-cyan-500 rounded-full flex items-center justify-center text-white font-bold text-xs">
                                ${a.userName?.charAt(0) || 'U'}
                              </div>
                              <span class="font-medium text-slate-800">${a.userName || 'Unknown'}</span>
                            </div>
                          </td>
                          <td class="py-3 text-slate-600">${a.checkInTime || '-'}</td>
                          <td class="py-3 text-slate-600">${a.checkOutTime || '-'}</td>
                          <td class="py-3">
                            <span class="status-badge rounded-full ${a.isLate ? 'bg-amber-100 text-amber-700' : 'bg-green-100 text-green-700'}">
                              ${a.isLate ? 'Terlambat' : 'Tepat Waktu'}
                            </span>
                          </td>
                        </tr>
                      `).join('')}
                    </tbody>
                  </table>
                </div>
              ` : '<p class="text-slate-500 text-center py-4">Belum ada presensi hari ini</p>'}
            </div>
          </div>
        `;
      }
    }

    // ====== PRESENSI ======
    function renderPresensi(content) {
      const today = new Date().toISOString().split('T')[0];
      const myAttendance = allData.filter(d => d.type === 'attendance' && d.userId === currentUser.id);
      const todayAttendance = myAttendance.find(a => a.date === today);

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div>
            <h2 class="text-2xl font-bold text-slate-800">Presensi Kehadiran 📍</h2>
            <p class="text-slate-500 mt-1">Absensi dengan foto wajah & geotagging</p>
          </div>

          <!-- Today's Status -->
          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <div class="flex items-center gap-4 mb-4">
              <div class="w-16 h-16 ${todayAttendance?.checkInTime ? 'gradient-success' : 'gradient-warning'} rounded-2xl flex items-center justify-center">
                <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="${todayAttendance?.checkInTime ? 'M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z' : 'M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z'}"/>
                </svg>
              </div>
              <div>
                <h3 class="font-semibold text-lg text-slate-800">${formatDate(new Date())}</h3>
                <p class="text-slate-500">${todayAttendance?.checkInTime ? `Sudah absen masuk: ${todayAttendance.checkInTime}` : 'Belum absen hari ini'}</p>
              </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
              <button onclick="${todayAttendance?.checkInTime ? 'showToast(\'Sudah absen masuk hari ini\', \'info\')' : 'startAttendance(\'in\')'}" 
                class="p-4 rounded-xl border-2 ${todayAttendance?.checkInTime ? 'border-green-200 bg-green-50' : 'border-dashed border-slate-300 hover:border-sky-500 hover:bg-sky-50'} transition-all">
                <div class="text-center">
                  <div class="text-3xl mb-2">${todayAttendance?.checkInTime ? '✅' : '🟢'}</div>
                  <p class="font-semibold text-slate-800">Absen Masuk</p>
                  <p class="text-sm text-slate-500">${todayAttendance?.checkInTime || 'Tap untuk absen'}</p>
                </div>
              </button>

              <button onclick="${!todayAttendance?.checkInTime ? 'showToast(\'Absen masuk terlebih dahulu\', \'error\')' : todayAttendance?.checkOutTime ? 'showToast(\'Sudah absen pulang hari ini\', \'info\')' : 'startAttendance(\'out\')'}" 
                class="p-4 rounded-xl border-2 ${todayAttendance?.checkOutTime ? 'border-green-200 bg-green-50' : !todayAttendance?.checkInTime ? 'border-slate-200 bg-slate-50 opacity-50' : 'border-dashed border-slate-300 hover:border-sky-500 hover:bg-sky-50'} transition-all">
                <div class="text-center">
                  <div class="text-3xl mb-2">${todayAttendance?.checkOutTime ? '✅' : '🔴'}</div>
                  <p class="font-semibold text-slate-800">Absen Pulang</p>
                  <p class="text-sm text-slate-500">${todayAttendance?.checkOutTime || (todayAttendance?.checkInTime ? 'Tap untuk absen' : 'Absen masuk dulu')}</p>
                </div>
              </button>
            </div>
          </div>

          <!-- Location Info -->
          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-3 flex items-center gap-2">
              <svg class="w-5 h-5 text-sky-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/>
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>
              </svg>
              Lokasi Kantor
            </h3>
            <div class="p-4 bg-slate-50 rounded-xl">
              <p class="font-medium text-slate-800">${OFFICE_LOCATION.name}</p>
              <p class="text-sm text-slate-500 mt-1">Jl. Raya Serang–Cilegon, Km. 03, Serang, Banten</p>
              <p class="text-xs text-slate-400 mt-2">Radius maksimal: ${OFFICE_LOCATION.radius} meter (1 km)</p>
              <p class="text-xs text-green-600 mt-1">💡 Anda akan diberitahu jarak saat absen</p>
            </div>
          </div>

          <!-- Attendance History -->
          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-4">Riwayat Presensi</h3>
            ${myAttendance.length > 0 ? `
              <div class="space-y-3">
                ${myAttendance.slice(-10).reverse().map(a => `
                  <div class="flex items-center justify-between p-3 bg-slate-50 rounded-xl">
                    <div>
                      <p class="font-medium text-slate-800">${formatDate(new Date(a.date))}</p>
                      <p class="text-sm text-slate-500">Masuk: ${a.checkInTime || '-'} | Pulang: ${a.checkOutTime || '-'}</p>
                    </div>
                    <span class="status-badge rounded-full ${a.isLate ? 'bg-amber-100 text-amber-700' : 'bg-green-100 text-green-700'}">
                      ${a.isLate ? 'Terlambat' : 'Tepat Waktu'}
                    </span>
                  </div>
                `).join('')}
              </div>
            ` : '<p class="text-slate-500 text-center py-4">Belum ada riwayat presensi</p>'}
          </div>
        </div>
      `;
    }

    async function startAttendance(type) {
      // Check location first
      if (!navigator.geolocation) {
        showToast('Browser tidak mendukung geolokasi', 'error');
        return;
      }

      showToast('Mengambil lokasi...', 'info');
      
      navigator.geolocation.getCurrentPosition(
        async (position) => {
          const { latitude, longitude } = position.coords;
          const distance = calculateDistance(latitude, longitude, OFFICE_LOCATION.lat, OFFICE_LOCATION.lng);
          
          if (distance > OFFICE_LOCATION.radius) {
            showToast(`Anda berada ${Math.round(distance)}m dari kantor (maks ${OFFICE_LOCATION.radius}m)`, 'error');
            return;
          }

          // Open camera with distance info
          openCameraModal(async (photoData) => {
            await processAttendance(type, latitude, longitude, photoData, distance);
          });
        },
        (error) => {
          showToast('Gagal mendapatkan lokasi: ' + error.message, 'error');
        },
        { enableHighAccuracy: true, timeout: 10000 }
      );
    }

    async function processAttendance(type, lat, lng, photoData, distance) {
      const today = new Date().toISOString().split('T')[0];
      const now = new Date();
      const timeString = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });
      
      const existingAttendance = allData.find(d => 
        d.type === 'attendance' && 
        d.userId === currentUser.id && 
        d.date === today
      );

      if (type === 'in') {
        const isLate = now.getHours() >= 8 && now.getMinutes() > 0;
        
        if (existingAttendance) {
          showToast('Sudah absen masuk hari ini', 'info');
          return;
        }

        const result = await window.dataSdk.create({
          type: 'attendance',
          userId: currentUser.id,
          userName: currentUser.name,
          userRole: currentUser.role,
          date: today,
          checkInTime: timeString,
          checkOutTime: null,
          checkInPhoto: photoData,
          checkOutPhoto: null,
          checkInLat: lat,
          checkInLng: lng,
          checkOutLat: null,
          checkOutLng: null,
          isLate: isLate,
          createdAt: now.toISOString()
        });

        if (result.isOk) {
          const distanceText = Math.round(distance);
          showToast(`Absen masuk berhasil! Jarak: ${distanceText}m dari kantor ${isLate ? '(Terlambat)' : ''}`, isLate ? 'warning' : 'success');
        } else {
          showToast('Gagal menyimpan presensi', 'error');
        }
      } else {
        if (!existingAttendance) {
          showToast('Belum absen masuk hari ini', 'error');
          return;
        }

        if (existingAttendance.checkOutTime) {
          showToast('Sudah absen pulang hari ini', 'info');
          return;
        }

        const result = await window.dataSdk.update({
          ...existingAttendance,
          checkOutTime: timeString,
          checkOutPhoto: photoData,
          checkOutLat: lat,
          checkOutLng: lng
        });

        if (result.isOk) {
          const distanceText = Math.round(distance);
          showToast(`Absen pulang berhasil! Jarak: ${distanceText}m dari kantor`, 'success');
        } else {
          showToast('Gagal menyimpan presensi', 'error');
        }
      }
    }

    // ====== AKTIVITAS ======
    function renderAktivitas(content) {
      const myActivities = allData.filter(d => d.type === 'activity' && d.userId === currentUser.id)
        .sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-bold text-slate-800">Log Aktivitas 📝</h2>
              <p class="text-slate-500 mt-1">Catat kegiatan harian magang</p>
            </div>
            <button onclick="showActivityForm()" class="gradient-primary text-white px-6 py-3 rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200 flex items-center gap-2">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
              </svg>
              Tambah Aktivitas
            </button>
          </div>

          <div id="activityFormContainer" class="hidden">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <h3 class="font-semibold text-slate-800 mb-4">Form Aktivitas Baru</h3>
              <div class="space-y-4">
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Deskripsi Kegiatan</label>
                  <textarea id="activityDesc" rows="3" placeholder="Jelaskan kegiatan yang dilakukan..." 
                    class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none resize-none"></textarea>
                </div>
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Dokumentasi (Opsional)</label>
                  <label class="file-label flex items-center justify-center gap-2 p-4 border-2 border-dashed border-slate-300 rounded-xl hover:border-sky-500 hover:bg-sky-50 transition-all">
                    <input type="file" id="activityFile" accept="image/*" onchange="handleFileSelect(this)">
                    <svg class="w-6 h-6 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"/>
                    </svg>
                    <span id="fileLabel" class="text-slate-500">Upload foto/dokumentasi</span>
                  </label>
                </div>
                <div class="flex gap-3">
                  <button onclick="submitActivity()" class="flex-1 gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all">
                    Simpan Aktivitas
                  </button>
                  <button onclick="hideActivityForm()" class="px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
                    Batal
                  </button>
                </div>
              </div>
            </div>
          </div>

          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-4">Riwayat Aktivitas</h3>
            ${myActivities.length > 0 ? `
              <div class="space-y-3">
                ${myActivities.map(a => `
                  <div class="p-4 bg-slate-50 rounded-xl">
                    <div class="flex items-start justify-between gap-4">
                      <div class="flex-1">
                        <p class="text-slate-800">${a.activity}</p>
                        <p class="text-xs text-slate-400 mt-2">${formatDateTime(new Date(a.createdAt))}</p>
                        ${a.activityNote ? `<p class="text-sm text-slate-600 mt-2 p-2 bg-white rounded-lg">💬 ${a.activityNote}</p>` : ''}
                      </div>
                      <span class="status-badge rounded-full ${getStatusColor(a.activityStatus)}">
                        ${getStatusLabel(a.activityStatus)}
                      </span>
                    </div>
                  </div>
                `).join('')}
              </div>
            ` : '<p class="text-slate-500 text-center py-4">Belum ada aktivitas tercatat</p>'}
          </div>
        </div>
      `;
    }

    let selectedFileData = null;

    function showActivityForm() {
      document.getElementById('activityFormContainer').classList.remove('hidden');
    }

    function hideActivityForm() {
      document.getElementById('activityFormContainer').classList.add('hidden');
      document.getElementById('activityDesc').value = '';
      document.getElementById('fileLabel').textContent = 'Upload foto/dokumentasi';
      selectedFileData = null;
    }

    function handleFileSelect(input) {
      if (input.files && input.files[0]) {
        const file = input.files[0];
        document.getElementById('fileLabel').textContent = file.name;
        
        const reader = new FileReader();
        reader.onload = (e) => {
          selectedFileData = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    }

    async function submitActivity() {
      const desc = document.getElementById('activityDesc').value.trim();
      
      if (!desc) {
        showToast('Masukkan deskripsi kegiatan', 'error');
        return;
      }

      if (allData.filter(d => d.type === 'activity').length >= 999) {
        showToast('Batas maksimum 999 data tercapai', 'error');
        return;
      }

      const result = await window.dataSdk.create({
        type: 'activity',
        userId: currentUser.id,
        userName: currentUser.name,
        userRole: currentUser.role,
        activity: desc,
        activityStatus: 'pending',
        activityNote: null,
        documentation: selectedFileData,
        createdAt: new Date().toISOString()
      });

      if (result.isOk) {
        showToast('Aktivitas berhasil disimpan!', 'success');
        hideActivityForm();
      } else {
        showToast('Gagal menyimpan aktivitas', 'error');
      }
    }

    // ====== IZIN/CUTI ======
    function renderIzin(content) {
      const myLeaves = allData.filter(d => d.type === 'leave' && d.userId === currentUser.id)
        .sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-bold text-slate-800">Pengajuan Izin/Cuti 📅</h2>
              <p class="text-slate-500 mt-1">Ajukan izin atau cuti dengan bukti pendukung</p>
            </div>
            <button onclick="showLeaveForm()" class="gradient-primary text-white px-6 py-3 rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200 flex items-center gap-2">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
              </svg>
              Ajukan Izin
            </button>
          </div>

          <div id="leaveFormContainer" class="hidden">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <h3 class="font-semibold text-slate-800 mb-4">Form Pengajuan Izin</h3>
              <div class="space-y-4">
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Jenis Izin</label>
                  <select id="leaveType" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    <option value="sakit">Sakit</option>
                    <option value="izin">Izin Keperluan</option>
                    <option value="cuti">Cuti</option>
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Tanggal</label>
                  <input type="date" id="leaveDate" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                </div>
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Alasan</label>
                  <textarea id="leaveReason" rows="3" placeholder="Jelaskan alasan izin/cuti..." 
                    class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none resize-none"></textarea>
                </div>
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Bukti Pendukung (Opsional)</label>
                  <label class="file-label flex items-center justify-center gap-2 p-4 border-2 border-dashed border-slate-300 rounded-xl hover:border-sky-500 hover:bg-sky-50 transition-all">
                    <input type="file" id="leaveProof" accept="image/*,.pdf" onchange="handleLeaveFileSelect(this)">
                    <svg class="w-6 h-6 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"/>
                    </svg>
                    <span id="leaveFileLabel" class="text-slate-500">Upload surat keterangan</span>
                  </label>
                </div>
                <div class="flex gap-3">
                  <button onclick="submitLeave()" class="flex-1 gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all">
                    Ajukan
                  </button>
                  <button onclick="hideLeaveForm()" class="px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
                    Batal
                  </button>
                </div>
              </div>
            </div>
          </div>

          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-4">Riwayat Pengajuan</h3>
            ${myLeaves.length > 0 ? `
              <div class="space-y-3">
                ${myLeaves.map(l => `
                  <div class="p-4 bg-slate-50 rounded-xl">
                    <div class="flex items-start justify-between gap-4">
                      <div>
                        <div class="flex items-center gap-2">
                          <span class="text-lg">${l.leaveType === 'sakit' ? '🤒' : l.leaveType === 'izin' ? '📝' : '🏖️'}</span>
                          <span class="font-medium text-slate-800 capitalize">${l.leaveType}</span>
                        </div>
                        <p class="text-sm text-slate-600 mt-1">${l.leaveReason}</p>
                        <p class="text-xs text-slate-400 mt-2">${formatDate(new Date(l.date || l.createdAt))}</p>
                      </div>
                      <span class="status-badge rounded-full ${getStatusColor(l.leaveStatus)}">
                        ${getStatusLabel(l.leaveStatus)}
                      </span>
                    </div>
                  </div>
                `).join('')}
              </div>
            ` : '<p class="text-slate-500 text-center py-4">Belum ada pengajuan izin</p>'}
          </div>
        </div>
      `;
    }

    let leaveProofData = null;

    function showLeaveForm() {
      document.getElementById('leaveFormContainer').classList.remove('hidden');
      document.getElementById('leaveDate').value = new Date().toISOString().split('T')[0];
    }

    function hideLeaveForm() {
      document.getElementById('leaveFormContainer').classList.add('hidden');
      document.getElementById('leaveReason').value = '';
      document.getElementById('leaveFileLabel').textContent = 'Upload surat keterangan';
      leaveProofData = null;
    }

    function handleLeaveFileSelect(input) {
      if (input.files && input.files[0]) {
        const file = input.files[0];
        document.getElementById('leaveFileLabel').textContent = file.name;
        
        const reader = new FileReader();
        reader.onload = (e) => {
          leaveProofData = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    }

    async function submitLeave() {
      const type = document.getElementById('leaveType').value;
      const date = document.getElementById('leaveDate').value;
      const reason = document.getElementById('leaveReason').value.trim();
      
      if (!reason) {
        showToast('Masukkan alasan izin', 'error');
        return;
      }

      if (allData.filter(d => d.type === 'leave').length >= 999) {
        showToast('Batas maksimum 999 data tercapai', 'error');
        return;
      }

      const result = await window.dataSdk.create({
        type: 'leave',
        userId: currentUser.id,
        userName: currentUser.name,
        userRole: currentUser.role,
        date: date,
        leaveType: type,
        leaveReason: reason,
        leaveStatus: 'pending',
        leaveProof: leaveProofData,
        createdAt: new Date().toISOString()
      });

      if (result.isOk) {
        showToast('Pengajuan izin berhasil!', 'success');
        hideLeaveForm();
      } else {
        showToast('Gagal mengajukan izin', 'error');
      }
    }

    // ====== VALIDASI (Pembimbing) ======
    function renderValidasi(content) {
      const pendingActivities = allData.filter(d => d.type === 'activity' && d.activityStatus === 'pending')
        .sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
      const pendingLeaves = allData.filter(d => d.type === 'leave' && d.leaveStatus === 'pending')
        .sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div>
            <h2 class="text-2xl font-bold text-slate-800">Validasi Aktivitas ✅</h2>
            <p class="text-slate-500 mt-1">Setujui atau tolak aktivitas mahasiswa</p>
          </div>

          <!-- Tabs (Kelola Akun) -->
          <div class="flex gap-2 bg-white p-2 rounded-xl shadow-sm border border-slate-100">
            <button onclick="switchUsersTab('participants')" id="tabParticipants" class="flex-1 py-2 px-4 rounded-lg font-medium transition-all bg-sky-100 text-sky-700">
              Peserta Magang
            </button>
            <button onclick="switchUsersTab('supervisors')" id="tabSupervisors" class="flex-1 py-2 px-4 rounded-lg font-medium transition-all text-slate-600 hover:bg-slate-100">
              Pembimbing
            </button>
          </div>

          <div id="activitiesSection">
            ${pendingActivities.length > 0 ? `
              <div class="space-y-4">
                ${pendingActivities.map(a => `
                  <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
                    <div class="flex items-start gap-4">
                      <div class="w-12 h-12 bg-gradient-to-br from-sky-400 to-cyan-500 rounded-full flex items-center justify-center text-white font-bold">
                        ${a.userName?.charAt(0) || 'U'}
                      </div>
                      <div class="flex-1">
                        <div class="flex items-center justify-between">
                          <p class="font-semibold text-slate-800">${a.userName || 'Unknown'}</p>
                          <span class="text-xs text-slate-400">${formatDateTime(new Date(a.createdAt))}</span>
                        </div>
                        <p class="text-slate-600 mt-2">${a.activity}</p>
                        ${a.documentation ? `
                          <img src="${a.documentation}" class="mt-3 rounded-xl max-h-48 object-cover" alt="Dokumentasi">
                        ` : ''}
                        <div class="mt-4 flex gap-2">
                          <input type="text" id="note_${a.__backendId}" placeholder="Catatan (opsional)" 
                            class="flex-1 px-3 py-2 rounded-lg border border-slate-200 text-sm focus:border-sky-500 focus:ring-1 focus:ring-sky-200 outline-none">
                          <button onclick="approveActivity('${a.__backendId}')" class="px-4 py-2 gradient-success text-white rounded-lg text-sm font-medium hover:opacity-90 transition-all">
                            ✓ Setujui
                          </button>
                          <button onclick="rejectActivity('${a.__backendId}')" class="px-4 py-2 gradient-danger text-white rounded-lg text-sm font-medium hover:opacity-90 transition-all">
                            ✕ Tolak
                          </button>
                        </div>
                      </div>
                    </div>
                  </div>
                `).join('')}
              </div>
            ` : '<div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-8 text-center"><p class="text-slate-500">Tidak ada aktivitas yang menunggu validasi</p></div>'}
          </div>

          <div id="leavesSection" class="hidden">
            ${pendingLeaves.length > 0 ? `
              <div class="space-y-4">
                ${pendingLeaves.map(l => `
                  <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
                    <div class="flex items-start gap-4">
                      <div class="w-12 h-12 bg-gradient-to-br from-amber-400 to-orange-500 rounded-full flex items-center justify-center text-white font-bold">
                        ${l.userName?.charAt(0) || 'U'}
                      </div>
                      <div class="flex-1">
                        <div class="flex items-center justify-between">
                          <p class="font-semibold text-slate-800">${l.userName || 'Unknown'}</p>
                          <span class="px-2 py-1 bg-amber-100 text-amber-700 text-xs rounded-full capitalize">${l.leaveType}</span>
                        </div>
                        <p class="text-slate-600 mt-2">${l.leaveReason}</p>
                        <p class="text-xs text-slate-400 mt-2">Tanggal: ${formatDate(new Date(l.date || l.createdAt))}</p>
                        <div class="mt-4 flex gap-2">
                          <button onclick="approveLeave('${l.__backendId}')" class="px-4 py-2 gradient-success text-white rounded-lg text-sm font-medium hover:opacity-90 transition-all">
                            ✓ Setujui
                          </button>
                          <button onclick="rejectLeave('${l.__backendId}')" class="px-4 py-2 gradient-danger text-white rounded-lg text-sm font-medium hover:opacity-90 transition-all">
                            ✕ Tolak
                          </button>
                        </div>
                      </div>
                    </div>
                  </div>
                `).join('')}
              </div>
            ` : '<div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-8 text-center"><p class="text-slate-500">Tidak ada izin yang menunggu validasi</p></div>'}
          </div>
        </div>
      `;
    }

    function switchValidationTab(tab) {
      document.getElementById('activitiesSection').classList.toggle('hidden', tab !== 'activities');
      document.getElementById('leavesSection').classList.toggle('hidden', tab !== 'leaves');
      document.getElementById('tabActivities').classList.toggle('bg-sky-100', tab === 'activities');
      document.getElementById('tabActivities').classList.toggle('text-sky-700', tab === 'activities');
      document.getElementById('tabActivities').classList.toggle('text-slate-600', tab !== 'activities');
      document.getElementById('tabLeaves').classList.toggle('bg-sky-100', tab === 'leaves');
      document.getElementById('tabLeaves').classList.toggle('text-sky-700', tab === 'leaves');
      document.getElementById('tabLeaves').classList.toggle('text-slate-600', tab !== 'leaves');
    }

    function switchUsersTab(tab) {
      document.getElementById('participantsSection').classList.toggle('hidden', tab !== 'participants');
      document.getElementById('supervisorsSection').classList.toggle('hidden', tab !== 'supervisors');
      document.getElementById('tabParticipants').classList.toggle('bg-sky-100', tab === 'participants');
      document.getElementById('tabParticipants').classList.toggle('text-sky-700', tab === 'participants');
      document.getElementById('tabParticipants').classList.toggle('text-slate-600', tab !== 'participants');
      document.getElementById('tabSupervisors').classList.toggle('bg-sky-100', tab === 'supervisors');
      document.getElementById('tabSupervisors').classList.toggle('text-sky-700', tab === 'supervisors');
      document.getElementById('tabSupervisors').classList.toggle('text-slate-600', tab !== 'supervisors');
    }

    async function approveActivity(id) {
      const activity = allData.find(d => d.__backendId === id);
      if (!activity) return;

      const note = document.getElementById(`note_${id}`)?.value || '';
      
      const result = await window.dataSdk.update({
        ...activity,
        activityStatus: 'approved',
        activityNote: note || 'Disetujui oleh pembimbing'
      });

      if (result.isOk) {
        showToast('Aktivitas disetujui!', 'success');
      } else {
        showToast('Gagal menyetujui aktivitas', 'error');
      }
    }

    async function rejectActivity(id) {
      const activity = allData.find(d => d.__backendId === id);
      if (!activity) return;

      const note = document.getElementById(`note_${id}`)?.value || '';
      
      const result = await window.dataSdk.update({
        ...activity,
        activityStatus: 'rejected',
        activityNote: note || 'Ditolak oleh pembimbing'
      });

      if (result.isOk) {
        showToast('Aktivitas ditolak', 'warning');
      } else {
        showToast('Gagal menolak aktivitas', 'error');
      }
    }

    async function approveLeave(id) {
      const leave = allData.find(d => d.__backendId === id);
      if (!leave) return;
      
      const result = await window.dataSdk.update({
        ...leave,
        leaveStatus: 'approved'
      });

      if (result.isOk) {
        showToast('Izin disetujui!', 'success');
      } else {
        showToast('Gagal menyetujui izin', 'error');
      }
    }

    async function rejectLeave(id) {
      const leave = allData.find(d => d.__backendId === id);
      if (!leave) return;
      
      const result = await window.dataSdk.update({
        ...leave,
        leaveStatus: 'rejected'
      });

      if (result.isOk) {
        showToast('Izin ditolak', 'warning');
      } else {
        showToast('Gagal menolak izin', 'error');
      }
    }

    // ====== EVALUASI ======
    function renderEvaluasi(content) {
      const uniqueUsers = [...new Set(allData.filter(d => d.type === 'attendance').map(a => JSON.stringify({ id: a.userId, name: a.userName })))].map(s => JSON.parse(s));
      const evaluations = allData.filter(d => d.type === 'evaluation');

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div>
            <h2 class="text-2xl font-bold text-slate-800">Evaluasi Mahasiswa ⭐</h2>
            <p class="text-slate-500 mt-1">Berikan penilaian kinerja peserta magang</p>
          </div>

          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-4">Daftar Peserta Magang</h3>
            ${uniqueUsers.length > 0 ? `
              <div class="space-y-3">
                ${uniqueUsers.map(u => {
                  const eval = evaluations.find(e => e.userId === u.id);
                  return `
                    <div class="flex items-center justify-between p-4 bg-slate-50 rounded-xl">
                      <div class="flex items-center gap-3">
                        <div class="w-10 h-10 bg-gradient-to-br from-sky-400 to-cyan-500 rounded-full flex items-center justify-center text-white font-bold">
                          ${u.name?.charAt(0) || 'U'}
                        </div>
                        <div>
                          <p class="font-medium text-slate-800">${u.name}</p>
                          ${eval ? `<p class="text-sm text-green-600">Sudah dievaluasi - Skor: ${eval.evaluationScore}</p>` : '<p class="text-sm text-slate-500">Belum dievaluasi</p>'}
                        </div>
                      </div>
                      <button onclick="showEvaluationForm('${u.id}', '${u.name}')" class="px-4 py-2 ${eval ? 'bg-slate-200 text-slate-700' : 'gradient-primary text-white'} rounded-lg text-sm font-medium hover:opacity-90 transition-all">
                        ${eval ? 'Edit Evaluasi' : 'Beri Evaluasi'}
                      </button>
                    </div>
                  `;
                }).join('')}
              </div>
            ` : '<p class="text-slate-500 text-center py-4">Belum ada peserta magang</p>'}
          </div>

          <div id="evaluationFormContainer" class="hidden">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <h3 class="font-semibold text-slate-800 mb-4">Form Evaluasi - <span id="evalUserName"></span></h3>
              <input type="hidden" id="evalUserId">
              <div class="space-y-4">
                <div class="grid grid-cols-2 gap-4">
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Disiplin (1-10)</label>
                    <input type="number" id="evalDiscipline" min="1" max="10" value="7" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Tanggung Jawab (1-10)</label>
                    <input type="number" id="evalResponsibility" min="1" max="10" value="7" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Keterampilan (1-10)</label>
                    <input type="number" id="evalSkill" min="1" max="10" value="7" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Kerjasama (1-10)</label>
                    <input type="number" id="evalTeamwork" min="1" max="10" value="7" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                </div>
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Catatan Tambahan</label>
                  <textarea id="evalNote" rows="3" placeholder="Catatan evaluasi..." 
                    class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none resize-none"></textarea>
                </div>
                <div class="flex gap-3">
                  <button onclick="submitEvaluation()" class="flex-1 gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all">
                    Simpan Evaluasi
                  </button>
                  <button onclick="hideEvaluationForm()" class="px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
                    Batal
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      `;
    }

    function showEvaluationForm(userId, userName) {
      document.getElementById('evaluationFormContainer').classList.remove('hidden');
      document.getElementById('evalUserId').value = userId;
      document.getElementById('evalUserName').textContent = userName;
      
      const existingEval = allData.find(d => d.type === 'evaluation' && d.userId === userId);
      if (existingEval) {
        document.getElementById('evalDiscipline').value = existingEval.evaluationDiscipline || 7;
        document.getElementById('evalResponsibility').value = existingEval.evaluationResponsibility || 7;
        document.getElementById('evalSkill').value = existingEval.evaluationSkill || 7;
        document.getElementById('evalTeamwork').value = existingEval.evaluationTeamwork || 7;
        document.getElementById('evalNote').value = existingEval.evaluationNote || '';
      }
    }

    function hideEvaluationForm() {
      document.getElementById('evaluationFormContainer').classList.add('hidden');
    }

    async function submitEvaluation() {
      const userId = document.getElementById('evalUserId').value;
      const discipline = parseInt(document.getElementById('evalDiscipline').value) || 7;
      const responsibility = parseInt(document.getElementById('evalResponsibility').value) || 7;
      const skill = parseInt(document.getElementById('evalSkill').value) || 7;
      const teamwork = parseInt(document.getElementById('evalTeamwork').value) || 7;
      const note = document.getElementById('evalNote').value.trim();
      
      const score = Math.round((discipline + responsibility + skill + teamwork) / 4 * 10);
      
      const existingEval = allData.find(d => d.type === 'evaluation' && d.userId === userId);
      
      let result;
      if (existingEval) {
        result = await window.dataSdk.update({
          ...existingEval,
          evaluationDiscipline: discipline,
          evaluationResponsibility: responsibility,
          evaluationSkill: skill,
          evaluationTeamwork: teamwork,
          evaluationScore: score,
          evaluationNote: note
        });
      } else {
        const user = allData.find(d => d.userId === userId);
        result = await window.dataSdk.create({
          type: 'evaluation',
          userId: userId,
          userName: user?.userName || 'Unknown',
          userRole: 'mahasiswa',
          evaluationDiscipline: discipline,
          evaluationResponsibility: responsibility,
          evaluationSkill: skill,
          evaluationTeamwork: teamwork,
          evaluationScore: score,
          evaluationNote: note,
          createdAt: new Date().toISOString()
        });
      }

      if (result.isOk) {
        showToast('Evaluasi berhasil disimpan!', 'success');
        hideEvaluationForm();
      } else {
        showToast('Gagal menyimpan evaluasi', 'error');
      }
    }

    // ====== MONITORING (Admin) ======
    function renderMonitoring(content) {
      const allAttendance = allData.filter(d => d.type === 'attendance');
      const allActivities = allData.filter(d => d.type === 'activity');
      const uniqueUsers = [...new Set(allAttendance.map(a => JSON.stringify({ id: a.userId, name: a.userName })))].map(s => JSON.parse(s));
      
      // Calculate stats
      const today = new Date().toISOString().split('T')[0];
      const todayAttendance = allAttendance.filter(a => a.date === today);
      const thisMonth = allAttendance.filter(a => a.date?.startsWith(new Date().toISOString().slice(0, 7)));
      const lateCount = thisMonth.filter(a => a.isLate).length;

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div>
            <h2 class="text-2xl font-bold text-slate-800">Monitoring Keseluruhan 📊</h2>
            <p class="text-slate-500 mt-1">Pantau semua aktivitas peserta magang</p>
          </div>

          <!-- Stats Cards -->
          <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
              <p class="text-sm text-slate-500">Peserta Magang</p>
              <p class="text-2xl font-bold text-slate-800 mt-1">${uniqueUsers.length}</p>
            </div>
            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
              <p class="text-sm text-slate-500">Hadir Hari Ini</p>
              <p class="text-2xl font-bold text-green-500 mt-1">${todayAttendance.length}</p>
            </div>
            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
              <p class="text-sm text-slate-500">Terlambat (Bulan Ini)</p>
              <p class="text-2xl font-bold text-amber-500 mt-1">${lateCount}</p>
            </div>
            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100">
              <p class="text-sm text-slate-500">Total Aktivitas</p>
              <p class="text-2xl font-bold text-sky-500 mt-1">${allActivities.length}</p>
            </div>
          </div>

          <!-- Attendance Chart Placeholder -->
          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-4">Grafik Kehadiran Mingguan</h3>
            <div class="flex items-end gap-2 h-40">
              ${[...Array(7)].map((_, i) => {
                const date = new Date();
                date.setDate(date.getDate() - 6 + i);
                const dateStr = date.toISOString().split('T')[0];
                const dayAttendance = allAttendance.filter(a => a.date === dateStr).length;
                const height = Math.max(10, (dayAttendance / Math.max(uniqueUsers.length, 1)) * 100);
                return `
                  <div class="flex-1 flex flex-col items-center gap-2">
                    <div class="w-full gradient-primary rounded-t-lg transition-all" style="height: ${height}%"></div>
                    <span class="text-xs text-slate-500">${date.toLocaleDateString('id-ID', { weekday: 'short' })}</span>
                  </div>
                `;
              }).join('')}
            </div>
          </div>

          <!-- User List -->
          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-4">Daftar Peserta Magang</h3>
            ${uniqueUsers.length > 0 ? `
              <div class="overflow-x-auto">
                <table class="w-full">
                  <thead>
                    <tr class="text-left text-sm text-slate-500 border-b border-slate-100">
                      <th class="pb-3">Nama</th>
                      <th class="pb-3">Total Hadir</th>
                      <th class="pb-3">Terlambat</th>
                      <th class="pb-3">Aktivitas</th>
                    </tr>
                  </thead>
                  <tbody>
                    ${uniqueUsers.map(u => {
                      const userAttendance = allAttendance.filter(a => a.userId === u.id);
                      const userLate = userAttendance.filter(a => a.isLate).length;
                      const userActivities = allActivities.filter(a => a.userId === u.id).length;
                      return `
                        <tr class="border-b border-slate-50">
                          <td class="py-3">
                            <div class="flex items-center gap-2">
                              <div class="w-8 h-8 bg-gradient-to-br from-sky-400 to-cyan-500 rounded-full flex items-center justify-center text-white font-bold text-xs">
                                ${u.name?.charAt(0) || 'U'}
                              </div>
                              <span class="font-medium text-slate-800">${u.name || 'Unknown'}</span>
                            </div>
                          </td>
                          <td class="py-3 text-slate-600">${userAttendance.length}</td>
                          <td class="py-3 text-amber-500">${userLate}</td>
                          <td class="py-3 text-slate-600">${userActivities}</td>
                        </tr>
                      `;
                    }).join('')}
                  </tbody>
                </table>
              </div>
            ` : '<p class="text-slate-500 text-center py-4">Belum ada peserta magang</p>'}
          </div>
        </div>
      `;
    }

    // ====== USERS (Admin) ======
    function renderUsers(content) {
      const participants = allData.filter(d => d.type === 'participant')
        .sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
      const supervisors = allData.filter(d => d.type === 'supervisor')
        .sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-bold text-slate-800">Kelola Akun 👥</h2>
              <p class="text-slate-500 mt-1">Kelola peserta magang dan pembimbing</p>
            </div>
          </div>

          <!-- Tabs (Kelola Akun) -->
          <div class="flex gap-2 bg-white p-2 rounded-xl shadow-sm border border-slate-100">
            <button onclick="switchUsersTab('participants')" id="tabParticipants" class="flex-1 py-2 px-4 rounded-lg font-medium transition-all bg-sky-100 text-sky-700">
              Peserta Magang (${participants.length})
            </button>
            <button onclick="switchUsersTab('supervisors')" id="tabSupervisors" class="flex-1 py-2 px-4 rounded-lg font-medium transition-all text-slate-600 hover:bg-slate-100">
              Pembimbing (${supervisors.length})
            </button>
          </div>

          <!-- SECTION: PARTICIPANTS -->
          <div id="participantsSection">
            <div class="flex items-center justify-end mb-4">
              <button onclick="showParticipantForm()" class="gradient-primary text-white px-6 py-3 rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200 flex items-center gap-2">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
                </svg>
                Tambah Peserta
              </button>
            </div>

          <div id="participantFormContainer" class="hidden">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <h3 class="font-semibold text-slate-800 mb-4">Form Pendaftaran Peserta Baru</h3>
              <div class="space-y-4">
                <!-- Foto Profil -->
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Foto Profil</label>
                  <div class="flex items-center gap-4">
                    <div id="participantPhotoPreview" class="w-24 h-24 bg-slate-100 rounded-full flex items-center justify-center overflow-hidden">
                      <svg class="w-12 h-12 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"/>
                      </svg>
                    </div>
                    <button onclick="openCameraModal((photo) => handleParticipantPhoto(photo))" class="px-4 py-2 bg-sky-100 text-sky-700 rounded-lg text-sm font-medium hover:bg-sky-200 transition-all">
                      📷 Ambil Foto
                    </button>
                  </div>
                </div>

                <!-- Data Pribadi -->
                <div class="grid md:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Nama Lengkap *</label>
                    <input type="text" id="participantName" placeholder="Nama lengkap" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">NIM/NIS *</label>
                    <input type="text" id="participantNim" placeholder="Nomor induk" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                </div>

                <div class="grid md:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Email *</label>
                    <input type="email" id="participantEmail" placeholder="email@example.com" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">No. Telepon *</label>
                    <input type="tel" id="participantPhone" placeholder="08xx-xxxx-xxxx" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                </div>

                <!-- Data Pendidikan -->
                <div class="grid md:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Institusi/Sekolah *</label>
                    <input type="text" id="participantInstitution" placeholder="Nama universitas/sekolah" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Jurusan/Bidang</label>
                    <input type="text" id="participantMajor" placeholder="Jurusan/program studi" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                </div>

                <!-- Alamat -->
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Alamat Lengkap *</label>
                  <textarea id="participantAddress" rows="2" placeholder="Alamat lengkap" 
                    class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none resize-none"></textarea>
                </div>

                <!-- Periode Magang -->
                <div class="grid md:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Tanggal Mulai *</label>
                    <input type="date" id="participantStartDate" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Tanggal Selesai *</label>
                    <input type="date" id="participantEndDate" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                </div>

                <!-- Pembimbing -->
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Pilih Pembimbing *</label>
                  <select id="participantSupervisor" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    <option value="">Pilih pembimbing</option>
                    <!-- Options will be populated by JS -->
                  </select>
                </div>

                <div class="flex gap-3 pt-2">
                  <button onclick="submitParticipant()" class="flex-1 gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all">
                    ��� Simpan Data Peserta
                  </button>
                  <button onclick="hideParticipantForm()" class="px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
                    Batal
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Daftar Peserta -->
          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <div class="flex items-center justify-between mb-4">
              <h3 class="font-semibold text-slate-800">Daftar Peserta Magang</h3>
              <span class="text-sm text-slate-500">${participants.length} peserta</span>
            </div>
            ${participants.length > 0 ? `
              <div class="space-y-4">
                ${participants.map(p => `
                  <div class="flex items-start gap-4 p-4 bg-slate-50 rounded-xl hover:bg-slate-100 transition-all">
                    <div class="w-16 h-16 rounded-full overflow-hidden bg-gradient-to-br from-sky-400 to-cyan-500 flex-shrink-0">
                      ${p.profilePhoto ? 
                        `<img src="${p.profilePhoto}" class="w-full h-full object-cover" alt="${p.userName}">` : 
                        `<div class="w-full h-full flex items-center justify-center text-white font-bold text-xl">${p.userName?.charAt(0) || 'U'}</div>`
                      }
                    </div>
                    <div class="flex-1 min-w-0">
                      <div class="flex items-start justify-between gap-2">
                        <div>
                          <p class="font-semibold text-slate-800">${p.userName}</p>
                          <p class="text-sm text-slate-500">${p.nim} • ${p.institution}</p>
                          ${p.major ? `<p class="text-xs text-slate-400 mt-1">${p.major}</p>` : ''}
                        </div>
                        <button onclick="viewParticipantDetail('${p.__backendId}')" class="px-3 py-1 bg-sky-100 text-sky-700 rounded-lg text-xs font-medium hover:bg-sky-200 transition-all flex-shrink-0">
                          Detail
                        </button>
                      </div>
                      <div class="flex flex-wrap gap-2 mt-3">
                        ${p.email ? `
                          <span class="inline-flex items-center gap-1 text-xs text-slate-600">
                            <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
                            </svg>
                            ${p.email}
                          </span>
                        ` : ''}
                        ${p.phone ? `
                          <span class="inline-flex items-center gap-1 text-xs text-slate-600">
                            <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/>
                            </svg>
                            ${p.phone}
                          </span>
                        ` : ''}
                      </div>
                      <div class="flex items-center gap-2 mt-2 text-xs text-slate-500">
                        <span>📅 ${formatDate(new Date(p.startDate))} - ${formatDate(new Date(p.endDate))}</span>
                        ${p.supervisor ? `<span>• 👨‍🏫 ${p.supervisor}</span>` : ''}
                      </div>
                    </div>
                  </div>
                `).join('')}
              </div>
            ` : '<p class="text-slate-500 text-center py-4">Belum ada peserta magang terdaftar</p>'}
          </div>
          </div>

          <!-- SECTION: SUPERVISORS -->
          <div id="supervisorsSection" class="hidden">
            <div class="flex items-center justify-end mb-4">
              <button onclick="showSupervisorForm()" class="gradient-primary text-white px-6 py-3 rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200 flex items-center gap-2">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
                </svg>
                Tambah Pembimbing
              </button>
            </div>

            <div id="supervisorFormContainer" class="hidden mb-6">
              <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
                <h3 class="font-semibold text-slate-800 mb-4">Form Pendaftaran Pembimbing Baru</h3>
                <div class="space-y-4">
                  <div class="grid md:grid-cols-2 gap-4">
                    <div>
                      <label class="block text-sm font-medium text-slate-700 mb-2">Nama Lengkap *</label>
                      <input type="text" id="supervisorName" placeholder="Nama lengkap" 
                        class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    </div>
                    <div>
                      <label class="block text-sm font-medium text-slate-700 mb-2">NIP *</label>
                      <input type="text" id="supervisorNip" placeholder="Nomor Induk Pegawai" 
                        class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    </div>
                  </div>

                  <div class="grid md:grid-cols-2 gap-4">
                    <div>
                      <label class="block text-sm font-medium text-slate-700 mb-2">Email *</label>
                      <input type="email" id="supervisorEmail" placeholder="email@example.com" 
                        class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    </div>
                    <div>
                      <label class="block text-sm font-medium text-slate-700 mb-2">No. Telepon *</label>
                      <input type="tel" id="supervisorPhone" placeholder="08xx-xxxx-xxxx" 
                        class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    </div>
                  </div>

                  <div class="grid md:grid-cols-2 gap-4">
                    <div>
                      <label class="block text-sm font-medium text-slate-700 mb-2">Jabatan</label>
                      <input type="text" id="supervisorPosition" placeholder="Jabatan" 
                        class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    </div>
                    <div>
                      <label class="block text-sm font-medium text-slate-700 mb-2">Bidang/Unit Kerja</label>
                      <input type="text" id="supervisorDepartment" placeholder="Bidang/Unit" 
                        class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    </div>
                  </div>

                  <div class="flex gap-3 pt-2">
                    <button onclick="submitSupervisor()" class="flex-1 gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all">
                      💾 Simpan Data Pembimbing
                    </button>
                    <button onclick="hideSupervisorForm()" class="px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
                      Batal
                    </button>
                  </div>
                </div>
              </div>
            </div>

            <!-- Daftar Pembimbing -->
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <div class="flex items-center justify-between mb-4">
                <h3 class="font-semibold text-slate-800">Daftar Pembimbing</h3>
                <span class="text-sm text-slate-500">${supervisors.length} pembimbing</span>
              </div>
              ${supervisors.length > 0 ? `
                <div class="space-y-3">
                  ${supervisors.map(s => `
                    <div class="flex items-center justify-between p-4 bg-slate-50 rounded-xl hover:bg-slate-100 transition-all">
                      <div class="flex items-center gap-3">
                        <div class="w-12 h-12 bg-gradient-to-br from-purple-400 to-indigo-500 rounded-full flex items-center justify-center text-white font-bold">
                          ${s.userName?.charAt(0) || 'P'}
                        </div>
                        <div>
                          <p class="font-semibold text-slate-800">${s.userName}</p>
                          <p class="text-sm text-slate-500">${s.nip || 'NIP belum diisi'}</p>
                          ${s.position ? `<p class="text-xs text-slate-400">${s.position}${s.department ? ' • ' + s.department : ''}</p>` : ''}
                        </div>
                      </div>
                      <div class="flex flex-col items-end gap-1">
                        ${s.email ? `<span class="text-xs text-slate-600">📧 ${s.email}</span>` : ''}
                        ${s.phone ? `<span class="text-xs text-slate-600">📱 ${s.phone}</span>` : ''}
                      </div>
                    </div>
                  `).join('')}
                </div>
              ` : '<p class="text-slate-500 text-center py-4">Belum ada pembimbing terdaftar</p>'}
            </div>
          </div>
        </div>

        <!-- Detail Modal -->
        <div id="participantDetailModal" class="fixed inset-0 z-[100] hidden items-center justify-center p-4 bg-black/70">
          <div class="bg-white rounded-2xl w-full max-w-2xl max-h-[90vh] overflow-y-auto">
            <div class="sticky top-0 bg-white p-4 border-b border-slate-100 flex items-center justify-between z-10">
              <h3 class="font-semibold text-slate-800">Detail Peserta Magang</h3>
              <button onclick="closeParticipantDetail()" class="p-2 hover:bg-slate-100 rounded-lg transition-colors">
                <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                </svg>
              </button>
            </div>
            <div id="participantDetailContent" class="p-6">
              <!-- Content will be populated by JS -->
            </div>
          </div>
        </div>
      `;
    }

    let participantPhotoData = null;

    function showParticipantForm() {
      document.getElementById('participantFormContainer').classList.remove('hidden');
      // Set default dates
      const today = new Date().toISOString().split('T')[0];
      document.getElementById('participantStartDate').value = today;
      const threeMonthsLater = new Date();
      threeMonthsLater.setMonth(threeMonthsLater.getMonth() + 3);
      document.getElementById('participantEndDate').value = threeMonthsLater.toISOString().split('T')[0];
      
      // Populate supervisor options
      const supervisors = allData.filter(d => d.type === 'supervisor');
      const supervisorSelect = document.getElementById('participantSupervisor');
      supervisorSelect.innerHTML = '<option value="">Pilih pembimbing</option>' +
        supervisors.map(s => `<option value="${s.userName}">${s.userName}</option>`).join('');
    }

    function hideParticipantForm() {
      document.getElementById('participantFormContainer').classList.add('hidden');
      // Clear form
      document.getElementById('participantName').value = '';
      document.getElementById('participantNim').value = '';
      document.getElementById('participantEmail').value = '';
      document.getElementById('participantPhone').value = '';
      document.getElementById('participantInstitution').value = '';
      document.getElementById('participantMajor').value = '';
      document.getElementById('participantAddress').value = '';
      document.getElementById('participantSupervisor').value = '';
      participantPhotoData = null;
      document.getElementById('participantPhotoPreview').innerHTML = `
        <svg class="w-12 h-12 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"/>
        </svg>
      `;
    }

    function handleParticipantPhoto(photoData) {
      participantPhotoData = photoData;
      document.getElementById('participantPhotoPreview').innerHTML = `
        <img src="${photoData}" class="w-full h-full object-cover" alt="Preview">
      `;
    }

    async function submitParticipant() {
      const name = document.getElementById('participantName').value.trim();
      const nim = document.getElementById('participantNim').value.trim();
      const email = document.getElementById('participantEmail').value.trim();
      const phone = document.getElementById('participantPhone').value.trim();
      const institution = document.getElementById('participantInstitution').value.trim();
      const major = document.getElementById('participantMajor').value.trim();
      const address = document.getElementById('participantAddress').value.trim();
      const startDate = document.getElementById('participantStartDate').value;
      const endDate = document.getElementById('participantEndDate').value;
      const supervisor = document.getElementById('participantSupervisor').value;

      // Validation
      if (!name || !nim || !email || !phone || !institution || !address || !startDate || !endDate || !supervisor) {
        showToast('Lengkapi semua field yang wajib diisi (*)', 'error');
        return;
      }

      if (allData.filter(d => d.type === 'participant').length >= 999) {
        showToast('Batas maksimum 999 peserta tercapai', 'error');
        return;
      }

      // Check duplicate NIM
      const existingNim = allData.find(d => d.type === 'participant' && d.nim === nim);
      if (existingNim) {
        showToast('NIM/NIS sudah terdaftar', 'error');
        return;
      }

      const result = await window.dataSdk.create({
        type: 'participant',
        userId: 'participant_' + Date.now(),
        userName: name,
        userRole: 'mahasiswa',
        nim: nim,
        email: email,
        phone: phone,
        institution: institution,
        major: major,
        address: address,
        startDate: startDate,
        endDate: endDate,
        supervisor: supervisor,
        profilePhoto: participantPhotoData,
        createdAt: new Date().toISOString()
      });

      if (result.isOk) {
        showToast('Peserta berhasil ditambahkan!', 'success');
        hideParticipantForm();
      } else {
        showToast('Gagal menambahkan peserta', 'error');
      }
    }

    // ====== SUPERVISOR MANAGEMENT ======
    function showSupervisorForm() {
      document.getElementById('supervisorFormContainer').classList.remove('hidden');
    }

    function hideSupervisorForm() {
      document.getElementById('supervisorFormContainer').classList.add('hidden');
      document.getElementById('supervisorName').value = '';
      document.getElementById('supervisorNip').value = '';
      document.getElementById('supervisorEmail').value = '';
      document.getElementById('supervisorPhone').value = '';
      document.getElementById('supervisorPosition').value = '';
      document.getElementById('supervisorDepartment').value = '';
    }

    async function submitSupervisor() {
      const name = document.getElementById('supervisorName').value.trim();
      const nip = document.getElementById('supervisorNip').value.trim();
      const email = document.getElementById('supervisorEmail').value.trim();
      const phone = document.getElementById('supervisorPhone').value.trim();
      const position = document.getElementById('supervisorPosition').value.trim();
      const department = document.getElementById('supervisorDepartment').value.trim();

      // Validation
      if (!name || !nip || !email || !phone) {
        showToast('Lengkapi semua field yang wajib diisi (*)', 'error');
        return;
      }

      if (allData.filter(d => d.type === 'supervisor').length >= 999) {
        showToast('Batas maksimum 999 pembimbing tercapai', 'error');
        return;
      }

      // Check duplicate NIP
      const existingNip = allData.find(d => d.type === 'supervisor' && d.nip === nip);
      if (existingNip) {
        showToast('NIP sudah terdaftar', 'error');
        return;
      }

      const result = await window.dataSdk.create({
        type: 'supervisor',
        userId: 'supervisor_' + Date.now(),
        userName: name,
        userRole: 'pembimbing',
        nip: nip,
        email: email,
        phone: phone,
        position: position,
        department: department,
        createdAt: new Date().toISOString()
      });

      if (result.isOk) {
        showToast('Pembimbing berhasil ditambahkan!', 'success');
        hideSupervisorForm();
      } else {
        showToast('Gagal menambahkan pembimbing', 'error');
      }
    }

    function viewParticipantDetail(id) {
      const participant = allData.find(d => d.__backendId === id);
      if (!participant) return;

      const modal = document.getElementById('participantDetailModal');
      const content = document.getElementById('participantDetailContent');

      // Get participant stats
      const attendance = allData.filter(d => d.type === 'attendance' && d.userId === participant.userId);
      const activities = allData.filter(d => d.type === 'activity' && d.userId === participant.userId);
      const evaluation = allData.find(d => d.type === 'evaluation' && d.userId === participant.userId);

      content.innerHTML = `
        <div class="space-y-6">
          <!-- Profile -->
          <div class="flex items-center gap-4">
            <div class="w-24 h-24 rounded-full overflow-hidden bg-gradient-to-br from-sky-400 to-cyan-500 flex-shrink-0">
              ${participant.profilePhoto ? 
                `<img src="${participant.profilePhoto}" class="w-full h-full object-cover" alt="${participant.userName}">` : 
                `<div class="w-full h-full flex items-center justify-center text-white font-bold text-3xl">${participant.userName?.charAt(0) || 'U'}</div>`
              }
            </div>
            <div>
              <h3 class="text-2xl font-bold text-slate-800">${participant.userName}</h3>
              <p class="text-slate-500">${participant.nim}</p>
              <span class="inline-block mt-2 px-3 py-1 bg-green-100 text-green-700 text-sm rounded-full">Aktif</span>
            </div>
          </div>

          <!-- Info Cards -->
          <div class="grid md:grid-cols-3 gap-4">
            <div class="bg-slate-50 rounded-xl p-4 text-center">
              <p class="text-2xl font-bold text-slate-800">${attendance.length}</p>
              <p class="text-sm text-slate-500 mt-1">Total Kehadiran</p>
            </div>
            <div class="bg-slate-50 rounded-xl p-4 text-center">
              <p class="text-2xl font-bold text-slate-800">${activities.filter(a => a.activityStatus === 'approved').length}</p>
              <p class="text-sm text-slate-500 mt-1">Aktivitas Disetujui</p>
            </div>
            <div class="bg-slate-50 rounded-xl p-4 text-center">
              <p class="text-2xl font-bold text-slate-800">${evaluation ? evaluation.evaluationScore : '-'}</p>
              <p class="text-sm text-slate-500 mt-1">Skor Evaluasi</p>
            </div>
          </div>

          <!-- Personal Info -->
          <div>
            <h4 class="font-semibold text-slate-800 mb-3">Informasi Pribadi</h4>
            <div class="space-y-2">
              <div class="flex justify-between py-2 border-b border-slate-100">
                <span class="text-slate-500">Email</span>
                <span class="text-slate-800 font-medium">${participant.email}</span>
              </div>
              <div class="flex justify-between py-2 border-b border-slate-100">
                <span class="text-slate-500">Telepon</span>
                <span class="text-slate-800 font-medium">${participant.phone}</span>
              </div>
              <div class="flex justify-between py-2 border-b border-slate-100">
                <span class="text-slate-500">Alamat</span>
                <span class="text-slate-800 font-medium text-right">${participant.address}</span>
              </div>
            </div>
          </div>

          <!-- Education Info -->
          <div>
            <h4 class="font-semibold text-slate-800 mb-3">Informasi Pendidikan</h4>
            <div class="space-y-2">
              <div class="flex justify-between py-2 border-b border-slate-100">
                <span class="text-slate-500">Institusi</span>
                <span class="text-slate-800 font-medium">${participant.institution}</span>
              </div>
              ${participant.major ? `
                <div class="flex justify-between py-2 border-b border-slate-100">
                  <span class="text-slate-500">Jurusan</span>
                  <span class="text-slate-800 font-medium">${participant.major}</span>
                </div>
              ` : ''}
            </div>
          </div>

          <!-- Internship Info -->
          <div>
            <h4 class="font-semibold text-slate-800 mb-3">Informasi Magang</h4>
            <div class="space-y-2">
              <div class="flex justify-between py-2 border-b border-slate-100">
                <span class="text-slate-500">Periode</span>
                <span class="text-slate-800 font-medium">${formatDate(new Date(participant.startDate))} - ${formatDate(new Date(participant.endDate))}</span>
              </div>
              ${participant.supervisor ? `
                <div class="flex justify-between py-2 border-b border-slate-100">
                  <span class="text-slate-500">Pembimbing</span>
                  <span class="text-slate-800 font-medium">${participant.supervisor}</span>
                </div>
              ` : ''}
              <div class="flex justify-between py-2 border-b border-slate-100">
                <span class="text-slate-500">Terdaftar Sejak</span>
                <span class="text-slate-800 font-medium">${formatDate(new Date(participant.createdAt))}</span>
              </div>
            </div>
          </div>
        </div>
      `;

      modal.classList.remove('hidden');
      modal.classList.add('flex');
    }

    function closeParticipantDetail() {
      const modal = document.getElementById('participantDetailModal');
      modal.classList.add('hidden');
      modal.classList.remove('flex');
    }

    // ====== LAPORAN ======
    function renderLaporan(content) {
      const allAttendance = allData.filter(d => d.type === 'attendance');
      const allActivities = allData.filter(d => d.type === 'activity');
      const evaluations = allData.filter(d => d.type === 'evaluation');

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div>
            <h2 class="text-2xl font-bold text-slate-800">Laporan & Rekap 📄</h2>
            <p class="text-slate-500 mt-1">Download laporan absensi dan evaluasi</p>
          </div>

          <div class="grid md:grid-cols-2 gap-4">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <div class="w-12 h-12 gradient-primary rounded-xl flex items-center justify-center mb-4">
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>
                </svg>
              </div>
              <h3 class="font-semibold text-slate-800 mb-2">Rekap Absensi</h3>
              <p class="text-sm text-slate-500 mb-4">Total ${allAttendance.length} data kehadiran</p>
              <button onclick="downloadReport('attendance')" class="w-full py-2 border-2 border-sky-500 text-sky-500 rounded-xl font-medium hover:bg-sky-50 transition-all">
                📥 Download CSV
              </button>
            </div>

            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <div class="w-12 h-12 gradient-success rounded-xl flex items-center justify-center mb-4">
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"/>
                </svg>
              </div>
              <h3 class="font-semibold text-slate-800 mb-2">Rekap Aktivitas</h3>
              <p class="text-sm text-slate-500 mb-4">Total ${allActivities.length} aktivitas tercatat</p>
              <button onclick="downloadReport('activities')" class="w-full py-2 border-2 border-green-500 text-green-500 rounded-xl font-medium hover:bg-green-50 transition-all">
                📥 Download CSV
              </button>
            </div>

            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <div class="w-12 h-12 gradient-warning rounded-xl flex items-center justify-center mb-4">
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/>
                </svg>
              </div>
              <h3 class="font-semibold text-slate-800 mb-2">Rekap Evaluasi</h3>
              <p class="text-sm text-slate-500 mb-4">Total ${evaluations.length} evaluasi</p>
              <button onclick="downloadReport('evaluations')" class="w-full py-2 border-2 border-amber-500 text-amber-500 rounded-xl font-medium hover:bg-amber-50 transition-all">
                📥 Download CSV
              </button>
            </div>

            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <div class="w-12 h-12 bg-gradient-to-br from-purple-500 to-indigo-600 rounded-xl flex items-center justify-center mb-4">
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>
                </svg>
              </div>
              <h3 class="font-semibold text-slate-800 mb-2">Laporan Lengkap</h3>
              <p class="text-sm text-slate-500 mb-4">Semua data dalam satu file</p>
              <button onclick="downloadReport('all')" class="w-full py-2 border-2 border-purple-500 text-purple-500 rounded-xl font-medium hover:bg-purple-50 transition-all">
                📥 Download CSV
              </button>
            </div>
          </div>
        </div>
      `;
    }

    function downloadReport(type) {
      let data = [];
      let filename = '';
      let headers = [];

      switch(type) {
        case 'attendance':
          headers = ['Tanggal', 'Nama', 'Jam Masuk', 'Jam Pulang', 'Status'];
          data = allData.filter(d => d.type === 'attendance').map(a => [
            a.date, a.userName, a.checkInTime || '-', a.checkOutTime || '-', a.isLate ? 'Terlambat' : 'Tepat Waktu'
          ]);
          filename = 'rekap_absensi.csv';
          break;
        case 'activities':
          headers = ['Tanggal', 'Nama', 'Aktivitas', 'Status', 'Catatan'];
          data = allData.filter(d => d.type === 'activity').map(a => [
            formatDate(new Date(a.createdAt)), a.userName, a.activity, getStatusLabel(a.activityStatus), a.activityNote || '-'
          ]);
          filename = 'rekap_aktivitas.csv';
          break;
        case 'evaluations':
          headers = ['Nama', 'Disiplin', 'Tanggung Jawab', 'Keterampilan', 'Kerjasama', 'Skor Total', 'Catatan'];
          data = allData.filter(d => d.type === 'evaluation').map(e => [
            e.userName, e.evaluationDiscipline, e.evaluationResponsibility, e.evaluationSkill, e.evaluationTeamwork, e.evaluationScore, e.evaluationNote || '-'
          ]);
          filename = 'rekap_evaluasi.csv';
          break;
        case 'all':
          headers = ['Tipe', 'Tanggal', 'Nama', 'Detail'];
          data = allData.map(d => {
            if (d.type === 'attendance') return ['Absensi', d.date, d.userName, `Masuk: ${d.checkInTime || '-'}, Pulang: ${d.checkOutTime || '-'}`];
            if (d.type === 'activity') return ['Aktivitas', formatDate(new Date(d.createdAt)), d.userName, d.activity];
            if (d.type === 'evaluation') return ['Evaluasi', formatDate(new Date(d.createdAt)), d.userName, `Skor: ${d.evaluationScore}`];
            return ['Lainnya', formatDate(new Date(d.createdAt)), d.userName || '-', '-'];
          });
          filename = 'laporan_lengkap.csv';
          break;
      }

      const csvContent = [headers.join(','), ...data.map(row => row.map(cell => `"${cell}"`).join(','))].join('\n');
      const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
      const link = document.createElement('a');
      link.href = URL.createObjectURL(blob);
      link.download = filename;
      link.click();
      
      showToast('Laporan berhasil diunduh!', 'success');
    }

    // ====== PENGUMUMAN ======
    function renderPengumuman(content) {
      const announcements = allData.filter(d => d.type === 'announcement')
        .sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

      const canCreate = currentUser.role === 'pembimbing' || currentUser.role === 'admin';

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-bold text-slate-800">Pengumuman 📢</h2>
              <p class="text-slate-500 mt-1">Informasi penting untuk peserta magang</p>
            </div>
            ${canCreate ? `
              <button onclick="showAnnouncementForm()" class="gradient-primary text-white px-6 py-3 rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200 flex items-center gap-2">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
                </svg>
                Buat Pengumuman
              </button>
            ` : ''}
          </div>

          ${canCreate ? `
            <div id="announcementFormContainer" class="hidden">
              <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
                <h3 class="font-semibold text-slate-800 mb-4">Buat Pengumuman Baru</h3>
                <div class="space-y-4">
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Judul</label>
                    <input type="text" id="announcementTitle" placeholder="Judul pengumuman" 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Isi Pengumuman</label>
                    <textarea id="announcementContent" rows="4" placeholder="Tulis pengumuman..." 
                      class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none resize-none"></textarea>
                  </div>
                  <div class="flex gap-3">
                    <button onclick="submitAnnouncement()" class="flex-1 gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all">
                      Publikasikan
                    </button>
                    <button onclick="hideAnnouncementForm()" class="px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
                      Batal
                    </button>
                  </div>
                </div>
              </div>
            </div>
          ` : ''}

          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-4">Daftar Pengumuman</h3>
            ${announcements.length > 0 ? `
              <div class="space-y-4">
                ${announcements.map(a => `
                  <div class="p-4 bg-slate-50 rounded-xl border-l-4 border-sky-500">
                    <h4 class="font-semibold text-slate-800">${a.announcementTitle}</h4>
                    <p class="text-slate-600 mt-2">${a.announcementContent}</p>
                    <p class="text-xs text-slate-400 mt-3">${formatDateTime(new Date(a.createdAt))}</p>
                  </div>
                `).join('')}
              </div>
            ` : '<p class="text-slate-500 text-center py-4">Belum ada pengumuman</p>'}
          </div>
        </div>
      `;
    }

    function showAnnouncementForm() {
      document.getElementById('announcementFormContainer').classList.remove('hidden');
    }

    function hideAnnouncementForm() {
      document.getElementById('announcementFormContainer').classList.add('hidden');
      document.getElementById('announcementTitle').value = '';
      document.getElementById('announcementContent').value = '';
    }

    async function submitAnnouncement() {
      const title = document.getElementById('announcementTitle').value.trim();
      const content = document.getElementById('announcementContent').value.trim();
      
      if (!title || !content) {
        showToast('Lengkapi judul dan isi pengumuman', 'error');
        return;
      }

      const result = await window.dataSdk.create({
        type: 'announcement',
        userId: currentUser.id,
        userName: currentUser.name,
        userRole: currentUser.role,
        announcementTitle: title,
        announcementContent: content,
        createdAt: new Date().toISOString()
      });

      if (result.isOk) {
        showToast('Pengumuman berhasil dipublikasikan!', 'success');
        hideAnnouncementForm();
      } else {
        showToast('Gagal membuat pengumuman', 'error');
      }
    }

    // ====== PESAN ======
    function renderPesan(content) {
      const myMessages = allData.filter(d => 
        d.type === 'message' && 
        (d.messageFrom === currentUser.id || d.messageTo === currentUser.id)
      ).sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

      const uniqueUsers = [...new Set(allData.filter(d => d.userId && d.userId !== currentUser.id).map(a => JSON.stringify({ id: a.userId, name: a.userName })))].map(s => JSON.parse(s));

      content.innerHTML = `
        <div class="space-y-6 fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-bold text-slate-800">Pesan Internal 💬</h2>
              <p class="text-slate-500 mt-1">Komunikasi dengan pembimbing/peserta magang</p>
            </div>
            <button onclick="showMessageForm()" class="gradient-primary text-white px-6 py-3 rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200 flex items-center gap-2">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
              </svg>
              Tulis Pesan
            </button>
          </div>

          <div id="messageFormContainer" class="hidden">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
              <h3 class="font-semibold text-slate-800 mb-4">Kirim Pesan Baru</h3>
              <div class="space-y-4">
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Kepada</label>
                  <select id="messageTo" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none">
                    <option value="">Pilih penerima</option>
                    ${uniqueUsers.map(u => `<option value="${u.id}">${u.name}</option>`).join('')}
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-slate-700 mb-2">Pesan</label>
                  <textarea id="messageContent" rows="4" placeholder="Tulis pesan..." 
                    class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 transition-all outline-none resize-none"></textarea>
                </div>
                <div class="flex gap-3">
                  <button onclick="sendMessage()" class="flex-1 gradient-primary text-white py-3 rounded-xl font-semibold hover:opacity-90 transition-all">
                    Kirim
                  </button>
                  <button onclick="hideMessageForm()" class="px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
                    Batal
                  </button>
                </div>
              </div>
            </div>
          </div>

          <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
            <h3 class="font-semibold text-slate-800 mb-4">Riwayat Pesan</h3>
            ${myMessages.length > 0 ? `
              <div class="space-y-3">
                ${myMessages.map(m => {
                  const isFromMe = m.messageFrom === currentUser.id;
                  const otherUser = allData.find(d => d.userId === (isFromMe ? m.messageTo : m.messageFrom));
                  return `
                    <div class="p-4 rounded-xl ${isFromMe ? 'bg-sky-50 ml-8' : 'bg-slate-50 mr-8'}">
                      <div class="flex items-center gap-2 mb-2">
                        <span class="text-xs ${isFromMe ? 'text-sky-600' : 'text-slate-600'}">${isFromMe ? 'Anda →' : '←'} ${otherUser?.userName || 'Unknown'}</span>
                      </div>
                      <p class="text-slate-800">${m.messageContent}</p>
                      <p class="text-xs text-slate-400 mt-2">${formatDateTime(new Date(m.createdAt))}</p>
                    </div>
                  `;
                }).join('')}
              </div>
            ` : '<p class="text-slate-500 text-center py-4">Belum ada pesan</p>'}
          </div>
        </div>
      `;
    }

    function showMessageForm() {
      document.getElementById('messageFormContainer').classList.remove('hidden');
    }

    function hideMessageForm() {
      document.getElementById('messageFormContainer').classList.add('hidden');
      document.getElementById('messageTo').value = '';
      document.getElementById('messageContent').value = '';
    }

    async function sendMessage() {
      const to = document.getElementById('messageTo').value;
      const content = document.getElementById('messageContent').value.trim();
      
      if (!to || !content) {
        showToast('Pilih penerima dan tulis pesan', 'error');
        return;
      }

      const toUser = allData.find(d => d.userId === to);

      const result = await window.dataSdk.create({
        type: 'message',
        userId: currentUser.id,
        userName: currentUser.name,
        userRole: currentUser.role,
        messageFrom: currentUser.id,
        messageTo: to,
        messageContent: content,
        createdAt: new Date().toISOString()
      });

      if (result.isOk) {
        showToast('Pesan berhasil dikirim!', 'success');
        hideMessageForm();
      } else {
        showToast('Gagal mengirim pesan', 'error');
      }
    }

    // ====== CAMERA MODAL ======
    function openCameraModal(callback) {
      photoCallback = callback;
      const modal = document.getElementById('cameraModal');
      modal.classList.remove('hidden');
      modal.classList.add('flex');
      startCamera();
    }

    function closeCameraModal() {
      const modal = document.getElementById('cameraModal');
      modal.classList.add('hidden');
      modal.classList.remove('flex');
      stopCamera();
      resetCameraUI();
    }

    async function startCamera() {
      try {
        cameraStream = await navigator.mediaDevices.getUserMedia({ 
          video: { facingMode: 'user', width: 640, height: 480 } 
        });
        const video = document.getElementById('cameraVideo');
        video.srcObject = cameraStream;
      } catch (err) {
        showToast('Tidak dapat mengakses kamera: ' + err.message, 'error');
        closeCameraModal();
      }
    }

    function stopCamera() {
      if (cameraStream) {
        cameraStream.getTracks().forEach(track => track.stop());
        cameraStream = null;
      }
    }

    function capturePhoto() {
      const video = document.getElementById('cameraVideo');
      const canvas = document.getElementById('cameraCanvas');
      const photo = document.getElementById('capturedPhoto');
      
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      
      const ctx = canvas.getContext('2d');
      ctx.translate(canvas.width, 0);
      ctx.scale(-1, 1);
      ctx.drawImage(video, 0, 0);
      
      capturedPhotoData = canvas.toDataURL('image/jpeg', 0.8);
      
      photo.src = capturedPhotoData;
      photo.classList.remove('hidden');
      video.classList.add('hidden');
      document.getElementById('cameraOverlay').classList.add('hidden');
      document.getElementById('captureBtn').classList.add('hidden');
      document.getElementById('retakeBtn').classList.remove('hidden');
      document.getElementById('usePhotoBtn').classList.remove('hidden');
    }

    function retakePhoto() {
      resetCameraUI();
      capturedPhotoData = null;
    }

    function resetCameraUI() {
      document.getElementById('cameraVideo').classList.remove('hidden');
      document.getElementById('capturedPhoto').classList.add('hidden');
      document.getElementById('cameraOverlay').classList.remove('hidden');
      document.getElementById('captureBtn').classList.remove('hidden');
      document.getElementById('retakeBtn').classList.add('hidden');
      document.getElementById('usePhotoBtn').classList.add('hidden');
    }

    function usePhoto() {
      if (photoCallback && capturedPhotoData) {
        photoCallback(capturedPhotoData);
      }
      closeCameraModal();
    }

    // ====== UTILITY FUNCTIONS ======
    function calculateDistance(lat1, lon1, lat2, lon2) {
      const R = 6371e3; // Earth's radius in meters
      const φ1 = lat1 * Math.PI / 180;
      const φ2 = lat2 * Math.PI / 180;
      const Δφ = (lat2 - lat1) * Math.PI / 180;
      const Δλ = (lon2 - lon1) * Math.PI / 180;

      const a = Math.sin(Δφ / 2) * Math.sin(Δφ / 2) +
                Math.cos(φ1) * Math.cos(φ2) *
                Math.sin(Δλ / 2) * Math.sin(Δλ / 2);
      const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));

      return R * c; // Distance in meters
    }

    function formatDate(date) {
      return date.toLocaleDateString('id-ID', { 
        weekday: 'long', 
        year: 'numeric', 
        month: 'long', 
        day: 'numeric' 
      });
    }

    function formatDateTime(date) {
      return date.toLocaleDateString('id-ID', { 
        day: 'numeric',
        month: 'short',
        year: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
      });
    }

    function getStatusColor(status) {
      switch(status) {
        case 'approved': return 'bg-green-100 text-green-700';
        case 'rejected': return 'bg-red-100 text-red-700';
        case 'pending': return 'bg-amber-100 text-amber-700';
        default: return 'bg-slate-100 text-slate-700';
      }
    }

    function getStatusLabel(status) {
      switch(status) {
        case 'approved': return 'Disetujui';
        case 'rejected': return 'Ditolak';
        case 'pending': return 'Menunggu';
        default: return status;
      }
    }

    function showToast(message, type = 'info') {
      const container = document.getElementById('toastContainer');
      const toast = document.createElement('div');
      
      const colors = {
        success: 'bg-green-500',
        error: 'bg-red-500',
        warning: 'bg-amber-500',
        info: 'bg-sky-500'
      };

      toast.className = `${colors[type]} text-white px-4 py-3 rounded-xl shadow-lg flex items-center gap-2 fade-in`;
      toast.innerHTML = `
        <span>${message}</span>
      `;
      
      container.appendChild(toast);
      
      setTimeout(() => {
        toast.style.opacity = '0';
        toast.style.transform = 'translateX(100px)';
        toast.style.transition = 'all 0.3s ease';
        setTimeout(() => toast.remove(), 300);
      }, 3000);
    }

    // ====== INIT ======
    document.addEventListener('DOMContentLoaded', () => {
      initApp();
      applyConfig();
      
      // Check for saved user
      const savedUser = localStorage.getItem('currentUser');
      if (savedUser) {
        currentUser = JSON.parse(savedUser);
        showMainApp();
      }
    });
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9c1d3d2f24c4fdb8',t:'MTc2OTA2NTkwNC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
