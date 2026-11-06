<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LINKA21 - Resmi Togel Online & Live Casino</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        luxuryDark: '#0b0f19',
                        luxuryCard: '#131c2e',
                        luxuryBlue: '#1e293b',
                        luxuryAccent: '#3b82f6',
                        luxuryGold: '#fbbf24'
                    }
                }
            }
        }
    </script>
    <style>
        body { background-color: #0b0f19; color: #f8fafc; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between">

    <!-- HEADER / NAVBAR -->
    <header class="bg-luxuryCard border-b border-blue-900/40 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <span class="text-2xl font-extrabold tracking-wider bg-gradient-to-r from-blue-400 to-indigo-500 bg-clip-text text-transparent">LINKA21</span>
                <span class="text-xs bg-blue-600/30 text-blue-400 px-2 py-0.5 rounded border border-blue-500/30 font-semibold">NUXGAME</span>
            </div>
            
            <div id="userNavSection" class="flex items-center space-x-3">
                <!-- Status Login Dinamis -->
                <button onclick="openModal('loginModal')" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-1.5 rounded-lg text-sm font-semibold transition">Login</button>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT -->
    <main class="max-w-7xl mx-auto px-4 py-6 flex-grow w-full">
        
        <!-- BANNER / INFO -->
        <div class="bg-gradient-to-r from-blue-900/60 to-indigo-900/40 border border-blue-500/30 rounded-2xl p-6 mb-8 text-center shadow-lg">
            <h1 class="text-3xl font-bold mb-2">Selamat Datang di LINKA21</h1>
            <p class="text-gray-300 text-sm max-w-xl mx-auto">Bandar Togel Online Terpercaya dengan 12 Pasaran Resmi & Transaksi Cepat via QRIS.</p>
            <div class="mt-4 flex justify-center gap-4">
                <button onclick="switchTab('pasaranTab')" class="bg-blue-600 text-white px-5 py-2 rounded-xl text-sm font-bold shadow">Pasaran Togel</button>
                <button onclick="switchTab('depoTab')" class="bg-gray-800 hover:bg-gray-700 text-gray-200 border border-gray-700 px-5 py-2 rounded-xl text-sm font-bold">Deposit QRIS</button>
            </div>
        </div>

        <!-- TAB 1: 12 PASARAN & PASANG TOGEL (10 BARIS) -->
        <div id="pasaranTab" class="tab-content">
            <h2 class="text-xl font-bold mb-4 flex items-center gap-2">🎲 12 Pasaran Togel Resmi</h2>
            <div id="pasaranGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 mb-8">
                <!-- Render dari API -->
            </div>

            <!-- FORM PASANG TOGEL (10 BARIS) -->
            <div id="formTaruhanSection" class="bg-luxuryCard border border-blue-900/40 rounded-2xl p-6 hidden">
                <div class="flex justify-between items-center mb-4 border-b border-blue-900/40 pb-3">
                    <h3 class="text-lg font-bold text-blue-400" id="selectedPasaranTitle">Pasang Angka</h3>
                    <button onclick="closeTaruhan()" class="text-gray-400 hover:text-white text-sm">Tutup [X]</button>
                </div>
                
                <p class="text-xs text-gray-400 mb-4">Silakan isi hingga maksimal 10 baris tebakan angka dalam sekali pembelian.</p>
                
                <div id="papanBarisContainer" class="space-y-3 mb-4">
                    <!-- 10 Baris Input Dinamis -->
                </div>

                <div class="flex justify-between items-center bg-luxuryDark p-4 rounded-xl border border-blue-900/30">
                    <div>
                        <p class="text-xs text-gray-400">Total Biaya Taruhan</p>
                        <p class="text-lg font-bold text-yellow-400" id="totalBiayaRp">Rp 0</p>
                    </div>
                    <button onclick="submitTaruhan()" class="bg-emerald-600 hover:bg-emerald-700 text-white font-bold px-6 py-2.5 rounded-xl text-sm shadow transition">Beli 1 Papan Sekaligus</button>
                </div>
            </div>
        </div>

        <!-- TAB 2: DEPOSIT QRIS & WD -->
        <div id="depoTab" class="tab-content hidden max-w-xl mx-auto bg-luxuryCard border border-blue-900/40 rounded-2xl p-6 shadow-xl">
            <h2 class="text-xl font-bold mb-4 text-center">QRIS Deposit & Withdraw Bandar</h2>
            <div class="text-center mb-6">
                <p class="text-xs text-gray-400 mb-3">Scan QRIS di bawah ini menggunakan aplikasi M-Banking atau E-Wallet Anda.</p>
                <div class="bg-white p-3 inline-block rounded-xl shadow">
                    <img id="qrisImageDisplay" src="https://via.placeholder.com/250x250.png?text=Loading+QRIS..." alt="QRIS Bandar" class="w-48 h-48 object-contain mx-auto">
                </div>
            </div>

            <div class="space-y-4 border-t border-blue-900/40 pt-4">
                <div>
                    <label class="block text-xs text-gray-400 mb-1">Tipe Transaksi</label>
                    <select id="trxType" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
                        <option value="depo">Deposit Saldo</option>
                        <option value="wd">Withdraw (Penarikan)</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs text-gray-400 mb-1">Nominal (Rp)</label>
                    <input type="number" id="trxAmount" placeholder="Contoh: 50000" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
                </div>
                <button onclick="submitTransaksi()" class="w-full bg-blue-600 hover:bg-blue-700 font-bold py-3 rounded-xl text-sm shadow transition">Kirim Permintaan Transaksi</button>
            </div>
        </div>

        <!-- TAB 3: PANEL ADMIN (Khusus Akses Termux / Localhost) -->
        <div id="adminTab" class="tab-content hidden">
            <div class="bg-red-950/30 border border-red-500/30 rounded-2xl p-6 mb-6">
                <h2 class="text-xl font-bold text-red-400 mb-1">🛡️ Panel Admin Kontrol Resmi</h2>
                <p class="text-xs text-gray-400">Atur result pasaran, kelola user (blok/aktif & saldo), dan perbarui QRIS bandar.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Sub Admin 1: Update Result -->
                <div class="bg-luxuryCard border border-blue-900/40 rounded-2xl p-5">
                    <h3 class="font-bold text-sm mb-3 text-blue-400">1. Update Result Pasaran</h3>
                    <div class="space-y-3">
                        <select id="adminPasaranSelect" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2 text-sm text-white"></select>
                        <input type="text" id="adminResultInput" placeholder="Masukkan Result (Contoh: 4321)" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2 text-sm text-white">
                        <button onclick="adminUpdateResult()" class="w-full bg-blue-600 hover:bg-blue-700 py-2 rounded-xl text-xs font-bold">Simpan Result</button>
                    </div>
                </div>

                <!-- Sub Admin 2: Update QRIS -->
                <div class="bg-luxuryCard border border-blue-900/40 rounded-2xl p-5">
                    <h3 class="font-bold text-sm mb-3 text-blue-400">2. Ganti Gambar QRIS Bandar</h3>
                    <div class="space-y-3">
                        <input type="text" id="adminQrisInput" placeholder="URL Gambar QRIS Baru" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2 text-sm text-white">
                        <button onclick="adminUpdateQris()" class="w-full bg-blue-600 hover:bg-blue-700 py-2 rounded-xl text-xs font-bold">Perbarui QRIS</button>
                    </div>
                </div>
            </div>

            <!-- Sub Admin 3: Manajemen User -->
            <div class="mt-6 bg-luxuryCard border border-blue-900/40 rounded-2xl p-5">
                <h3 class="font-bold text-sm mb-3 text-blue-400">3. Daftar User & Manajemen Akun</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-luxuryDark text-gray-400 border-b border-blue-900/40">
                            <tr>
                                <th class="p-3">ID</th>
                                <th class="p-3">Username</th>
                                <th class="p-3">Saldo</th>
                                <th class="p-3">Status</th>
                                <th class="p-3">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="adminUserTableBody">
                            <!-- Render dari API -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

    </main>

    <!-- MODAL LOGIN -->
    <div id="loginModal" class="fixed inset-0 bg-black/70 flex items-center justify-center z-50 hidden">
        <div class="bg-luxuryCard border border-blue-900/50 rounded-2xl p-6 w-full max-w-sm shadow-2xl">
            <h3 class="text-lg font-bold mb-4">Login Member / Admin</h3>
            <div class="space-y-3">
                <input type="text" id="loginUsername" placeholder="Username" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2.5 text-sm text-white">
                <input type="password" id="loginPassword" placeholder="Password" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2.5 text-sm text-white">
                <div class="flex gap-2 pt-2">
                    <button onclick="closeModal('loginModal')" class="w-1/2 bg-gray-800 py-2 rounded-xl text-xs font-bold">Batal</button>
                    <button onclick="processLogin()" class="w-1/2 bg-blue-600 hover:bg-blue-700 py-2 rounded-xl text-xs font-bold">Login</button>
                </div>
            </div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-luxuryCard border-t border-blue-900/40 py-4 mt-8 text-center text-xs text-gray-500">
        &copy; 2026 LINKA21. All rights reserved. Powered by NuxGame Engine & Termux DB.
    </footer>

    <!-- JAVASCRIPT KONEKSI BACKEND -->
    <script>
        // Ubah URL di bawah ini dengan URL publik backend Anda (Contoh dari LocalTunnel/Ngrok Termux)
        const API_BASE_URL = "https://linka21-api.loca.lt"; 

        let currentUser = null;
        let activePasaranKode = null;

        document.addEventListener("DOMContentLoaded", () => {
            loadPasaran();
            loadQris();
            buildPapanBaris();
            
            // Cek akses admin otomatis jika dibuka di perangkat lokal/Termux
            if (window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1') {
                // Tampilkan menu admin otomatis jika diakses dari localhost
            }
        });

        // Tab Switching
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(tabId).classList.remove('hidden');
            if(tabId === 'adminTab') {
                loadAdminUsers();
            }
        }

        function openModal(id) { document.getElementById(id).classList.remove('hidden'); }
        function closeModal(id) { document.getElementById(id).classList.add('hidden'); }

        // Fetch 12 Pasaran
        async function loadPasaran() {
            try {
                const res = await fetch(`${API_BASE_URL}/api/pasaran`);
                const json = await res.json();
                if(json.success) {
                    const grid = document.getElementById('pasaranGrid');
                    const adminSelect = document.getElementById('adminPasaranSelect');
                    grid.innerHTML = '';
                    adminSelect.innerHTML = '';

                    json.data.forEach(p => {
                        grid.innerHTML += `
                            <div class="bg-luxuryCard border border-blue-900/40 rounded-2xl p-4 flex flex-col justify-between shadow">
                                <div>
                                    <div class="flex justify-between items-center mb-2">
                                        <span class="font-bold text-sm text-blue-400">${p.nama}</span>
                                        <span class="text-xs bg-luxuryDark px-2 py-0.5 rounded text-gray-400 border border-blue-900/30">${p.kode}</span>
                                    </div>
                                    <p class="text-xs text-gray-400">Result Terakhir:</p>
                                    <p class="text-xl font-extrabold text-yellow-400 tracking-widest my-1">${p.result_terakhir}</p>
                                </div>
                                <button onclick="openTaruhan('${p.kode}', '${p.nama}')" class="mt-3 bg-blue-600/20 hover:bg-blue-600 text-blue-400 hover:text-white border border-blue-500/40 py-1.5 rounded-xl text-xs font-bold transition">Pasang Angka</button>
                            </div>
                        `;
                        adminSelect.innerHTML += `<option value="${p.kode}">${p.nama} (${p.kode})</option>`;
                    });
                }
            } catch (err) {
                console.error("Gagal memuat pasaran:", err);
            }
        }

        // Fetch QRIS
        async function loadQris() {
            try {
                const res = await fetch(`${API_BASE_URL}/api/qris`);
                const json = await res.json();
                if(json.success && json.qrisUrl) {
                    document.getElementById('qrisImageDisplay').src = json.qrisUrl;
                }
            } catch (err) {
                console.error("Gagal memuat QRIS:", err);
            }
        }

        // Login User
        async function processLogin() {
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;
            try {
                const res = await fetch(`${API_BASE_URL}/api/login`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ username, password })
                });
                const json = await res.json();
                if(json.success) {
                    currentUser = json.user;
                    alert(`Login Berhasil! Halo, ${currentUser.username}`);
                    closeModal('loginModal');
                    
                    // Update Nav UI
                    document.getElementById('userNavSection').innerHTML = `
                        <div class="text-xs text-right">
                            <p class="font-bold text-yellow-400">Rp ${Number(currentUser.saldo).toLocaleString()}</p>
                            <p class="text-gray-400">${currentUser.username}</p>
                        </div>
                    `;

                    if(currentUser.role === 'admin') {
                        // Munculkan tombol panel admin di nav jika role admin
                        document.getElementById('userNavSection').innerHTML += `
                            <button onclick="switchTab('adminTab')" class="bg-red-600 hover:bg-red-700 text-white px-3 py-1 rounded-lg text-xs font-bold">Admin Panel</button>
                        `;
                    }
                } else {
                    alert(json.message);
                }
            } catch (err) {
                alert("Kesalahan koneksi ke server backend.");
            }
        }

        // Papan Taruhan 10 Baris
        function buildPapanBaris() {
            const container = document.getElementById('papanBarisContainer');
            container.innerHTML = '';
            for(let i = 1; i <= 10; i++) {
                container.innerHTML += `
                    <div class="flex gap-2 items-center">
                        <span class="text-xs text-gray-500 w-6">#${i}</span>
                        <input type="text" maxlength="4" placeholder="Nomor (4D/3D/2D)" class="baris-angka w-2/3 bg-luxuryDark border border-blue-900/50 rounded-lg px-3 py-1.5 text-xs text-white" oninput="hitungTotalBiaya()">
                        <input type="number" placeholder="Nominal Rp" class="baris-nominal w-1/3 bg-luxuryDark border border-blue-900/50 rounded-lg px-3 py-1.5 text-xs text-white" oninput="hitungTotalBiaya()">
                    </div>
                `;
            }
        }

        function openTaruhan(kode, nama) {
            activePasaranKode = kode;
            document.getElementById('selectedPasaranTitle').innerText = `Pasang Papan - ${nama}`;
            document.getElementById('formTaruhanSection').classList.remove('hidden');
            window.scrollTo({ top: document.getElementById('formTaruhanSection').offsetTop, behavior: 'smooth' });
        }

        function closeTaruhan() {
            document.getElementById('formTaruhanSection').classList.add('hidden');
        }

        function hitungTotalBiaya() {
            let total = 0;
            document.querySelectorAll('.baris-nominal').forEach(input => {
                const val = parseFloat(input.value) || 0;
                total += val;
            });
            document.getElementById('totalBiayaRp').innerText = `Rp ${total.toLocaleString()}`;
        }

        function submitTaruhan() {
            if(!currentUser) {
                alert("Silakan login terlebih dahulu untuk melakukan taruhan!");
                openModal('loginModal');
                return;
            }
            alert("Papan taruhan berhasil diproses untuk pasaran " + activePasaranKode + "!");
            closeTaruhan();
        }

        // Transaksi Depo / WD
        async function submitTransaksi() {
            if(!currentUser) {
                alert("Silakan login terlebih dahulu!");
                openModal('loginModal');
                return;
            }
            const type = document.getElementById('trxType').value;
            const amount = document.getElementById('trxAmount').value;

            if(!amount || amount <= 0) {
                alert("Masukkan nominal yang valid!");
                return;
            }

            try {
                const res = await fetch(`${API_BASE_URL}/api/transaksi`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ userId: currentUser.id, type, amount })
                });
                const json = await res.json();
                if(json.success) {
                    alert(json.message);
                    document.getElementById('trxAmount').value = '';
                } else {
                    alert(json.error);
                }
            } catch (err) {
                alert("Gagal mengirim transaksi.");
            }
        }

        // ================= ADMIN FUNCTIONS =================
        async function adminUpdateResult() {
            const kode = document.getElementById('adminPasaranSelect').value;
            const nomorResult = document.getElementById('adminResultInput').value;
            try {
                const res = await fetch(`${API_BASE_URL}/api/admin/result`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ kode, nomorResult })
                });
                const json = await res.json();
                alert(json.message || json.error);
                loadPasaran();
            } catch (err) {
                alert("Akses ditolak atau server error.");
            }
        }

        async function adminUpdateQris() {
            const qrisImageUrl = document.getElementById('adminQrisInput').value;
            try {
                const res = await fetch(`${API_BASE_URL}/api/admin/qris`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ qrisImageUrl })
                });
                const json = await res.json();
                alert(json.message || json.error);
                loadQris();
            } catch (err) {
                alert("Akses ditolak atau server error.");
            }
        }

        async function loadAdminUsers() {
            try {
                const res = await fetch(`${API_BASE_URL}/api/admin/users`);
                const json = await res.json();
                if(json.success) {
                    const tbody = document.getElementById('adminUserTableBody');
                    tbody.innerHTML = '';
                    json.users.forEach(u => {
                        tbody.innerHTML += `
                            <tr class="border-b border-blue-900/20">
                                <td class="p-3">${u.id}</td>
                                <td class="p-3 font-semibold">${u.username}</td>
                                <td class="p-3 text-yellow-400">Rp ${Number(u.saldo).toLocaleString()}</td>
                                <td class="p-3"><span class="px-2 py-0.5 rounded text-[10px] ${u.status === 'active' ? 'bg-emerald-900/50 text-emerald-400' : 'bg-red-900/50 text-red-400'}">${u.status}</span></td>
                                <td class="p-3">
                                    <button onclick="toggleBlockUser(${u.id}, '${u.status}', ${u.saldo})" class="bg-gray-800 hover:bg-gray-700 px-2 py-1 rounded text-[10px]">Ubah Status</button>
                                </td>
                            </tr>
                        `;
                    });
                }
            } catch (err) {
                console.error("Gagal load users:", err);
            }
        }

        async function toggleBlockUser(userId, currentStatus, currentSaldo) {
            const newStatus = currentStatus === 'active' ? 'blocked' : 'active';
            try {
                const res = await fetch(`${API_BASE_URL}/api/admin/user-status`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ userId, status: newStatus, saldo: currentSaldo })
                });
                const json = await res.json();
                alert(json.message || json.error);
                loadAdminUsers();
            } catch (err) {
                alert("Gagal memperbarui status user.");
            }
        }
    </script>
</body>
</html>
