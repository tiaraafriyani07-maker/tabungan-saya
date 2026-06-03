<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>🐷 Tabungan Cerdas - Kelola Uang & Impianku</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Poppins', 'Comic Neue', 'Quicksand', system-ui, sans-serif;
        }

        body {
            background: linear-gradient(145deg, #f9f0c1 0%, #f7e5a3 100%);
            min-height: 100vh;
            padding: 20px;
        }

        /* Container utama */
        .container {
            max-width: 1300px;
            margin: 0 auto;
        }

        /* Header dan profile */
        .header {
            background: #fff6e0;
            border-radius: 48px;
            padding: 20px 30px;
            margin-bottom: 25px;
            box-shadow: 0 15px 25px rgba(0,0,0,0.1);
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            border: 3px solid #ffcf9a;
        }

        .title-area h1 {
            font-size: 2rem;
            color: #c27e3a;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .title-area p {
            color: #b97f48;
            font-weight: 500;
        }

        .saldo-area {
            background: #ffefcf;
            padding: 12px 28px;
            border-radius: 60px;
            text-align: center;
            box-shadow: inset 0 -2px 0 #e0bc84, 0 8px 12px rgba(0,0,0,0.05);
        }

        .saldo-label {
            font-size: 1rem;
            letter-spacing: 1px;
            color: #a5662a;
        }

        .saldo-nominal {
            font-size: 2.5rem;
            font-weight: 800;
            color: #f5a623;
            text-shadow: 2px 2px 0 #ffe0a3;
            line-height: 1;
        }

        /* grid dua kolom utama */
        .dashboard {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 24px;
            margin-bottom: 30px;
        }

        /* kartu style */
        .card {
            background: rgba(255, 252, 235, 0.95);
            border-radius: 40px;
            padding: 20px 24px;
            box-shadow: 0 12px 20px rgba(99, 57, 34, 0.15);
            backdrop-filter: blur(2px);
            border: 1px solid #ffe2b5;
            transition: 0.2s;
        }

        .card h2 {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 1.7rem;
            color: #b45f2b;
            border-bottom: 3px dashed #ffd29d;
            padding-bottom: 12px;
            margin-bottom: 20px;
        }

        /* form style */
        .form-group {
            margin-bottom: 18px;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 12px;
        }

        .form-group label {
            width: 90px;
            font-weight: 600;
            color: #a35f2c;
        }

        input, select {
            flex: 1;
            padding: 12px 18px;
            border-radius: 60px;
            border: 2px solid #f5cd94;
            background: white;
            font-size: 1rem;
            outline: none;
            transition: 0.2s;
        }

        input:focus, select:focus {
            border-color: #f7b45a;
            box-shadow: 0 0 0 3px #ffe2af;
        }

        button {
            background: #fec165;
            border: none;
            padding: 12px 24px;
            border-radius: 60px;
            font-weight: bold;
            font-size: 1rem;
            color: #5e2e12;
            cursor: pointer;
            transition: 0.15s;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 4px 0 #b4622a;
        }

        button:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #b4622a;
        }

        .btn-danger {
            background: #ffb0a7;
            box-shadow: 0 4px 0 #b15a4a;
            color: #691c0c;
        }

        .btn-small {
            padding: 6px 14px;
            font-size: 0.8rem;
        }

        /* daftar transaksi */
        .transaksi-list, .wishlist-list {
            max-height: 270px;
            overflow-y: auto;
            margin-top: 15px;
        }

        .item-transaksi, .item-wish {
            background: #fff9ef;
            border-radius: 50px;
            padding: 10px 18px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-left: 8px solid #fcc577;
            transition: 0.1s;
        }

        .item-transaksi.pemasukan {
            border-left-color: #7bc47f;
        }

        .item-transaksi.pengeluaran {
            border-left-color: #f7a07a;
        }

        .info-transaksi {
            display: flex;
            flex-direction: column;
        }

        .keterangan {
            font-weight: 600;
            color: #7a481f;
        }

        .nominal {
            font-weight: 800;
            font-size: 1.1rem;
        }

        .nominal.plus {
            color: #2e7d32;
        }

        .nominal.minus {
            color: #c7362b;
        }

        .tanggal {
            font-size: 0.7rem;
            color: #a68457;
        }

        .aksi-hapus {
            background: none;
            box-shadow: none;
            padding: 5px 12px;
            background-color: #ffe0bf;
            color: #b45a2b;
        }

        .aksi-hapus:active {
            transform: scale(0.95);
        }

        /* wishlist */
        .wish-progress {
            margin: 8px 0 5px;
            background-color: #f3e1c0;
            border-radius: 30px;
            height: 12px;
            width: 100%;
            overflow: hidden;
        }

        .progress-fill {
            background: #f5b042;
            width: 0%;
            height: 100%;
            border-radius: 30px;
        }

        .wish-actions {
            display: flex;
            gap: 8px;
        }

        .btn-beli {
            background: #7ab87e;
            box-shadow: 0 3px 0 #3f6b3a;
            color: white;
            font-size: 0.7rem;
            padding: 4px 12px;
        }

        /* ringkasan barang */
        .summary {
            background: #ffefcf;
            border-radius: 32px;
            padding: 18px 25px;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 10px;
        }

        .summary-item {
            background: white;
            border-radius: 30px;
            padding: 6px 20px;
            font-weight: bold;
        }

        @media (max-width: 800px) {
            .dashboard {
                grid-template-columns: 1fr;
            }
            .header {
                flex-direction: column;
                text-align: center;
                gap: 15px;
            }
            .form-group label {
                width: 70px;
            }
        }

        footer {
            text-align: center;
            margin-top: 25px;
            color: #bc7a3e;
            font-weight: 500;
        }
    </style>
</head>
<body>
<div class="container">
    <div class="header">
        <div class="title-area">
            <h1>🐷 Tabungan Cerdas <span style="font-size: 1.8rem;">🎒</span></h1>
            <p>📚 catat pemasukan & pengeluaran, wujudkan barang impian!</p>
        </div>
        <div class="saldo-area">
            <div class="saldo-label">💰 Total Tabunganmu</div>
            <div class="saldo-nominal" id="totalSaldo">Rp 0</div>
        </div>
    </div>

    <div class="dashboard">
        <!-- Kiri: Pencatatan Keuangan -->
        <div class="card">
            <h2>📝 Catat Uang</h2>
            <div style="margin-bottom: 20px; display: flex; gap: 12px; flex-wrap: wrap;">
                <button id="btnPemasukan" style="background:#9fdf9f; box-shadow:0 4px 0 #568a34;">➕ Pemasukan</button>
                <button id="btnPengeluaran" class="btn-danger">➖ Pengeluaran</button>
            </div>

            <div id="formContainer">
                <!-- form dinamis akan muncul disini (pemasukan/pengeluaran) -->
            </div>

            <h3 style="margin: 20px 0 8px 0;">📋 Riwayat Transaksi</h3>
            <div class="transaksi-list" id="transaksiList">
                <!-- daftar transaksi -->
                <div style="text-align:center; color: #c28142;">Belum ada transaksi, ayo catat!</div>
            </div>
            <div class="summary">
                <div class="summary-item">📈 Total Masuk: <span id="totalPemasukan">Rp 0</span></div>
                <div class="summary-item">📉 Total Keluar: <span id="totalPengeluaran">Rp 0</span></div>
            </div>
        </div>

        <!-- Kanan: Wishlist Barang yang Ingin Dibeli -->
        <div class="card">
            <h2>🎁 Wishlist Impian</h2>
            <div class="form-group">
                <label>Nama Barang:</label>
                <input type="text" id="namaBarang" placeholder="contoh: Sepatu baru, Buku, Tas, Skincare" style="flex:2;">
            </div>
            <div class="form-group">
                <label>Harga (Rp):</label>
                <input type="number" id="hargaBarang" placeholder="Harga yang ingin dibeli">
            </div>
            <button id="tambahWishlistBtn">✨ Tambah ke Wishlist</button>

            <h3 style="margin: 24px 0 8px 0;">💭 Barang Impian & Progress</h3>
            <div class="wishlist-list" id="wishlistContainer">
                <div style="text-align:center; color:#c28142;">Tambah barang impianmu ✨</div>
            </div>
        </div>
    </div>

    <footer>
        💡 Tips: Catat setiap pemasukan & pengeluaran, lalu beli barang dari wishlist jika tabungan cukup!
    </footer>
</div>

<script>
    // ---------- DATA ----------
    let transactions = [];     // array { id, type, amount, description, date }
    let wishlist = [];         // array { id, name, price, bought: false }
    let nextId = 1;
    let nextWishId = 1;

    // Load dari localStorage jika ada
    function loadData() {
        const savedTrans = localStorage.getItem("tabungan_transactions");
        const savedWish = localStorage.getItem("tabungan_wishlist");
        if(savedTrans) {
            transactions = JSON.parse(savedTrans);
            if(transactions.length) {
                // cari max id untuk nextId
                const maxId = transactions.reduce((max, t) => Math.max(max, t.id), 0);
                nextId = maxId + 1;
            } else nextId = 1;
        } else {
            // contoh data awal agar tidak kosong
            transactions = [
                { id: nextId++, type: "pemasukan", amount: 50000, description: "Uang saku mingguan", date: new Date().toLocaleDateString() },
                { id: nextId++, type: "pemasukan", amount: 20000, description: "Hadiah ranking", date: new Date().toLocaleDateString() },
                { id: nextId++, type: "pengeluaran", amount: 15000, description: "Beli snack", date: new Date().toLocaleDateString() }
            ];
        }
        if(savedWish) {
            wishlist = JSON.parse(savedWish);
            if(wishlist.length) {
                const maxW = wishlist.reduce((max, w) => Math.max(max, w.id), 0);
                nextWishId = maxW + 1;
            }
        } else {
            wishlist = [
                { id: nextWishId++, name: "📚 Novel Favorit", price: 85000, bought: false },
                { id: nextWishId++, name: "🎧 Earphone baru", price: 120000, bought: false },
                { id: nextWishId++, name: "🖍️ Alat Lukis", price: 95000, bought: false }
            ];
        }
        updateAllUI();
    }

    function saveToLocal() {
        localStorage.setItem("tabungan_transactions", JSON.stringify(transactions));
        localStorage.setItem("tabungan_wishlist", JSON.stringify(wishlist));
    }

    // Hitung saldo sekarang
    function calculateSaldo() {
        let totalMasuk = 0;
        let totalKeluar = 0;
        transactions.forEach(t => {
            if(t.type === "pemasukan") totalMasuk += t.amount;
            else totalKeluar += t.amount;
        });
        return totalMasuk - totalKeluar;
    }

    // update tampilan total saldo dan ringkasan
    function updateSaldoUI() {
        const saldo = calculateSaldo();
        document.getElementById("totalSaldo").innerText = formatRupiah(saldo);
        // total pemasukan & pengeluaran
        let sumIn = 0, sumOut = 0;
        transactions.forEach(t => {
            if(t.type === "pemasukan") sumIn += t.amount;
            else sumOut += t.amount;
        });
        document.getElementById("totalPemasukan").innerText = formatRupiah(sumIn);
        document.getElementById("totalPengeluaran").innerText = formatRupiah(sumOut);
    }

    function formatRupiah(angka) {
        return "Rp " + angka.toLocaleString('id-ID');
    }

    // render daftar transaksi
    function renderTransactions() {
        const container = document.getElementById("transaksiList");
        if(!transactions.length) {
            container.innerHTML = '<div style="text-align:center; color:#c28142;">📭 Belum ada transaksi, ayo catat!</div>';
            return;
        }
        container.innerHTML = "";
        // urutkan dari yang terbaru (id descending)
        [...transactions].reverse().forEach(tr => {
            const div = document.createElement("div");
            div.className = `item-transaksi ${tr.type === "pemasukan" ? "pemasukan" : "pengeluaran"}`;
            const nominalClass = tr.type === "pemasukan" ? "plus" : "minus";
            const sign = tr.type === "pemasukan" ? "+ " : "- ";
            div.innerHTML = `
                <div class="info-transaksi">
                    <div class="keterangan">${escapeHtml(tr.description)}</div>
                    <div class="nominal ${nominalClass}">${sign}${formatRupiah(tr.amount)}</div>
                    <div class="tanggal">📅 ${tr.date}</div>
                </div>
                <button class="aksi-hapus btn-small" data-id="${tr.id}">🗑️ Hapus</button>
            `;
            container.appendChild(div);
        });
        // tambahkan event hapus
        document.querySelectorAll(".aksi-hapus").forEach(btn => {
            btn.addEventListener("click", (e) => {
                const id = parseInt(btn.getAttribute("data-id"));
                hapusTransaksi(id);
            });
        });
    }

    function hapusTransaksi(id) {
        transactions = transactions.filter(t => t.id !== id);
        saveToLocal();
        updateAllUI();
    }

    // tambah transaksi (type: pemasukan/pengeluaran)
    function addTransaction(type, amount, description) {
        if(!amount || amount <= 0) {
            alert("Nominal harus lebih dari 0!");
            return false;
        }
        if(!description.trim()) {
            alert("Mohon isi keterangan!");
            return false;
        }
        // cek jika pengeluaran melebihi saldo (opsional, tapi biar edukatif)
        if(type === "pengeluaran") {
            const saldoSekarang = calculateSaldo();
            if(amount > saldoSekarang) {
                if(!confirm(`⚠️ Saldo saat ini ${formatRupiah(saldoSekarang)}. Pengeluaran ini akan membuat tabunganmu minus. Tetap lanjut?`)) {
                    return false;
                }
            }
        }
        const newTrans = {
            id: nextId++,
            type: type,
            amount: amount,
            description: description.trim(),
            date: new Date().toLocaleDateString('id-ID')
        };
        transactions.push(newTrans);
        saveToLocal();
        updateAllUI();
        return true;
    }

    // ---------- Wishlist ----------
    function renderWishlist() {
        const container = document.getElementById("wishlistContainer");
        if(!wishlist.length) {
            container.innerHTML = '<div style="text-align:center; color:#c28142;">✨ Tambahkan barang impianmu di sini ✨</div>';
            return;
        }
        container.innerHTML = "";
        wishlist.forEach(item => {
            const saldoSaatIni = calculateSaldo();
            const progress = Math.min(100, (saldoSaatIni / item.price) * 100);
            const sudahCukup = saldoSaatIni >= item.price;
            const boughtStatus = item.bought ? " (Sudah dibeli ✅)" : "";
            const div = document.createElement("div");
            div.className = "item-wish";
            div.innerHTML = `
                <div style="flex:1">
                    <div style="display:flex; justify-content:space-between; flex-wrap:wrap;">
                        <strong style="font-size:1rem;">🎀 ${escapeHtml(item.name)}${boughtStatus}</strong>
                        <span style="background:#f5e2c1; border-radius:30px; padding:3px 12px;">${formatRupiah(item.price)}</span>
                    </div>
                    ${!item.bought ? `
                        <div class="wish-progress">
                            <div class="progress-fill" style="width: ${progress}%;"></div>
                        </div>
                        <div style="font-size:0.7rem; margin-top: 4px;">💵 Tabungan: ${formatRupiah(saldoSaatIni)} / ${formatRupiah(item.price)} (${Math.floor(progress)}%)</div>
                    ` : `<div style="font-size:0.75rem; color:#528a34;">✅ Barang sudah kamu miliki! Selamat!</div>`}
                </div>
                <div class="wish-actions">
                    ${!item.bought ? `<button class="btn-beli btn-small" data-id="${item.id}">🛒 Beli</button>` : ''}
                    <button class="aksi-hapus btn-small" data-wishid="${item.id}" style="background:#f7cfaa;">🗑️ Hapus</button>
                </div>
            `;
            container.appendChild(div);
        });
        // Event beli barang
        document.querySelectorAll(".btn-beli").forEach(btn => {
            btn.addEventListener("click", (e) => {
                const id = parseInt(btn.getAttribute("data-id"));
                beliBarangDariWishlist(id);
            });
        });
        // Event hapus wishlist
        document.querySelectorAll("[data-wishid]").forEach(btn => {
            btn.addEventListener("click", (e) => {
                const id = parseInt(btn.getAttribute("data-wishid"));
                hapusWishlistItem(id);
            });
        });
    }

    function hapusWishlistItem(id) {
        if(confirm("Hapus barang dari wishlist?")) {
            wishlist = wishlist.filter(item => item.id !== id);
            saveToLocal();
            updateAllUI();
        }
    }

    function beliBarangDariWishlist(id) {
        const item = wishlist.find(i => i.id === id);
        if(!item) return;
        if(item.bought) {
            alert("Barang ini sudah pernah dibeli!");
            return;
        }
        const saldoSekarang = calculateSaldo();
        if(saldoSekarang >= item.price) {
            if(confirm(`Beli ${item.name} seharga ${formatRupiah(item.price)}? Uang akan dikurangi dari tabungan.`)) {
                // membuat transaksi pengeluaran otomatis
                const newTrans = {
                    id: nextId++,
                    type: "pengeluaran",
                    amount: item.price,
                    description: `Membeli ${item.name} (dari wishlist)`,
                    date: new Date().toLocaleDateString('id-ID')
                };
                transactions.push(newTrans);
                // tandai barang sebagai sudah dibeli
                item.bought = true;
                saveToLocal();
                updateAllUI();
                alert(`🎉 Selamat! Kamu berhasil membeli ${item.name}. Barang ditandai selesai!`);
            }
        } else {
            alert(`💰 Tabunganmu belum cukup! Butuh ${formatRupiah(item.price - saldoSekarang)} lagi. Yuk tambah pemasukan atau hemat pengeluaran.`);
        }
    }

    // fungsi untuk menambah wishlist baru
    function tambahWishlist(nama, harga) {
        if(!nama.trim()) {
            alert("Nama barang tidak boleh kosong!");
            return false;
        }
        if(isNaN(harga) || harga <= 0) {
            alert("Harga barang harus lebih dari 0!");
            return false;
        }
        const newWish = {
            id: nextWishId++,
            name: nama.trim(),
            price: harga,
            bought: false
        };
        wishlist.push(newWish);
        saveToLocal();
        updateAllUI();
        return true;
    }

    // update semua UI secara konsisten
    function updateAllUI() {
        updateSaldoUI();
        renderTransactions();
        renderWishlist();
    }

    // helper escape html
    function escapeHtml(str) {
        return str.replace(/[&<>]/g, function(m) {
            if(m === '&') return '&amp;';
            if(m === '<') return '&lt;';
            if(m === '>') return '&gt;';
            return m;
        });
    }

    // Dinamis form pemasukan / pengeluaran
    let currentType = "pemasukan";
    function renderForm() {
        const container = document.getElementById("formContainer");
        const isPemasukan = (currentType === "pemasukan");
        container.innerHTML = `
            <div class="form-group">
                <label>Keterangan:</label>
                <input type="text" id="descTrans" placeholder="${isPemasukan ? 'Contoh: Uang saku, hadiah' : 'Contoh: Jajan, transport'}" value="">
            </div>
            <div class="form-group">
                <label>Nominal (Rp):</label>
                <input type="number" id="amountTrans" placeholder="0" min="1">
            </div>
            <button id="simpanTransaksiBtn" style="background: ${isPemasukan ? '#9fdf9f' : '#ffb0a7'}">✅ Simpan ${isPemasukan ? 'Pemasukan' : 'Pengeluaran'}</button>
        `;
        const simpanBtn = document.getElementById("simpanTransaksiBtn");
        if(simpanBtn) {
            simpanBtn.addEventListener("click", () => {
                const desc = document.getElementById("descTrans").value;
                const amount = parseInt(document.getElementById("amountTrans").value);
                if(addTransaction(currentType, amount, desc)) {
                    // reset form biar bersih opsional
                    document.getElementById("descTrans").value = "";
                    document.getElementById("amountTrans").value = "";
                }
            });
        }
    }

    // event tombol pemasukan/pengeluaran
    document.getElementById("btnPemasukan").addEventListener("click", () => {
        currentType = "pemasukan";
        renderForm();
    });
    document.getElementById("btnPengeluaran").addEventListener("click", () => {
        currentType = "pengeluaran";
        renderForm();
    });

    // tambah wishlist
    document.getElementById("tambahWishlistBtn").addEventListener("click", () => {
        const nama = document.getElementById("namaBarang").value;
        const harga = parseInt(document.getElementById("hargaBarang").value);
        if(tambahWishlist(nama, harga)) {
            document.getElementById("namaBarang").value = "";
            document.getElementById("hargaBarang").value = "";
        }
    });

    // inisialisasi
    loadData();
    renderForm();   // default form pemasukan
    // set current type = pemasukan awal
    currentType = "pemasukan";
    renderForm();
</script>
</body>
</html>
