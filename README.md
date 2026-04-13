 
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Report: Enterprise Drone Program Readiness</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
 
        :root {
            --blackout: #000000;
            --deep-space: #303617;
            --electric-green: #B0CC33;
            --titanium: #D9D9D9;
            --white: #FFFFFF;
        }
 
        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--deep-space);
            color: var(--white);
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
            border-bottom: 3px solid var(--electric-green);
            color: var(--electric-green);
            font-weight: 600;
        }
 
        .tab-content { display: none; }
        .tab-content.active { display: block; animation: fadeIn 0.4s ease-in-out; }
 
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
 
        .interactive-card {
            background: var(--blackout);
            border-radius: 0.75rem;
            box-shadow: 0 4px 24px rgba(0,0,0,0.4);
            border: 1px solid rgba(176, 204, 51, 0.15);
            transition: border-color 0.3s ease;
        }
 
        .interactive-card:hover {
            border-color: rgba(176, 204, 51, 0.35);
        }
 
        .step-btn.active {
            background-color: var(--electric-green);
            color: var(--blackout);
            border-color: var(--electric-green);
            font-weight: 700;
        }
 
        /* Sticky nav */
        .sticky-nav {
            background: rgba(0, 0, 0, 0.92);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(176, 204, 51, 0.2);
        }
 
        /* CTA button */
        .cta-btn {
            background-color: var(--electric-green);
            color: var(--blackout);
            font-weight: 700;
            transition: background-color 0.2s ease, transform 0.2s ease;
        }
 
        .cta-btn:hover {
            background-color: var(--titanium);
            transform: translateY(-2px);
        }
 
        /* Scenario buttons */
        .scenario-btn-active {
            background-color: var(--electric-green) !important;
            color: var(--blackout) !important;
            border-color: var(--electric-green) !important;
            font-weight: 700;
        }
 
        /* Step buttons default */
        .step-btn {
            background: var(--blackout);
            color: var(--titanium);
            border: 1px solid rgba(217,217,217,0.2);
            transition: all 0.2s ease;
        }
 
        .step-btn:hover:not(.active) {
            border-color: var(--electric-green);
            color: var(--electric-green);
        }
 
        /* Cause detail panel */
        .cause-panel-active {
            background: rgba(176, 204, 51, 0.07) !important;
            border: 1px solid rgba(176, 204, 51, 0.25) !important;
        }
 
        /* Stat box */
        .stat-box {
            background: rgba(176, 204, 51, 0.08);
            border-left: 4px solid var(--electric-green);
        }
 
        /* Warning box */
        .warning-box {
            background: rgba(48, 54, 23, 0.8);
            border: 1px solid rgba(176, 204, 51, 0.3);
        }
 
        /* Select element */
        select {
            background-color: var(--blackout) !important;
            color: var(--white) !important;
            border: 1px solid rgba(176, 204, 51, 0.3) !important;
        }
 
        select:focus {
            outline: none;
            border-color: var(--electric-green) !important;
            box-shadow: 0 0 0 2px rgba(176, 204, 51, 0.2);
        }
 
        select option {
            background-color: var(--blackout);
            color: var(--white);
        }
 
        /* Header gradient */
        .hero-header {
            background: linear-gradient(180deg, var(--blackout) 0%, var(--deep-space) 100%);
        }
 
        /* Divider */
        .hero-divider {
            border-color: rgba(176, 204, 51, 0.2);
        }
 
        /* Scenario toggle bar */
        .scenario-bar {
            background: rgba(0,0,0,0.4);
            border: 1px solid rgba(217,217,217,0.1);
            border-radius: 9999px;
            padding: 4px;
            display: inline-flex;
            gap: 4px;
        }
 
        .scenario-btn {
            padding: 8px 20px;
            border-radius: 9999px;
            font-size: 0.875rem;
            font-weight: 500;
            border: none;
            cursor: pointer;
            transition: all 0.2s ease;
            color: var(--titanium);
            background: transparent;
        }
 
        .scenario-btn.active {
            background-color: var(--electric-green);
            color: var(--blackout);
            font-weight: 700;
        }
 
        /* Section labels */
        .section-label {
            display: inline-block;
            border: 1px solid var(--electric-green);
            color: var(--electric-green);
            font-size: 0.65rem;
            font-weight: 700;
            letter-spacing: 0.15em;
            text-transform: uppercase;
            padding: 2px 10px;
            border-radius: 2px;
            margin-bottom: 12px;
        }
 
        /* Stat highlight */
        .stat-value {
            color: var(--electric-green);
            font-weight: 900;
        }
 
        /* Step detail card */
        .step-detail-card {
            background: var(--blackout);
            border-top: 4px solid var(--electric-green);
            border-radius: 0.75rem;
            border-left: 1px solid rgba(176,204,51,0.15);
            border-right: 1px solid rgba(176,204,51,0.15);
            border-bottom: 1px solid rgba(176,204,51,0.15);
        }
 
        /* Deliverables box */
        .deliverables-box {
            background: rgba(176, 204, 51, 0.06);
            border: 1px solid rgba(176, 204, 51, 0.2);
            border-radius: 0.5rem;
        }
 
        .goal-box {
            background: rgba(48, 54, 23, 0.6);
            border: 1px solid rgba(176, 204, 51, 0.15);
            border-radius: 0.5rem;
        }
 
        /* Footer */
        footer {
            background: var(--blackout);
            border-top: 1px solid rgba(176, 204, 51, 0.15);
        }
    </style>
</head>
<body class="antialiased flex flex-col min-h-screen">
 
    <nav class="sticky-nav w-full sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center gap-2 font-bold text-xl tracking-tight" style="color: var(--white);">
                    <img src="RAPTOR LOGO.v4.jpg" alt="Raptor Aeronautics" class="h-12 w-12 object-contain rounded-sm">
                    UAS Safety <span style="color: var(--titanium); font-weight: 300;">Interactive</span>
                </div>
                <div class="hidden md:flex space-x-8">
                    <button class="nav-btn active px-1 pt-1 text-sm font-medium transition-colors" style="color: var(--titanium);" data-target="panel-overview">Overview & Context</button>
                    <button class="nav-btn px-1 pt-1 text-sm font-medium transition-colors" style="color: var(--titanium);" data-target="panel-gaps">Interactive Gap Analysis</button>
                    <button class="nav-btn px-1 pt-1 text-sm font-medium transition-colors" style="color: var(--titanium);" data-target="panel-forecast">Risk Forecaster</button>
                    <button class="nav-btn px-1 pt-1 text-sm font-medium transition-colors" style="color: var(--titanium);" data-target="panel-solution">Readiness Framework</button>
                </div>
            </div>
        </div>
    </nav>
 
    <header class="hero-header text-white py-20 px-6">
        <div class="max-w-4xl mx-auto text-center">
            <span class="section-label">Tactical Intelligence</span>
            <h1 class="text-3xl md:text-5xl font-black mb-4 tracking-tight leading-tight">
                Bridging the Gap Between <span style="color: var(--electric-green);">Drone Operations</span> and <span style="color: var(--titanium);">Aviation Safety</span>
            </h1>
            <p class="text-lg mb-10 leading-relaxed" style="color: var(--titanium);">
                Explore the critical vulnerabilities in scaling enterprise drone programs, and interact with the metrics driving the need for formal Safety Management Systems (SMS).
            </p>
            <button class="cta-btn py-4 px-10 rounded-full shadow-lg text-sm uppercase tracking-widest mb-10">
                Initiate Your Program Readiness Check
            </button>
            <div class="inline-flex items-center justify-center space-x-10 border-t hero-divider pt-8 w-full">
                <div class="text-center">
                    <div class="text-4xl font-black" style="color: var(--electric-green);">78%</div>
                    <div class="text-xs uppercase tracking-wider mt-1" style="color: var(--titanium);">Lack Formal SMS</div>
                </div>
                <div class="h-12 w-px" style="background: rgba(217,217,217,0.2);"></div>
                <div class="text-center">
                    <div class="text-4xl font-black" style="color: var(--titanium);">4.2x</div>
                    <div class="text-xs uppercase tracking-wider mt-1" style="color: var(--titanium);">Incident Growth YoY</div>
                </div>
            </div>
        </div>
    </header>
 
    <main class="flex-grow max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 w-full">
 
        <!-- OVERVIEW -->
        <section id="panel-overview" class="tab-content active">
            <div class="mb-10 text-center">
                <span class="section-label">Root Cause Analysis</span>
                <h2 class="text-2xl font-bold mb-3" style="color: var(--white);">The Root of Program Failures</h2>
                <p class="leading-relaxed max-w-3xl mx-auto" style="color: var(--titanium);">
                    This section identifies vulnerabilities faced by enterprise drone fleets over the past 36 months. Understanding the root causes of failure is the first step toward operational resilience. Interact with the chart to view key insights regarding each category of program failure.
                </p>
            </div>
 
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-start">
                <div class="interactive-card p-6">
                    <h3 class="text-xs font-bold uppercase tracking-widest mb-6 text-center" style="color: var(--titanium);">Failure Root Cause Distribution</h3>
                    <div class="chart-container">
                        <canvas id="causeChart"></canvas>
                    </div>
                    <p class="text-xs text-center mt-4" style="color: rgba(217,217,217,0.5);">Click segments to load contextual analysis.</p>
                </div>
 
                <div class="interactive-card p-8 h-full flex flex-col justify-center transition-all duration-300" id="cause-detail-panel">
                    <div class="text-4xl mb-4" id="cause-icon">🔍</div>
                    <h3 class="text-xl font-bold mb-3" style="color: var(--white);" id="cause-title">Select a category</h3>
                    <p class="leading-relaxed" style="color: var(--titanium);" id="cause-desc">Click on a segment in the doughnut chart to the left to explore the deep dive qualitative analysis regarding why these specific failures occur in enterprise operations lacking aviation grade safety management.</p>
                    <div class="mt-6 p-4 stat-box rounded text-sm hidden" id="cause-stat-box">
                        <span class="font-bold block mb-1" style="color: var(--electric-green);">Key Insight:</span>
                        <span style="color: var(--titanium);" id="cause-insight"></span>
                    </div>
                </div>
            </div>
        </section>
 
        <!-- GAP ANALYSIS -->
        <section id="panel-gaps" class="tab-content">
            <div class="mb-10 text-center">
                <span class="section-label">Maturity Analysis</span>
                <h2 class="text-2xl font-bold mb-3" style="color: var(--white);">Interactive Benchmarking: The Aviation Standard Gap</h2>
                <p class="leading-relaxed max-w-3xl mx-auto" style="color: var(--titanium);">
                    Traditional aviation relies on stringent protocols (Part 135/121). Drone programs often operate on ad-hoc rules. This section visualizes the disparity. Use the selector below to model different levels of enterprise drone program maturity against the gold standard of crewed aviation safety practices.
                </p>
            </div>
 
            <div class="interactive-card p-6 lg:p-10">
                <div class="flex flex-col md:flex-row justify-between items-center mb-8 p-4 rounded-lg" style="background: rgba(176,204,51,0.06); border: 1px solid rgba(176,204,51,0.2);">
                    <label for="maturitySelect" class="font-semibold mb-2 md:mb-0 mr-4" style="color: var(--white);">Select Program Maturity Level to Model:</label>
                    <select id="maturitySelect" class="text-sm rounded-lg block p-2.5 cursor-pointer">
                        <option value="average">Average Enterprise Program (Status Quo)</option>
                        <option value="novice">Early-Stage / Novice Program</option>
                        <option value="advanced">Advanced (Post Audit) Program</option>
                    </select>
                </div>
 
                <div class="grid grid-cols-1 lg:grid-cols-5 gap-8 items-center">
                    <div class="lg:col-span-3">
                        <div class="chart-container">
                            <canvas id="radarChart"></canvas>
                        </div>
                    </div>
                    <div class="lg:col-span-2 space-y-4">
                        <h4 class="font-bold border-b pb-2" style="color: var(--white); border-color: rgba(176,204,51,0.2);">Analysis Context</h4>
                        <p class="text-sm" style="color: var(--titanium);" id="radar-context">The "Average" enterprise program scores reasonably well in basic flight SOPs but demonstrates a critical, systemic failure in establishing proactive Incident Root Cause Analysis loops and preventative maintenance tracking, relying instead on break:fix methodologies.</p>
                        <div class="warning-box rounded p-4 mt-6">
                            <h5 class="font-bold text-sm mb-1 flex items-center gap-2" style="color: var(--electric-green);">
                                <span class="text-lg">⚠️</span> Critical Vulnerability Identified
                            </h5>
                            <p class="text-xs leading-relaxed" style="color: var(--titanium);" id="radar-warning">A gap larger than 40 points in 'Risk Assessment' severely limits BVLOS (Beyond Visual Line of Sight) waiver approvals from the FAA.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
 
        <!-- RISK FORECASTER -->
        <section id="panel-forecast" class="tab-content">
            <div class="mb-10 text-center">
                <span class="section-label">Trend Forecast</span>
                <h2 class="text-2xl font-bold mb-3" style="color: var(--white);">Risk Escalation Forecaster</h2>
                <p class="leading-relaxed max-w-3xl mx-auto" style="color: var(--titanium);">
                    As flight hours scale exponentially, risk does not scale linearly if foundational safety systems are weak; it compounds. This interactive forecaster demonstrates the projected unmitigated safety incidents relative to flight volume. Toggle between growth scenarios to see the impact of operational scaling without SMS intervention.
                </p>
            </div>
 
            <div class="interactive-card p-6">
                <div class="flex justify-center gap-0 mb-8">
                    <div class="scenario-bar">
                        <button class="scenario-btn active" data-scenario="moderate">Moderate Scaling (Base Model)</button>
                        <button class="scenario-btn" data-scenario="aggressive">Aggressive Automation Scaling</button>
                    </div>
                </div>
 
                <div class="chart-container relative" style="height: 450px;">
                    <canvas id="mixedChart"></canvas>
                </div>
 
                <div class="mt-8 text-center max-w-2xl mx-auto">
                    <p class="text-sm" style="color: var(--titanium);">Without a <span style="color: var(--electric-green); font-weight: 700;">positive safety culture</span> embedded into the operational foundation, safety incidents and unmitigated risks grow at a disproportionate rate to flight volume.</p>
                </div>
            </div>
        </section>
 
        <!-- READINESS FRAMEWORK -->
        <section id="panel-solution" class="tab-content">
            <div class="mb-10 text-center">
                <span class="section-label">Phased Integration</span>
                <h2 class="text-2xl font-bold mb-3" style="color: var(--white);">The Program Readiness Framework</h2>
                <p class="leading-relaxed max-w-3xl mx-auto" style="color: var(--titanium);">
                    To mitigate these compounding risks and close the aviation safety gap, we deploy a structured, four phase engagement. This transforms a drone program from a reactive tool into a proactive, aviation grade operation. Click each phase to reveal the underlying methodology.
                </p>
            </div>
 
            <div class="flex flex-col md:flex-row gap-4 mb-8 justify-center">
                <button class="step-btn active px-6 py-3 rounded-lg font-semibold transition-all w-full md:w-auto text-left md:text-center" data-step="1">1. Deep Audit</button>
                <div class="hidden md:flex items-center font-bold" style="color: rgba(217,217,217,0.3);">➔</div>
                <button class="step-btn px-6 py-3 rounded-lg font-semibold transition-all w-full md:w-auto text-left md:text-center" data-step="2">2. Gap Analysis</button>
                <div class="hidden md:flex items-center font-bold" style="color: rgba(217,217,217,0.3);">➔</div>
                <button class="step-btn px-6 py-3 rounded-lg font-semibold transition-all w-full md:w-auto text-left md:text-center" data-step="3">3. SMS Integration</button>
                <div class="hidden md:flex items-center font-bold" style="color: rgba(217,217,217,0.3);">➔</div>
                <button class="step-btn px-6 py-3 rounded-lg font-semibold transition-all w-full md:w-auto text-left md:text-center" data-step="4">4. Monitoring</button>
            </div>
 
            <div class="step-detail-card p-8" id="step-detail-container">
                <h3 class="text-2xl font-bold mb-2" style="color: var(--white);" id="step-title">Phase 1: Comprehensive Baseline Audit</h3>
                <p class="leading-relaxed mb-6" style="color: var(--titanium);" id="step-desc">A forensic review of your current operational reality. We step outside the boardroom and review actual flight logs, maintenance spreadsheets, and pilot currency records to determine ground truth vs. documented policy.</p>
 
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="deliverables-box p-4">
                        <h4 class="font-semibold text-sm uppercase tracking-wide mb-2" style="color: var(--electric-green);">Key Deliverables</h4>
                        <ul class="text-sm space-y-2 list-disc list-inside" style="color: var(--titanium);" id="step-list">
                            <li>Documentation discrepancy report</li>
                            <li>Pilot currency evaluation matrix</li>
                            <li>Hardware lifecycle review</li>
                        </ul>
                    </div>
                    <div class="goal-box p-4">
                        <h4 class="font-semibold text-sm uppercase tracking-wide mb-2" style="color: var(--titanium);">Goal</h4>
                        <p class="text-sm" style="color: var(--titanium);" id="step-goal">Establish a factual baseline to prevent building safety systems on inaccurate assumptions regarding current compliance levels.</p>
                    </div>
                </div>
            </div>
 
            <div class="mt-16 text-center">
                <button class="cta-btn py-4 px-10 rounded-full shadow-lg text-sm uppercase tracking-widest">
                    Initiate Your Program Readiness Check
                </button>
            </div>
        </section>
 
    </main>
 
    <footer class="py-8 text-center text-sm mt-auto" style="color: var(--titanium);">
        <div class="max-w-7xl mx-auto px-6">
            <p>&copy; 2026 Raptor Aeronautics LLC | Data visualizations reflect modeled industry trends, derived from publicly available FAA incident data, HFACS research on unmanned systems and IS-BAO Stage 3 operating standards.</p>
        </div>
    </footer>
 
    <script>
        // Chart.js global defaults
        Chart.defaults.color = '#D9D9D9';
        Chart.defaults.font.family = 'Inter';
 
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
                    if (Array.isArray(label)) return label.join(' ');
                    return label;
                }
            },
            backgroundColor: 'rgba(0, 0, 0, 0.95)',
            titleFont: { size: 14, family: 'Inter', weight: 'bold' },
            bodyFont: { size: 13, family: 'Inter' },
            padding: 12,
            cornerRadius: 6,
            displayColors: true,
            titleColor: '#B0CC33',
            bodyColor: '#D9D9D9'
        };
 
        // NAV
        document.querySelectorAll('.nav-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                document.querySelectorAll('.nav-btn').forEach(b => {
                    b.classList.remove('active');
                    b.style.color = '#D9D9D9';
                });
                e.target.classList.add('active');
                e.target.style.color = '#B0CC33';
                document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
                document.getElementById(e.target.getAttribute('data-target')).classList.add('active');
            });
        });
 
        // DOUGHNUT
        const causeDataDetails = {
            0: { title: "Procedural Compliance", icon: "📑", desc: "Failures occurring when pilots deviate from established Standard Operating Procedures (SOPs). Often symptomatic of overly complex, unreadable, or outdated manual sets that don't reflect field reality.", insight: "Simplifying SOPs and instituting universal preflight checklists reduced these errors by 40% in post audit programs." },
            1: { title: "Inadequate Training", icon: "👨‍✈️", desc: "Accidents caused by pilots lacking specific training for complex scenarios (e.g., strong magnetic interference, automated flight modes, autonomous system failsafes). Part 107 certification does not equate to mission readiness.", insight: "Programs lacking scenario based training experience 3x higher hardware attrition rates." },
            2: { title: "Hardware/Software", icon: "⚙️", desc: "System failures, firmware glitches, or component degradation. While heavily scrutinized, they represent a minority of total failures compared to human factors.", insight: "Implementing proactive maintenance schedules catches 85% of hardware issues before flight." },
            3: { title: "Environmental Factors", icon: "🌩️", desc: "Loss of assets due to unpredicted micro weather events, sudden wind shear, or bird strikes. Often exacerbated by poor preflight weather risk assessment.", insight: "Applying the impact of environmental factors on aircraft performance mitigates severe environmental losses." }
        };
 
        const causeCtx = document.getElementById('causeChart').getContext('2d');
        const causeChart = new Chart(causeCtx, {
            type: 'doughnut',
            data: {
                labels: ['Procedural Non Compliance', 'Inadequate Pilot Training', 'Hardware/Software Failure', 'Unmitigated Environmental Factors'].map(l => wrapLabel(l)),
                datasets: [{
                    data: [42, 31, 18, 9],
                    backgroundColor: ['#B0CC33', '#FFFFFF', '#D9D9D9', '#303617'],
                    borderWidth: 2,
                    borderColor: '#000000',
                    hoverOffset: 6
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '70%',
                plugins: {
                    legend: { position: 'bottom', labels: { font: { family: 'Inter' }, usePointStyle: true, padding: 20, color: '#D9D9D9' } },
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
                        document.getElementById('cause-detail-panel').classList.add('cause-panel-active');
                    }
                }
            }
        });
 
        // RADAR
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
                        backgroundColor: 'rgba(217, 217, 217, 0.08)',
                        borderColor: '#D9D9D9',
                        pointBackgroundColor: '#D9D9D9',
                        borderWidth: 2,
                        borderDash: [5, 5]
                    },
                    {
                        label: 'Program Maturity Profile',
                        data: maturityProfiles.average.data,
                        backgroundColor: 'rgba(176, 204, 51, 0.25)',
                        borderColor: '#B0CC33',
                        pointBackgroundColor: '#B0CC33',
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
                    legend: { position: 'bottom', labels: { font: { family: 'Inter' }, usePointStyle: true, color: '#D9D9D9' } }
                },
                scales: {
                    r: {
                        min: 0,
                        max: 100,
                        angleLines: { color: 'rgba(176, 204, 51, 0.1)' },
                        grid: { color: 'rgba(176, 204, 51, 0.1)' },
                        pointLabels: { font: { family: 'Inter', size: 12, weight: '500' }, color: '#D9D9D9' },
                        ticks: { display: false, stepSize: 20 }
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
 
        // MIXED CHART
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
                        borderColor: '#B0CC33',
                        backgroundColor: '#B0CC33',
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
                        backgroundColor: 'rgba(217, 217, 217, 0.2)',
                        hoverBackgroundColor: 'rgba(217, 217, 217, 0.35)',
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
                    legend: { position: 'top', labels: { font: { family: 'Inter' }, usePointStyle: true, color: '#D9D9D9' } }
                },
                scales: {
                    x: { grid: { display: false }, ticks: { font: { family: 'Inter' }, color: '#D9D9D9' } },
                    y: {
                        type: 'linear', display: true, position: 'left',
                        title: { display: true, text: 'Flight Hours', font: { family: 'Inter', weight: 'bold' }, color: '#D9D9D9' },
                        grid: { color: 'rgba(176, 204, 51, 0.08)' },
                        ticks: { color: '#D9D9D9' }
                    },
                    y1: {
                        type: 'linear', display: true, position: 'right',
                        title: { display: true, text: 'Safety Incidents', font: { family: 'Inter', weight: 'bold' }, color: '#B0CC33' },
                        grid: { drawOnChartArea: false },
                        ticks: { color: '#B0CC33' }
                    }
                }
            }
        });
 
        document.querySelectorAll('.scenario-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                document.querySelectorAll('.scenario-btn').forEach(b => b.classList.remove('active'));
                e.target.classList.add('active');
                const scenario = e.target.getAttribute('data-scenario');
                mixedChart.data.datasets[0].data = forecastData[scenario].incidents;
                mixedChart.data.datasets[1].data = forecastData[scenario].flightHours;
                mixedChart.update();
            });
        });
 
        // STEP DETAILS
        const stepDetails = {
            "1": {
                title: "Phase 1: Comprehensive Baseline Audit",
                desc: "A forensic review of your current operational reality. We step outside the boardroom and review actual flight logs, maintenance spreadsheets, and pilot currency records to determine ground truth vs. documented policy.",
                list: ["Documentation discrepancy report", "Pilot currency evaluation matrix", "Hardware lifecycle review"],
                goal: "Establish a factual baseline to prevent building safety systems on inaccurate assumptions regarding current compliance levels."
            },
            "2": {
                title: "Phase 2: Safety Gap Analysis",
                desc: "We cross reference the findings from Phase 1 against established crewed aviation standards. We identify exactly where the procedural gaps lie and score the associated liability risks.",
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
                desc: "An SMS is only as good as its adherence. Phase 4 establishes automated tracking for pilot currency, predictive maintenance schedules, and incident trend analysis to ensure long term compliance.",
                list: ["Dashboard creation for executive oversight", "Automated currency alert implementation", "Quarterly SMS effectiveness reviews"],
                goal: "Transition the program from reactive hazard management to proactive, data driven operational excellence."
            }
        };
 
        document.querySelectorAll('.step-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                document.querySelectorAll('.step-btn').forEach(b => b.classList.remove('active'));
                e.target.classList.add('active');
 
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
