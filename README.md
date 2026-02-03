# Tugas-tia-2
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Warehouse QR Scan System</title>
<script src="https://unpkg.com/html5-qrcode"></script>

<style>
body {
    margin: 0;
    font-family: "Segoe UI", Arial, sans-serif;
    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
    color: #ffffff;
}

header {
    background: #0a0a0a;
    padding: 28px;
    text-align: center;
    font-size: 34px;
    font-weight: 700;
    letter-spacing: 2px;
    box-shadow: 0 6px 15px rgba(0,0,0,0.6);
}

.container {
    display: flex;
    justify-content: center;
    gap: 50px;
    padding: 50px;
    flex-wrap: wrap;
}

.card {
    background: #111c24;
    border-radius: 22px;
    padding: 35px;
    width: 460px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.7);
}

.card h2 {
    text-align: center;
    font-size: 28px;
    margin-bottom: 30px;
    padding-bottom: 12px;
    border-bottom: 3px solid #00b4ff;
    letter-spacing: 1px;
}

#reader {
    width: 100%;
}

.data-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 22px 0;
    font-size: 24px;
}

.label {
    color: #9fd9ff;
}

.value {
    font-weight: 700;
}

.ok {
    color: #00ff9c;
}

.reject {
    color: #ff4d4d;
}

footer {
    text-align: center;
    padding: 22px;
    color: #cccccc;
    font-size: 14px;
}
</style>
</head>

<body>

<header>WAREHOUSE QR SCAN SYSTEM</header>

<div class="container">

    <!-- SCANNER -->
    <div class="card">
        <h2>SCAN QR CODE</h2>
        <div id="reader"></div>
    </div>

    <!-- HASIL -->
    <div class="card">
        <h2>DETAIL PRODUK</h2>

        <div class="data-row">
            <span class="label">Nama Produk</span>
            <span id="nama" class="value">-</span>
        </div>

        <div class="data-row">
            <span class="label">Berat (KG)</span>
            <span id="berat" class="value">-</span>
        </div>

        <div class="data-row">
            <span class="label">Status</span>
            <span id="status" class="value">-</span>
        </div>
    </div>

</div>

<footer>Soal Test Programmer – Sistem Gudang</footer>

<script>
/* ===== DATABASE SESUAI TABEL DI SOAL ===== */
const database = {
    "1": { nama: "Indomie Kari", berat: "100", status: "OKE" },
    "2": { nama: "Indomie Soto", berat: "500", status: "REJECT" },
    "3": { nama: "Indomie Goreng", berat: "600", status: "OKE" },
    "4": { nama: "Sarimi", berat: "400", status: "REJECT" },
    "5": { nama: "Supermi", berat: "200", status: "OKE" }
};

function onScanSuccess(decodedText) {

    // Ambil angka ID dari QR (contoh: 1INDOMIEKARI100OKE)
    const id = decodedText.match(/\d+/)?.[0];

    if (!database[id]) {
        alert("Produk tidak ditemukan!");
        return;
    }

    const data = database[id];

    document.getElementById("nama").innerText = data.nama;
    document.getElementById("berat").innerText = data.berat + " KG";

    const statusEl = document.getElementById("status");
    statusEl.innerText = data.status;
    statusEl.className = "value " + (data.status === "OKE" ? "ok" : "reject");
}

/* AKTIFKAN SCANNER */
new Html5Qrcode("reader").start(
    { facingMode: "environment" },
    { fps: 10, qrbox: 300 },
    onScanSuccess
);
</script>

</body>
</html>
