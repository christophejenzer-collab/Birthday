<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ausflug-Abstimmung</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
 
        :root {
            --primary: #667eea;
            --secondary: #667eea;
            --accent: #1A1A2E;
            --success: #06D6A0;
            --light-bg: #F3F4F9;
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
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }
 
        .header p {
            font-size: 1.1em;
            opacity: 0.95;
        }
 
        /* Steps Navigation */
        .steps-nav {
            display: flex;
            gap: 8px;
            padding: 15px 20px;
            background: var(--light-bg);
            overflow-x: auto;
            justify-content: center;
        }
 
        .step-indicator {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            cursor: pointer;
            transition: var(--transition);
            background: white;
            color: #999;
            border: 2px solid #ddd;
            font-size: 0.9em;
        }
 
        .step-indicator.active {
            background: #667eea;
            color: white;
            border-color: #667eea;
            transform: scale(1.1);
        }
 
        .step-indicator.completed {
            background: var(--success);
            color: white;
            border-color: var(--success);
        }
 
        /* Content Area */
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
 
        /* Selection Step */
        .selection-container {
            margin-bottom: 20px;
        }
 
        .selection-container h3 {
            color: var(--accent);
            margin-bottom: 20px;
            font-size: 1.3em;
        }
 
        .person-section {
            background: var(--light-bg);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 25px;
            border-left: 5px solid #667eea;
        }
 
        .person-section h4 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.15em;
        }
 
        .trip-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
 
        .trip-option {
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
 
        .trip-option:hover {
            border-color: #667eea;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.1);
            transform: translateX(5px);
        }
 
        .trip-option.selected {
            background: rgba(102, 126, 234, 0.08);
            border-color: #667eea;
            font-weight: 600;
        }
 
        .trip-checkbox {
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
 
        .trip-option.selected .trip-checkbox {
            background: #667eea;
            border-color: #667eea;
            color: white;
        }
 
        .trip-text {
            flex: 1;
        }
 
        .trip-text strong {
            display: block;
            color: var(--accent);
            margin-bottom: 3px;
        }
 
        .trip-text small {
            color: #999;
        }
 
        /* Date Selection Step */
        .calendar-section {
            margin-bottom: 25px;
        }
 
        .calendar-section h4 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.1em;
        }
 
        .date-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(70px, 1fr));
            gap: 10px;
            margin-bottom: 20px;
        }
 
        .date-option {
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            padding: 12px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.9em;
        }
 
        .date-option:hover {
            border-color: #667eea;
            transform: scale(1.05);
        }
 
        .date-option.selected {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }
 
        .date-option .day {
            font-weight: bold;
            display: block;
        }
 
        .date-option .date {
            font-size: 0.85em;
            opacity: 0.8;
            display: block;
        }
 
        /* Results Step */
        .results-container {
            text-align: center;
        }
 
        .results-container h2 {
            color: var(--accent);
            margin-bottom: 25px;
            font-size: 1.6em;
        }
 
        .results-ranking {
            margin-bottom: 30px;
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
 
        .ranking-position.first {
            background: #667eea;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.3);
        }
 
        .ranking-position.second {
            background: #667eea;
        }
 
        .ranking-position.third {
            background: #667eea;
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
 
        .date-ranking {
            background: var(--light-bg);
            border-radius: 15px;
            padding: 20px;
            margin-top: 25px;
        }
 
        .date-ranking h3 {
            color: #667eea;
            margin-bottom: 15px;
        }
 
        .date-item {
            background: white;
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
 
        .date-item-date {
            font-weight: bold;
            color: var(--accent);
        }
 
        .date-item-votes {
            background: #667eea;
            color: white;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 0.85em;
            font-weight: bold;
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
 
        /* Input Fields */
        input[type="text"],
        textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 1em;
            font-family: inherit;
            transition: var(--transition);
            margin-bottom: 15px;
        }
 
        input[type="text"]:focus,
        textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 4px rgba(102, 126, 234, 0.1);
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
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
 
        @keyframes bounce {
            0%, 100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-10px);
            }
        }
 
        /* Mobile Optimization */
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
 
            .date-grid {
                grid-template-columns: repeat(3, 1fr);
            }
 
            .steps-nav {
                padding: 12px 10px;
            }
 
            .step-indicator {
                width: 40px;
                height: 40px;
                font-size: 0.8em;
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
 
            .person-section {
                padding: 15px;
            }
 
            .ranking-item {
                flex-direction: column;
                text-align: center;
            }
 
            .ranking-info {
                text-align: center;
            }
        }
 
        /* Success Animation */
        .success-message {
            background: linear-gradient(135deg, var(--success), #00D98E);
            color: white;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            animation: slideDown 0.5s ease-out;
            text-align: center;
            font-weight: bold;
        }
 
        /* Loading */
        .spinner {
            border: 4px solid rgba(102, 126, 234, 0.1);
            border-top: 4px solid #667eea;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
 
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <h1>🎉 Geburtstagsabenteuer</h1>
            <p>Wir suchen gemeinsam den perfekten Ausflug!</p>
        </div>
 
        <!-- Steps Navigation -->
        <div class="steps-nav">
            <div class="step-indicator active" data-step="0">1</div>
            <div class="step-indicator" data-step="1">2</div>
            <div class="step-indicator" data-step="2">3</div>
            <div class="step-indicator" data-step="3">4</div>
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
                        Danach wählt jeder ihre/seine Top 3 Lieblings-Ausflüge aus und wir bestimmen gemeinsam den besten Termin!
                    </p>
                </div>
                <div class="button-group">
                    <button class="btn-primary" onclick="nextStep()">Jetzt starten →</button>
                </div>
            </div>
 
            <!-- Step 2: Selection -->
            <div class="step" data-step="1">
                <div class="selection-container">
                    <h3>📍 Wählt eure Top 3 Ausflüge</h3>
                    <p style="color: #666; margin-bottom: 25px; font-size: 0.95em;">
                        Jede Person wählt ihre 3 Lieblings-Ausflüge aus. Je höher gewählt, desto mehr Punkte gibt es!
                    </p>
 
                    <div id="peopleContainer"></div>
                </div>
                <div class="button-group">
                    <button class="btn-secondary btn-small" onclick="prevStep()">← Zurück</button>
                    <button class="btn-primary" onclick="nextStep()">Weiter →</button>
                </div>
            </div>
 
            <!-- Step 3: Date Selection -->
            <div class="step" data-step="2">
                <div class="calendar-section">
                    <h3>📅 Wählt die besten Termine</h3>
                    <p style="color: #666; margin-bottom: 25px; font-size: 0.95em;">
                        Jede Person markiert die Tage, an denen sie Zeit hat.
                    </p>
 
                    <div id="datesContainer"></div>
                </div>
                <div class="button-group">
                    <button class="btn-secondary btn-small" onclick="prevStep()">← Zurück</button>
                    <button class="btn-primary" onclick="nextStep()">Zu den Ergebnissen →</button>
                </div>
            </div>
 
            <!-- Step 4: Results -->
            <div class="step" data-step="3">
                <div class="results-container">
                    <h2>🏆 Die Ergebnisse sind da!</h2>
                    
                    <div class="results-ranking">
                        <h3 style="color: var(--accent); margin-bottom: 20px;">Top Ausflüge:</h3>
                        <div id="resultsRanking"></div>
                    </div>
 
                    <div class="date-ranking">
                        <h3>📅 Verfügbare Termine:</h3>
                        <div id="dateResults"></div>
                    </div>
 
                    <div style="margin-top: 30px; padding: 15px; background: var(--light-bg); border-radius: 10px;">
                        <p style="color: #666; font-size: 0.9em; margin-bottom: 10px;">
                            💡 <strong>Nächste Schritte:</strong>
                        </p>
                        <p style="color: #666; font-size: 0.9em; line-height: 1.6;">
                            1. Den #1 Ausflug auswählen<br>
                            2. Den besten gemeinsamen Termin festlegen<br>
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
        // Configuration
        const config = {
            people: ['Chayenne', 'Joel', 'Mirjam'],
            sampleTrips: [
                { name: 'Wanderung Appenzell', description: 'Wunderschöne Berglandschaft' },
                { name: 'Rhine Falls', description: 'Europas grösster Wasserfall' },
                { name: 'Jungfraujoch', description: 'Top of Europe' },
                { name: 'Luzerner Seenfahrt', description: 'Entspannungsfahrt' },
                { name: 'Gorges du Trient', description: 'Abenteuer-Klettersteig' },
                { name: 'Axalp-Panorama', description: 'Atemberaubender Aussichtspunkt' },
                { name: 'Rigi Kulm', description: 'Klassische Bergbahn-Wanderung' },
                { name: 'Oeschinen Lake', description: 'Bergkristallklares Wasser' },
                { name: 'Säntis', description: 'Mit Appenzell-Bahn' },
                { name: 'Creux du Van', description: 'Spektakuläre Felswände' }
            ],
            dates: generateDates(14),
        };
 
        let currentStep = 0;
        let data = {
            selections: {},
            dates: {},
        };
 
        // Initialize
        function init() {
            config.people.forEach(person => {
                data.selections[person] = [];
                data.dates[person] = [];
            });
            renderStep();
            renderPeople();
            renderDates();
        }
 
        // Generate next 60 days
        function generateDates(days) {
            const result = [];
            const today = new Date();
            for (let i = 1; i <= days; i++) {
                const date = new Date(today);
                date.setDate(today.getDate() + i);
                result.push(date);
            }
            return result;
        }
 
        // Render People Selection
        function renderPeople() {
            const container = document.getElementById('peopleContainer');
            container.innerHTML = config.people.map(person => `
                <div class="person-section">
                    <h4>👤 ${person}</h4>
                    <div class="trip-list">
                        ${config.sampleTrips.map((trip, idx) => `
                            <div class="trip-option ${data.selections[person]?.includes(idx) ? 'selected' : ''}" 
                                 onclick="selectTrip('${person}', ${idx})">
                                <div class="trip-checkbox">
                                    ${data.selections[person]?.includes(idx) ? '✓' : ''}
                                </div>
                                <div class="trip-text">
                                    <strong>${trip.name}</strong>
                                    <small>${trip.description}</small>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `).join('');
        }
 
        // Select Trip
        function selectTrip(person, tripIndex) {
            if (!data.selections[person].includes(tripIndex)) {
                if (data.selections[person].length < 3) {
                    data.selections[person].push(tripIndex);
                }
            } else {
                data.selections[person] = data.selections[person].filter(i => i !== tripIndex);
            }
            renderPeople();
        }
 
        // Render Dates
        function renderDates() {
            const container = document.getElementById('datesContainer');
            const dateOptions = config.dates.map(date => {
                const dateStr = date.toISOString().split('T')[0];
                const day = ['So', 'Mo', 'Di', 'Mi', 'Do', 'Fr', 'Sa'][date.getDay()];
                const dateNum = date.getDate();
                return { dateStr, day, dateNum, date };
            });
 
            const people = config.people;
            container.innerHTML = people.map(person => `
                <div class="person-section">
                    <h4>👤 ${person}</h4>
                    <div class="date-grid">
                        ${dateOptions.map(({ dateStr, day, dateNum }) => `
                            <div class="date-option ${data.dates[person]?.includes(dateStr) ? 'selected' : ''}"
                                 onclick="toggleDate('${person}', '${dateStr}')">
                                <span class="day">${day}</span>
                                <span class="date">${dateNum}</span>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `).join('');
        }
 
        // Toggle Date
        function toggleDate(person, dateStr) {
            if (data.dates[person].includes(dateStr)) {
                data.dates[person] = data.dates[person].filter(d => d !== dateStr);
            } else {
                data.dates[person].push(dateStr);
            }
            renderDates();
        }
 
        // Calculate Results
        function calculateResults() {
            // Trip ranking
            const tripVotes = {};
            config.sampleTrips.forEach((_, idx) => {
                tripVotes[idx] = 0;
            });
 
            config.people.forEach(person => {
                const selections = data.selections[person];
                selections.forEach((tripIdx, position) => {
                    // 3 Punkte für Platz 1, 2 für Platz 2, 1 für Platz 3
                    tripVotes[tripIdx] += (3 - position);
                });
            });
 
            const tripRanking = Object.entries(tripVotes)
                .map(([idx, votes]) => ({
                    name: config.sampleTrips[parseInt(idx)].name,
                    votes,
                    idx: parseInt(idx)
                }))
                .sort((a, b) => b.votes - a.votes)
                .filter(item => item.votes > 0);
 
            // Date ranking
            const dateVotes = {};
            config.people.forEach(person => {
                data.dates[person].forEach(date => {
                    dateVotes[date] = (dateVotes[date] || 0) + 1;
                });
            });
 
            const dateRanking = Object.entries(dateVotes)
                .map(([date, votes]) => ({ date, votes }))
                .sort((a, b) => b.votes - a.votes);
 
            return { tripRanking, dateRanking };
        }
 
        // Render Results
        function renderResults() {
            const { tripRanking, dateRanking } = calculateResults();
            const maxVotes = tripRanking[0]?.votes || 1;
 
            // Trip Results
            const tripHTML = tripRanking.map((item, idx) => {
                const percentage = (item.votes / maxVotes) * 100;
                const medals = ['🥇', '🥈', '🥉'];
                const medal = medals[idx] || '•';
                const positionClass = idx === 0 ? 'first' : idx === 1 ? 'second' : 'third';
 
                return `
                    <div class="ranking-item">
                        <div class="ranking-position ${positionClass}">
                            ${idx + 1}
                        </div>
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
 
            document.getElementById('resultsRanking').innerHTML = tripHTML || '<p>Keine Votes</p>';
 
            // Date Results
            const dateHTML = dateRanking.slice(0, 5).map(item => {
                const date = new Date(item.date);
                const day = ['So', 'Mo', 'Di', 'Mi', 'Do', 'Fr', 'Sa'][date.getDay()];
                const formatted = `${day}, ${date.getDate()}.${date.getMonth() + 1}.`;
 
                return `
                    <div class="date-item">
                        <span class="date-item-date">${formatted}</span>
                        <span class="date-item-votes">${item.votes} ${item.votes === 1 ? 'Person' : 'Personen'}</span>
                    </div>
                `;
            }).join('');
 
            document.getElementById('dateResults').innerHTML = dateHTML || '<p>Keine Termine verfügbar</p>';
        }
 
        // Navigation
        function nextStep() {
            if (currentStep < 3) {
                currentStep++;
                renderStep();
            }
            if (currentStep === 3) {
                renderResults();
            }
        }
 
        function prevStep() {
            if (currentStep > 0) {
                currentStep--;
                renderStep();
            }
        }
 
        function renderStep() {
            document.querySelectorAll('.step').forEach((el, idx) => {
                el.classList.toggle('active', idx === currentStep);
            });
 
            document.querySelectorAll('.step-indicator').forEach((el, idx) => {
                el.classList.toggle('active', idx === currentStep);
                el.classList.toggle('completed', idx < currentStep);
            });
        }
 
        // Reset
        function resetAll() {
            currentStep = 0;
            config.people.forEach(person => {
                data.selections[person] = [];
                data.dates[person] = [];
            });
            renderStep();
            renderPeople();
            renderDates();
        }
 
        // Share
        function shareResults() {
            const { tripRanking, dateRanking } = calculateResults();
            const topTrip = tripRanking[0]?.name || 'Noch keine Wahl';
            const topDate = dateRanking[0]?.date || 'Noch kein Termin';
            
            const text = `Unser Geburtstagsabenteuer: ${topTrip} am ${topDate}! 🎉`;
            
            if (navigator.share) {
                navigator.share({ title: 'Geburtstagsausflug', text });
            } else {
                alert(text);
            }
        }
 
        // Initialize on load
        window.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
 
