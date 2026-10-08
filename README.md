<!DOCTYPE html>
<html lang="id">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>ExpiryGuard AI</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: Arial, Helvetica, sans-serif;
            background: #f3f6fb;
            color: #1f2937;
        }
        
        header {
            background: linear-gradient(135deg, #2563eb, #7c3aed);
            color: white;
            padding: 25px 7%;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo-icon {
            width: 58px;
            height: 58px;
            border-radius: 16px;
            background: rgba(255, 255, 255, .18);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
        }
        
        .logo h1 {
            font-size: 26px;
        }
        
        .logo p {
            margin-top: 5px;
            opacity: .85;
        }
        
        main {
            width: 92%;
            max-width: 1200px;
            margin: 30px auto;
        }
        /* DASHBOARD */
        
        .dashboard {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 18px;
            margin-bottom: 25px;
        }
        
        .stat {
            background: white;
            padding: 22px;
            border-radius: 18px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, .06);
        }
        
        .stat-icon {
            font-size: 28px;
        }
        
        .stat h2 {
            font-size: 30px;
            margin: 8px 0 3px;
        }
        
        .stat p {
            color: #6b7280;
        }
        
        .stat.aman {
            border-left: 5px solid #22c55e;
        }
        
        .stat.segera {
            border-left: 5px solid #f59e0b;
        }
        
        .stat.expired {
            border-left: 5px solid #ef4444;
        }
        /* CARD */
        
        .card {
            background: white;
            border-radius: 20px;
            padding: 28px;
            margin-bottom: 25px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, .06);
        }
        
        .title {
            margin-bottom: 20px;
        }
        
        .title h2 {
            margin-bottom: 5px;
        }
        
        .title p {
            color: #6b7280;
        }
        /* SCANNER */
        
        .scanner-container {
            max-width: 700px;
            margin: auto;
        }
        
        .camera-box {
            position: relative;
            width: 100%;
            background: #111827;
            border-radius: 20px;
            overflow: hidden;
            min-height: 350px;
        }
        
        #video {
            width: 100%;
            height: 400px;
            object-fit: cover;
            display: block;
            background: #111827;
        }
        
        .scan-frame {
            position: absolute;
            width: 70%;
            height: 120px;
            border: 3px solid #22c55e;
            border-radius: 15px;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            pointer-events: none;
            box-shadow: 0 0 20px rgba(34, 197, 94, .4);
        }
        
        .scan-frame:after {
            content: "";
            position: absolute;
            left: 5%;
            right: 5%;
            top: 50%;
            height: 2px;
            background: #22c55e;
            box-shadow: 0 0 10px #22c55e;
            animation: scan 1.5s infinite;
        }
        
        @keyframes scan {
            0% {
                transform: translateY(-45px);
            }
            50% {
                transform: translateY(45px);
            }
            100% {
                transform: translateY(-45px);
            }
        }
        
        .camera-status {
            position: absolute;
            bottom: 15px;
            left: 15px;
            right: 15px;
            background: rgba(0, 0, 0, .7);
            color: white;
            padding: 10px;
            border-radius: 10px;
            text-align: center;
            font-size: 14px;
        }
        
        .camera-controls {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 15px;
        }
        
        button {
            border: 0;
            padding: 13px 18px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            transition: .2s;
        }
        
        button:hover {
            transform: translateY(-2px);
        }
        
        .btn-blue {
            background: #2563eb;
            color: white;
        }
        
        .btn-red {
            background: #ef4444;
            color: white;
        }
        
        .btn-green {
            background: #16a34a;
            color: white;
        }
        
        .btn-dark {
            background: #111827;
            color: white;
        }
        
        button:disabled {
            opacity: .5;
            cursor: not-allowed;
            transform: none;
        }
        
        .camera-select {
            flex: 1;
            min-width: 200px;
            padding: 13px;
            border: 1px solid #d1d5db;
            border-radius: 10px;
        }
        /* MANUAL */
        
        .manual {
            margin-top: 25px;
            padding-top: 25px;
            border-top: 1px solid #e5e7eb;
        }
        
        .manual p {
            color: #6b7280;
            margin-bottom: 10px;
        }
        
        .manual-row {
            display: flex;
            gap: 10px;
        }
        
        input,
        select {
            width: 100%;
            padding: 13px;
            border: 1px solid #d1d5db;
            border-radius: 10px;
            font-size: 15px;
        }
        
        .manual-row input {
            flex: 1;
        }
        /* FORM */
        
        .form-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 18px;
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        
        .form-group label {
            font-weight: bold;
        }
        
        .save {
            width: 100%;
            margin-top: 20px;
            background: #7c3aed;
            color: white;
            font-size: 16px;
        }
        /* AI */
        
        .ai-result {
            display: none;
            border-top: 5px solid #7c3aed;
        }
        
        .ai-head {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .robot {
            width: 60px;
            height: 60px;
            border-radius: 17px;
            background: #ede9fe;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
        }
        
        .ai-head p {
            color: #6b7280;
            margin-top: 4px;
        }
        
        .status {
            display: flex;
            gap: 18px;
            align-items: center;
            padding: 20px;
            border-radius: 15px;
            background: #dcfce7;
            margin-bottom: 18px;
        }
        
        .status.warning {
            background: #fef3c7;
        }
        
        .status.danger {
            background: #fee2e2;
        }
        
        .status-icon {
            font-size: 40px;
        }
        
        .speech {
            background: #f8fafc;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 18px;
        }
        
        .speech h3 {
            margin-bottom: 10px;
        }
        
        .speech p {
            line-height: 1.7;
            margin-bottom: 15px;
        }
        
        .recommendation {
            background: #fff7ed;
            padding: 20px;
            border-radius: 15px;
        }
        
        .recipe-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 12px;
            margin-top: 15px;
        }
        
        .recipe {
            background: white;
            padding: 15px;
            border-radius: 12px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, .05);
        }
        /* PRODUCTS */
        
        .products {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 18px;
        }
        
        .product-card {
            border: 1px solid #e5e7eb;
            border-radius: 15px;
            padding: 20px;
        }
        
        .product-card h3 {
            margin-bottom: 10px;
        }
        
        .product-card p {
            color: #6b7280;
            margin: 6px 0;
        }
        
        .badge {
            display: inline-block;
            padding: 6px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
            margin-top: 10px;
        }
        
        .badge.aman {
            background: #dcfce7;
            color: #166534;
        }
        
        .badge.segera {
            background: #fef3c7;
            color: #92400e;
        }
        
        .badge.expired {
            background: #fee2e2;
            color: #991b1b;
        }
        
        .empty {
            color: #6b7280;
            text-align: center;
            padding: 30px;
        }
        /* FOOTER */
        
        footer {
            text-align: center;
            background: #111827;
            color: white;
            padding: 30px;
            line-height: 1.8;
        }
        /* RESPONSIVE */
        
        @media(max-width:800px) {
            .dashboard {
                grid-template-columns: repeat(2, 1fr);
            }
            .form-grid {
                grid-template-columns: 1fr;
            }
        }
        
        @media(max-width:550px) {
            .dashboard {
                grid-template-columns: 1fr;
            }
            .manual-row {
                flex-direction: column;
            }
            .camera-controls {
                flex-direction: column;
            }
            .camera-select {
                width: 100%;
            }
            #video {
                height: 320px;
            }
            .card {
                padding: 20px;
            }
        }
    </style>
</head>

<body>

    <header>

        <div class="logo">

            <div class="logo-icon">
                🤖
            </div>

            <div>
                <h1>ExpiryGuard AI</h1>
                <p>Smart Food Expiry Assistant</p>
            </div>

        </div>

    </header>


    <main>

        <!-- DASHBOARD -->

        <section class="dashboard">

            <div class="stat">

                <div class="stat-icon">📦</div>

                <h2 id="totalProduk">0</h2>

                <p>Total Produk</p>

            </div>


            <div class="stat aman">

                <div class="stat-icon">🟢</div>

                <h2 id="produkAman">0</h2>

                <p>Aman</p>

            </div>


            <div class="stat segera">

                <div class="stat-icon">🟠</div>

                <h2 id="produkSegera">0</h2>

                <p>Segera Expired</p>

            </div>


            <div class="stat expired">

                <div class="stat-icon">🔴</div>

                <h2 id="produkExpired">0</h2>

                <p>Expired</p>

            </div>

        </section>


        <!-- SCANNER -->

        <section class="card">

            <div class="title">

                <h2>📷 Scan Barcode Produk</h2>

                <p>
                    Arahkan barcode produk ke kamera
                </p>

            </div>


            <div class="scanner-container">

                <div class="camera-box">

                    <video id="video" autoplay muted playsinline></video>

                    <div class="scan-frame"></div>

                    <div class="camera-status" id="cameraStatus">
                        Kamera belum dinyalakan
                    </div>

                </div>


                <div class="camera-controls">

                    <button class="btn-blue" id="startBtn" onclick="startCamera()">
                    📷 Mulai Kamera
                </button>


                    <button class="btn-red" id="stopBtn" onclick="stopCamera()" disabled>
                    ⛔ Stop Kamera
                </button>


                    <button class="btn-green" onclick="switchCamera()">
                    🔄 Ganti Kamera
                </button>


                    <select class="camera-select" id="cameraSelect" onchange="changeCamera()">

                    <option value="">
                        Pilih kamera
                    </option>

                </select>

                </div>


                <!-- MANUAL -->

                <div class="manual">

                    <p>
                        Jika kamera tidak bisa membaca barcode, masukkan barcode secara manual.
                    </p>

                    <div class="manual-row">

                        <input type="text" id="barcodeInput" placeholder="Contoh: 8991234567890">

                        <button class="btn-dark" onclick="cariBarcode()">
                        🔎 Cari
                    </button>

                    </div>

                </div>

            </div>

        </section>


        <!-- INFORMASI PRODUK -->

        <section class="card">

            <div class="title">

                <h2>📦 Informasi Produk</h2>

                <p>
                    Data akan otomatis terisi setelah barcode ditemukan.
                </p>

            </div>


            <div class="form-grid">

                <div class="form-group">

                    <label>Barcode</label>

                    <input type="text" id="barcode" placeholder="Barcode">

                </div>


                <div class="form-group">

                    <label>Nama Produk</label>

                    <input type="text" id="namaProduk" placeholder="Nama produk">

                </div>


                <div class="form-group">

                    <label>Kategori</label>

                    <select id="kategori">

                    <option value="Makanan">
                        🍱 Makanan
                    </option>

                    <option value="Minuman">
                        🥤 Minuman
                    </option>

                </select>

                </div>


                <div class="form-group">

                    <label>Tanggal Expired</label>

                    <input type="date" id="tanggalExpired">

                </div>

            </div>


            <button class="save" onclick="simpanProduk()">
            🤖 Simpan & Analisis AI
        </button>

        </section>


        <!-- AI RESULT -->

        <section class="card ai-result" id="aiResult">

            <div class="ai-head">

                <div class="robot">
                    🤖
                </div>

                <div>

                    <h2>AI Food Assistant</h2>

                    <p>
                        Analisis status produk
                    </p>

                </div>

            </div>


            <div class="status" id="statusBox">

                <div class="status-icon" id="statusIcon">
                    🟢
                </div>

                <div>

                    <h2 id="statusText">
                        AMAN
                    </h2>

                    <p id="statusDescription">
                        Produk masih aman.
                    </p>

                </div>

            </div>


            <div class="speech">

                <h3>
                    🤖 AI Mengatakan:
                </h3>

                <p id="aiSpeech">
                    -
                </p>

                <button class="btn-dark" onclick="bicaraAI()">
                🔊 Dengarkan AI
            </button>

            </div>


            <div class="recommendation" id="recommendation">

                <h3>
                    🍳 Rekomendasi Olahan
                </h3>

                <p>
                    Gunakan produk sebelum masa simpannya habis.
                </p>

                <div class="recipe-list" id="recipeList"></div>

            </div>

        </section>


        <!-- LIST PRODUK -->

        <section class="card">

            <div class="title">

                <h2>📋 Daftar Produk</h2>

                <p>
                    Semua produk yang tersimpan di aplikasi.
                </p>

            </div>


            <div class="products" id="productList"></div>

        </section>

    </main>


    <footer>

        <p>© 2026 ExpiryGuard AI</p>

        <p>
            Smart Food Expiry & Recipe Assistant
        </p>

    </footer>


    <script>
        /* =====================================================
                                   DATABASE PRODUK CONTOH
                                ===================================================== */

        const productDatabase = {

            "8991234567890": {
                nama: "Susu UHT",
                kategori: "Minuman"
            },

            "8991001234567": {
                nama: "Roti Tawar",
                kategori: "Makanan"
            },

            "8992001234568": {
                nama: "Keju Cheddar",
                kategori: "Makanan"
            },

            "8993001234569": {
                nama: "Susu Coklat",
                kategori: "Minuman"
            },

            "8994001234570": {
                nama: "Yogurt",
                kategori: "Minuman"
            },

            "8995001234571": {
                nama: "Telur Ayam",
                kategori: "Makanan"
            }

        };


        /* =====================================================
           RESEP
        ===================================================== */

        const recipes = {

            "Susu UHT": [
                "🥞 Pancake",
                "🍞 French Toast",
                "🍮 Puding Susu"
            ],

            "Roti Tawar": [
                "🍞 Garlic Bread",
                "🍮 Bread Pudding",
                "🥪 Sandwich"
            ],

            "Keju Cheddar": [
                "🍝 Mac & Cheese",
                "🍕 Pizza",
                "🥪 Grilled Cheese"
            ],

            "Susu Coklat": [
                "🥤 Milkshake",
                "🍫 Puding Coklat",
                "🥞 Pancake Coklat"
            ],

            "Yogurt": [
                "🥤 Smoothie",
                "🍓 Yogurt Bowl",
                "🍰 Yogurt Cake"
            ],

            "Telur Ayam": [
                "🍳 Omelette",
                "🥚 Telur Balado",
                "🍚 Nasi Goreng Telur"
            ]

        };


        /* =====================================================
           VARIABLE SCANNER
        ===================================================== */

        let stream = null;

        let currentCameraId = null;

        let cameras = [];

        let scanning = false;

        let scanAnimation = null;

        let currentAIText = "";

        let products =
            JSON.parse(
                localStorage.getItem(
                    "expiryProducts"
                )
            ) || [];


        /* =====================================================
           ELEMENT
        ===================================================== */

        const video =
            document.getElementById("video");

        const cameraStatus =
            document.getElementById("cameraStatus");

        const cameraSelect =
            document.getElementById("cameraSelect");

        const startBtn =
            document.getElementById("startBtn");

        const stopBtn =
            document.getElementById("stopBtn");


        /* =====================================================
           CEK BROWSER
        ===================================================== */

        function checkBrowser() {

            if (!navigator.mediaDevices ||
                !navigator.mediaDevices.getUserMedia) {

                cameraStatus.innerText =
                    "❌ Browser tidak mendukung akses kamera.";

                startBtn.disabled = true;

                return false;
            }

            return true;
        }


        /* =====================================================
           AMBIL DAFTAR KAMERA
        ===================================================== */

        async function getCameras() {

            try {

                const devices =
                    await navigator.mediaDevices.enumerateDevices();

                cameras =
                    devices.filter(
                        device =>
                        device.kind === "videoinput"
                    );

                cameraSelect.innerHTML =
                    '<option value="">Pilih kamera</option>';

                cameras.forEach(
                    (camera, index) => {

                        const option =
                            document.createElement("option");

                        option.value =
                            camera.deviceId;

                        option.textContent =
                            camera.label ||
                            `Kamera ${index + 1}`;

                        cameraSelect.appendChild(
                            option
                        );

                    }
                );

            } catch (error) {

                console.error(error);

            }

        }


        /* =====================================================
           MULAI KAMERA
        ===================================================== */

        async function startCamera(deviceId = null) {

            if (!checkBrowser()) {
                return;
            }

            stopCamera(false);

            try {

                const constraints = {

                    audio: false,

                    video: deviceId ? {
                        deviceId: {
                            exact: deviceId
                        }
                    } : {
                        facingMode: {
                            ideal: "environment"
                        },

                        width: {
                            ideal: 1280
                        },

                        height: {
                            ideal: 720
                        }
                    }

                };


                stream =
                    await navigator.mediaDevices
                    .getUserMedia(
                        constraints
                    );


                video.srcObject =
                    stream;


                await video.play();


                const track =
                    stream.getVideoTracks()[0];

                currentCameraId =
                    track.getSettings().deviceId;


                cameraStatus.innerText =
                    "🟢 Kamera aktif. Arahkan barcode ke kotak hijau.";


                startBtn.disabled = true;

                stopBtn.disabled = false;


                await getCameras();


                if (currentCameraId) {

                    cameraSelect.value =
                        currentCameraId;

                }


                mulaiScanBarcode();


            } catch (error) {

                console.error(
                    "Camera error:",
                    error
                );


                let message =
                    "❌ Kamera tidak dapat digunakan.";


                if (error.name === "NotAllowedError") {

                    message =
                        "❌ Izin kamera ditolak. Izinkan kamera di browser.";

                } else if (error.name === "NotFoundError") {

                    message =
                        "❌ Kamera tidak ditemukan.";

                } else if (error.name === "NotReadableError") {

                    message =
                        "❌ Kamera sedang digunakan aplikasi lain.";

                } else if (error.name === "SecurityError") {

                    message =
                        "❌ Browser memblokir kamera. Gunakan HTTPS atau localhost.";

                }


                cameraStatus.innerText =
                    message;


                alert(message);

            }

        }


        /* =====================================================
           STOP CAMERA
        ===================================================== */

        function stopCamera(showMessage = true) {

            scanning = false;


            if (scanAnimation) {

                cancelAnimationFrame(
                    scanAnimation
                );

                scanAnimation = null;

            }


            if (stream) {

                stream
                    .getTracks()
                    .forEach(
                        track =>
                        track.stop()
                    );

                stream = null;

            }


            video.srcObject = null;


            startBtn.disabled = false;

            stopBtn.disabled = true;


            if (showMessage) {

                cameraStatus.innerText =
                    "Kamera dihentikan.";

            }

        }


        /* =====================================================
           GANTI CAMERA
        ===================================================== */

        async function changeCamera() {

            const id =
                cameraSelect.value;

            if (id) {

                await startCamera(id);

            }

        }


        async function switchCamera() {

            if (cameras.length < 2) {

                await getCameras();

            }


            if (cameras.length < 2) {

                alert(
                    "Perangkat hanya memiliki satu kamera."
                );

                return;

            }


            const currentIndex =
                cameras.findIndex(
                    camera =>
                    camera.deviceId ===
                    currentCameraId
                );


            const nextIndex =
                (currentIndex + 1) %
                cameras.length;


            await startCamera(
                cameras[nextIndex].deviceId
            );

        }


        /* =====================================================
           BARCODE SCANNER
        ===================================================== */

        function mulaiScanBarcode() {

            if (!("BarcodeDetector" in window)) {

                cameraStatus.innerText =
                    "⚠️ Scanner otomatis tidak didukung browser ini. Gunakan input barcode manual.";

                return;

            }


            scanning = true;


            const supportedFormats = [
                "aztec",
                "code_128",
                "code_39",
                "code_93",
                "codabar",
                "data_matrix",
                "ean_13",
                "ean_8",
                "itf",
                "pdf417",
                "qr_code",
                "upc_a",
                "upc_e"
            ];


            let detector;


            try {

                detector =
                    new BarcodeDetector({
                        formats: supportedFormats
                    });

            } catch (error) {

                console.log(
                    "Format detector fallback"
                );

                detector =
                    new BarcodeDetector();

            }


            async function scan() {

                if (!scanning ||
                    !stream ||
                    video.readyState <
                    2
                ) {

                    scanAnimation =
                        requestAnimationFrame(
                            scan
                        );

                    return;

                }


                try {

                    const barcodes =
                        await detector.detect(
                            video
                        );


                    if (
                        barcodes &&
                        barcodes.length > 0
                    ) {

                        const code =
                            barcodes[0].rawValue;


                        if (code) {

                            scanning = false;


                            document
                                .getElementById(
                                    "barcodeInput"
                                )
                                .value =
                                code;


                            cameraStatus.innerText =
                                "✅ Barcode ditemukan: " +
                                code;


                            cariBarcode();


                            setTimeout(
                                () => {
                                    if (stream) {
                                        mulaiScanBarcode();
                                    }
                                },
                                1500
                            );


                            return;

                        }

                    }

                } catch (error) {

                    console.log(
                        "Scan:",
                        error
                    );

                }


                scanAnimation =
                    requestAnimationFrame(
                        scan
                    );

            }


            scan();

        }


        /* =====================================================
           CARI BARCODE
        ===================================================== */

        function cariBarcode() {

            const code =
                document
                .getElementById(
                    "barcodeInput"
                )
                .value
                .trim();


            if (!code) {

                alert(
                    "Masukkan barcode terlebih dahulu."
                );

                return;

            }


            document
                .getElementById(
                    "barcode"
                )
                .value =
                code;


            const product =
                productDatabase[code];


            if (product) {

                document
                    .getElementById(
                        "namaProduk"
                    )
                    .value =
                    product.nama;


                document
                    .getElementById(
                        "kategori"
                    )
                    .value =
                    product.kategori;


                alert(
                    "✅ Produk ditemukan!\n\n" +
                    product.nama
                );

            } else {

                document
                    .getElementById(
                        "namaProduk"
                    )
                    .focus();


                alert(
                    "Barcode terbaca: " +
                    code +
                    "\n\nProduk belum ada di database contoh. Silakan masukkan nama produk."
                );

            }

        }


        /* =====================================================
           SIMPAN PRODUK
        ===================================================== */

        function simpanProduk() {

            const barcode =
                document
                .getElementById(
                    "barcode"
                )
                .value
                .trim();


            const nama =
                document
                .getElementById(
                    "namaProduk"
                )
                .value
                .trim();


            const kategori =
                document
                .getElementById(
                    "kategori"
                )
                .value;


            const expired =
                document
                .getElementById(
                    "tanggalExpired"
                )
                .value;


            if (!nama) {

                alert(
                    "Nama produk wajib diisi."
                );

                return;

            }


            if (!expired) {

                alert(
                    "Tanggal expired wajib diisi."
                );

                return;

            }


            const product = {

                id: Date.now(),

                barcode: barcode,

                nama: nama,

                kategori: kategori,

                expired: expired

            };


            products.push(product);


            localStorage.setItem(
                "expiryProducts",
                JSON.stringify(products)
            );


            analisisAI(product);

            tampilkanProduk();

            updateDashboard();

        }


        /* =====================================================
           ANALISIS AI
        ===================================================== */

        function analisisAI(product) {

            const today =
                new Date();

            today.setHours(
                0, 0, 0, 0
            );


            const expiry =
                new Date(
                    product.expired +
                    "T00:00:00"
                );

            expiry.setHours(
                0, 0, 0, 0
            );


            const difference =
                expiry - today;


            const days =
                Math.ceil(
                    difference /
                    (
                        1000 *
                        60 *
                        60 *
                        24
                    )
                );


            let status;

            let icon;

            let description;

            let speech;


            if (days < 0) {

                status =
                    "EXPIRED";

                icon =
                    "🔴";

                description =
                    "Produk sudah melewati tanggal kedaluwarsa.";

                speech =
                    `Produk ${product.nama} sudah expired. Produk ini sebaiknya tidak dikonsumsi atau digunakan untuk membuat makanan.`;

            } else if (days <= 7) {

                status =
                    "SEGERA EXPIRED";

                icon =
                    "🟠";

                description =
                    `Produk akan expired dalam ${days} hari.`;

                speech =
                    `Produk ${product.nama} akan segera expired dalam ${days} hari. Sebaiknya segera digunakan jika kemasan masih baik dan produk tidak menunjukkan tanda kerusakan.`;

            } else {

                status =
                    "AMAN";

                icon =
                    "🟢";

                description =
                    `Produk masih memiliki ${days} hari sebelum tanggal expired.`;

                speech =
                    `Produk ${product.nama} masih dalam masa simpan berdasarkan tanggal yang dimasukkan. Produk memiliki ${days} hari sebelum expired.`;

            }


            currentAIText =
                speech;


            document
                .getElementById(
                    "aiResult"
                )
                .style.display =
                "block";


            document
                .getElementById(
                    "statusIcon"
                )
                .innerText =
                icon;


            document
                .getElementById(
                    "statusText"
                )
                .innerText =
                status;


            document
                .getElementById(
                    "statusDescription"
                )
                .innerText =
                description;


            document
                .getElementById(
                    "aiSpeech"
                )
                .innerText =
                speech;


            const statusBox =
                document.getElementById(
                    "statusBox"
                );


            statusBox.className =
                "status";


            if (status === "SEGERA EXPIRED") {

                statusBox.classList.add(
                    "warning"
                );

            }


            if (status === "EXPIRED") {

                statusBox.classList.add(
                    "danger"
                );

            }


            tampilkanRekomendasi(
                product,
                status
            );


            document
                .getElementById(
                    "aiResult"
                )
                .scrollIntoView({
                    behavior: "smooth"
                });

        }


        /* =====================================================
           REKOMENDASI
        ===================================================== */

        function tampilkanRekomendasi(
            product,
            status
        ) {

            const recommendation =
                document.getElementById(
                    "recommendation"
                );


            const recipeList =
                document.getElementById(
                    "recipeList"
                );


            recipeList.innerHTML = "";


            if (status === "EXPIRED") {

                recommendation.style.display =
                    "none";

                return;

            }


            recommendation.style.display =
                "block";


            const list =
                recipes[product.nama] || [
                    "🍳 Omelette",
                    "🥗 Salad",
                    "🍲 Sup",
                    "🥪 Sandwich"
                ];


            list.forEach(
                recipe => {

                    const div =
                        document.createElement(
                            "div"
                        );


                    div.className =
                        "recipe";


                    div.innerText =
                        recipe;


                    recipeList.appendChild(
                        div
                    );

                }
            );

        }


        /* =====================================================
           SUARA AI
        ===================================================== */

        function bicaraAI() {

            if (!currentAIText) {

                alert(
                    "Belum ada hasil analisis AI."
                );

                return;

            }


            if (!("speechSynthesis" in window)) {

                alert(
                    "Browser tidak mendukung Text To Speech."
                );

                return;

            }


            speechSynthesis.cancel();


            const utterance =
                new SpeechSynthesisUtterance(
                    currentAIText
                );


            utterance.lang =
                "id-ID";

            utterance.rate =
                0.9;

            utterance.pitch =
                1;


            speechSynthesis.speak(
                utterance
            );

        }


        /* =====================================================
           HITUNG STATUS
        ===================================================== */

        function hitungStatus(date) {

            const today =
                new Date();

            today.setHours(
                0, 0, 0, 0
            );


            const expiry =
                new Date(
                    date +
                    "T00:00:00"
                );


            expiry.setHours(
                0, 0, 0, 0
            );


            const days =
                Math.ceil(
                    (
                        expiry -
                        today
                    ) /
                    (
                        1000 *
                        60 *
                        60 *
                        24
                    )
                );


            if (days < 0) {

                return {
                    text: "EXPIRED",
                    class: "expired",
                    icon: "🔴"
                };

            }


            if (days <= 7) {

                return {
                    text: "SEGERA EXPIRED",
                    class: "segera",
                    icon: "🟠"
                };

            }


            return {
                text: "AMAN",
                class: "aman",
                icon: "🟢"
            };

        }


        /* =====================================================
           TAMPILKAN PRODUK
        ===================================================== */

        function tampilkanProduk() {

            const container =
                document.getElementById(
                    "productList"
                );


            container.innerHTML = "";


            if (products.length === 0) {

                container.innerHTML =
                    `
            <div class="empty">
                📦 Belum ada produk.
                <br>
                Silakan scan barcode terlebih dahulu.
            </div>
            `;

                return;

            }


            products
                .slice()
                .reverse()
                .forEach(
                    product => {

                        const status =
                            hitungStatus(
                                product.expired
                            );


                        const card =
                            document.createElement(
                                "div"
                            );


                        card.className =
                            "product-card";


                        card.innerHTML = `

                <h3>
                    ${escapeHTML(product.nama)}
                </h3>

                <p>
                    📦 Barcode:
                    ${escapeHTML(
                        product.barcode ||
                        "-"
                    )}
                </p>

                <p>
                    🏷️
                    ${escapeHTML(
                        product.kategori
                    )}
                </p>

                <p>
                    📅 Expired:
                    ${escapeHTML(
                        product.expired
                    )}
                </p>

                <span
                    class="badge ${status.class}"
                >
                    ${status.icon}
                    ${status.text}
                </span>

            `;


                        container.appendChild(
                            card
                        );

                    }
                );

        }


        /* =====================================================
           DASHBOARD
        ===================================================== */

        function updateDashboard() {

            let aman = 0;

            let segera = 0;

            let expired = 0;


            products.forEach(
                product => {

                    const status =
                        hitungStatus(
                            product.expired
                        );


                    if (
                        status.text ===
                        "AMAN"
                    ) {

                        aman++;

                    } else if (
                        status.text ===
                        "SEGERA EXPIRED"
                    ) {

                        segera++;

                    } else {

                        expired++;

                    }

                }
            );


            document.getElementById(
                    "totalProduk"
                ).innerText =
                products.length;


            document.getElementById(
                    "produkAman"
                ).innerText =
                aman;


            document.getElementById(
                    "produkSegera"
                ).innerText =
                segera;


            document.getElementById(
                    "produkExpired"
                ).innerText =
                expired;

        }


        /* =====================================================
           SECURITY HTML
        ===================================================== */

        function escapeHTML(value) {

            return String(value)
                .replace(
                    /&/g,
                    "&amp;"
                )
                .replace(
                    /</g,
                    "&lt;"
                )
                .replace(
                    />/g,
                    "&gt;"
                )
                .replace(
                    /"/g,
                    "&quot;"
                )
                .replace(
                    /'/g,
                    "&#039;"
                );

        }


        /* =====================================================
           INITIAL
        ===================================================== */

        window.addEventListener(
            "load",
            async() => {

                checkBrowser();

                tampilkanProduk();

                updateDashboard();

                await getCameras();

            }
        );


        /* =====================================================
           HANDLE CAMERA DEVICE CHANGE
        ===================================================== */

        if (
            navigator.mediaDevices &&
            navigator.mediaDevices.addEventListener
        ) {

            navigator.mediaDevices.addEventListener(
                "devicechange",
                async() => {

                    await getCameras();

                }
            );

        }
    </script>

</body>

</html>
