
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Report: Enterprise Drone Program Readiness</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #fafaf9;
            color: #1c1917;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 650px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container { height: 400px; }
        }
        .nav-btn.active {
            border-bottom: 3px solid #0d9488;
            color: #0d9488;
            font-weight: 600;
        }
        .tab-content { display: none; }
        .tab-content.active { display: block; animation: fadeIn 0.4s ease-in-out; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .interactive-card {
            background: #ffffff;
            border-radius: 0.75rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05), 0 2px 4px -1px rgba(0, 0, 0, 0.03);
            border: 1px solid #e7e5e4;
        }
        .step-btn.active {
            background-color: #0d9488;
            color: white;
            border-color: #0d9488;
        }
    </style>
</head>
<body class="antialiased selection:bg-teal-100 selection:text-teal-900 flex flex-col min-h-screen">

    <nav class="bg-white sticky top-0 z-50 border-b border-stone-200 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center gap-2 font-bold text-xl text-stone-800 tracking-tight">
                    <span class="text-teal-600 text-2xl">⛑️</span> UAS Programs <span class="font-light text-stone-400">Interactive</span>
                </div>
                <div class="hidden md:flex space-x-8">
                    <button class="nav-btn active px-1 pt-1 text-sm font-medium text-stone-500 hover:text-teal-600 transition-colors" data-target="panel-overview">Overview & Context</button>
                    <button class="nav-btn px-1 pt-1 text-sm font-medium text-stone-500 hover:text-teal-600 transition-colors" data-target="panel-gaps">Interactive Gap Analysis</button>
                    <button class="nav-btn px-1 pt-1 text-sm font-medium text-stone-500 hover:text-teal-600 transition-colors" data-target="panel-forecast">Risk Forecaster</button>
                    <button class="nav-btn px-1 pt-1 text-sm font-medium text-stone-500 hover:text-teal-600 transition-colors" data-target="panel-solution">Readiness Framework</button>
                </div>
            </div>
        </div>
    </nav>

    <header class="bg-stone-900 text-stone-50 py-16 px-6">
        <div class="max-w-4xl mx-auto text-center">
            <h1 class="text-3xl md:text-5xl font-bold mb-4 tracking-tight leading-tight">Bridging the Gap Between <span class="text-teal-400">Drone Operations</span> and <span class="text-amber-400">Aviation Safety</span></h1>
            <p class="text-lg text-stone-300 mb-8 leading-relaxed">Explore the critical vulnerabilities in scaling enterprise drone programs, and interact with the metrics driving the need for formal Safety Management Systems (SMS).</p>
            <button class="bg-teal-600 text-white font-bold py-4 px-10 rounded-full hover:bg-amber-600 transition-colors shadow-lg hover:shadow-xl transform hover:-translate-y-1 duration-200">
                    Initiate Your Program Readiness Check
                </button>
            <div class="inline-flex items-center justify-center space-x-8 border-t border-stone-700 pt-8 mt-4 w-full">
                <div class="text-center">
                    <div class="text-3xl font-black text-teal-400">78%</div>
                    <div class="text-xs uppercase tracking-wider text-stone-400 mt-1">Lack Formal SMS</div>
                </div>
                <div class="h-12 w-px bg-stone-700"></div>
                <div class="text-center">
                    <div class="text-3xl font-black text-amber-400">4.2x</div>
                    <div class="text-xs uppercase tracking-wider text-stone-400 mt-1">Incident Growth YoY</div>
                </div>
            </div>
        </div>
    </header>

    <main class="flex-grow max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 w-full">

        <section id="panel-overview" class="tab-content active">
            <div class="mb-10 text-center">
                <h2 class="text-2xl font-bold text-stone-800 mb-3">The Root of Program Failures</h2>
                <p class="text-stone-600 leading-relaxed max-w-3xl mx-auto">This section identifies vulnerabilities faced by enterprise drone fleets over the past 36 months. Understanding the root causes of failure is the first step toward operational resilience. Interact with the chart to view key insights regarding each category of program failure.</p>
            </div>
            
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-start">
                <div class="interactive-card p-6">
                    <h3 class="text-sm font-semibold uppercase tracking-wider text-stone-500 mb-6 text-center">Failure Root Cause Distribution</h3>
                    <div class="chart-container">
                        <canvas id="causeChart"></canvas>
                    </div>
                    <p class="text-xs text-center text-stone-400 mt-4">Click segments to load contextual analysis.</p>
                </div>
                
                <div class="interactive-card p-8 bg-stone-100 h-full flex flex-col justify-center transition-all duration-300" id="cause-detail-panel">
                    <div class="text-teal-600 text-4xl mb-4" id="cause-icon">🔍</div>
                    <h3 class="text-xl font-bold text-stone-800 mb-3" id="cause-title">Select a category</h3>
                    <p class="text-stone-600 leading-relaxed" id="cause-desc">Click on a segment in the doughnut chart to the left to explore the deep dive qualitative analysis regarding why these specific failures occur in enterprise operations lacking aviation grade safety management.</p>
                    <div class="mt-6 p-4 bg-white border-l-4 border-teal-500 rounded text-sm text-stone-700 hidden" id="cause-stat-box">
                        <span class="font-bold block mb-1">Key Insight:</span>
                        <span id="cause-insight"></span>
                    </div>
                </div>
            </div>
        </section>

        <section id="panel-gaps" class="tab-content">
            <div class="mb-10 text-center">
                <h2 class="text-2xl font-bold text-stone-800 mb-3">Interactive Benchmarking: The Aviation Standard Gap</h2>
                <p class="text-stone-600 leading-relaxed max-w-3xl mx-auto">Traditional aviation relies on stringent protocols (Part 135/121). Drone programs often operate on ad-hoc rules. This section visualizes the disparity. Use the selector below to model different levels of enterprise drone program maturity against the gold standard of crewed aviation safety practices.</p>
            </div>

            <div class="interactive-card p-6 lg:p-10">
                <div class="flex flex-col md:flex-row justify-between items-center mb-8 bg-stone-50 p-4 rounded-lg border border-stone-200">
                    <label for="maturitySelect" class="font-semibold text-stone-700 mb-2 md:mb-0 mr-4">Select Program Maturity Level to Model:</label>
                    <select id="maturitySelect" class="bg-white border border-stone-300 text-stone-900 text-sm rounded-lg focus:ring-teal-500 focus:border-teal-500 block p-2.5 shadow-sm outline-none cursor-pointer">
                        <option value="average">Average Enterprise Program (Status Quo)</option>
                        <option value="novice">Early-Stage / Novice Program</option>
                        <option value="advanced">Advanced (Pre-Audit) Program</option>
                    </select>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-5 gap-8 items-center">
                    <div class="lg:col-span-3">
                        <div class="chart-container">
                            <canvas id="radarChart"></canvas>
                        </div>
                    </div>
                    <div class="lg:col-span-2 space-y-4">
                        <h4 class="font-bold text-stone-800 border-b border-stone-200 pb-2">Analysis Context</h4>
                        <p class="text-sm text-stone-600" id="radar-context">The "Average" enterprise program scores reasonably well in basic flight SOPs but demonstrates a critical, systemic failure in establishing proactive Incident Root Cause Analysis loops and preventative maintenance tracking, relying instead on break:fix methodologies.</p>
                        <div class="bg-amber-50 border border-amber-200 rounded p-4 mt-6">
                            <h5 class="text-amber-800 font-bold text-sm mb-1 flex items-center gap-2"><span class="text-lg">⚠️</span> Critical Vulnerability Identified</h5>
                            <p class="text-xs text-amber-700 leading-relaxed" id="radar-warning">A gap larger than 40 points in 'Risk Assessment' severely limits BVLOS (Beyond Visual Line of Sight) waiver approvals from the FAA.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="panel-forecast" class="tab-content">
            <div class="mb-10 text-center">
                <h2 class="text-2xl font-bold text-stone-800 mb-3">Risk Escalation Forecaster</h2>
                <p class="text-stone-600 leading-relaxed max-w-3xl mx-auto">As flight hours scale exponentially, risk does not scale linearly if foundational safety systems are weak; it compounds. This interactive forecaster demonstrates the projected unmitigated safety incidents relative to flight volume. Toggle between growth scenarios to see the impact of operational scaling without SMS intervention.</p>
            </div>

            <div class="interactive-card p-6">
                <div class="flex justify-center gap-4 mb-8">
                    <button class="scenario-btn px-4 py-2 rounded-full text-sm font-medium border transition-colors bg-teal-600 text-white border-teal-600" data-scenario="moderate">Moderate Scaling (Base Model)</button>
                    <button class="scenario-btn px-4 py-2 rounded-full text-sm font-medium border border-stone-300 text-stone-600 transition-colors" data-scenario="aggressive">Aggressive Automation Scaling</button>
                </div>

                <div class="chart-container relative" style="height: 450px;">
                    <canvas id="mixedChart"></canvas>
                </div>
                
                <div class="mt-8 text-center max-w-2xl mx-auto">
                    <p class="text-sm text-stone-500 font-italics">Without a <span class="text-teal-600 font-bold"> positive safety culture </span> embedded into the operational foundation, safety incidents and unmitigated risks grow at a disproportionate rate to flight volume.</p>
                </div>
            </div>
        </section>

        <section id="panel-solution" class="tab-content">
            <div class="mb-10 text-center">
                <h2 class="text-2xl font-bold text-stone-800 mb-3">The Program Readiness Framework</h2>
                <p class="text-stone-600 leading-relaxed max-w-3xl mx-auto">To mitigate these compounding risks and close the aviation safety gap, we deploy a structured, four phase engagement. This transforms a drone program from a reactive tool into a proactive, aviation-grade operation. Click each phase to reveal the underlying methodology.</p>
            </div>

            <div class="flex flex-col md:flex-row gap-4 mb-8 justify-center">
                <button class="step-btn active px-6 py-3 rounded-lg border border-stone-200 font-semibold text-stone-700 transition-all w-full md:w-auto text-left md:text-center shadow-sm" data-step="1">1. Deep Audit</button>
                <div class="hidden md:flex items-center text-stone-300 font-bold">➔</div>
                <button class="step-btn px-6 py-3 rounded-lg border border-stone-200 font-semibold text-stone-700 hover:bg-stone-50 transition-all w-full md:w-auto text-left md:text-center shadow-sm" data-step="2">2. Gap Analysis</button>
                <div class="hidden md:flex items-center text-stone-300 font-bold">➔</div>
                <button class="step-btn px-6 py-3 rounded-lg border border-stone-200 font-semibold text-stone-700 hover:bg-stone-50 transition-all w-full md:w-auto text-left md:text-center shadow-sm" data-step="3">3. SMS Integration</button>
                <div class="hidden md:flex items-center text-stone-300 font-bold">➔</div>
                <button class="step-btn px-6 py-3 rounded-lg border border-stone-200 font-semibold text-stone-700 hover:bg-stone-50 transition-all w-full md:w-auto text-left md:text-center shadow-sm" data-step="4">4. Monitoring</button>
            </div>

            <div class="interactive-card p-8 bg-white border-t-4 border-teal-600" id="step-detail-container">
                <h3 class="text-2xl font-bold text-stone-800 mb-2" id="step-title">Phase 1: Comprehensive Baseline Audit</h3>
                <p class="text-stone-600 leading-relaxed mb-6" id="step-desc">A forensic review of your current operational reality. We step outside the boardroom and review actual flight logs, maintenance spreadsheets, and pilot currency records to determine ground truth vs. documented policy.</p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-stone-50 p-4 rounded border border-stone-200">
                        <h4 class="font-semibold text-sm text-teal-700 uppercase tracking-wide mb-2">Key Deliverables</h4>
                        <ul class="text-sm text-stone-600 space-y-2 list-disc list-inside" id="step-list">
                            <li>Documentation discrepancy report</li>
                            <li>Pilot currency evaluation matrix</li>
                            <li>Hardware lifecycle review</li>
                        </ul>
                    </div>
                    <div class="bg-stone-50 p-4 rounded border border-stone-200">
                        <h4 class="font-semibold text-sm text-amber-700 uppercase tracking-wide mb-2">Goal</h4>
                        <p class="text-sm text-stone-600" id="step-goal">Establish a factual baseline to prevent building safety systems on inaccurate assumptions regarding current compliance levels.</p>
                    </div>
                </div>
            </div>
            
            <div class="mt-16 text-center">
                <button class="bg-teal-600 text-white font-bold py-4 px-10 rounded-full hover:bg-amber-600 transition-colors shadow-lg hover:shadow-xl transform hover:-translate-y-1 duration-200">
                    Initiate Your Program Readiness Check
                </button>
            </div>
        </section>

    </main>

    <footer class="bg-stone-100 border-t border-stone-200 py-8 text-center text-stone-500 text-sm mt-auto">
        <div class="max-w-7xl mx-auto px-6">
            <p>&copy; 2026 Raptor Aeronautics Analytics. Data visualizations represent modeled benchmarks derived from publicly available UAS industry research, FAA incident records, and crewed aviation safety standards. They are illustrative, not empirical..</p>
        </div>
    </footer>

    <script>
        const wrapLabel = (label, maxChars = 16) => {
            if (label.length <= maxChars) return label;
            const words = label.split(' ');
            const lines = [];
            let currentLine = '';
            words.forEach(word => {
                if ((currentLine + word).length > maxChars) {
                    if (currentLine) lines.push(currentLine.trim());
                    currentLine = word + ' ';
                } else {
                    currentLine += word + ' ';
                }
            });
            if (currentLine) lines.push(currentLine.trim());
            return lines;
        };

        const commonTooltipConfig = {
            callbacks: {
                title: function(tooltipItems) {
                    const item = tooltipItems[0];
                    let label = item.chart.data.labels[item.dataIndex];
                    if (Array.isArray(label)) {
                        return label.join(' ');
                    } else {
                        return label;
                    }
                }
            },
            backgroundColor: 'rgba(28, 25, 23, 0.95)',
            titleFont: { size: 14, family: 'Inter', weight: 'bold' },
            bodyFont: { size: 13, family: 'Inter' },
            padding: 12,
            cornerRadius: 6,
            displayColors: true
        };

        document.querySelectorAll('.nav-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active', 'border-b-[3px]', 'border-teal-600', 'text-teal-600'));
                e.target.classList.add('active', 'border-b-[3px]', 'border-teal-600', 'text-teal-600');
                
                document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
                const targetId = e.target.getAttribute('data-target');
                document.getElementById(targetId).classList.add('active');
            });
        });

        const causeDataDetails = {
            0: { title: "Procedural Compliance", icon: "📑", desc: "Failures occurring when pilots deviate from established Standard Operating Procedures (SOPs). Often symptomatic of overly complex, unreadable, or outdated manual sets that don't reflect field reality.", insight: "Simplifying SOPs and instituting universal preflight checklists reduced these errors by 40% in post-audit programs." },
            1: { title: "Inadequate Training", icon: "👨‍✈️", desc: "Accidents caused by pilots lacking specific training for complex scenarios (e.g., strong magnetic interference, automated flight modes, autonomous system failsafes). Part 107 certification does not equate to mission readiness.", insight: "Programs lacking scenario based training experience 3x higher hardware attrition rates." },
            2: { title: "Hardware/Software", icon: "⚙️", desc: "System failures, firmware glitches, or component degradation. While heavily scrutinized, they represent a minority of total failures compared to human factors.", insight: "Implementing proactive maintenance schedules catches 85% of hardware issues before flight." },
            3: { title: "Environmental Factors", icon: "🌩️", desc: "Loss of assets due to unpredicted micro weather events, sudden wind shear, or bird strikes. Often exacerbated by poor preflight weather risk assessment.", insight: "Applying the impact of environmental factors on aircraft performance (performance optimization) mitigates severe environmental losses." }
        };

        const causeCtx = document.getElementById('causeChart').getContext('2d');
        const causeChart = new Chart(causeCtx, {
            type: 'doughnut',
            data: {
                labels: ['Procedural Non Compliance', 'Inadequate Pilot Training', 'Hardware/Software Failure', 'Unmitigated Environmental Factors'].map(l => wrapLabel(l)),
                datasets: [{
                    data: [42, 31, 18, 9],
                    backgroundColor: ['#1c1917', '#0d9488', '#d97706', '#d6d3d1'],
                    borderWidth: 2,
                    borderColor: '#ffffff',
                    hoverOffset: 6
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '70%',
                plugins: {
                    legend: { position: 'bottom', labels: { font: { family: 'Inter' }, usePointStyle: true, padding: 20, color: '#444' } },
                    tooltip: commonTooltipConfig
                },
                onClick: (event, elements) => {
                    if (elements.length > 0) {
                        const idx = elements[0].index;
                        const data = causeDataDetails[idx];
                        document.getElementById('cause-icon').textContent = data.icon;
                        document.getElementById('cause-title').textContent = data.title;
                        document.getElementById('cause-desc').textContent = data.desc;
                        document.getElementById('cause-insight').textContent = data.insight;
                        document.getElementById('cause-stat-box').classList.remove('hidden');
                        document.getElementById('cause-detail-panel').classList.remove('bg-stone-100');
                        document.getElementById('cause-detail-panel').classList.add('bg-teal-50', 'border', 'border-teal-100');
                    }
                }
            }
        });

        const maturityProfiles = {
            average: {
                data: [50, 70, 45, 25, 60],
                context: "The 'Average' enterprise program scores reasonably well in basic flight SOPs but demonstrates a critical, systemic failure in establishing proactive Incident Root Cause Analysis loops and preventative maintenance tracking, relying instead on break:fix methodologies.",
                warning: "A gap larger than 40 points in 'Risk Assessment' severely limits BVLOS (Beyond Visual Line of Sight) waiver approvals from the FAA."
            },
            novice: {
                data: [20, 40, 20, 10, 30],
                context: "Novice programs heavily rely on hardware capability rather than operational procedure. Training is usually limited to vendor provided basics, and documentation is almost entirely reactive or non existent.",
                warning: "Operating at this maturity level poses severe liability risks. Insurance providers are beginning to aggressively audit programs in this state prior to payout."
            },
            advanced: {
                data: [85, 95, 90, 80, 95],
                context: "Advanced programs have engaged in formal SMS integration. They operate like modern airlines: heavily procedural, utilizing predictive maintenance, continuous training loops, and formal safety reporting cultures.",
                warning: "Even at advanced stages, 'Incident Root Cause Analysis' requires continuous cultural reinforcement to prevent reporting complacency."
            }
        };

        const radarCtx = document.getElementById('radarChart').getContext('2d');
        const radarLabelsRaw = ["Preventative Maintenance", "Pilot Currency", "Preflight Risk Assessment", "Root Cause Analysis", "Standard Operating Procedures"];
        const radarChart = new Chart(radarCtx, {
            type: 'radar',
            data: {
                labels: radarLabelsRaw.map(l => wrapLabel(l)),
                datasets: [
                    {
                        label: 'Crewed Aviation Standard',
                        data: [100, 100, 100, 100, 100],
                        backgroundColor: 'rgba(13, 148, 136, 0.1)',
                        borderColor: '#0d9488',
                        pointBackgroundColor: '#0d9488',
                        borderWidth: 2,
                        borderDash: [5, 5]
                    },
                    {
                        label: 'Program Maturity Profile',
                        data: maturityProfiles.average.data,
                        backgroundColor: 'rgba(217, 119, 6, 0.3)',
                        borderColor: '#d97706',
                        pointBackgroundColor: '#d97706',
                        borderWidth: 2,
                        fill: true
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    tooltip: commonTooltipConfig,
                    legend: { position: 'bottom', labels: { font: { family: 'Inter' }, usePointStyle: true, color: '#444' } }
                },
                scales: {
                    r: {
                        angleLines: { color: 'rgba(0,0,0,0.05)' },
                        grid: { color: 'rgba(0,0,0,0.05)' },
                        pointLabels: { font: { family: 'Inter', size: 12, weight: '500' }, color: '#1c1917' },
                        ticks: { display: false, min: 0, max: 100, stepSize: 20 }
                    }
                }
            }
        });

        document.getElementById('maturitySelect').addEventListener('change', (e) => {
            const profile = maturityProfiles[e.target.value];
            radarChart.data.datasets[1].data = profile.data;
            radarChart.update();
            
            document.getElementById('radar-context').style.opacity = 0;
            document.getElementById('radar-warning').style.opacity = 0;
            
            setTimeout(() => {
                document.getElementById('radar-context').textContent = profile.context;
                document.getElementById('radar-warning').textContent = profile.warning;
                document.getElementById('radar-context').style.opacity = 1;
                document.getElementById('radar-warning').style.opacity = 1;
                document.getElementById('radar-context').style.transition = "opacity 0.3s";
                document.getElementById('radar-warning').style.transition = "opacity 0.3s";
            }, 150);
        });

        const forecastData = {
            moderate: { flightHours: [10, 25, 45, 75, 110, 150], incidents: [5, 14, 38, 85, 150, 240] },
            aggressive: { flightHours: [10, 35, 80, 160, 280, 450], incidents: [5, 22, 75, 190, 410, 780] }
        };

        const mixedCtx = document.getElementById('mixedChart').getContext('2d');
        const mixedLabelsRaw = ["Year 1", "Year 2", "Year 3", "Year 4 (Proj.)", "Year 5 (Proj.)", "Year 6 (Proj.)"];
        const mixedChart = new Chart(mixedCtx, {
            type: 'bar',
            data: {
                labels: mixedLabelsRaw.map(l => wrapLabel(l)),
                datasets: [
                    {
                        type: 'line',
                        label: 'Unmitigated Safety Incidents (Risk)',
                        data: forecastData.moderate.incidents,
                        borderColor: '#d97706',
                        backgroundColor: '#d97706',
                        borderWidth: 3,
                        tension: 0.3,
                        pointRadius: 5,
                        pointHoverRadius: 8,
                        yAxisID: 'y1'
                    },
                    {
                        type: 'bar',
                        label: 'Enterprise Flight Hours (x1000)',
                        data: forecastData.moderate.flightHours,
                        backgroundColor: '#e7e5e4',
                        hoverBackgroundColor: '#d6d3d1',
                        borderRadius: 4,
                        yAxisID: 'y'
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                interaction: { mode: 'index', intersect: false },
                plugins: {
                    tooltip: commonTooltipConfig,
                    legend: { position: 'top', labels: { font: { family: 'Inter' }, usePointStyle: true, color: '#444' } }
                },
                scales: {
                    x: { grid: { display: false }, ticks: { font: { family: 'Inter' }, color: '#444' } },
                    y: {
                        type: 'linear', display: true, position: 'left',
                        title: { display: true, text: 'Flight Hours', font: { family: 'Inter', weight: 'bold' }, color: '#444' },
                        grid: { color: 'rgba(0,0,0,0.05)' }, ticks: { color: '#444' }
                    },
                    y1: {
                        type: 'linear', display: true, position: 'right',
                        title: { display: true, text: 'Safety Incidents', font: { family: 'Inter', weight: 'bold', color: '#d97706' } },
                        grid: { drawOnChartArea: false }, ticks: { color: '#d97706' }
                    }
                }
            }
        });

        document.querySelectorAll('.scenario-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                document.querySelectorAll('.scenario-btn').forEach(b => {
                    b.classList.remove('bg-teal-600', 'text-white', 'border-teal-600');
                    b.classList.add('bg-transparent', 'text-stone-600', 'border-stone-300');
                });
                
                e.target.classList.remove('bg-transparent', 'text-stone-600', 'border-stone-300');
                e.target.classList.add('bg-teal-600', 'text-white', 'border-teal-600');
                
                const scenario = e.target.getAttribute('data-scenario');
                mixedChart.data.datasets[0].data = forecastData[scenario].incidents;
                mixedChart.data.datasets[1].data = forecastData[scenario].flightHours;
                mixedChart.update();
            });
        });

        const stepDetails = {
            "1": {
                title: "Phase 1: Comprehensive Baseline Audit",
                desc: "A forensic review of your current operational reality. We step outside the boardroom and review actual flight logs, maintenance spreadsheets, and pilot currency records to determine ground truth vs. documented policy.",
                list: ["Documentation discrepancy report", "Pilot currency evaluation matrix", "Hardware lifecycle review"],
                goal: "Establish a factual baseline to prevent building safety systems on inaccurate assumptions regarding current compliance levels."
            },
            "2": {
                title: "Phase 2: Safety Gap Analysis",
                desc: "We cross-reference the findings from Phase 1 against established crewed aviation standards. We identify exactly where the procedural gaps lie and score the associated liability risks.",
                list: ["Aviation standard benchmark report", "Liability risk scoring", "Regulatory vulnerability assessment"],
                goal: "Provide executive leadership with a clear, quantified understanding of where the program falls short of defendable aviation standards."
            },
            "3": {
                title: "Phase 3: SMS Architecture & Integration",
                desc: "We don't just point out flaws; we build you the solution. We construct a formal Safety Management System (SMS) scaled specifically for uncrewed operations, including digital reporting tools and updated SOPs.",
                list: ["Customized SMS Manual generation", "Digital risk assessment tool deployment", "Non punitive reporting system setup"],
                goal: "Embed a systemic safety culture into daily operations that satisfies regulators, insurers, and internal risk managers."
            },
            "4": {
                title: "Phase 4: Continuous Metrics Monitoring",
                desc: "An SMS is only as good as its adherence. Phase 4 establishes automated tracking for pilot currency, predictive maintenance schedules, and incident trend analysis to ensure long-term compliance.",
                list: ["Dashboard creation for executive oversight", "Automated currency alert implementation", "Quarterly SMS effectiveness reviews"],
                goal: "Transition the program from reactive hazard management to proactive, data-driven operational excellence."
            }
        };

        document.querySelectorAll('.step-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                document.querySelectorAll('.step-btn').forEach(b => {
                    b.classList.remove('active', 'bg-teal-600', 'text-white', 'border-teal-600');
                    b.classList.add('bg-white', 'text-stone-700');
                });
                e.target.classList.remove('bg-white', 'text-stone-700');
                e.target.classList.add('active', 'bg-teal-600', 'text-white', 'border-teal-600');

                const step = e.target.getAttribute('data-step');
                const data = stepDetails[step];
                
                const container = document.getElementById('step-detail-container');
                container.style.opacity = 0;
                
                setTimeout(() => {
                    document.getElementById('step-title').textContent = data.title;
                    document.getElementById('step-desc').textContent = data.desc;
                    document.getElementById('step-goal').textContent = data.goal;
                    
                    const ul = document.getElementById('step-list');
                    ul.innerHTML = '';
                    data.list.forEach(item => {
                        const li = document.createElement('li');
                        li.textContent = item;
                        ul.appendChild(li);
                    });
                    
                    container.style.opacity = 1;
                    container.style.transition = "opacity 0.3s ease-in-out";
                }, 200);
            });
        });

    </script>
</body>
</html>
