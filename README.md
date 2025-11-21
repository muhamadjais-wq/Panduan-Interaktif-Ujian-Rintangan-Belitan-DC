# Panduan-Interaktif-Ujian-Rintangan-Belitan-DC
<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Panduan Ujian Rintangan Belitan DC</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Chosen Palette: Calm Harmony - Neutrals (gray-50, white) with Blue accent -->
    <!-- Application Structure Plan: A tabbed SPA structure ('Gambaran', 'Prosedur', 'Jadual & Pengiraan') was chosen. This segments the technical topic into a logical, user-controlled flow (What/Why -> How -> Do/Analyze). This is more usable than a long scroll, allowing users to focus on one concept at a time. Interactivity is concentrated in the 'Pengiraan' (Calculation) section, turning a static report into an active learning tool. -->
    <!-- Visualization & Content Choices: 1. Report: Intro -> Goal: Inform -> Viz: Text (HTML) -> Interaction: None -> Justification: Foundational concepts. 2. Report: How-to -> Goal: Organize/Inform -> Viz: HTML/Tailwind step-flow diagram (using borders/flex) -> Interaction: Click-to-expand details -> Justification: Visual flow is clearer than text; interaction hides complexity. (No SVG/Mermaid). 3. Report: Table/Calculation -> Goal: Relate/Analyze -> Viz: HTML Table + Interactive HTML Form (Calculator) + Chart.js Line Chart -> Interaction: User inputs data into calculator, JS computes/displays result; Chart.js visualizes temp-resistance relationship -> Justification: An interactive calculator is far superior to a static example. The chart visually explains *why* the calculation is needed. (No SVG). -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        .chart-container {
            position: relative;
            height: 300px;
            max-height: 300px;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }
        .nav-link.active {
            border-bottom-width: 2px;
            border-color: #2563eb;
            color: #2563eb;
        }
        .content-section {
            display: none;
        }
        .content-section.active {
            display: block;
        }
        .step {
            display: flex;
            align-items: center;
            margin-bottom: 1rem;
        }
        .step-number {
            width: 2.5rem;
            height: 2.5rem;
            border-radius: 50%;
            background-color: #3b82f6;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            flex-shrink: 0;
        }
        .step-line {
            height: 2px;
            width: 2rem;
            background-color: #9ca3af;
        }
        .step-content {
            padding-left: 1rem;
            flex-grow: 1;
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-700 font-sans">

    <div class="container mx-auto p-4 md:p-8 max-w-5xl">
        <header>
            <h1 class="text-3xl md:text-4xl font-bold text-gray-900 text-center mb-8">
                Panduan Interaktif: Ujian Rintangan Belitan DC
            </h1>
        </header>

        <nav class="flex justify-center flex-wrap space-x-2 sm:space-x-4 mb-8 border-b border-gray-300">
            <button class="nav-link py-2 px-3 sm:px-4 font-medium text-gray-600 hover:text-blue-600 active" data-target="gambaran">
                Gambaran Keseluruhan
            </button>
            <button class="nav-link py-2 px-3 sm:px-4 font-medium text-gray-600 hover:text-blue-600" data-target="prosedur">
                Prosedur Ujian
            </button>
            <button class="nav-link py-2 px-3 sm:px-4 font-medium text-gray-600 hover:text-blue-600" data-target="pengiraan">
                Jadual & Pengiraan
            </button>
        </nav>

        <main>
            <section id="gambaran" class="content-section active">
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h2 class="text-2xl font-semibold text-gray-900 mb-4">Apakah Ujian Rintangan Belitan DC?</h2>
                    <p class="mb-4">
                        Ujian Rintangan Belitan DC adalah ujian diagnostik penting yang dilakukan pada mesin elektrik seperti transformer, motor, dan penjana. Ia mengukur rintangan DC (arus terus) bagi belitan (gegelung wayar) di dalam peralatan tersebut. Ujian ini menggunakan Hukum Ohm (R = V/I) dengan menyuntik arus DC yang diketahui dan mengukur voltan yang terhasil.
                    </p>
                    <p class="mb-4">
                        Bahagian ini memberikan pengenalan kepada tujuan dan kepentingan ujian ini. Memahami 'mengapa' adalah langkah pertama sebelum mempelajari 'bagaimana'.
                    </p>
                    
                    <h3 class="text-xl font-semibold text-gray-900 mb-3">Tujuan Utama Ujian</h3>
                    <ul class="list-disc list-inside space-y-2 text-gray-700">
                        <li>
                            <span class="font-medium text-gray-800">Mengesahkan Kesinambungan:</span> Memastikan tiada litar terbuka (belitan putus) di dalam gegelung.
                        </li>
                        <li>
                            <span class="font-medium text-gray-800">Mengesan Litar Pintas:</span> Nilai rintangan yang sangat rendah boleh menunjukkan litar pintas antara lilitan.
                        </li>
                        <li>
                            <span class="font-medium text-gray-800">Memeriksa Sambungan:</span> Mengesan sambungan yang longgar atau berkarat pada terminal atau penukar tap (tap changer).
                        </li>
<li>
                            <span class="font-medium text-gray-800">Penanda Aras (Benchmark):</span> Mewujudkan nilai rintangan asas (baseline) untuk perbandingan dalam ujian penyelenggaraan akan datang.
                        </li>
                        <li>
                            <span class="font-medium text-gray-800">Pengiraan Kerugian:</span> Data rintangan digunakan untuk mengira kerugian I²R (kerugian kuprum) dalam peralatan.
                        </li>
                    </ul>
                </div>
            </section>

            <section id="prosedur" class="content-section">
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h2 class="text-2xl font-semibold text-gray-900 mb-4">Prosedur Langkah-demi-Langkah</h2>
                    <p class="mb-6">
                        Melakukan ujian ini memerlukan ketelitian dan langkah keselamatan. Bahagian ini menggariskan prosedur am. Aliran visual di bawah membantu anda memahami proses dari persediaan hingga selesai. Sentiasa rujuk manual peralatan anda untuk arahan khusus.
                    </p>

                    <div>
                        <div class="step">
                            <div class="step-number">1</div>
                            <div class="step-line hidden sm:block"></div>
                            <div class="step-content">
                                <h3 class="font-semibold text-lg text-gray-800">Keselamatan & Asingan</h3>
                                <p>Pastikan peralatan <span class="font-bold text-red-600">dinyah-tenaga</span> sepenuhnya dan diasingkan daripada litar. Gunakan Prosedur 'Lock-Out, Tag-Out' (LOTO).</p>
                            </div>
                        </div>

                        <div class="step">
                            <div class="step-number">2</div>
                            <div class="step-line hidden sm:block"></div>
                            <div class="step-content">
                                <h3 class="font-semibold text-lg text-gray-800">Sambungan Peralatan Uji</h3>
                                <p>Sambungkan alat pengukur rintangan (ohmmeter atau set ujian khas) merentasi terminal belitan yang hendak diuji (cth., Fasa U ke Fasa V).</p>
                            </div>
                        </div>

                        <div class="step">
                            <div class="step-number">3</div>
                            <div class="step-line hidden sm:block"></div>
                            <div class="step-content">
                                <h3 class="font-semibold text-lg text-gray-800">Rekod Suhu Ambien</h3>
                                <p>Ukur dan rekod suhu belitan (T<sub>m</sub>). Ini adalah <span class="font-bold">kritikal</span> untuk pembetulan kemudian. Gunakan pengimbas haba atau termometer sentuh.</p>
                            </div>
                        </div>

                        <div class="step">
                            <div class="step-number">4</div>
                            <div class="step-line hidden sm:block"></div>
                            <div class="step-content">
                                <h3 class="font-semibold text-lg text-gray-800">Suntik Arus & Stabilkan</h3>
                                <p>Sapukan arus DC. Oleh kerana belitan bersifat induktif, tunggu sehingga bacaan voltan dan arus stabil. Ini mungkin mengambil masa beberapa saat hingga beberapa minit.</p>
                            </div>
                        </div>
                        
                        <div class="step">
                            <div class="step-number">5</div>
                            <div class="step-line hidden sm:block"></div>
                            <div class="step-content">
                                <h3 class="font-semibold text-lg text-gray-800">Ambil Bacaan</h3>
                                <p>Setelah stabil, rekod nilai Arus (I) yang disuntik dan Voltan (V) yang diukur. Kebanyakan alat moden akan mengira Rintangan (R = V/I) secara automatik.</p>
                            </div>
                        </div>
                        
                        <div class="step">
                            <div class="step-number">6</div>
                            <div class="step-line hidden sm:block"></div>
                            <div class="step-content">
                                <h3 class="font-semibold text-lg text-gray-800">Nyahcas (Discharge)</h3>
                                <p>Sebelum memutuskan sambungan, <span class="font-bold text-red-600">nyahcas</span> belitan dengan selamat. Belitan yang dicas boleh menyimpan tenaga yang berbahaya.</p>
                            </div>
                        </div>
                        
                        <div class="step">
                            <div class="step-number">7</div>
                            <div class="step-content">
                                <h3 class="font-semibold text-lg text-gray-800">Ulang & Betulkan</h3>
                                <p>Ulang langkah 2-6 untuk semua belitan (cth., V-W, W-U). Betulkan semua bacaan rintangan kepada suhu standard (cth., 75°C).</p>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <section id="pengiraan" class="content-section">
                <p class="mb-6 text-center">
                    Bahagian ini adalah nadi analisis. Ia menyediakan jadual contoh untuk merekod data anda dan kalkulator interaktif untuk melakukan pembetulan suhu—langkah paling penting dalam mentafsir keputusan anda.
                </p>

                <div class="bg-white p-6 rounded-lg shadow-md mb-6">
                    <h2 class="text-2xl font-semibold text-gray-900 mb-4">Jadual Rekod Ujian (Contoh)</h2>
                    <p class="mb-4">Gunakan jadual seperti ini untuk merekodkan bacaan anda di tapak. Konsistensi adalah kunci.</p>
                    <div class="overflow-x-auto">
                        <table class="min-w-full divide-y divide-gray-200">
                            <thead class="bg-gray-100">
                                <tr>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-600 uppercase tracking-wider">Belitan (Fasa)</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-600 uppercase tracking-wider">Arus Ujian (A)</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-600 uppercase tracking-wider">Voltan Diukur (V)</th>
                                    <th class="px-4 py-3 text-left text-xs font-medium text-gray-600 uppercase tracking-wider">Rintangan Diukur (Ω)</th>
                                </tr>
                            </thead>
                            <tbody class="bg-white divide-y divide-gray-200">
                                <tr>
                                    <td class="px-4 py-3 whitespace-nowrap">Merah - Kuning (U-V)</td>
                                    <td class="px-4 py-3 whitespace-nowrap">10.0 A</td>
                                    <td class="px-4 py-3 whitespace-nowrap">0.150 V</td>
                                    <td class="px-4 py-3 whitespace-nowrap">0.0150 Ω</td>
                                </tr>
                                <tr>
                                    <td class="px-4 py-3 whitespace-nowrap">Kuning - Biru (V-W)</td>
                                    <td class="px-4 py-3 whitespace-nowrap">10.0 A</td>
                                    <td class="px-4 py-3 whitespace-nowrap">0.151 V</td>
                                    <td class="px-4 py-3 whitespace-nowrap">0.0151 Ω</td>
                                </tr>
                                <tr>
                                    <td class="px-4 py-3 whitespace-nowrap">Biru - Merah (W-U)</td>
                                    <td class="px-4 py-3 whitespace-nowrap">10.0 A</td>
                                    <td class="px-4 py-3 whitespace-nowrap">0.149 V</td>
                                    <td class="px-4 py-3 whitespace-nowrap">0.0149 Ω</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-white p-6 rounded-lg shadow-md">
                        <h2 class="text-2xl font-semibold text-gray-900 mb-4">Kalkulator Pembetulan Suhu</h2>
                        <p class="mb-4 text-sm">Rintangan konduktor berubah dengan suhu. Untuk membandingkan keputusan, kita mesti membetulkan semua bacaan kepada suhu standard (T<sub>s</sub>).</p>
                        
                        <div class="space-y-4">
                            <div>
                                <label for="rm" class="block text-sm font-medium text-gray-800">Rintangan Diukur (R<sub>m</sub>) (Ω)</label>
                                <input type="number" id="rm" value="0.0150" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500">
                            </div>
                            <div>
                                <label for="tm" class="block text-sm font-medium text-gray-800">Suhu Ambien/Diukur (T<sub>m</sub>) (°C)</label>
                                <input type="number" id="tm" value="25" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500">
                            </div>
                            <div>
                                <label for="ts" class="block text-sm font-medium text-gray-800">Suhu Standard (T<sub>s</sub>) (°C)</label>
                                <input type="number" id="ts" value="75" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500">
                            </div>
                            <div>
                                <label for="material" class="block text-sm font-medium text-gray-800">Bahan Belitan</label>
                                <select id="material" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500">
                                    <option value="234.5">Kuprum (Copper)</option>
                                    <option value="225">Aluminium</option>
                                </select>
                            </div>
                            
                            <button id="calculateBtn" class="w-full bg-blue-600 text-white font-bold py-2 px-4 rounded-md hover:bg-blue-700 transition duration-300">
                                Kira Rintangan Dibetulkan
                            </button>
                            
                            <div class="mt-4 p-4 bg-gray-100 rounded-md text-center">
                                <h3 class="text-lg font-medium text-gray-800">Rintangan Dibetulkan (R<sub>s</sub>):</h3>
                                <p id="result" class="text-2xl font-bold text-blue-600 mt-1">0.0179 Ω</p>
                            </div>
                            <p class="text-xs text-center text-gray-600 mt-2">Formula: R<sub>s</sub> = R<sub>m</sub> * (K + T<sub>s</sub>) / (K + T<sub>m</sub>)</p>
                        </div>
                    </div>
                    
                    <div class="bg-white p-6 rounded-lg shadow-md">
                        <h2 class="text-2xl font-semibold text-gray-900 mb-4">Visual: Rintangan lwn Suhu</h2>
                        <p class="mb-4 text-sm">Graf ini menunjukkan mengapa pembetulan penting. Rintangan (paksi-Y) bagi gegelung kuprum meningkat secara linear dengan peningkatan suhu (paksi-X).</p>
                        <div class="chart-container">
                            <canvas id="tempChart"></canvas>
                        </div>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const navLinks = document.querySelectorAll('.nav-link');
            const contentSections = document.querySelectorAll('.content-section');
            const calculateBtn = document.getElementById('calculateBtn');

            function updateActiveTab(targetId) {
                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('data-target') === targetId) {
                        link.classList.add('active');
                    }
                });

                contentSections.forEach(section => {
                    section.classList.remove('active');
                    if (section.id === targetId) {
                        section.classList.add('active');
                    }
                });
            }

            navLinks.forEach(link => {
                link.addEventListener('click', (e) => {
                    const targetId = e.currentTarget.getAttribute('data-target');
                    updateActiveTab(targetId);
                });
            });

            function performCalculation() {
                const Rm = parseFloat(document.getElementById('rm').value);
                const Tm = parseFloat(document.getElementById('tm').value);
                const Ts = parseFloat(document.getElementById('ts').value);
                const K = parseFloat(document.getElementById('material').value);
                const resultEl = document.getElementById('result');

                if (isNaN(Rm) || isNaN(Tm) || isNaN(Ts) || isNaN(K)) {
                    resultEl.textContent = "Sila isi semua medan";
                    return;
                }

                const Rs = Rm * (K + Ts) / (K + Tm);
                resultEl.textContent = Rs.toFixed(6) + ' Ω';
            }
            
            calculateBtn.addEventListener('click', performCalculation);

            const ctx = document.getElementById('tempChart').getContext('2d');
            const K_cu = 234.5;
            const R_20 = 1.0; 
            const temperatures = [0, 20, 40, 60, 75, 100];
            const resistances = temperatures.map(T => R_20 * (K_cu + T) / (K_cu + 20));

            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: temperatures.map(t => t + '°C'),
                    datasets: [{
                        label: 'Rintangan Kuprum (Dinormalkan)',
                        data: resistances,
                        borderColor: 'rgb(37, 99, 235)',
                        backgroundColor: 'rgba(37, 99, 235, 0.1)',
                        fill: true,
                        tension: 0.1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: 'Suhu Belitan (°C)'
                            }
                        },
                        y: {
                            title: {
                                display: true,
                                text: 'Rintangan Relatif (Ω)'
                            },
                            beginAtZero: false
                        }
                    },
                    plugins: {
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    let label = context.dataset.label || '';
                                    if (label) {
                                        label += ': ';
                                    }
                                    if (context.parsed.y !== null) {
                                        label += context.parsed.y.toFixed(3) + ' Ω';
                                    }
                                    return label;
                                }
                            }
                        }
                    }
                }
            });

            performCalculation();
            updateActiveTab('gambaran');
        });
    </script>

</body>
</html>
