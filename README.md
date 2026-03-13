<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Familienausflug - Gemeinsam abstimmen</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
 
        :root {
            --primary: #667eea;
            --light-bg: #F3F4F9;
            --accent: #1A1A2E;
            --success: #06D6A0;
            --card-shadow: 0 10px 40px rgba(102, 126, 234, 0.15);
            --transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        }
 
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #667eea 100%);
            min-height: 100vh;
            color: #333;
            padding: 10px;
        }
 
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            overflow: hidden;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }
 
        /* Header */
        .header {
            background: #667eea;
            color: white;
            padding: 30px 20px;
            text-align: center;
            animation: slideDown 0.6s ease-out;
        }
 
        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            font-weight: 700;
        }
 
        .header p {
            font-size: 1.1em;
            opacity: 0.95;
        }
 
        /* Progress Bar */
        .progress-container {
            background: var(--light-bg);
            padding: 20px;
        }
 
        .progress-steps {
            display: flex;
            gap: 10px;
            justify-content: space-between;
            margin-bottom: 15px;
        }
 
        .step-dot {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: white;
            border: 2px solid #ddd;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: #999;
            transition: var(--transition);
            cursor: pointer;
        }
 
        .step-dot.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
            transform: scale(1.1);
        }
 
        .step-dot.completed {
            background: var(--success);
            color: white;
            border-color: var(--success);
        }
 
        .progress-bar {
            height: 4px;
            background: #e0e0e0;
            border-radius: 2px;
            overflow: hidden;
        }
 
        .progress-fill {
            height: 100%;
            background: var(--primary);
            transition: width 0.5s ease;
        }
 
        /* Content */
        .content {
            flex: 1;
            padding: 30px 20px;
            animation: fadeIn 0.5s ease-out;
        }
 
        .step {
            display: none;
        }
 
        .step.active {
            display: block;
            animation: fadeIn 0.5s ease-out;
        }
 
        /* Welcome Step */
        .welcome-content {
            text-align: center;
        }
 
        .emoji {
            font-size: 4em;
            margin: 20px 0;
            animation: bounce 2s infinite;
        }
 
        .welcome-content h2 {
            font-size: 1.8em;
            color: var(--accent);
            margin: 20px 0;
            font-weight: 600;
        }
 
        .welcome-content p {
            font-size: 1.05em;
            color: #666;
            line-height: 1.6;
            margin: 15px 0;
        }
 
        .link-box {
            background: rgba(102, 126, 234, 0.08);
            border: 2px solid #667eea;
            border-radius: 15px;
            padding: 15px;
            margin: 20px 0;
            cursor: pointer;
            transition: var(--transition);
        }
 
        .link-box:hover {
            transform: translateY(-3px);
            box-shadow: var(--card-shadow);
        }
 
        .link-box a {
            color: #667eea;
            text-decoration: none;
            font-weight: bold;
            word-break: break-all;
        }
 
        /* Route Selection */
        .person-section {
            background: var(--light-bg);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 25px;
            border-left: 5px solid #667eea;
        }
 
        .person-section h3 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.3em;
        }
 
        .route-intro {
            background: white;
            border: 2px solid #667eea;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            text-align: center;
        }
 
        .route-intro h4 {
            color: #667eea;
            font-size: 1.1em;
            margin-bottom: 10px;
        }
 
        .route-intro p {
            color: #666;
            font-size: 0.95em;
            line-height: 1.5;
        }
 
        .route-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
            max-height: 400px;
            overflow-y: auto;
        }
 
        .route-item {
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 12px;
            padding: 15px;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 12px;
        }
 
        .route-item:hover {
            border-color: #667eea;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.1);
            transform: translateX(5px);
        }
 
        .route-item.selected {
            background: rgba(102, 126, 234, 0.08);
            border-color: #667eea;
            font-weight: 600;
        }
 
        .route-checkbox {
            width: 24px;
            height: 24px;
            border: 2px solid #ddd;
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: var(--transition);
            flex-shrink: 0;
        }
 
        .route-item.selected .route-checkbox {
            background: #667eea;
            border-color: #667eea;
            color: white;
        }
 
        .route-info {
            flex: 1;
        }
 
        .route-name {
            font-weight: bold;
            color: var(--accent);
            display: block;
            margin-bottom: 3px;
        }
 
        .route-desc {
            font-size: 0.85em;
            color: #999;
        }
 
        /* Date Selection */
        .calendar-container {
            background: var(--light-bg);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 25px;
        }
 
        .calendar-container h4 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.1em;
        }
 
        .month-selector {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 25px;
        }
 
        .month-btn {
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            padding: 12px;
            cursor: pointer;
            transition: var(--transition);
            text-align: center;
            font-weight: 500;
            color: #666;
            font-size: 0.9em;
        }
 
        .month-btn:hover {
            border-color: #667eea;
        }
 
        .month-btn.selected {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }
 
        .day-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(50px, 1fr));
            gap: 8px;
        }
 
        .day-btn {
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            padding: 10px 5px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.85em;
        }
 
        .day-btn:hover {
            border-color: #667eea;
            transform: scale(1.05);
        }
 
        .day-btn.selected {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }
 
        .day-label {
            font-weight: bold;
            display: block;
            font-size: 0.7em;
            color: #666;
        }
 
        .day-number {
            display: block;
            font-weight: bold;
        }
 
        /* Results */
        .results-container {
            text-align: center;
        }
 
        .results-container h2 {
            color: var(--accent);
            margin-bottom: 25px;
            font-size: 1.6em;
        }
 
        .results-section {
            margin-bottom: 30px;
        }
 
        .results-section h3 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.2em;
            text-align: left;
        }
 
        .ranking-item {
            background: white;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 15px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
            animation: slideUp 0.5s ease-out;
        }
 
        .ranking-position {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: #667eea;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 1.3em;
            flex-shrink: 0;
        }
 
        .ranking-info {
            flex: 1;
            text-align: left;
        }
 
        .ranking-title {
            font-weight: bold;
            color: var(--accent);
            margin-bottom: 3px;
        }
 
        .ranking-votes {
            font-size: 0.9em;
            color: #666;
        }
 
        .vote-bar {
            width: 100%;
            height: 6px;
            background: #e0e0e0;
            border-radius: 3px;
            margin-top: 8px;
            overflow: hidden;
        }
 
        .vote-bar-fill {
            height: 100%;
            background: #667eea;
            transition: width 0.5s ease-out;
            border-radius: 3px;
        }
 
        /* Buttons */
        .button-group {
            display: flex;
            gap: 10px;
            margin-top: 30px;
            flex-wrap: wrap;
            justify-content: center;
        }
 
        button {
            padding: 14px 30px;
            border: none;
            border-radius: 12px;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
            transition: var(--transition);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
 
        .btn-primary {
            background: #667eea;
            color: white;
            flex: 1;
            min-width: 150px;
        }
 
        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.3);
        }
 
        .btn-secondary {
            background: white;
            color: #667eea;
            border: 2px solid #667eea;
            flex: 1;
            min-width: 150px;
        }
 
        .btn-secondary:hover {
            background: var(--light-bg);
        }
 
        .btn-small {
            padding: 10px 20px;
            font-size: 0.9em;
            min-width: auto;
        }
 
        /* Animations */
        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
 
        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
 
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
 
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
 
        /* Mobile */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 2em;
            }
 
            .content {
                padding: 20px 15px;
            }
 
            .button-group {
                flex-direction: column;
            }
 
            button {
                width: 100%;
            }
 
            .month-selector {
                grid-template-columns: repeat(2, 1fr);
            }
 
            .step-dot {
                width: 35px;
                height: 35px;
                font-size: 0.9em;
            }
        }
 
        @media (max-width: 480px) {
            body {
                padding: 0;
            }
 
            .container {
                border-radius: 0;
                min-height: 100vh;
            }
 
            .header {
                padding: 20px 15px;
            }
 
            .header h1 {
                font-size: 1.6em;
            }
 
            .month-selector {
                grid-template-columns: repeat(2, 1fr);
            }
 
            .day-grid {
                grid-template-columns: repeat(3, 1fr);
            }
 
            .route-list {
                max-height: 300px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <h1>🎉 Familienausflug</h1>
            <p>Gemeinsam zum perfekten Abenteuer</p>
        </div>
 
        <!-- Progress -->
        <div class="progress-container">
            <div class="progress-steps">
                <div class="step-dot active" data-step="0">1</div>
                <div class="step-dot" data-step="1">2</div>
                <div class="step-dot" data-step="2">3</div>
                <div class="step-dot" data-step="3">4</div>
            </div>
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
        </div>
 
        <!-- Content -->
        <div class="content">
            <!-- Step 1: Welcome -->
            <div class="step active" data-step="0">
                <div class="welcome-content">
                    <div class="emoji">🎂</div>
                    <h2>Willkommen!</h2>
                    <p>Wir haben eine besondere Überraschung für euch vorbereitet.</p>
                    <p>Gemeinsam wollen wir einen unvergesslichen Ausflug unternehmen!</p>
                    
                    <p style="margin-top: 30px; color: #666; font-size: 0.95em;">
                        Inspirieren lassen? Schaut auf <strong>Suisse Partout</strong>:
                    </p>
                    <div class="link-box">
                        <a href="https://suissepartout.ch/de/" target="_blank">
                            🌍 Zur Ausflugsdatenbank
                        </a>
                    </div>
 
                    <p style="margin-top: 20px; font-size: 0.9em; color: #999;">
                        Dann wählt jeder seine Top 3 Lieblings-Ausflüge aus und wir bestimmen gemeinsam den besten Termin!
                    </p>
                </div>
                <div class="button-group">
                    <button class="btn-primary" onclick="nextStep()">Jetzt starten →</button>
                </div>
            </div>
 
            <!-- Step 2: Route Selection (nacheinander pro Person) -->
            <div class="step" data-step="1">
                <div id="routeContainer"></div>
                <div class="button-group">
                    <button class="btn-secondary btn-small" onclick="prevStep()">← Zurück</button>
                    <button class="btn-primary" onclick="nextStep()">Weiter →</button>
                </div>
            </div>
 
            <!-- Step 3: Date Selection (Monat → Tage) -->
            <div class="step" data-step="2">
                <div id="dateContainer"></div>
                <div class="button-group">
                    <button class="btn-secondary btn-small" onclick="prevStep()">← Zurück</button>
                    <button class="btn-primary" onclick="nextStep()">Zu den Ergebnissen →</button>
                </div>
            </div>
 
            <!-- Step 4: Results -->
            <div class="step" data-step="3">
                <div class="results-container">
                    <h2>🏆 Die Ergebnisse sind da!</h2>
                    
                    <div class="results-section">
                        <h3>Top Ausflüge:</h3>
                        <div id="resultsRanking"></div>
                    </div>
 
                    <div class="results-section">
                        <h3>📅 Beste Termine:</h3>
                        <div id="dateResults"></div>
                    </div>
 
                    <div style="margin-top: 30px; padding: 15px; background: var(--light-bg); border-radius: 10px;">
                        <p style="color: #666; font-size: 0.9em; margin-bottom: 10px;">
                            💡 <strong>Nächste Schritte:</strong>
                        </p>
                        <p style="color: #666; font-size: 0.9em; line-height: 1.6;">
                            1. Den #1 Ausflug auswählen<br>
                            2. Den besten Termin festlegen<br>
                            3. Das Abenteuer wird Realität! 🚀
                        </p>
                    </div>
                </div>
                <div class="button-group">
                    <button class="btn-secondary btn-small" onclick="resetAll()">Nochmal von vorne</button>
                    <button class="btn-primary" onclick="shareResults()">Teilen</button>
                </div>
            </div>
        </div>
    </div>
 
    <script>
        // Alle verfügbaren Ausflüge (erweiterbar)
        const allRoutes = [
            { name: 'Wanderung Appenzell Alps', desc: 'Wunderschöne Berglandschaft', region: 'Ostschweiz' },
            { name: 'Rhine Falls', desc: 'Europas grösster Wasserfall', region: 'Zürich' },
            { name: 'Jungfraujoch', desc: 'Top of Europe - 3454m', region: 'Berner Oberland' },
            { name: 'Luzerner Seenfahrt', desc: 'Entspannungsfahrt mit Schiff', region: 'Zentralschweiz' },
            { name: 'Gorges du Trient', desc: 'Abenteuer-Klettersteig', region: 'Wallis' },
            { name: 'Axalp-Panorama', desc: 'Atemberaubender Aussichtspunkt', region: 'Berner Oberland' },
            { name: 'Rigi Kulm', desc: 'Klassische Bergbahn-Wanderung', region: 'Zentralschweiz' },
            { name: 'Oeschinen Lake', desc: 'Kristallklares Bergwasser', region: 'Berner Oberland' },
            { name: 'Säntis', desc: 'Mit nostalgischer Appenzell-Bahn', region: 'Ostschweiz' },
            { name: 'Creux du Van', desc: 'Spektakuläre Felswände', region: 'Jura' },
            { name: 'Mont-Blanc Umrundung', desc: 'Mehrtagesausflug möglich', region: 'Wallis' },
            { name: 'Blausee', desc: 'Durchsichtiges Bergsee-Wunder', region: 'Interlaken' },
            { name: 'Lauterbrunnen Tal', desc: 'Wasserfälle & Wanderungen', region: 'Berner Oberland' },
            { name: 'Schaffhausen Altstadt', desc: 'Mittelalterlicher Charme', region: 'Schaffhausen' },
            { name: 'Pizol Panorama', desc: 'Aussichtsreiche Bergwanderung', region: 'St. Gallen' },
        ];
 
        const config = {
            people: ['Person 1', 'Person 2', 'Person 3'],
            routes: allRoutes,
        };
 
        let currentStep = 0;
        let currentPersonRoute = 0;
        let selectedMonth = null;
        let currentPersonDate = 0;
 
        let data = {
            selections: {},
            dates: {},
        };
 
        // ===== INITIALIZATION =====
        function init() {
            config.people.forEach(person => {
                data.selections[person] = [];
                data.dates[person] = [];
            });
            renderStep();
            renderRoutes();
            renderDates();
            updateProgress();
        }
 
        // ===== ROUTE SELECTION (NACHEINANDER PRO PERSON) =====
        function renderRoutes() {
            const container = document.getElementById('routeContainer');
            
            if (currentPersonRoute >= config.people.length) {
                container.innerHTML = '<p style="text-align: center; padding: 20px; color: #667eea; font-weight: bold;">✓ Alle Personen haben ihre Top 3 gewählt!</p>';
                return;
            }
 
            const person = config.people[currentPersonRoute];
            const selected = data.selections[person] || [];
 
            let html = `
                <div class="person-section">
                    <h3>👤 ${person}</h3>
                    <div class="route-intro">
                        <h4>Wähle deine Top 3 Ausflüge</h4>
                        <p>Klick auf deine 3 liebsten Ausflüge. Du kannst sie noch ändern!</p>
                        <p style="font-size: 0.85em; margin-top: 10px; font-weight: bold;">
                            (${selected.length} von 3 ausgewählt)
                        </p>
                    </div>
                    <div class="route-list">
                        ${config.routes.map((route, idx) => `
                            <div class="route-item ${selected.includes(idx) ? 'selected' : ''}" 
                                 onclick="toggleRoute(${idx})">
                                <div class="route-checkbox">
                                    ${selected.includes(idx) ? '✓' : ''}
                                </div>
                                <div class="route-info">
                                    <span class="route-name">${route.name}</span>
                                    <span class="route-desc">${route.desc} • ${route.region}</span>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `;
 
            container.innerHTML = html;
        }
 
        function toggleRoute(routeIdx) {
            const person = config.people[currentPersonRoute];
            const selected = data.selections[person];
 
            if (selected.includes(routeIdx)) {
                data.selections[person] = selected.filter(i => i !== routeIdx);
            } else if (selected.length < 3) {
                data.selections[person].push(routeIdx);
            }
            renderRoutes();
        }
 
        // ===== DATE SELECTION (MONAT → TAGE) =====
        function renderDates() {
            const container = document.getElementById('dateContainer');
            
            if (currentPersonDate >= config.people.length) {
                container.innerHTML = '<p style="text-align: center; padding: 20px; color: #667eea; font-weight: bold;">✓ Alle Personen haben ihre Termine gewählt!</p>';
                return;
            }
 
            const person = config.people[currentPersonDate];
 
            // Wenn kein Monat gewählt, zeige Monat-Auswahl
            if (selectedMonth === null) {
                const months = ['Januar', 'Februar', 'März', 'April', 'Mai', 'Juni', 
                               'Juli', 'August', 'September', 'Oktober', 'November', 'Dezember'];
                
                let html = `
                    <div class="calendar-container">
                        <h4>👤 ${person} - Wähle einen Monat</h4>
                        <div class="month-selector">
                            ${months.map((month, idx) => `
                                <button class="month-btn" onclick="selectMonth(${idx})">
                                    ${month}
                                </button>
                            `).join('')}
                        </div>
                    </div>
                `;
                container.innerHTML = html;
            } else {
                // Zeige Tage-Auswahl für gewählten Monat
                const days = getDaysInMonth(selectedMonth);
                const months = ['Januar', 'Februar', 'März', 'April', 'Mai', 'Juni', 
                               'Juli', 'August', 'September', 'Oktober', 'November', 'Dezember'];
                
                let html = `
                    <div class="calendar-container">
                        <h4>👤 ${person} - Wähle Tage im ${months[selectedMonth]}</h4>
                        <div style="margin-bottom: 15px;">
                            <button class="month-btn" onclick="selectedMonth = null; renderDates();" style="width: 100%;">
                                ← Zurück zum Monat
                            </button>
                        </div>
                        <div class="day-grid">
                            ${Array.from({ length: days }, (_, i) => {
                                const day = i + 1;
                                const dateStr = `2024-${String(selectedMonth + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                                const dayName = new Date(2024, selectedMonth, day).toLocaleDateString('de-CH', { weekday: 'short' });
                                const isSelected = data.dates[person] && data.dates[person].includes(dateStr);
                                
                                return `
                                    <button class="day-btn ${isSelected ? 'selected' : ''}" onclick="toggleDate('${dateStr}')">
                                        <span class="day-label">${dayName}</span>
                                        <span class="day-number">${day}</span>
                                    </button>
                                `;
                            }).join('')}
                        </div>
                        <p style="margin-top: 15px; font-size: 0.9em; color: #666; text-align: center; font-weight: bold;">
                            ${data.dates[person] ? data.dates[person].length : 0} Tage ausgewählt
                        </p>
                    </div>
                `;
                container.innerHTML = html;
            }
        }
 
        function getDaysInMonth(month) {
            return new Date(2024, month + 1, 0).getDate();
        }
 
        function selectMonth(monthIdx) {
            selectedMonth = monthIdx;
            renderDates();
        }
 
        function toggleDate(dateStr) {
            const person = config.people[currentPersonDate];
            if (!data.dates[person]) data.dates[person] = [];
 
            if (data.dates[person].includes(dateStr)) {
                data.dates[person] = data.dates[person].filter(d => d !== dateStr);
            } else {
                data.dates[person].push(dateStr);
            }
            renderDates();
        }
 
        // ===== NAVIGATION =====
        function nextStep() {
            // Validierung für Route-Step
            if (currentStep === 1) {
                const person = config.people[currentPersonRoute];
                if (data.selections[person].length === 0) {
                    alert(`Bitte wähle mindestens einen Ausflug für ${person}!`);
                    return;
                }
 
                currentPersonRoute++;
                if (currentPersonRoute < config.people.length) {
                    renderRoutes();
                    return;
                }
            }
 
            // Validierung für Date-Step
            if (currentStep === 2) {
                const person = config.people[currentPersonDate];
                if (!data.dates[person] || data.dates[person].length === 0) {
                    alert(`Bitte wähle mindestens einen Termin für ${person}!`);
                    return;
                }
 
                currentPersonDate++;
                if (currentPersonDate < config.people.length) {
                    selectedMonth = null;
                    renderDates();
                    return;
                }
            }
 
            if (currentStep < 3) {
                currentStep++;
                renderStep();
            }
            if (currentStep === 3) {
                renderResults();
            }
            updateProgress();
        }
 
        function prevStep() {
            if (currentStep > 0) {
                if (currentStep === 1 && currentPersonRoute > 0) {
                    currentPersonRoute--;
                    renderRoutes();
                } else if (currentStep === 2 && currentPersonDate > 0) {
                    currentPersonDate--;
                    selectedMonth = null;
                    renderDates();
                } else if (currentStep > 1) {
                    currentStep--;
                    renderStep();
                }
            }
            updateProgress();
        }
 
        function renderStep() {
            document.querySelectorAll('.step').forEach((el, idx) => {
                el.classList.toggle('active', idx === currentStep);
            });
        }
 
        // ===== RESULTS =====
        function renderResults() {
            // Route Ranking
            const routeVotes = {};
            config.routes.forEach((_, idx) => {
                routeVotes[idx] = 0;
            });
 
            config.people.forEach(person => {
                const selections = data.selections[person];
                selections.forEach((routeIdx, position) => {
                    routeVotes[routeIdx] += (3 - position);
                });
            });
 
            const routeRanking = Object.entries(routeVotes)
                .map(([idx, votes]) => ({
                    name: config.routes[parseInt(idx)].name,
                    votes,
                    idx: parseInt(idx)
                }))
                .sort((a, b) => b.votes - a.votes)
                .filter(item => item.votes > 0);
 
            // Date Ranking
            const dateVotes = {};
            config.people.forEach(person => {
                if (data.dates[person]) {
                    data.dates[person].forEach(date => {
                        dateVotes[date] = (dateVotes[date] || 0) + 1;
                    });
                }
            });
 
            const dateRanking = Object.entries(dateVotes)
                .map(([date, votes]) => ({ date, votes }))
                .sort((a, b) => b.votes - a.votes);
 
            // Route HTML
            const maxVotes = routeRanking[0]?.votes || 1;
            const routeHTML = routeRanking.map((item, idx) => {
                const percentage = (item.votes / maxVotes) * 100;
                return `
                    <div class="ranking-item">
                        <div class="ranking-position">${idx + 1}</div>
                        <div class="ranking-info">
                            <div class="ranking-title">${item.name}</div>
                            <div class="ranking-votes">${item.votes} Punkte</div>
                            <div class="vote-bar">
                                <div class="vote-bar-fill" style="width: ${percentage}%"></div>
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
 
            document.getElementById('resultsRanking').innerHTML = routeHTML || '<p>Keine Votes</p>';
 
            // Date HTML
            const dateHTML = dateRanking.slice(0, 5).map(item => {
                const date = new Date(item.date + 'T12:00:00');
                const formatted = date.toLocaleDateString('de-CH', { weekday: 'short', year: 'numeric', month: '2-digit', day: '2-digit' });
                return `
                    <div class="ranking-item">
                        <div class="ranking-position">${item.votes}</div>
                        <div class="ranking-info" style="text-align: left;">
                            <div class="ranking-title">${formatted}</div>
                            <div class="ranking-votes">${item.votes} ${item.votes === 1 ? 'Person' : 'Personen'}</div>
                        </div>
                    </div>
                `;
            }).join('');
 
            document.getElementById('dateResults').innerHTML = dateHTML || '<p>Keine Termine</p>';
        }
 
        function updateProgress() {
            const progress = ((currentStep) / 3) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
 
            document.querySelectorAll('.step-dot').forEach((el, idx) => {
                el.classList.toggle('active', idx === currentStep);
                el.classList.toggle('completed', idx < currentStep);
            });
        }
 
        function resetAll() {
            currentStep = 0;
            currentPersonRoute = 0;
            currentPersonDate = 0;
            selectedMonth = null;
            config.people.forEach(person => {
                data.selections[person] = [];
                data.dates[person] = [];
            });
            renderStep();
            renderRoutes();
            renderDates();
            updateProgress();
        }
 
        function shareResults() {
            const topRoute = Object.entries(data.selections)
                .flatMap(([_, routes]) => routes)
                .reduce((acc, idx) => {
                    acc[idx] = (acc[idx] || 0) + 1;
                    return acc;
                }, {});
            
            const bestRoute = Object.entries(topRoute).sort((a, b) => b[1] - a[1])[0];
            const text = `Unser Familienausflug: ${config.routes[bestRoute[0]].name}! 🏔️ ✈️ 🗺️`;
            
            if (navigator.share) {
                navigator.share({ title: 'Familienausflug', text });
            } else {
                alert(text);
            }
        }
 
        // Initialize
        window.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
 
