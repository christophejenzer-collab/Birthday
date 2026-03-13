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
 
        html, body {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
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
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
            padding: 8px;
            position: relative;
            overflow-x: hidden;
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
            position: relative;
            z-index: 1;
        }
 
        /* Header */
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px 18px;
            text-align: center;
            animation: slideDown 0.6s ease-out;
            position: relative;
            overflow: hidden;
        }
 
        .header h1 {
            font-size: 2em;
            margin-bottom: 5px;
            font-weight: 700;
            position: relative;
            z-index: 2;
        }
 
        .header p {
            font-size: 0.9em;
            opacity: 0.95;
            position: relative;
            z-index: 2;
        }
 
        /* Progress Bar */
        .progress-container {
            background: var(--light-bg);
            padding: 12px;
        }
 
        .progress-steps {
            display: flex;
            gap: 6px;
            justify-content: space-between;
            margin-bottom: 10px;
        }
 
        .step-dot {
            width: 34px;
            height: 34px;
            border-radius: 50%;
            background: white;
            border: 2px solid #ddd;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: #999;
            transition: var(--transition);
            font-size: 0.75em;
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
            padding: 20px 15px;
            animation: fadeIn 0.5s ease-out;
            overflow-y: auto;
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
            font-size: 3em;
            margin: 10px 0;
            animation: bounce 2s infinite;
        }
 
        .welcome-content h2 {
            font-size: 1.4em;
            color: var(--accent);
            margin: 12px 0;
            font-weight: 600;
        }
 
        .welcome-content p {
            font-size: 0.95em;
            color: #666;
            line-height: 1.4;
            margin: 10px 0;
        }
 
        .link-box {
            background: rgba(102, 126, 234, 0.08);
            border: 2px solid #667eea;
            border-radius: 12px;
            padding: 12px;
            margin: 15px 0;
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
            font-size: 0.9em;
        }
 
        /* Person Highlight */
        .person-highlight {
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.2), rgba(102, 126, 234, 0.1));
            border: 2px solid #667eea;
            border-radius: 12px;
            padding: 12px;
            margin-bottom: 15px;
            text-align: center;
            animation: slideDown 0.5s ease-out;
        }
 
        .person-highlight h3 {
            color: #667eea;
            font-size: 1.2em;
            margin: 0;
        }
 
        .person-highlight p {
            color: #666;
            font-size: 0.85em;
            margin: 6px 0 0 0;
        }
 
        /* Route Selection */
        .person-section {
            background: var(--light-bg);
            border-radius: 12px;
            padding: 12px;
            margin-bottom: 12px;
            border-left: 5px solid #667eea;
        }
 
        .route-intro {
            background: white;
            border: 2px solid #667eea;
            border-radius: 10px;
            padding: 12px;
            margin-bottom: 12px;
            text-align: center;
        }
 
        .route-intro h4 {
            color: #667eea;
            font-size: 0.95em;
            margin-bottom: 6px;
        }
 
        .route-intro p {
            color: #666;
            font-size: 0.85em;
            line-height: 1.3;
        }
 
        .route-list {
            display: flex;
            flex-direction: column;
            gap: 8px;
            max-height: 300px;
            overflow-y: auto;
        }
 
        .route-item {
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            padding: 10px;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 8px;
        }
 
        .route-item:hover {
            border-color: #667eea;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.1);
            transform: translateX(3px);
        }
 
        .route-item.selected {
            background: rgba(102, 126, 234, 0.08);
            border-color: #667eea;
            font-weight: 600;
        }
 
        .route-checkbox {
            width: 22px;
            height: 22px;
            border: 2px solid #ddd;
            border-radius: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: var(--transition);
            flex-shrink: 0;
            font-size: 0.8em;
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
            margin-bottom: 2px;
            font-size: 0.95em;
        }
 
        .route-desc {
            font-size: 0.8em;
            color: #999;
        }
 
        /* Results */
        .results-container {
            text-align: center;
        }
 
        .results-container h2 {
            color: var(--accent);
            margin-bottom: 15px;
            font-size: 1.3em;
        }
 
        .results-section {
            margin-bottom: 20px;
        }
 
        .results-section h3 {
            color: #667eea;
            margin-bottom: 10px;
            font-size: 0.95em;
            text-align: left;
        }
 
        .ranking-item {
            background: white;
            border-radius: 10px;
            padding: 10px;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
            animation: slideUp 0.5s ease-out;
        }
 
        .ranking-position {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: #667eea;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 0.95em;
            flex-shrink: 0;
        }
 
        .ranking-info {
            flex: 1;
            text-align: left;
        }
 
        .ranking-title {
            font-weight: bold;
            color: var(--accent);
            margin-bottom: 2px;
            font-size: 0.85em;
        }
 
        .ranking-votes {
            font-size: 0.75em;
            color: #666;
        }
 
        .vote-bar {
            width: 100%;
            height: 4px;
            background: #e0e0e0;
            border-radius: 2px;
            margin-top: 5px;
            overflow: hidden;
        }
 
        .vote-bar-fill {
            height: 100%;
            background: #667eea;
            transition: width 0.5s ease-out;
            border-radius: 2px;
        }
 
        /* Final Message */
        .final-message {
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.15), rgba(6, 214, 160, 0.15));
            border: 2px solid #667eea;
            border-radius: 12px;
            padding: 15px;
            text-align: center;
            margin: 15px 0;
            animation: slideUp 0.6s ease-out;
        }
 
        .final-message h3 {
            color: #667eea;
            font-size: 1.1em;
            margin-bottom: 8px;
        }
 
        .final-message p {
            color: #333;
            font-size: 0.9em;
            line-height: 1.4;
            margin: 6px 0;
        }
 
        .final-message .names {
            font-weight: bold;
            color: #667eea;
            font-size: 1em;
            margin: 10px 0;
        }
 
        /* Buttons */
        .button-group {
            display: flex;
            gap: 6px;
            margin-top: 15px;
            flex-wrap: wrap;
            justify-content: center;
        }
 
        button {
            padding: 11px 22px;
            border: none;
            border-radius: 10px;
            font-size: 0.9em;
            font-weight: bold;
            cursor: pointer;
            transition: var(--transition);
            text-transform: uppercase;
            letter-spacing: 0.3px;
        }
 
        .btn-primary {
            background: #667eea;
            color: white;
            flex: 1;
            min-width: 130px;
        }
 
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.3);
        }
 
        .btn-secondary {
            background: white;
            color: #667eea;
            border: 2px solid #667eea;
            flex: 1;
            min-width: 130px;
        }
 
        .btn-secondary:hover {
            background: var(--light-bg);
        }
 
        .btn-small {
            padding: 9px 16px;
            font-size: 0.8em;
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
                transform: translateY(15px);
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
            50% { transform: translateY(-8px); }
        }
 
        /* Tablet */
        @media (max-width: 768px) {
            .container {
                max-width: 100%;
            }
 
            .header h1 {
                font-size: 1.8em;
            }
 
            .content {
                padding: 20px 15px;
            }
 
            .button-group {
                gap: 6px;
            }
 
            button {
                padding: 11px 20px;
                font-size: 0.9em;
            }
 
            .route-list {
                max-height: 300px;
            }
        }
 
        /* Mobile */
        @media (max-width: 480px) {
            body {
                padding: 0;
            }
 
            .container {
                border-radius: 0;
                max-width: 100%;
            }
 
            .header {
                padding: 18px 12px;
            }
 
            .header h1 {
                font-size: 1.4em;
                margin-bottom: 4px;
            }
 
            .header p {
                font-size: 0.85em;
            }
 
            .progress-container {
                padding: 12px;
            }
 
            .progress-steps {
                gap: 5px;
                margin-bottom: 10px;
            }
 
            .step-dot {
                width: 32px;
                height: 32px;
                font-size: 0.7em;
            }
 
            .content {
                padding: 18px 12px;
            }
 
            .welcome-content h2 {
                font-size: 1.3em;
                margin: 12px 0;
            }
 
            .welcome-content p {
                font-size: 0.9em;
                margin: 10px 0;
            }
 
            .emoji {
                font-size: 2.8em;
                margin: 10px 0;
            }
 
            .person-highlight {
                padding: 12px;
                margin-bottom: 15px;
            }
 
            .person-highlight h3 {
                font-size: 1.2em;
            }
 
            .person-highlight p {
                font-size: 0.85em;
            }
 
            .link-box {
                padding: 10px;
                margin: 12px 0;
            }
 
            .route-intro {
                padding: 12px;
                margin-bottom: 12px;
            }
 
            .route-intro h4 {
                font-size: 0.95em;
            }
 
            .route-intro p {
                font-size: 0.85em;
            }
 
            .route-list {
                max-height: 250px;
                gap: 8px;
            }
 
            .route-item {
                padding: 10px;
                gap: 8px;
            }
 
            .route-checkbox {
                width: 20px;
                height: 20px;
            }
 
            .route-name {
                font-size: 0.9em;
            }
 
            .route-desc {
                font-size: 0.75em;
            }
 
            .results-container h2 {
                font-size: 1.2em;
                margin-bottom: 15px;
            }
 
            .results-section h3 {
                font-size: 0.95em;
                margin-bottom: 10px;
            }
 
            .ranking-item {
                padding: 10px;
                gap: 10px;
                margin-bottom: 8px;
            }
 
            .ranking-position {
                width: 36px;
                height: 36px;
                font-size: 0.95em;
            }
 
            .ranking-title {
                font-size: 0.85em;
            }
 
            .ranking-votes {
                font-size: 0.75em;
            }
 
            .final-message {
                padding: 15px;
                margin: 15px 0;
            }
 
            .final-message h3 {
                font-size: 1.1em;
            }
 
            .final-message p {
                font-size: 0.9em;
            }
 
            .final-message .names {
                font-size: 1em;
                margin: 12px 0;
            }
 
            .button-group {
                gap: 6px;
                margin-top: 15px;
            }
 
            button {
                padding: 10px 16px;
                font-size: 0.8em;
                min-width: 120px;
            }
 
            .btn-small {
                padding: 9px 14px;
                font-size: 0.8em;
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
                    
                    <p style="margin-top: 20px; color: #666; font-size: 0.9em;">
                        Inspirieren lassen? Schaut auf <strong>Suisse Partout</strong>:
                    </p>
                    <div class="link-box">
                        <a href="https://suissepartout.ch/de/" target="_blank">
                            🌍 Zur Ausflugsdatenbank
                        </a>
                    </div>
 
                    <p style="margin-top: 15px; font-size: 0.85em; color: #999;">
                        Dann wählt jeder seine Top 3 Lieblings-Ausflüge aus!
                    </p>
                </div>
                <div class="button-group">
                    <button class="btn-primary" onclick="nextStep()">Jetzt starten →</button>
                </div>
            </div>
 
            <!-- Step 2: Route Selection -->
            <div class="step" data-step="1">
                <div id="personHighlight" class="person-highlight"></div>
                <div id="routeContainer"></div>
                <div class="button-group">
                    <button class="btn-secondary btn-small" onclick="prevStep()">← Zurück</button>
                    <button class="btn-primary" onclick="nextStep()">Weiter →</button>
                </div>
            </div>
 
            <!-- Step 3: Results -->
            <div class="step" data-step="2">
                <div class="results-container">
                    <h2>🏆 Die Ergebnisse sind da!</h2>
                    
                    <div class="results-section">
                        <h3>Top Ausflüge:</h3>
                        <div id="resultsRanking"></div>
                    </div>
 
                    <div class="final-message">
                        <h3>📅 Jetzt geht's los!</h3>
                        <p>Glückwunsch! Die Abstimmung ist fertig.</p>
                        <p>Der Gewinner ist die Top-Wahl aller!</p>
                        <div class="names">
                            Chayenne • Joel • Mirjam
                        </div>
                        <p style="margin-top: 15px; font-size: 0.95em;">
                            Terminabsprache folgt im persönlichen Gespräch 💬
                        </p>
                    </div>
 
                    <div style="margin-top: 20px; padding: 12px; background: var(--light-bg); border-radius: 10px;">
                        <p style="color: #666; font-size: 0.85em; margin-bottom: 8px;">
                            💡 <strong>Nächste Schritte:</strong>
                        </p>
                        <p style="color: #666; font-size: 0.85em; line-height: 1.5;">
                            1. Den #1 Ausflug absprechen<br>
                            2. Den Termin gemeinsam festlegen<br>
                            3. Das Abenteuer wird Realität! 🚀
                        </p>
                    </div>
                </div>
                <div class="button-group">
                    <button class="btn-secondary btn-small" onclick="resetAll()">Nochmal</button>
                    <button class="btn-primary" onclick="shareResults()">Teilen</button>
                </div>
            </div>
        </div>
    </div>
 
    <script>
        // Alle verfügbaren Ausflüge
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
            people: ['👧 Chayenne', '👦 Joel', '👩 Mirjam'],
            routes: allRoutes,
        };
 
        let currentStep = 0;
        let currentPersonRoute = 0;
 
        let data = {
            selections: {},
        };
 
        // Initialisierung
        function init() {
            config.people.forEach(person => {
                data.selections[person] = [];
            });
            renderStep();
            renderRoutes();
            updateProgress();
        }
 
        // Route Selection
        function renderRoutes() {
            const container = document.getElementById('routeContainer');
            const highlight = document.getElementById('personHighlight');
            
            if (currentPersonRoute >= config.people.length) {
                container.innerHTML = '<p style="text-align: center; padding: 15px; color: #667eea; font-weight: bold;">✓ Alle Personen fertig!</p>';
                highlight.innerHTML = '';
                return;
            }
 
            const person = config.people[currentPersonRoute];
            const selected = data.selections[person] || [];
 
            // Highlight
            highlight.innerHTML = `
                <h3>${person}</h3>
                <p>Dein Turn! 📱 Gib das Handy weiter, wenn du fertig bist</p>
            `;
 
            let html = `
                <div class="person-section">
                    <div class="route-intro">
                        <h4>🎯 Top 3 Ausflüge wählen</h4>
                        <p>Klick auf deine 3 liebsten Ausflüge!</p>
                        <p style="font-size: 0.8em; margin-top: 8px; font-weight: bold; color: #667eea;">
                            ${selected.length} von 3 ausgewählt
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
 
        // Navigation
        function nextStep() {
            if (currentStep === 1) {
                const person = config.people[currentPersonRoute];
                if (data.selections[person].length === 0) {
                    alert(`Bitte wähle mindestens einen Ausflug!`);
                    return;
                }
                currentPersonRoute++;
                if (currentPersonRoute < config.people.length) {
                    renderRoutes();
                    return;
                }
            }
 
            if (currentStep < 2) {
                currentStep++;
                renderStep();
            }
            if (currentStep === 2) {
                renderResults();
            }
            updateProgress();
        }
 
        function prevStep() {
            if (currentStep > 0) {
                if (currentStep === 1 && currentPersonRoute > 0) {
                    currentPersonRoute--;
                    renderRoutes();
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
 
        // Results
        function renderResults() {
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
        }
 
        function updateProgress() {
            const progress = ((currentStep) / 2) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
 
            document.querySelectorAll('.step-dot').forEach((el, idx) => {
                el.classList.toggle('active', idx === currentStep);
                el.classList.toggle('completed', idx < currentStep);
            });
        }
 
        function resetAll() {
            currentStep = 0;
            currentPersonRoute = 0;
            config.people.forEach(person => {
                data.selections[person] = [];
            });
            renderStep();
            renderRoutes();
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
            const text = `Unser Familienausflug: ${config.routes[bestRoute[0]].name}! 🏔️ ✈️`;
            
            if (navigator.share) {
                navigator.share({ title: 'Familienausflug', text });
            } else {
                alert(text);
            }
        }
 
        window.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
 
