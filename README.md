<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LINKA21 - Bandar Togel Online Resmi</title>
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
    <style>body { background-color: #0b0f19; color: #f8fafc; font-family: sans-serif; }</style>
</head>
<body class="min-h-screen flex flex-col justify-between">

    <!-- HEADER / NAVBAR -->
    <header class="bg-luxuryCard border-b border-blue-900/40 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 py-3 flex justify-between items-center">
            <span class="text-2xl font-extrabold tracking-wider text-blue-400">LINKA21</span>
            <div class="flex items-center space-x-3">
                <!-- Tombol Pengaturan URL Tunnel Cloudflare -->
                <button onclick="bukaSettingUrl()" class="text-xs bg-slate-800 hover:bg-slate-700 text-gray-300 px-3 py-1.5 rounded-lg border border-slate-700 transition font-semibold" title="Atur URL Cloudflare Tunnel Termux">⚙️ Server</button>
                
                <div id="userNavSection" class="flex items-center space-x-2">
                    <button onclick="openModal('loginModal')" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-1.5 rounded-lg text-sm font-semibold transition">Login</button>
                    <button onclick="openModal('registerModal')" class="bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-1.5 rounded-lg text-sm font-semibold transition">Daftar</button>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT -->
    <main class="max-w-7xl mx-auto px-4 py-6 flex-grow w-full">
        <!-- BANNER -->
        <div class="bg-gradient-to-r from-blue-900/60 to-indigo-900/40 border border-blue-500/30 rounded-2xl p-6 mb-8 text-center shadow-xl">
            <h1 class="text-3xl font-bold mb-2">Selamat Datang di LINKA21</h1>
            <p class="text-gray-300 text-sm max-w-xl mx-auto">Bandar Togel Online Resmi dengan 12 Pasaran & Sistem Pembelian 1 Papan (10 Baris).</p>
            <div class="mt-4 flex justify-center gap-4">
                <button onclick="switchTab('pasaranTab')" class="bg-blue-600 text-white px-5 py-2 rounded-xl text-sm font-bold shadow">Pasaran Togel</button>
                <button onclick="switchTab('depoTab')" class="bg-gray-800 hover:bg-gray-700 text-gray-200 border border-gray-700 px-5 py-2 rounded-xl text-sm font-bold">Deposit & Withdraw</button>
            </div>
        </div>

        <!-- TAB 1: 12 PASARAN & TARUHAN 10 BARIS -->
        <div id="pasaranTab" class="tab-content">
            <h2 class="text-xl font-bold mb-4">🎲 12 Pasaran Togel Resmi</h2>
            <div id="pasaranGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 mb-8">
                <!-- Data loaded via API Cloudflare -->
            </div>

            <!-- FORM TARUHAN -->
            <div id="formTaruhanSection" class="bg-luxuryCard border border-blue-900/40 rounded-2xl p-6 hidden shadow-2xl">
                <div class="flex justify-between items-center mb-4 border-b border-blue-900/40 pb-3">
                    <h3 class="text-lg font-bold text-blue-400" id="selectedPasaranTitle">Pasang Angka Papan</h3>
                    <button onclick="closeTaruhan()" class="text-gray-400 hover:text-white text-sm font-bold">Tutup [X]</button>
                </div>
                <p class="text-xs text-gray-400 mb-4">Isi maksimal <strong>10 baris tebakan angka</strong> dalam sekali transaksi pembelian 1 papan.</p>
                <div id="papanBarisContainer" class="space-y-3 mb-4"></div>
                <div class="flex justify-between items-center bg-luxuryDark p-4 rounded-xl border border-blue-900/30">
                    <div>
                        <p class="text-xs text-gray-400">Total Biaya</p>
                        <p class="text-lg font-bold text-yellow-400" id="totalBiayaRp">Rp 0</p>
                    </div>
                    <button onclick="submitTaruhan()" class="bg-emerald-600 hover:bg-emerald-700 text-white font-bold px-6 py-2.5 rounded-xl text-sm shadow transition">Beli 1 Papan</button>
                </div>
            </div>
        </div>

        <!-- TAB 2: DEPOSIT QRIS & WITHDRAW -->
        <div id="depoTab" class="tab-content hidden max-w-xl mx-auto bg-luxuryCard border border-blue-900/40 rounded-2xl p-6 shadow-xl">
            <h2 class="text-xl font-bold mb-4 text-center">Form Transaksi (Deposit QRIS / Withdraw)</h2>
            
            <!-- Gambar QRIS Bandar -->
            <div id="qrisContainer" class="text-center mb-6">
                <p class="text-xs text-gray-400 mb-3">Scan QRIS di bawah ini untuk Deposit:</p>
                <div class="bg-white p-3 inline-block rounded-xl shadow">
                    <img id="qrisImageDisplay" src="https://via.placeholder.com/250x250.png?text=Memuat+QRIS..." alt="QRIS Bandar" class="w-48 h-48 object-contain mx-auto">
                </div>
            </div>

            <div class="space-y-4 border-t border-blue-900/40 pt-4">
                <div>
                    <label class="block text-xs text-gray-400 mb-1">Tipe Transaksi</label>
                    <select id="trxType" onchange="toggleTrxForm()" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
                        <option value="depo">Deposit Saldo</option>
                        <option value="wd">Withdraw (Penarikan)</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs text-gray-400 mb-1">Nominal (Rp)</label>
                    <input type="number" id="trxAmount" placeholder="Contoh: 50000" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
                </div>
                
                <!-- Info Rekening Tampil Otomatis saat WD -->
                <div id="infoRekeningWd" class="bg-luxuryDark p-4 rounded-xl border border-blue-900/30 text-xs text-gray-300 hidden">
                    <p class="text-blue-400 font-bold mb-2">📋 Rekening Tujuan Withdraw Anda:</p>
                    <p>Bank / E-Wallet: <span id="wdBank" class="text-white font-semibold"></span></p>
                    <p>No Rekening: <span id="wdNoRek" class="text-yellow-400 font-semibold"></span></p>
                    <p>Atas Nama: <span id="wdNama" class="text-white font-semibold"></span></p>
                </div>

                <!-- Keterangan Pengirim khusus Deposit -->
                <div id="infoKetDepo">
                    <label class="block text-xs text-gray-400 mb-1">Keterangan / Nama Pengirim / Ref Transfer QRIS</label>
                    <input type="text" id="trxKeterangan" placeholder="Contoh: Transfer BCA a.n Budi / No Ref 12345" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-blue-500">
                </div>

                <button onclick="submitTransaksi()" class="w-full bg-blue-600 hover:bg-blue-700 font-bold py-3 rounded-xl text-sm shadow transition">Kirim Permintaan Transaksi</button>
            </div>
        </div>
    </main>

    <!-- MODAL LOGIN -->
    <div id="loginModal" class="fixed inset-0 bg-black/70 flex items-center justify-center z-50 hidden">
        <div class="bg-luxuryCard border border-blue-900/50 rounded-2xl p-6 w-full max-w-sm shadow-2xl space-y-3">
            <h3 class="text-lg font-bold">Login Member</h3>
            <input type="text" id="loginUsername" placeholder="Username" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2.5 text-sm text-white">
            <input type="password" id="loginPassword" placeholder="Password" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2.5 text-sm text-white">
            <div class="flex gap-2 pt-2">
                <button onclick="closeModal('loginModal')" class="w-1/2 bg-gray-800 py-2 rounded-xl text-xs font-bold">Batal</button>
                <button onclick="processLogin()" class="w-1/2 bg-blue-600 hover:bg-blue-700 py-2 rounded-xl text-xs font-bold">Login</button>
            </div>
        </div>
    </div>

    <!-- MODAL REGISTER DENGAN DATA BANK -->
    <div id="registerModal" class="fixed inset-0 bg-black/70 flex items-center justify-center z-50 hidden">
        <div class="bg-luxuryCard border border-blue-900/50 rounded-2xl p-6 w-full max-w-md shadow-2xl space-y-3">
            <h3 class="text-lg font-bold text-emerald-400">Daftar Akun & Rekening Bank</h3>
            <input type="text" id="regUsername" placeholder="Username" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2 text-sm text-white">
            <input type="password" id="regPassword" placeholder="Password" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2 text-sm text-white">
            <select id="regBank" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2 text-sm text-white">
                <option value="">Pilih Bank / E-Wallet</option>
                <option value="BCA">BCA</option>
                <option value="BRI">BRI</option>
                <option value="MANDIRI">MANDIRI</option>
                <option value="BNI">BNI</option>
                <option value="DANA">DANA</option>
                <option value="OVO">OVO</option>
                <option value="GOPAY">GOPAY</option>
            </select>
            <input type="text" id="regNoRek" placeholder="Nomor Rekening / No HP Akun" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2 text-sm text-white">
            <input type="text" id="regNamaPemilik" placeholder="Nama Pemilik Rekening Sesuai Buku/Akun" class="w-full bg-luxuryDark border border-blue-900/50 rounded-xl px-3 py-2 text-sm text-white">
            <div class="flex gap-2 pt-2">
                <button onclick="closeModal('registerModal')" class="w-1/2 bg-gray-800 py-2 rounded-xl text-xs font-bold">Batal</button>
                <button onclick="processRegister()" class="w-1/2 bg-emerald-600 hover:bg-emerald-700 py-2 rounded-xl text-xs font-bold">Daftar</button>
            </div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-luxuryCard border-t border-blue-900/40 py-4 mt-8 text-center text-xs text-gray-500">
        &copy; 2026 LINKA21. All rights reserved. Powered by NuxGame Engine & Termux DB.
    </footer>

    <!-- JAVASCRIPT KONEKSI CLOUDFLARE TUNNEL -->
    <script>
        // Mengambil URL Cloudflare Tunnel dari memori browser (LocalStorage) atau default localhost
        let API_BASE_URL = localStorage.getItem('linka21_api_url') || "http://localhost:5000";

        let currentUser = null;
        let activePasaranKode = null;

        document.addEventListener("DOMContentLoaded", () => {
            loadPasaran();
            loadQris();
            buildPapanBaris();
        });

        // Fungsi untuk mengatur URL Cloudflare Tunnel secara instan
        function bukaSettingUrl() {
            let urlBaru = prompt("Masukkan URL Cloudflare Tunnel Termux Anda (Contoh: https://xxxx.trycloudflare.com):", API_BASE_URL);
            if(urlBaru) {
                API_BASE_URL = urlBaru.trim().replace(/\/$/, ""); // Hapus garis miring di akhir jika ada
                localStorage.setItem('linka21_api_url', API_BASE_URL);
                alert("URL Server Cloudflare berhasil disimpan! Halaman akan dimuat ulang.");
                location.reload();
            }
        }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(tabId).classList.remove('hidden');
        }

        function openModal(id) { document.getElementById(id).classList.remove('hidden'); }
        function closeModal(id) { document.getElementById(id).classList.add('hidden'); }

        function toggleTrxForm() {
            const type = document.getElementById('trxType').value;
            if(type === 'wd') {
                document.getElementById('infoRekeningWd').classList.remove('hidden');
                document.getElementById('infoKetDepo').classList.add('hidden');
                document.getElementById('qrisContainer').classList.add('hidden');
                if(currentUser) {
                    document.getElementById('wdBank').innerText = currentUser.nama_bank || '-';
                    document.getElementById('wdNoRek').innerText = currentUser.no_rekening || '-';
                    document.getElementById('wdNama').innerText = currentUser.nama_pemilik || '-';
                }
            } else {
                document.getElementById('infoRekeningWd').classList.add('hidden');
                document.getElementById('infoKetDepo').classList.remove('hidden');
                document.getElementById('qrisContainer').classList.remove('hidden');
            }
        }

        async function loadPasaran() {
            try {
                const res = await fetch(`${API_BASE_URL}/api/pasaran`);
                const json = await res.json();
                if(json.success) {
                    const grid = document.getElementById('pasaranGrid');
                    grid.innerHTML = '';
                    json.data.forEach(p => {
                        let statusPasar = p.status_buka || 'OPEN';
                        let isClosed = statusPasar === 'CLOSE';

                        grid.innerHTML += `
                            <div class="bg-luxuryCard border border-blue-900/40 rounded-2xl p-4 flex flex-col justify-between shadow">
                                <div>
                                    <div class="flex justify-between items-center mb-2">
                                        <span class="font-bold text-sm text-blue-400">${p.nama}</span>
                                        <span class="text-xs px-2 py-0.5 rounded font-bold ${isClosed ? 'bg-red-950 text-red-400' : 'bg-emerald-950 text-emerald-400'}">${statusPasar}</span>
                                    </div>
                                    <p class="text-xs text-gray-400">Result Terakhir:</p>
                                    <p class="text-xl font-extrabold text-yellow-400 tracking-widest my-1">${p.result_terakhir || '0000'}</p>
                                </div>
                                ${isClosed ? 
                                    '<button disabled class="mt-3 bg-gray-800 text-gray-500 py-1.5 rounded-xl text-xs font-bold cursor-not-allowed">Pasaran Tutup</button>' : 
                                    `<button onclick="openTaruhan('${p.kode}', '${p.nama}')" class="mt-3 bg-blue-600/20 hover:bg-blue-600 text-blue-400 hover:text-white border border-blue-500/40 py-1.5 rounded-xl text-xs font-bold transition">Pasang Angka</button>`
                                }
                            </div>
                        `;
                    });
                }
            } catch (err) {
                console.error("Gagal terhubung ke Cloudflare Tunnel:", err);
            }
        }

        async function loadQris() {
            try {
                const res = await fetch(`${API_BASE_URL}/api/qris`);
                const json = await res.json();
                if(json.success && json.qrisUrl) {
                    document.getElementById('qrisImageDisplay').src = json.qrisUrl;
                }
            } catch (err) {
                console.error("Gagal memuat QRIS", err);
            }
        }

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
                    alert(`Login Berhasil! Selamat datang, ${currentUser.username}`);
                    closeModal('loginModal');
                    document.getElementById('userNavSection').innerHTML = `
                        <div class="text-xs text-right">
                            <p class="font-bold text-yellow-400">Rp ${Number(currentUser.saldo).toLocaleString()}</p>
                            <p class="text-gray-400">${currentUser.username} (${currentUser.nama_bank || 'Bank'})</p>
                        </div>
                    `;
                } else {
                    alert(json.message);
                }
            } catch (err) {
                alert("Kesalahan koneksi ke server Cloudflare Termux.");
            }
        }

        async function processRegister() {
            const username = document.getElementById('regUsername').value;
            const password = document.getElementById('regPassword').value;
            const nama_bank = document.getElementById('regBank').value;
            const no_rekening = document.getElementById('regNoRek').value;
            const nama_pemilik = document.getElementById('regNamaPemilik').value;

            if(!nama_bank || !no_rekening || !nama_pemilik) {
                alert("Data rekening bank wajib diisi lengkap untuk keperluan penarikan WD!");
                return;
            }

            try {
                const res = await fetch(`${API_BASE_URL}/api/register`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ username, password, nama_bank, no_rekening, nama_pemilik })
                });
                const json = await res.json();
                if(json.success) {
                    alert("Registrasi Berhasil! Silakan Login.");
                    closeModal('registerModal');
                    openModal('loginModal');
                } else {
                    alert(json.error);
                }
            } catch (err) {
                alert("Gagal melakukan registrasi ke server.");
            }
        }

        function buildPapanBaris() {
            const container = document.getElementById('papanBarisContainer');
            container.innerHTML = '';
            for(let i = 1; i <= 10; i++) {
                container.innerHTML += `
                    <div class="flex gap-2 items-center">
                        <span class="text-xs text-gray-500 w-6">#${i}</span>
                        <input type="text" maxlength="4" placeholder="Angka (4D/3D/2D)" class="baris-angka w-2/3 bg-luxuryDark border border-blue-900/50 rounded-lg px-3 py-1.5 text-xs text-white" oninput="hitungTotalBiaya()">
                        <input type="number" placeholder="Nominal" class="baris-nominal w-1/3 bg-luxuryDark border border-blue-900/50 rounded-lg px-3 py-1.5 text-xs text-white" oninput="hitungTotalBiaya()">
                    </div>
                `;
            }
        }

        function openTaruhan(kode, nama) {
            activePasaranKode = kode;
            document.getElementById('selectedPasaranTitle').innerText = `Pasang Papan - ${nama}`;
            document.getElementById('formTaruhanSection').classList.remove('hidden');
        }

        function closeTaruhan() {
            document.getElementById('formTaruhanSection').classList.add('hidden');
        }

        function hitungTotalBiaya() {
            let total = 0;
            document.querySelectorAll('.baris-nominal').forEach(i => total += parseFloat(i.value) || 0);
            document.getElementById('totalBiayaRp').innerText = `Rp ${total.toLocaleString()}`;
        }

        async function submitTaruhan() {
            if(!currentUser) {
                alert("Silakan login terlebih dahulu!");
                openModal('loginModal');
                return;
            }
            const taruhanList = [];
            document.querySelectorAll('#papanBarisContainer > div').forEach(el => {
                const angka = el.querySelector('.baris-angka').value.trim();
                const nominal = parseFloat(el.querySelector('.baris-nominal').value) || 0;
                if(angka && nominal > 0) taruhanList.push({ angka, nominal });
            });

            if(taruhanList.length === 0) {
                alert("Isi minimal 1 baris angka dan nominal taruhan!");
                return;
            }

            try {
                const res = await fetch(`${API_BASE_URL}/api/taruhan`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ userId: currentUser.id, pasaranKode: activePasaranKode, taruhanList })
                });
                const json = await res.json();
                alert(json.message || json.error);
                if(json.success) {
                    buildPapanBaris();
                    closeTaruhan();
                }
            } catch (err) {
                alert("Gagal mengirim taruhan ke server.");
            }
        }

        async function submitTransaksi() {
            if(!currentUser) {
                alert("Silakan login terlebih dahulu!");
                openModal('loginModal');
                return;
            }
            const type = document.getElementById('trxType').value;
            const amount = document.getElementById('trxAmount').value;
            let keterangan = '';

            if(type === 'depo') {
                keterangan = document.getElementById('trxKeterangan').value.trim();
                if(!keterangan) {
                    alert("Harap isi keterangan / nama pengirim / referensi transfer QRIS!");
                    return;
                }
            } else {
                keterangan = `WD ke Bank: ${currentUser.nama_bank} - ${currentUser.no_rekening} a.n ${currentUser.nama_pemilik}`;
            }

            if(!amount || amount <= 0) {
                alert("Masukkan nominal yang valid!");
                return;
            }

            try {
                const res = await fetch(`${API_BASE_URL}/api/transaksi`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ userId: currentUser.id, type, amount, keterangan })
                });
                const json = await res.json();
                alert(json.message || json.error);
                if(json.success) {
                    document.getElementById('trxAmount').value = '';
                    document.getElementById('trxKeterangan').value = '';
                }
            } catch (err) {
                alert("Gagal mengirim transaksi ke server.");
            }
        }
    </script>
</body>
</html>

