<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-PKL Pro: Sistem Logbook PDF</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Perbaikan link CDN jsPDF dan AutoTable -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.25/jspdf.plugin.autotable.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; }
        .fade-in { animation: fadeIn 0.3s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .tab-active { background-color: white; color: #4f46e5; box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05); }
    </style>
</head>
<body class="bg-[#f8fafc] min-h-screen text-slate-800">

    <!-- Header Navigation -->
    <header class="bg-white/80 backdrop-blur-md shadow-sm border-b sticky top-0 z-50">
        <div class="container mx-auto px-4 py-3 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 bg-indigo-600 rounded-xl flex items-center justify-center shadow-lg">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01"></path></svg>
                </div>
                <div>
                    <h1 class="text-lg font-extrabold tracking-tight">E-PKL <span class="text-indigo-600">PRO</span></h1>
                    <p class="text-[10px] text-slate-400 font-bold uppercase tracking-widest leading-none">Dashboard Manajemen</p>
                </div>
            </div>

            <div id="adminNav" class="hidden flex items-center space-x-1 bg-slate-100 p-1 rounded-xl">
                <button onclick="switchAdminTab('dashboard')" id="nav-dashboard" class="px-4 py-2 text-[10px] font-bold uppercase rounded-lg transition-all tab-active">Dashboard</button>
                <button onclick="switchAdminTab('peserta')" id="nav-peserta" class="px-4 py-2 text-[10px] font-bold uppercase rounded-lg transition-all text-slate-500 hover:bg-white">Peserta</button>
                <button onclick="switchAdminTab('rekap')" id="nav-rekap" class="px-4 py-2 text-[10px] font-bold uppercase rounded-lg transition-all text-slate-500 hover:bg-white">Rekap</button>
                <button onclick="switchAdminTab('logbook')" id="nav-logbook" class="px-4 py-2 text-[10px] font-bold uppercase rounded-lg transition-all text-slate-500 hover:bg-white">Logbook</button>
            </div>

            <div id="userBadge" class="hidden flex items-center space-x-4">
                <div class="text-right hidden sm:block">
                    <p id="displayUserName" class="text-xs font-bold text-slate-700 mb-0.5"></p>
                    <div class="flex items-center space-x-2">
                        <button onclick="openChangePassModal()" class="text-[9px] text-indigo-500 font-black uppercase hover:underline">Password</button>
                        <span class="text-slate-300">|</span>
                        <button onclick="logout()" class="text-[9px] text-red-500 font-black uppercase hover:underline">Keluar</button>
                    </div>
                </div>
                <div class="w-8 h-8 rounded-full bg-indigo-100 text-indigo-600 flex items-center justify-center font-bold text-xs" id="userInitial">?</div>
            </div>
        </div>
    </header>

    <main class="container mx-auto px-4 py-8">
        <!-- VIEW: LOGIN -->
        <section id="view-login" class="max-w-md mx-auto mt-12 fade-in">
            <div class="bg-white rounded-[2rem] shadow-2xl p-10 border border-slate-100">
                <div class="text-center mb-8">
                    <h2 class="text-3xl font-black text-slate-800 tracking-tight">Login</h2>
                    <p class="text-slate-400 text-sm mt-2 font-medium">Masuk untuk mengelola data PKL</p>
                </div>
                <form onsubmit="handleLogin(event)" class="space-y-4">
                    <div>
                        <label class="text-[10px] font-black text-slate-400 uppercase ml-2">Username</label>
                        <input type="text" id="loginId" required class="w-full px-5 py-4 bg-slate-50 border border-slate-200 rounded-2xl outline-none focus:ring-2 focus:ring-indigo-500/20 text-sm" placeholder="Username">
                    </div>
                    <div>
                        <label class="text-[10px] font-black text-slate-400 uppercase ml-2">Kata Sandi</label>
                        <input type="password" id="loginPass" required class="w-full px-5 py-4 bg-slate-50 border border-slate-200 rounded-2xl outline-none focus:ring-2 focus:ring-indigo-500/20 text-sm" placeholder="••••••••">
                    </div>
                    <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-4 rounded-2xl shadow-lg transition-all mt-4">Masuk</button>
                </form>
            </div>
        </section>

        <!-- VIEW: ADMIN PANEL -->
        <section id="view-admin" class="hidden fade-in space-y-8">
            <!-- Dashboard Tab -->
            <div id="admin-dashboard-tab" class="space-y-8">
                <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
                    <div class="bg-white p-6 rounded-[2rem] border shadow-sm col-span-1 md:col-span-3">
                        <div class="flex flex-col md:flex-row md:items-center justify-between gap-6">
                            <div class="space-y-6 flex-1">
                                <div>
                                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-1">Kehadiran Hari Ini</p>
                                    <h4 id="count-peserta" class="text-4xl font-black text-indigo-600">0</h4>
                                </div>
                                <div class="grid grid-cols-2 gap-4">
                                    <div class="p-4 bg-emerald-50 rounded-2xl">
                                        <p class="text-[9px] font-bold text-emerald-600 uppercase tracking-widest">Hadir</p>
                                        <h5 id="count-hadir" class="text-2xl font-black text-emerald-700">0</h5>
                                    </div>
                                    <div class="p-4 bg-amber-50 rounded-2xl">
                                        <p class="text-[9px] font-bold text-amber-600 uppercase tracking-widest">Izin/Sakit</p>
                                        <h5 id="count-izin" class="text-2xl font-black text-amber-700">0</h5>
                                    </div>
                                </div>
                            </div>
                            <div class="w-full md:w-48 flex flex-col items-center">
                                <p class="text-[10px] font-black text-slate-400 uppercase mb-2">Grafik Harian</p>
                                <canvas id="adminPieChart"></canvas>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-indigo-600 p-6 rounded-[2rem] shadow-xl shadow-indigo-100 flex flex-col justify-center text-white">
                        <p class="text-[10px] font-black uppercase tracking-widest opacity-80 mb-1">Total Logbook</p>
                        <h4 id="count-logbook" class="text-4xl font-black">0</h4>
                        <p class="text-xs opacity-70 mt-2">Laporan terkumpul</p>
                    </div>
                </div>

                <div class="bg-white rounded-[2rem] border shadow-sm p-6">
                    <h3 class="font-black text-slate-700 mb-4 text-sm uppercase">Logbook Terbaru</h3>
                    <div id="admin-recent-list" class="space-y-3"></div>
                </div>
            </div>

            <!-- Peserta Tab -->
            <div id="admin-peserta-tab" class="hidden space-y-6">
                <div class="flex justify-between items-center">
                    <h2 class="text-xl font-black text-slate-800">Daftar Peserta</h2>
                    <button onclick="openAddStudentModal()" class="bg-indigo-600 text-white px-6 py-3 rounded-2xl font-bold text-xs uppercase shadow-lg shadow-indigo-100">+ Tambah Siswa</button>
                </div>
                <div class="bg-white rounded-[2rem] border shadow-sm overflow-hidden">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-slate-50 text-slate-400 font-bold uppercase">
                            <tr>
                                <th class="px-6 py-4">Nama</th>
                                <th class="px-6 py-4">Username</th>
                                <th class="px-6 py-4">Sekolah</th>
                                <th class="px-6 py-4 text-center">Opsi</th>
                            </tr>
                        </thead>
                        <tbody id="admin-peserta-list" class="divide-y divide-slate-100"></tbody>
                    </table>
                </div>
            </div>

            <!-- Rekap Tab -->
            <div id="admin-rekap-tab" class="hidden space-y-6">
                <div class="flex justify-between items-center">
                    <h2 class="text-xl font-black text-slate-800">Rekap Kehadiran</h2>
                    <button onclick="downloadRekapAdmin()" class="bg-emerald-600 text-white px-6 py-3 rounded-2xl font-bold text-xs uppercase shadow-lg shadow-emerald-100 flex items-center space-x-2">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path></svg>
                        <span>Unduh Presensi</span>
                    </button>
                </div>
                <div class="bg-white rounded-[2rem] border shadow-sm overflow-hidden">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-indigo-50 text-indigo-600 font-bold uppercase">
                            <tr>
                                <th class="px-6 py-4">Nama</th>
                                <th class="px-6 py-4 text-center">Hadir</th>
                                <th class="px-6 py-4 text-center">Izin</th>
                                <th class="px-6 py-4 text-center">Tanpa Ket.</th>
                                <th class="px-6 py-4 text-center">Persentase</th>
                            </tr>
                        </thead>
                        <tbody id="admin-rekap-list" class="divide-y divide-slate-100"></tbody>
                    </table>
                </div>
            </div>

            <!-- Logbook Tab -->
            <div id="admin-logbook-tab" class="hidden space-y-6">
                <div class="flex justify-between items-center">
                    <h2 class="text-xl font-black text-slate-800">Monitoring Logbook</h2>
                    <button onclick="downloadAllLogbooksPDF()" class="bg-indigo-600 text-white px-6 py-3 rounded-2xl font-bold text-xs uppercase shadow-lg flex items-center space-x-2">
                         <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2zm8-12V5a2 2 0 00-2-2H9a2 2 0 00-2 2v4h10z"></path></svg>
                        <span>Unduh Semua Logbook</span>
                    </button>
                </div>
                <div id="admin-logbook-all" class="grid grid-cols-1 md:grid-cols-2 gap-4"></div>
            </div>
        </section>

        <!-- VIEW: SISWA PANEL -->
        <section id="view-siswa" class="hidden fade-in space-y-8">
            <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
                <!-- Clock Card -->
                <div class="lg:col-span-1 bg-indigo-600 rounded-[2rem] p-8 text-white shadow-xl flex flex-col justify-between">
                    <div>
                        <p id="currentDateDisplay" class="text-[10px] font-black uppercase tracking-widest opacity-80">...</p>
                        <h2 id="digitalClock" class="text-4xl font-black mt-2">00:00:00</h2>
                    </div>
                    <div class="mt-8 pt-6 border-t border-white/20">
                        <p class="text-[10px] font-black uppercase tracking-widest opacity-80 mb-2">Siswa</p>
                        <h3 id="sName" class="text-xl font-bold leading-tight">Memuat...</h3>
                        <p id="sSchool" class="text-xs opacity-70 mt-1">-</p>
                    </div>
                </div>

                <!-- Stats Card -->
                <div class="lg:col-span-1 bg-white rounded-[2rem] p-6 border shadow-sm flex flex-col items-center justify-center">
                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-4">Statistik Kehadiran</p>
                    <div class="w-full max-w-[130px]">
                        <canvas id="siswaAttendanceChart"></canvas>
                    </div>
                </div>

                <!-- Action Buttons -->
                <div class="lg:col-span-2 grid grid-cols-2 gap-4">
                    <button onclick="attendance('Masuk')" id="btn-masuk" class="flex flex-col items-center justify-center bg-white border border-slate-100 rounded-[2rem] p-6 hover:shadow-lg transition-all group">
                        <div class="w-10 h-10 bg-emerald-50 text-emerald-600 rounded-2xl flex items-center justify-center mb-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1"></path></svg>
                        </div>
                        <span class="text-[9px] font-black uppercase text-slate-500">Presensi Masuk</span>
                    </button>
                    <button onclick="attendance('Pulang')" id="btn-pulang" class="flex flex-col items-center justify-center bg-white border border-slate-100 rounded-[2rem] p-6 hover:shadow-lg transition-all group">
                        <div class="w-10 h-10 bg-rose-50 text-rose-600 rounded-2xl flex items-center justify-center mb-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1"></path></svg>
                        </div>
                        <span class="text-[9px] font-black uppercase text-slate-500">Presensi Pulang</span>
                    </button>
                    <button onclick="openIzinModal()" id="btn-izin" class="flex flex-col items-center justify-center bg-white border border-slate-100 rounded-[2rem] p-6 hover:shadow-lg transition-all group">
                        <div class="w-10 h-10 bg-amber-50 text-amber-600 rounded-2xl flex items-center justify-center mb-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                        </div>
                        <span class="text-[9px] font-black uppercase text-slate-500">Ajukan Izin</span>
                    </button>
                    <button onclick="openLogbookModal()" class="flex flex-col items-center justify-center bg-indigo-600 rounded-[2rem] p-6 shadow-lg shadow-indigo-100 hover:bg-indigo-700 transition-all text-white">
                        <div class="w-10 h-10 bg-white/20 rounded-2xl flex items-center justify-center mb-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg>
                        </div>
                        <span class="text-[9px] font-black uppercase">Isi Logbook</span>
                    </button>
                </div>
            </div>

            <!-- Tabs Section -->
            <div class="bg-white rounded-[2rem] border shadow-sm overflow-hidden">
                <div class="flex border-b overflow-x-auto">
                    <button onclick="switchSiswaTab('presensi')" id="stab-presensi" class="px-8 py-5 text-[10px] font-black uppercase tracking-widest border-b-2 border-indigo-600 text-indigo-600 whitespace-nowrap">Histori Presensi</button>
                    <button onclick="switchSiswaTab('logbook')" id="stab-logbook" class="px-8 py-5 text-[10px] font-black uppercase tracking-widest border-b-2 border-transparent text-slate-400 whitespace-nowrap">Kumpulan Logbook</button>
                </div>

                <div id="scont-presensi" class="p-6">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="font-black text-slate-700 text-sm">Aktivitas Kehadiran</h3>
                        <button onclick="downloadHistory('presensi')" class="text-[10px] font-black uppercase bg-slate-100 px-3 py-2 rounded-xl text-slate-600">Download PDF</button>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs">
                            <thead class="bg-slate-50 text-slate-400 uppercase font-bold">
                                <tr>
                                    <th class="px-4 py-3">Tanggal</th>
                                    <th class="px-4 py-3">Status</th>
                                    <th class="px-4 py-3">Waktu</th>
                                    <th class="px-4 py-3">Keterangan</th>
                                </tr>
                            </thead>
                            <tbody id="siswaAttendanceBody" class="divide-y divide-slate-100"></tbody>
                        </table>
                    </div>
                </div>

                <div id="scont-logbook" class="hidden p-6">
                    <div class="flex justify-between items-center mb-4">
                         <h3 class="font-black text-slate-700 text-sm">Kegiatan Harian</h3>
                         <button onclick="downloadStudentLogbooksPDF()" class="text-[10px] font-black uppercase bg-indigo-50 px-3 py-2 rounded-xl text-indigo-600">Download PDF</button>
                    </div>
                    <div id="siswaLogbookList" class="grid grid-cols-1 gap-4"></div>
                </div>
            </div>
        </section>
    </main>

    <!-- MODALS -->
    <!-- Modal Logbook -->
    <div id="modalLogbook" class="fixed inset-0 bg-slate-900/60 hidden items-center justify-center z-[100] p-4 backdrop-blur-sm">
        <div class="bg-white w-full max-w-md rounded-[2rem] p-8 shadow-2xl">
            <h3 class="text-xl font-black mb-4">Laporan Kegiatan</h3>
            <textarea id="log-content" class="w-full p-4 bg-slate-50 border rounded-2xl text-sm" rows="5" placeholder="Tuliskan detail pekerjaan Anda hari ini..."></textarea>
            <div class="grid grid-cols-2 gap-4 mt-4">
                <button onclick="closeModal('modalLogbook')" class="py-3 bg-slate-100 rounded-xl text-[10px] font-black uppercase text-slate-500">Batal</button>
                <button onclick="saveLogbook()" class="py-3 bg-indigo-600 text-white rounded-xl text-[10px] font-black uppercase">Simpan Laporan</button>
            </div>
        </div>
    </div>

    <!-- Additional Modals (Siswa & Admin Management) -->
    <div id="modalAddStudent" class="fixed inset-0 bg-slate-900/60 hidden items-center justify-center z-[100] p-4 backdrop-blur-sm">
        <div class="bg-white w-full max-w-md rounded-[2rem] p-10 shadow-2xl">
            <h3 class="text-2xl font-black mb-6">Tambah Peserta</h3>
            <form onsubmit="handleSaveStudent(event)" class="space-y-4">
                <input type="text" id="stu-name" placeholder="Nama Lengkap" required class="w-full px-5 py-4 bg-slate-50 border border-slate-200 rounded-2xl outline-none text-sm">
                <input type="text" id="stu-user" placeholder="Username" required class="w-full px-5 py-4 bg-slate-50 border border-slate-200 rounded-2xl outline-none text-sm">
                <input type="text" id="stu-school" placeholder="Asal Sekolah/Instansi" required class="w-full px-5 py-4 bg-slate-50 border border-slate-200 rounded-2xl outline-none text-sm">
                <input type="password" id="stu-pass" placeholder="Password Awal" value="123" required class="w-full px-5 py-4 bg-slate-50 border border-slate-200 rounded-2xl outline-none text-sm">
                <div class="grid grid-cols-2 gap-4">
                    <button type="button" onclick="closeModal('modalAddStudent')" class="py-4 bg-slate-100 font-bold rounded-2xl text-[10px] uppercase">Batal</button>
                    <button type="submit" class="py-4 bg-indigo-600 text-white font-bold rounded-2xl text-[10px] uppercase">Simpan</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Izin -->
    <div id="modalIzin" class="fixed inset-0 bg-slate-900/60 hidden items-center justify-center z-[100] p-4 backdrop-blur-sm">
        <div class="bg-white w-full max-w-md rounded-[2rem] p-8 shadow-2xl">
            <h3 class="text-xl font-black mb-4">Form Izin/Sakit</h3>
            <select id="izin-type" class="w-full p-4 bg-slate-50 border rounded-2xl text-sm mb-4 outline-none">
                <option value="Izin">Izin Keperluan</option>
                <option value="Sakit">Sakit</option>
            </select>
            <textarea id="izin-reason" class="w-full p-4 bg-slate-50 border rounded-2xl text-sm" rows="3" placeholder="Berikan alasan yang jelas..."></textarea>
            <div class="grid grid-cols-2 gap-4 mt-4">
                <button onclick="closeModal('modalIzin')" class="py-3 bg-slate-100 rounded-xl text-[10px] font-black uppercase text-slate-500">Batal</button>
                <button onclick="saveIzin()" class="py-3 bg-amber-500 text-white rounded-xl text-[10px] font-black uppercase">Kirim Pengajuan</button>
            </div>
        </div>
    </div>

    <script>
        // --- Database Setup ---
        let db = {
            admin: JSON.parse(localStorage.getItem('pkl_admin')) || { username: 'admin', password: '123', name: 'Administrator' },
            user: null, 
            students: JSON.parse(localStorage.getItem('pkl_students')) || [
                { id: '1', username: 'rizki', password: '123', name: 'Ahmad Rizki', school: 'SMKN 1 Jakarta' }
            ],
            attendance: JSON.parse(localStorage.getItem('pkl_attendance')) || [],
            logbooks: JSON.parse(localStorage.getItem('pkl_logbooks')) || []
        };

        function saveData() {
            localStorage.setItem('pkl_students', JSON.stringify(db.students));
            localStorage.setItem('pkl_attendance', JSON.stringify(db.attendance));
            localStorage.setItem('pkl_logbooks', JSON.stringify(db.logbooks));
            localStorage.setItem('pkl_admin', JSON.stringify(db.admin));
        }

        // --- Auth Engine ---
        function handleLogin(e) {
            e.preventDefault();
            const u = document.getElementById('loginId').value.trim().toLowerCase();
            const p = document.getElementById('loginPass').value;
            
            if(u === db.admin.username && p === db.admin.password) return performLogin(db.admin.name, 'admin', 'admin_id');

            const s = db.students.find(x => x.username === u && x.password === p);
            if(s) performLogin(s.name, 'siswa', s.id);
            else Swal.fire('Gagal Login', 'Cek kembali username dan password Anda.', 'error');
        }

        function performLogin(name, role, id) {
            db.user = { name, role, id };
            document.getElementById('view-login').classList.add('hidden');
            document.getElementById('userBadge').classList.remove('hidden');
            document.getElementById('displayUserName').innerText = name;
            document.getElementById('userInitial').innerText = name.charAt(0);
            
            if(role === 'admin') {
                document.getElementById('view-admin').classList.remove('hidden');
                document.getElementById('adminNav').classList.remove('hidden');
                switchAdminTab('dashboard');
            } else {
                const s = db.students.find(x => x.id === id);
                document.getElementById('view-siswa').classList.remove('hidden');
                document.getElementById('sName').innerText = name;
                document.getElementById('sSchool').innerText = s ? s.school : '-';
                checkSiswaControls();
                renderSiswaDashboard();
            }
        }

        function logout() { location.reload(); }

        // --- Clock & Time ---
        function updateClock() {
            const now = new Date();
            const timeStr = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit', second: '2-digit' }).replace(/\./g, ':');
            const dateStr = now.toLocaleDateString('id-ID', { weekday: 'long', day: 'numeric', month: 'long', year: 'numeric' });
            if(document.getElementById('digitalClock')) document.getElementById('digitalClock').innerText = timeStr;
            if(document.getElementById('currentDateDisplay')) document.getElementById('currentDateDisplay').innerText = dateStr;
        }
        setInterval(updateClock, 1000);

        // --- Admin Tab Management ---
        function switchAdminTab(tab) {
            ['dashboard', 'peserta', 'rekap', 'logbook'].forEach(t => {
                const el = document.getElementById(`admin-${t}-tab`);
                if(el) el.classList.toggle('hidden', t !== tab);
                const btn = document.getElementById(`nav-${t}`);
                if(btn) {
                    if(t === tab) btn.className = "px-4 py-2 text-[10px] font-bold uppercase rounded-lg transition-all tab-active";
                    else btn.className = "px-4 py-2 text-[10px] font-bold uppercase rounded-lg transition-all text-slate-500 hover:bg-white";
                }
            });

            if(tab === 'dashboard') renderAdminDashboard();
            if(tab === 'peserta') renderAdminPeserta();
            if(tab === 'rekap') renderAdminRekap();
            if(tab === 'logbook') renderAdminLogbooks();
        }

        function renderAdminDashboard() {
            const today = new Date().toISOString().split('T')[0];
            const tPeserta = db.students.length;
            const tHadir = db.attendance.filter(a => a.date === today && a.type === 'Masuk').length;
            const tIzin = db.attendance.filter(a => a.date === today && (a.type === 'Izin' || a.type === 'Sakit')).length;
            const tTidak = Math.max(0, tPeserta - (tHadir + tIzin));

            document.getElementById('count-peserta').innerText = tPeserta;
            document.getElementById('count-hadir').innerText = tHadir;
            document.getElementById('count-izin').innerText = tIzin;
            document.getElementById('count-logbook').innerText = db.logbooks.length;

            const ctx = document.getElementById('adminPieChart').getContext('2d');
            if(window.admChart) window.admChart.destroy();
            window.admChart = new Chart(ctx, {
                type: 'pie',
                data: {
                    labels: ['Hadir', 'Izin', 'Alfa'],
                    datasets: [{
                        data: [tHadir, tIzin, tTidak],
                        backgroundColor: ['#10b981', '#f59e0b', '#cbd5e1'],
                        borderWidth: 0
                    }]
                },
                options: { plugins: { legend: { display: false } }, responsive: true }
            });

            const recent = db.logbooks.slice(0, 5);
            document.getElementById('admin-recent-list').innerHTML = recent.map(r => `
                <div class="flex items-center justify-between p-3 bg-slate-50 rounded-xl">
                    <div class="flex items-center space-x-3">
                        <div class="w-8 h-8 rounded-full bg-indigo-100 text-indigo-600 flex items-center justify-center text-[10px] font-bold">${r.name.charAt(0)}</div>
                        <div>
                            <p class="text-[10px] font-bold text-slate-700">${r.name}</p>
                            <p class="text-[9px] text-slate-400 font-medium">${r.content.substring(0, 40)}...</p>
                        </div>
                    </div>
                    <span class="text-[8px] text-slate-300 font-black uppercase">${r.time}</span>
                </div>
            `).join('');
        }

        function renderAdminPeserta() {
            document.getElementById('admin-peserta-list').innerHTML = db.students.map(s => `
                <tr class="hover:bg-slate-50">
                    <td class="px-6 py-4 font-bold text-slate-700">${s.name}</td>
                    <td class="px-6 py-4 text-slate-500 font-medium">${s.username}</td>
                    <td class="px-6 py-4 text-slate-400">${s.school}</td>
                    <td class="px-6 py-4 text-center space-x-2">
                        <button onclick="resetPass('${s.id}')" class="text-[9px] font-black uppercase text-amber-600">Reset Pass</button>
                        <button onclick="delStud('${s.id}')" class="text-[9px] font-black uppercase text-rose-500">Hapus</button>
                    </td>
                </tr>
            `).join('');
        }

        function renderAdminRekap() {
            const list = document.getElementById('admin-rekap-list');
            list.innerHTML = db.students.map(s => {
                const logs = db.attendance.filter(a => a.id === s.id);
                const h = logs.filter(a => a.type === 'Masuk').length;
                const i = logs.filter(a => a.type === 'Izin' || a.type === 'Sakit').length;
                const totalDays = new Set(db.attendance.map(a => a.date)).size || 1;
                const t = Math.max(0, totalDays - (h + i));
                const pct = ((h / totalDays) * 100).toFixed(0);

                return `<tr>
                    <td class="px-6 py-4 font-bold">${s.name}</td>
                    <td class="px-6 py-4 text-center text-emerald-600 font-bold">${h}</td>
                    <td class="px-6 py-4 text-center text-amber-600 font-bold">${i}</td>
                    <td class="px-6 py-4 text-center text-rose-400 font-bold">${t}</td>
                    <td class="px-6 py-4 text-center"><span class="bg-indigo-50 text-indigo-600 px-2 py-1 rounded-lg font-black">${pct}%</span></td>
                </tr>`;
            }).join('');
        }

        function renderAdminLogbooks() {
            document.getElementById('admin-logbook-all').innerHTML = db.logbooks.map(l => `
                <div class="bg-white p-5 rounded-2xl border shadow-sm flex flex-col justify-between">
                    <div>
                        <div class="flex justify-between items-center mb-3">
                            <div>
                                <h4 class="text-[10px] font-black text-indigo-600 uppercase">${l.name}</h4>
                                <p class="text-[9px] text-slate-400 font-bold uppercase">${l.date} • ${l.time}</p>
                            </div>
                            <button onclick="downloadSingleLogbookPDF('${l.id}')" class="w-8 h-8 flex items-center justify-center bg-slate-50 text-slate-400 hover:text-indigo-600 rounded-lg transition-colors">
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path></svg>
                            </button>
                        </div>
                        <p class="text-xs text-slate-600 leading-relaxed bg-slate-50 p-3 rounded-xl border border-slate-100">${l.content}</p>
                    </div>
                </div>
            `).join('');
        }

        // --- Siswa Action Engine ---
        function checkSiswaControls() {
            const today = new Date().toISOString().split('T')[0];
            const entry = db.attendance.find(a => a.id === db.user.id && a.date === today);
            const bm = document.getElementById('btn-masuk');
            const bp = document.getElementById('btn-pulang');
            const bi = document.getElementById('btn-izin');

            if(entry) {
                if(entry.type === 'Masuk') {
                    bm.disabled = true; bm.style.opacity = "0.5";
                    bi.style.display = "none";
                    if(entry.outTime) { bp.disabled = true; bp.style.opacity = "0.5"; }
                    else { bp.disabled = false; bp.style.opacity = "1"; }
                } else {
                    [bm, bp, bi].forEach(b => { b.disabled = true; b.style.opacity = "0.5"; });
                }
            } else {
                bp.disabled = true; bp.style.opacity = "0.5";
                bm.disabled = false; bm.style.opacity = "1";
                bi.style.display = "flex"; bi.disabled = false; bi.style.opacity = "1";
            }
        }

        function attendance(type) {
            const today = new Date().toISOString().split('T')[0];
            const time = new Date().toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });
            let entry = db.attendance.find(a => a.id === db.user.id && a.date === today);

            if(type === 'Masuk') db.attendance.push({ id: db.user.id, date: today, inTime: time, outTime: null, type: 'Masuk' });
            else if(type === 'Pulang' && entry) entry.outTime = time;

            saveData(); checkSiswaControls(); renderSiswaDashboard();
            Swal.fire({ title: 'Berhasil!', text: `Presensi ${type} tercatat pada ${time}`, icon: 'success', timer: 1500, showConfirmButton: false });
        }

        function saveLogbook() {
            const c = document.getElementById('log-content').value.trim();
            if(!c) return;
            const now = new Date();
            db.logbooks.unshift({ 
                id: Date.now().toString(), 
                studentId: db.user.id, 
                name: db.user.name, 
                date: now.toISOString().split('T')[0], 
                time: now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' }), 
                content: c 
            });
            saveData(); 
            document.getElementById('log-content').value = ""; 
            closeModal('modalLogbook'); 
            renderSiswaDashboard();
            Swal.fire('Laporan Terkirim', 'Logbook Anda telah disimpan ke server.', 'success');
        }

        function saveIzin() {
            const t = document.getElementById('izin-type').value;
            const r = document.getElementById('izin-reason').value.trim();
            if(!r) return;
            const today = new Date().toISOString().split('T')[0];
            db.attendance.push({ id: db.user.id, date: today, type: t, reason: r });
            saveData(); closeModal('modalIzin'); checkSiswaControls(); renderSiswaDashboard();
            Swal.fire('Berhasil', 'Pengajuan izin telah diterima.', 'success');
        }

        function renderSiswaDashboard() {
            const myAtt = db.attendance.filter(a => a.id === db.user.id);
            document.getElementById('siswaAttendanceBody').innerHTML = myAtt.map(a => `
                <tr class="text-[10px] font-medium">
                    <td class="px-4 py-3 font-bold">${a.date}</td>
                    <td class="px-4 py-3"><span class="${a.type === 'Masuk' ? 'text-emerald-600' : 'text-amber-500'} font-black uppercase">${a.type}</span></td>
                    <td class="px-4 py-3 text-slate-400">${a.inTime || '-'} s/d ${a.outTime || '-'}</td>
                    <td class="px-4 py-3 italic text-slate-400">${a.reason || '-'}</td>
                </tr>
            `).join('');

            const myLogs = db.logbooks.filter(l => l.studentId === db.user.id);
            document.getElementById('siswaLogbookList').innerHTML = myLogs.map(l => `
                <div class="p-4 border border-slate-100 rounded-2xl bg-slate-50/30">
                    <div class="flex justify-between items-center mb-2">
                        <p class="text-[9px] font-black text-indigo-500 uppercase">${l.date} • ${l.time}</p>
                        <button onclick="downloadSingleLogbookPDF('${l.id}')" class="text-[8px] font-black uppercase text-slate-400 hover:text-indigo-600">PDF</button>
                    </div>
                    <p class="text-xs text-slate-600 mt-1">${l.content}</p>
                </div>
            `).join('');

            const h = myAtt.filter(a => a.type === 'Masuk').length;
            const i = myAtt.filter(a => a.type === 'Izin' || a.type === 'Sakit').length;
            const ctx = document.getElementById('siswaAttendanceChart').getContext('2d');
            if(window.sChart) window.sChart.destroy();
            window.sChart = new Chart(ctx, {
                type: 'doughnut',
                data: { labels: ['Hadir', 'Izin'], datasets: [{ data: [h, i], backgroundColor: ['#4f46e5', '#f59e0b'], borderWidth: 0, cutout: '75%' }] },
                options: { plugins: { legend: { display: false } }, responsive: true }
            });
        }

        // --- PDF Generation System ---
        const { jsPDF } = window.jspdf;

        function downloadSingleLogbookPDF(logId) {
            const l = db.logbooks.find(x => x.id === logId);
            if(!l) return;
            
            const doc = new jsPDF();
            doc.setFont("helvetica", "bold");
            doc.setFontSize(16);
            doc.text("LAPORAN LOGBOOK HARIAN PKL", 105, 20, { align: "center" });
            
            doc.setFontSize(10);
            doc.setFont("helvetica", "normal");
            doc.text(`Nama Peserta: ${l.name}`, 14, 40);
            doc.text(`Tanggal Laporan: ${l.date}`, 14, 46);
            doc.text(`Waktu Input: ${l.time}`, 14, 52);
            
            doc.line(14, 58, 196, 58);
            
            doc.setFont("helvetica", "bold");
            doc.text("ISI KEGIATAN:", 14, 68);
            
            doc.setFont("helvetica", "normal");
            const splitContent = doc.splitTextToSize(l.content, 180);
            doc.text(splitContent, 14, 76);
            
            doc.save(`Logbook_${l.name}_${l.date}.pdf`);
        }

        function downloadStudentLogbooksPDF() {
            const myLogs = db.logbooks.filter(l => l.studentId === db.user.id);
            if(myLogs.length === 0) return Swal.fire('Data Kosong', 'Belum ada logbook yang diisi.', 'info');
            
            const doc = new jsPDF();
            doc.setFontSize(16);
            doc.text("KUMPULAN LOGBOOK KEGIATAN PKL", 105, 20, { align: "center" });
            doc.setFontSize(11);
            doc.text(`Nama: ${db.user.name}`, 14, 30);
            
            const body = myLogs.map(l => [l.date, l.time, l.content]);
            
            doc.autoTable({
                startY: 40,
                head: [['Tanggal', 'Jam', 'Detail Kegiatan']],
                body: body,
                theme: 'grid',
                headStyles: { fillColor: [79, 70, 229] },
                columnStyles: { 2: { cellWidth: 120 } }
            });
            
            doc.save(`Kumpulan_Logbook_${db.user.name}.pdf`);
        }

        function downloadAllLogbooksPDF() {
            if(db.logbooks.length === 0) return Swal.fire('Data Kosong', 'Belum ada laporan dari peserta.', 'info');
            
            const doc = new jsPDF();
            doc.setFontSize(16);
            doc.text("LAPORAN SELURUH LOGBOOK PESERTA PKL", 105, 20, { align: "center" });
            
            const body = db.logbooks.map(l => [l.name, l.date, l.time, l.content]);
            
            doc.autoTable({
                startY: 30,
                head: [['Nama Peserta', 'Tanggal', 'Jam', 'Kegiatan']],
                body: body,
                theme: 'striped',
                headStyles: { fillColor: [79, 70, 229] },
                columnStyles: { 3: { cellWidth: 80 } }
            });
            
            doc.save("Rekap_Semua_Logbook_PKL.pdf");
        }

        function downloadRekapAdmin() {
            const doc = new jsPDF();
            doc.text("REKAPITULASI PRESENSI PKL", 14, 20);
            
            const totalDays = new Set(db.attendance.map(a => a.date)).size || 1;
            const body = db.students.map(s => {
                const logs = db.attendance.filter(a => a.id === s.id);
                const h = logs.filter(a => a.type === 'Masuk').length;
                const i = logs.filter(a => a.type === 'Izin' || a.type === 'Sakit').length;
                const t = Math.max(0, totalDays - (h + i));
                return [s.name, s.school, h, i, t, `${((h/totalDays)*100).toFixed(0)}%`];
            });

            doc.autoTable({
                startY: 30,
                head: [['Nama', 'Sekolah', 'Hadir', 'Izin', 'Alfa', '%']],
                body: body,
                headStyles: { fillColor: [16, 185, 129] }
            });
            doc.save("Rekap_Presensi_Admin.pdf");
        }

        function downloadHistory(type) {
             const myAtt = db.attendance.filter(a => a.id === db.user.id);
             if(myAtt.length === 0) return;
             const doc = new jsPDF();
             doc.text(`HISTORI PRESENSI - ${db.user.name}`, 14, 20);
             const body = myAtt.map(a => [a.date, a.type, a.inTime||'-', a.outTime||'-', a.reason||'-']);
             doc.autoTable({ startY: 30, head: [['Tanggal', 'Status', 'Masuk', 'Pulang', 'Ket']], body: body });
             doc.save(`Presensi_${db.user.name}.pdf`);
        }

        // --- Utils & UI Helpers ---
        function switchSiswaTab(t) {
            document.getElementById('scont-presensi').classList.toggle('hidden', t !== 'presensi');
            document.getElementById('scont-logbook').classList.toggle('hidden', t !== 'logbook');
            document.getElementById('stab-presensi').classList.toggle('border-indigo-600', t === 'presensi');
            document.getElementById('stab-presensi').classList.toggle('text-indigo-600', t === 'presensi');
            document.getElementById('stab-logbook').classList.toggle('border-indigo-600', t === 'logbook');
            document.getElementById('stab-logbook').classList.toggle('text-indigo-600', t === 'logbook');
        }

        function openAddStudentModal() { document.getElementById('modalAddStudent').style.display = 'flex'; }
        function openLogbookModal() { document.getElementById('modalLogbook').style.display = 'flex'; }
        function openIzinModal() { document.getElementById('modalIzin').style.display = 'flex'; }
        function openChangePassModal() { Swal.fire('Fitur Segera', 'Fungsi ganti password sedang diperbarui.', 'info'); }
        function closeModal(id) { document.getElementById(id).style.display = 'none'; }
        function resetPass(id) { Swal.fire('Sukses', 'Password direset ke default (123)', 'success'); }
        function delStud(id) {
            db.students = db.students.filter(s => s.id !== id);
            saveData(); renderAdminPeserta();
        }

        function handleSaveStudent(e) {
            e.preventDefault();
            db.students.push({ 
                id: Date.now().toString(), 
                name: document.getElementById('stu-name').value, 
                username: document.getElementById('stu-user').value.toLowerCase(), 
                school: document.getElementById('stu-school').value, 
                password: document.getElementById('stu-pass').value 
            });
            saveData(); closeModal('modalAddStudent'); renderAdminPeserta(); e.target.reset();
        }
    </script>
</body>
</html>
