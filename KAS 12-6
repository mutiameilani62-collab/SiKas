<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Pembayaran Kas Kelas</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Poppins', sans-serif; }
        .fade-in { animation: fadeIn 0.5s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .custom-scrollbar::-webkit-scrollbar { height: 8px; width: 8px; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background-color: #cbd5e1; border-radius: 4px; }
    </style>
</head>
<body class="bg-gray-100 text-gray-800 h-screen overflow-hidden flex flex-col">

    <!-- Navbar -->
    <nav class="bg-indigo-600 text-white shadow-lg z-10 flex-none">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex items-center gap-2">
                    <i class="fa-solid fa-wallet text-xl"></i>
                    <span class="font-bold text-lg tracking-wide">Kas Kelas Kita</span>
                </div>
                <div id="nav-user-info" class="hidden flex items-center gap-4">
                    <span id="user-display-name" class="text-sm font-medium bg-indigo-700 py-1 px-3 rounded-full"></span>
                    <button onclick="app.logout()" class="text-white hover:text-red-200 transition">
                        <i class="fa-solid fa-right-from-bracket"></i> Keluar
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Konten Utama -->
    <main class="flex-grow overflow-y-auto p-4 relative custom-scrollbar">
        
        <!-- TAMPILAN LOGIN -->
        <div id="view-login" class="max-w-md mx-auto mt-10 bg-white p-8 rounded-2xl shadow-xl fade-in">
            <div class="text-center mb-6">
                <div class="bg-indigo-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4 text-indigo-600">
                    <i class="fa-solid fa-user-lock text-2xl"></i>
                </div>
                <h2 class="text-2xl font-bold text-gray-800">Login Sistem</h2>
                <p class="text-gray-500 text-sm">Masukkan ID Absen (01-36)</p>
            </div>
            
            <form onsubmit="app.handleLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">ID Pengguna</label>
                    <input type="number" id="login-id" oninput="app.togglePasswordField()" class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 outline-none transition" placeholder="Contoh: 25 atau 01" required>
                </div>
                
                <div id="password-container" class="hidden animate-pulse">
                    <label class="block text-sm font-medium text-gray-700 mb-1">Kata Sandi Admin</label>
                    <div class="relative">
                        <input type="password" id="login-password" class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 outline-none transition" placeholder="Masukkan password admin">
                        <i class="fa-solid fa-key absolute right-3 top-4 text-gray-400"></i>
                    </div>
                </div>

                <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 rounded-lg transition shadow-md hover:shadow-lg transform hover:-translate-y-0.5">
                    Masuk Aplikasi
                </button>
            </form>
        </div>

        <!-- DASHBOARD SISWA -->
        <div id="view-student" class="hidden max-w-lg mx-auto fade-in space-y-6">
            <div class="bg-white rounded-2xl shadow-lg overflow-hidden relative border-t-4 border-indigo-500">
                <div class="bg-gradient-to-r from-blue-500 to-indigo-600 p-6 text-white text-center">
                    <p class="text-sm opacity-90 mb-1">Status Tagihan Kas Anda</p>
                    <h1 id="student-bill-amount" class="text-4xl font-bold mb-2">Rp 0</h1>
                    <span id="student-status-badge" class="px-3 py-1 rounded-full text-xs font-bold bg-white/20 uppercase tracking-wider">LUNAS</span>
                </div>
                <div class="p-6">
                    <button onclick="app.openPaymentModal()" class="w-full bg-green-500 hover:bg-green-600 text-white font-bold py-3 rounded-xl shadow-lg transition flex items-center justify-center gap-2">
                        <i class="fa-solid fa-money-bill-wave"></i> Bayar Kas Sekarang
                    </button>
                </div>
            </div>

            <div class="bg-white rounded-2xl shadow-md p-6">
                <h3 class="font-bold text-gray-700 mb-4 flex items-center gap-2">
                    <i class="fa-solid fa-clock-rotate-left text-indigo-500"></i> Riwayat Pembayaran Anda
                </h3>
                <div id="student-history-list" class="space-y-3 h-64 overflow-y-auto pr-2 custom-scrollbar">
                    <p class="text-center text-gray-400 text-sm italic py-4">Belum ada riwayat pembayaran.</p>
                </div>
            </div>
        </div>

        <!-- DASHBOARD ADMIN -->
        <div id="view-admin" class="hidden max-w-6xl mx-auto fade-in space-y-6 pb-20">
            <!-- Statistik -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="bg-white p-5 rounded-xl shadow-sm border-l-4 border-green-500">
                    <p class="text-gray-500 text-xs uppercase font-bold">Saldo Kas Kelas (Terkumpul)</p>
                    <p id="admin-total-collected" class="text-2xl font-bold text-gray-800">Rp 0</p>
                </div>
                <div class="bg-white p-5 rounded-xl shadow-sm border-l-4 border-red-500">
                    <p class="text-gray-500 text-xs uppercase font-bold">Total Piutang (Belum Bayar)</p>
                    <p id="admin-total-debt" class="text-2xl font-bold text-gray-800">Rp 0</p>
                </div>
                <div class="bg-white p-5 rounded-xl shadow-sm flex flex-col justify-center items-center text-center">
                    <p class="text-gray-500 text-xs uppercase font-bold mb-2">Kontrol Mingguan</p>
                    <button onclick="app.simulateWeeklyTrigger()" class="w-full bg-indigo-600 text-white hover:bg-indigo-700 px-4 py-2 rounded-lg font-medium text-sm transition">
                        <i class="fa-solid fa-plus-circle mr-1"></i> Tambah Tagihan Rp 5rb
                    </button>
                </div>
            </div>

            <!-- Tabel Data Siswa -->
            <div class="bg-white rounded-xl shadow-md overflow-hidden flex flex-col h-[550px]">
                <div class="px-6 py-4 border-b border-gray-100 flex justify-between items-center bg-gray-50">
                    <h3 class="font-bold text-gray-700">Database Keuangan Siswa (01-36)</h3>
                </div>
                <div class="overflow-x-auto overflow-y-auto flex-grow custom-scrollbar">
                    <table class="w-full text-sm text-left border-collapse">
                        <thead class="text-xs text-gray-700 uppercase bg-gray-100 sticky top-0 z-20">
                            <tr>
                                <th class="px-4 py-3 border-b">ID</th>
                                <th class="px-4 py-3 border-b">Nama Siswa</th>
                                <th class="px-4 py-3 border-b text-right">Telah Dibayar</th>
                                <th class="px-4 py-3 border-b text-right">Sisa Tagihan</th>
                                <th class="px-4 py-3 border-b text-center">Status</th>
                                <th class="px-4 py-3 border-b text-center">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="admin-users-table">
                            <!-- Injeksi via JS -->
                        </tbody>
                    </table>
                </div>
            </div>

             <div class="bg-white rounded-xl shadow-md p-6">
                <h3 class="font-bold text-gray-700 mb-4">Log Aktivitas Terbaru</h3>
                <div id="admin-log-list" class="h-40 overflow-y-auto space-y-2 text-sm border p-3 rounded-lg bg-gray-50 custom-scrollbar">
                    <!-- Logs -->
                </div>
            </div>
        </div>
    </main>

    <!-- Modal Pembayaran (Langkah 1: Pilih Nominal & Metode) -->
    <div id="payment-modal" class="fixed inset-0 bg-black/50 hidden z-50 flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-sm rounded-2xl p-6 shadow-2xl">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-bold">Bayar Kas</h3>
                <button onclick="app.closePaymentModal()"><i class="fa-solid fa-times text-gray-400"></i></button>
            </div>
            <div class="mb-4 bg-indigo-50 p-3 rounded-lg border border-indigo-100">
                <p class="text-xs text-indigo-600 font-bold">Tagihan Anda:</p>
                <p id="modal-bill-amount" class="text-xl font-bold text-indigo-800">Rp 0</p>
            </div>
            <form onsubmit="app.handleNextPaymentStep(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-gray-500 mb-1 uppercase">Nominal Pembayaran</label>
                    <input type="number" id="pay-amount" class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-indigo-500 outline-none" placeholder="Masukkan nominal (Rp)" required>
                </div>
                <div>
                    <label class="block text-xs font-bold text-gray-500 mb-1 uppercase">Pilih Metode Pembayaran</label>
                    <div class="grid grid-cols-2 gap-2">
                        <label class="border p-3 rounded-lg flex flex-col items-center gap-2 cursor-pointer hover:bg-gray-50 transition border-indigo-200">
                            <input type="radio" name="pay-method" value="QRIS" class="hidden" checked onchange="app.updateMethodStyle()">
                            <i class="fa-solid fa-qrcode text-2xl text-indigo-600"></i>
                            <span class="text-xs font-bold">QRIS</span>
                        </label>
                        <label class="border p-3 rounded-lg flex flex-col items-center gap-2 cursor-pointer hover:bg-gray-50 transition">
                            <input type="radio" name="pay-method" value="BANK" class="hidden" onchange="app.updateMethodStyle()">
                            <i class="fa-solid fa-building-columns text-2xl text-indigo-600"></i>
                            <span class="text-xs font-bold">BANK</span>
                        </label>
                    </div>
                </div>
                <button type="submit" class="w-full bg-indigo-600 text-white font-bold py-3 rounded-lg hover:bg-indigo-700 transition">Lanjut Pembayaran</button>
            </form>
        </div>
    </div>

    <!-- Modal Instruksi Pembayaran (Langkah 2) -->
    <div id="instruction-modal" class="fixed inset-0 bg-black/50 hidden z-50 flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-sm rounded-2xl p-6 shadow-2xl text-center">
            <h3 id="instruction-title" class="text-lg font-bold mb-4">Instruksi Pembayaran</h3>
            
            <div id="instruction-content-qris" class="hidden space-y-4">
                <div class="bg-white border-2 border-dashed border-gray-300 p-4 inline-block rounded-xl">
                    <!-- Placeholder QR Code -->
                    <div class="w-48 h-48 bg-gray-200 flex items-center justify-center mx-auto rounded">
                        <i class="fa-solid fa-qrcode text-6xl text-gray-400"></i>
                    </div>
                </div>
                <p class="text-sm text-gray-600">Scan QRIS di atas menggunakan aplikasi dompet digital Anda (Gopay, OVO, Dana, dll).</p>
            </div>

            <div id="instruction-content-bank" class="hidden space-y-4">
                <div class="bg-indigo-50 p-4 rounded-xl text-left">
                    <p class="text-xs font-bold text-gray-400 uppercase">Nomor Rekening Bendahara:</p>
                    <div class="flex justify-between items-center mt-1">
                        <span class="text-lg font-bold font-mono tracking-widest text-indigo-900">123-456-7890</span>
                        <button onclick="app.copyToClipboard('1234567890')" class="text-xs bg-indigo-200 text-indigo-700 px-2 py-1 rounded">SALIN</button>
                    </div>
                    <p class="text-xs font-medium text-indigo-600 mt-2">Bank: Bank Mandiri / BCA (A.N. Bendahara Kelas)</p>
                </div>
                <p class="text-sm text-gray-600">Silakan transfer sesuai nominal ke nomor rekening di atas.</p>
            </div>

            <div class="mt-6 space-y-2">
                <button onclick="app.processFinalPayment()" class="w-full bg-green-600 text-white font-bold py-3 rounded-lg hover:bg-green-700 transition">Konfirmasi Saya Sudah Bayar</button>
                <button onclick="app.closeInstructionModal()" class="w-full text-gray-400 text-sm font-medium">Batalkan</button>
            </div>
        </div>
    </div>

    <!-- Modal Edit Tagihan -->
    <div id="edit-bill-modal" class="fixed inset-0 bg-black/50 hidden z-50 flex items-center justify-center p-4">
        <div class="bg-white w-full max-w-sm rounded-2xl p-6 shadow-2xl">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-bold">Edit Tagihan</h3>
                <button onclick="app.closeEditBillModal()"><i class="fa-solid fa-times text-gray-400"></i></button>
            </div>
            <p id="edit-modal-name" class="text-sm text-gray-600 mb-4 font-semibold"></p>
            <form onsubmit="app.saveBillChange(event)" class="space-y-4">
                <input type="hidden" id="edit-bill-id">
                <input type="number" id="edit-bill-amount" class="w-full p-3 border rounded-lg outline-none" placeholder="Nominal tagihan baru" required>
                <button type="submit" class="w-full bg-indigo-600 text-white font-bold py-3 rounded-lg transition">Simpan</button>
            </form>
        </div>
    </div>

    <script>
        const ADMIN_PASS = "mutiameilani07";

        const generateUsers = () => {
            let users = [];
            const studentNames = { 
                "01": "RAKA", "02": "AGNES", "03": "AKHTAR", "04": "ALBANY", "05": "ALYA",
                "06": "BUNGA", "07": "APRILA", "08": "TATA", "09": "CHAYLA", "10": "CINTA",
                "11": "DANDRE", "12": "FARAH", "13": "FIMEL", "14": "HABIBAH", "15": "INDAH",
                "16": "KAISYA", "17": "KANIA", "18": "KEYLA", "19": "KEYZA", "20": "SIFA",
                "21": "LUSI", "22": "FEBRI", "23": "DESTA", "24": "VINO", "25": "MUTI", 
                "26": "NADIN", "27": "NAJWA", "28": "NAZWA", "29": "OKTA", "30": "RASSYA",
                "31": "FIRA", "32": "JEVERA", "33": "WISNU", "34": "ZAHRA AWAL", "35": "NAYLUNA", "36": "SATRIA"
            };

            for (let i = 1; i <= 36; i++) {
                let id = i < 10 ? `0${i}` : `${i}`;
                users.push({ 
                    id, 
                    name: studentNames[id] || `Siswa Absen ${id}`, 
                    role: id === '25' ? 'admin' : 'siswa' 
                });
            }
            return users;
        };

        const DB = {
            users: generateUsers(),
            bills: {
                "01": 60000, "02": 50000, "03": 60000, "04": 60000, "05": 0,
                "06": 100000, "07": 60000, "08": 0, "09": 95000, "10": 60000,
                "11": 0, "12": 60000, "13": 60000, "14": 80000, "15": 55000,
                "16": 40000, "17": 35000, "18": 0, "19": 60000, "20": 45000,
                "21": 0, "22": 85000, "23": 50000, "24": 60000, "25": 0,
                "26": 50000, "27": 60000, "28": 35000, "29": 45000, "30": 60000,
                "31": 0, "32": 0, "33": 120000, "34": 40000, "35": 100000, "36": 60000
            }, 
            payments: [], 
            logs: []
        };

        const app = {
            currentUser: null,
            pendingPayment: null,

            init() { this.switchView('login'); },
            formatRupiah(n) { return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', minimumFractionDigits: 0 }).format(n); },
            
            togglePasswordField() {
                const id = document.getElementById('login-id').value;
                const container = document.getElementById('password-container');
                const passInput = document.getElementById('login-password');
                if (id === "25") {
                    container.classList.remove('hidden');
                    passInput.setAttribute('required', 'true');
                } else {
                    container.classList.add('hidden');
                    passInput.removeAttribute('required');
                    passInput.value = "";
                }
            },

            handleLogin(e) {
                e.preventDefault();
                const idStr = document.getElementById('login-id').value;
                const id = idStr.padStart(2, '0');
                const password = document.getElementById('login-password').value;
                const user = DB.users.find(u => u.id === id);
                
                if (user) {
                    if (user.role === 'admin' && password !== ADMIN_PASS) {
                        Swal.fire('Login Gagal', 'Kata sandi salah!', 'error');
                        return;
                    }
                    this.currentUser = user;
                    document.getElementById('nav-user-info').classList.remove('hidden');
                    document.getElementById('user-display-name').textContent = user.name;
                    if(user.role === 'admin') { this.renderAdminDashboard(); this.switchView('admin'); }
                    else { this.renderStudentDashboard(); this.switchView('student'); }
                } else { Swal.fire('Error', 'ID Absen tidak ditemukan (01-36)', 'error'); }
            },

            logout() { this.currentUser = null; document.getElementById('nav-user-info').classList.add('hidden'); this.switchView('login'); },
            switchView(v) { ['login', 'student', 'admin'].forEach(x => document.getElementById(`view-${x}`).classList.toggle('hidden', x !== v)); },

            renderStudentDashboard() {
                const bill = DB.bills[this.currentUser.id] || 0;
                document.getElementById('student-bill-amount').textContent = this.formatRupiah(bill);
                const badge = document.getElementById('student-status-badge');
                badge.textContent = bill <= 0 ? 'LUNAS' : 'BELUM LUNAS';
                badge.className = `px-3 py-1 rounded-full text-xs font-bold ${bill <= 0 ? 'bg-green-500' : 'bg-red-500'} text-white uppercase tracking-wider`;
                
                const history = DB.payments.filter(p => p.id === this.currentUser.id).sort((a,b) => new Date(b.date) - new Date(a.date));
                document.getElementById('student-history-list').innerHTML = history.length ? history.map(p => `
                    <div class="flex justify-between items-center bg-gray-50 p-3 rounded-lg border-l-4 border-green-500">
                        <div class="flex flex-col">
                            <span class="text-xs text-gray-500">${new Date(p.date).toLocaleDateString()}</span>
                            <span class="text-[10px] text-gray-400 uppercase font-bold">${p.method || 'CASH'}</span>
                        </div>
                        <span class="font-bold text-green-600">+ ${this.formatRupiah(p.amount)}</span>
                    </div>
                `).join('') : '<p class="text-center text-gray-400 text-sm italic py-4">Belum ada riwayat pembayaran.</p>';
            },

            openPaymentModal() {
                document.getElementById('modal-bill-amount').textContent = this.formatRupiah(DB.bills[this.currentUser.id] || 0);
                document.getElementById('pay-amount').value = DB.bills[this.currentUser.id] || "";
                document.getElementById('payment-modal').classList.remove('hidden');
                this.updateMethodStyle();
            },
            closePaymentModal() { document.getElementById('payment-modal').classList.add('hidden'); },

            updateMethodStyle() {
                const radios = document.getElementsByName('pay-method');
                radios.forEach(r => {
                    const label = r.parentElement;
                    if (r.checked) {
                        label.classList.add('border-indigo-500', 'bg-indigo-50');
                        label.classList.remove('border-gray-200');
                    } else {
                        label.classList.remove('border-indigo-500', 'bg-indigo-50');
                        label.classList.add('border-gray-200');
                    }
                });
            },

            handleNextPaymentStep(e) {
                e.preventDefault();
                const amt = parseInt(document.getElementById('pay-amount').value);
                const method = document.querySelector('input[name="pay-method"]:checked').value;
                
                if (amt <= 0) return;

                this.pendingPayment = { amount: amt, method: method };
                this.closePaymentModal();
                this.openInstructionModal(method);
            },

            openInstructionModal(method) {
                const modal = document.getElementById('instruction-modal');
                const title = document.getElementById('instruction-title');
                const qrisContent = document.getElementById('instruction-content-qris');
                const bankContent = document.getElementById('instruction-content-bank');

                qrisContent.classList.add('hidden');
                bankContent.classList.add('hidden');

                if (method === 'QRIS') {
                    title.textContent = "Pembayaran via QRIS";
                    qrisContent.classList.remove('hidden');
                } else {
                    title.textContent = "Pembayaran via Transfer Bank";
                    bankContent.classList.remove('hidden');
                }

                modal.classList.remove('hidden');
            },

            closeInstructionModal() {
                document.getElementById('instruction-modal').classList.add('hidden');
                this.pendingPayment = null;
            },

            processFinalPayment() {
                if (!this.pendingPayment) return;

                const { amount, method } = this.pendingPayment;
                
                DB.bills[this.currentUser.id] = Math.max(0, (DB.bills[this.currentUser.id] || 0) - amount);
                DB.payments.push({ 
                    id: this.currentUser.id, 
                    name: this.currentUser.name, 
                    amount: amount, 
                    method: method,
                    date: new Date().toISOString() 
                });
                
                DB.logs.unshift({ 
                    date: new Date(), 
                    type: 'BAYAR', 
                    message: `${this.currentUser.name} bayar ${this.formatRupiah(amount)} via ${method}` 
                });

                this.closeInstructionModal();
                this.renderStudentDashboard();
                Swal.fire('Terima Kasih!', 'Pembayaran Anda sedang divalidasi oleh bendahara.', 'success');
            },

            copyToClipboard(text) {
                const el = document.createElement('textarea');
                el.value = text;
                document.body.appendChild(el);
                el.select();
                document.execCommand('copy');
                document.body.removeChild(el);
                Swal.fire({ title: 'Tersalin!', text: 'Nomor rekening berhasil disalin.', icon: 'success', toast: true, position: 'top-end', timer: 2000, showConfirmButton: false });
            },

            renderAdminDashboard() {
                const table = document.getElementById('admin-users-table');
                let totalColl = 0, totalDebt = 0, html = '';
                
                const payMap = DB.payments.reduce((acc, p) => { 
                    acc[p.id] = (acc[p.id] || 0) + p.amount; 
                    totalColl += p.amount; 
                    return acc; 
                }, {});

                const sortedStudents = DB.users.filter(u => u.id !== '25').sort((a,b) => parseInt(a.id) - parseInt(b.id));

                sortedStudents.forEach(u => {
                    const bill = DB.bills[u.id] || 0;
                    const paid = payMap[u.id] || 0;
                    totalDebt += bill;
                    html += `
                        <tr class="hover:bg-gray-50 border-b">
                            <td class="px-4 py-4 font-mono font-bold">${u.id}</td>
                            <td class="px-4 py-4">${u.name}</td>
                            <td class="px-4 py-4 text-right font-bold text-green-600">${this.formatRupiah(paid)}</td>
                            <td class="px-4 py-4 text-right font-bold text-red-600">${this.formatRupiah(bill)}</td>
                            <td class="px-4 py-4 text-center">
                                <span class="px-2 py-1 rounded text-[10px] font-bold ${bill === 0 ? 'bg-green-100 text-green-700' : 'bg-red-100 text-red-700'}">
                                    ${bill === 0 ? 'LUNAS' : 'TUNGGAK'}
                                </span>
                            </td>
                            <td class="px-4 py-4 text-center">
                                <button onclick="app.openEditBillModal('${u.id}')" class="text-indigo-600 hover:text-indigo-900"><i class="fa-solid fa-edit"></i></button>
                            </td>
                        </tr>
                    `;
                });
                table.innerHTML = html;
                document.getElementById('admin-total-collected').textContent = this.formatRupiah(totalColl);
                document.getElementById('admin-total-debt').textContent = this.formatRupiah(totalDebt);
                document.getElementById('admin-log-list').innerHTML = DB.logs.map(l => `<div class="p-1 border-b text-[10px]"><span class="text-gray-400">${l.date.toLocaleTimeString()}</span> <strong class="text-indigo-600">[${l.type}]</strong> ${l.message}</div>`).join('') || '<p class="text-gray-400 text-center py-2">Belum ada aktivitas.</p>';
            },

            openEditBillModal(id) {
                const u = DB.users.find(x => x.id === id);
                document.getElementById('edit-bill-id').value = id;
                document.getElementById('edit-modal-name').textContent = `ID ${u.id} - ${u.name}`;
                document.getElementById('edit-bill-amount').value = DB.bills[id];
                document.getElementById('edit-bill-modal').classList.remove('hidden');
            },
            closeEditBillModal() { document.getElementById('edit-bill-modal').classList.add('hidden'); },
            saveBillChange(e) {
                e.preventDefault();
                const id = document.getElementById('edit-bill-id').value;
                const amt = parseInt(document.getElementById('edit-bill-amount').value);
                DB.logs.unshift({ date: new Date(), type: 'EDIT', message: `Tagihan ID ${id} diubah ke ${this.formatRupiah(amt)}` });
                DB.bills[id] = amt;
                this.closeEditBillModal();
                this.renderAdminDashboard();
                Swal.fire('Berhasil', 'Tagihan telah diperbarui', 'success');
            },

            simulateWeeklyTrigger() {
                Swal.fire({ 
                    title: 'Update Kas Mingguan?', 
                    text: "Semua siswa akan mendapat tambahan tagihan Rp 5.000.", 
                    icon: 'question',
                    showCancelButton: true,
                    confirmButtonText: 'Ya, Update'
                }).then(r => {
                    if(r.isConfirmed) {
                        DB.users.forEach(u => { if(u.id!=='25') DB.bills[u.id] = (DB.bills[u.id] || 0) + 5000; });
                        DB.logs.unshift({ date: new Date(), type: 'SISTEM', message: 'Tagihan mingguan Rp 5.000 ditambahkan.' });
                        this.renderAdminDashboard();
                        Swal.fire('Berhasil', 'Tagihan mingguan berhasil diterapkan.', 'success');
                    }
                });
            }
        };
        app.init();
    </script>
</body>
</html>
