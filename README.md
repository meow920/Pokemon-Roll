<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Pokémon Card Roller | Mythical 1 in 18M</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #1a2a3a 0%, #0f1a24 100%);
            font-family: 'Segoe UI', 'Poppins', system-ui, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .app-container {
            max-width: 650px;
            width: 100%;
            background: rgba(30, 40, 55, 0.8);
            backdrop-filter: blur(14px);
            border-radius: 48px;
            box-shadow: 0 25px 45px rgba(0,0,0,0.4), 0 0 0 1px rgba(255,215,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(105deg, #2c3e4e, #1e2f3c);
            padding: 1rem 1.8rem;
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            flex-wrap: wrap;
            gap: 10px;
            border-bottom: 2px solid #f5b642;
        }

        .title h1 {
            font-size: 1.6rem;
            font-weight: 800;
            background: linear-gradient(135deg, #FFD966, #FFB347);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .user-info {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .username-display {
            color: #FFD966;
            font-weight: bold;
        }

        .logout-btn {
            background: none;
            border: 1px solid #ff8888;
            color: #ff8888;
            padding: 5px 12px;
            border-radius: 30px;
            cursor: pointer;
            font-size: 0.8rem;
        }

        .tabs {
            display: flex;
            background: #1e2f3c;
        }

        .tab-btn {
            flex: 1;
            background: none;
            border: none;
            padding: 12px;
            font-weight: bold;
            color: #aaa;
            cursor: pointer;
            transition: 0.2s;
        }

        .tab-btn.active {
            background: #2c3e4e;
            color: #FFD966;
            border-bottom: 2px solid #FFB347;
        }

        .panel {
            padding: 1.8rem;
            display: none;
        }

        .panel.active {
            display: block;
        }

        .odds-bar {
            background: #0f1a24;
            border-radius: 40px;
            padding: 12px 18px;
            margin-bottom: 20px;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            gap: 8px;
            font-size: 0.7rem;
        }

        .odds-item {
            color: #ddd;
        }

        .odds-value {
            color: #FFD966;
            font-weight: bold;
        }

        .card-display {
            background: #1e2f3c;
            border-radius: 32px;
            padding: 20px;
            text-align: center;
            margin-bottom: 20px;
            transition: 0.2s;
            box-shadow: inset 0 0 15px rgba(0,0,0,0.3), 0 5px 15px rgba(0,0,0,0.2);
            position: relative;
            overflow: hidden;
        }

        .card-image {
            width: 180px;
            height: 250px;
            object-fit: contain;
            margin: 0 auto;
            background: #2c3e4e;
            border-radius: 20px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
            transition: 0.2s;
        }

        .card-name {
            margin-top: 15px;
            font-size: 1.3rem;
            font-weight: bold;
            color: white;
        }

        .card-rarity {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 40px;
            font-size: 0.7rem;
            font-weight: bold;
            margin-top: 8px;
        }

        .roll-btn {
            background: linear-gradient(105deg, #FFB347, #FF8C00);
            border: none;
            width: 100%;
            padding: 14px;
            border-radius: 60px;
            font-weight: bold;
            font-size: 1.1rem;
            color: #1a2a3a;
            cursor: pointer;
            transition: 0.2s;
        }

        .roll-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .admin-section {
            margin-bottom: 25px;
            background: #1e2f3c;
            border-radius: 24px;
            padding: 18px;
        }

        .admin-title {
            color: #FFB347;
            margin-bottom: 12px;
        }

        .slider-group {
            margin-bottom: 15px;
        }

        .slider-group label {
            display: block;
            color: #ddd;
            font-size: 0.8rem;
            margin-bottom: 5px;
        }

        input[type="range"] {
            width: 100%;
        }

        .force-select {
            margin-top: 15px;
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }

        .force-btn {
            background: #2c3e4e;
            border: none;
            padding: 6px 12px;
            border-radius: 40px;
            color: white;
            cursor: pointer;
        }

        .force-btn.active {
            background: #FFB347;
            color: #1a2a3a;
        }

        .save-rates {
            background: #FF8C00;
            border: none;
            padding: 8px 15px;
            border-radius: 40px;
            font-weight: bold;
            margin-top: 12px;
            cursor: pointer;
        }

        .login-form, .register-form {
            background: #1e2f3c;
            border-radius: 24px;
            padding: 1.5rem;
            margin-bottom: 20px;
        }

        .login-form input, .register-form input {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            background: #0f1a24;
            border: 1px solid #2c3e4e;
            border-radius: 30px;
            color: white;
        }

        .login-btn, .register-btn {
            background: #FFB347;
            border: none;
            width: 100%;
            padding: 10px;
            border-radius: 30px;
            font-weight: bold;
            margin-top: 10px;
            cursor: pointer;
        }

        .error-msg {
            color: #ff8888;
            font-size: 0.8rem;
            margin-top: 8px;
        }

        /* Rolling animation */
        @keyframes cardFlip {
            0% { transform: rotateY(0deg); opacity: 0.3; }
            50% { transform: rotateY(180deg); filter: brightness(1.5); }
            100% { transform: rotateY(360deg); opacity: 1; }
        }
        .rolling {
            animation: cardFlip 0.6s ease-in-out;
        }

        @keyframes sparkle {
            0% { opacity: 0; transform: scale(0.5); }
            50% { opacity: 1; transform: scale(1.2); background: radial-gradient(circle, #FFD966, #FF8C00); }
            100% { opacity: 0; transform: scale(1.5); }
        }
        .sparkle {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 100px;
            height: 100px;
            background: radial-gradient(circle, #FFD966, #FF8C00);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            animation: sparkle 0.5s ease-out forwards;
            pointer-events: none;
        }

        .inventory-grid {
            max-height: 400px;
            overflow-y: auto;
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .inventory-card {
            background: #1e2f3c;
            border-radius: 16px;
            padding: 8px;
            text-align: center;
            width: 100px;
        }

        .inventory-card img {
            width: 80px;
            height: 110px;
            object-fit: contain;
        }
    </style>
</head>
<body>

<div class="app-container" id="app">
    <div class="header">
        <div class="title">
            <h1>⚡ Pokémon Card Roller</h1>
        </div>
        <div class="user-info" id="userInfo">
            <span class="username-display" id="usernameSpan">Guest</span>
            <button class="logout-btn" id="logoutBtn" style="display: none;">Logout</button>
        </div>
    </div>

    <!-- Unauthenticated panel -->
    <div id="authPanel" class="panel active">
        <div class="login-form">
            <h3 style="color:white;">Login</h3>
            <input type="text" id="loginUsername" placeholder="Username">
            <input type="password" id="loginPassword" placeholder="Password">
            <button class="login-btn" id="doLogin">Login</button>
            <div id="loginError" class="error-msg"></div>
        </div>
        <div class="register-form">
            <h3 style="color:white;">Register</h3>
            <input type="text" id="regUsername" placeholder="Username">
            <input type="password" id="regPassword" placeholder="Password">
            <button class="register-btn" id="doRegister">Create Account</button>
            <div id="regError" class="error-msg"></div>
        </div>
    </div>

    <!-- Main app panel -->
    <div id="mainPanel" class="panel" style="display: none;">
        <div class="tabs">
            <button class="tab-btn active" data-tab="roller">🎲 ROLLER</button>
            <button class="tab-btn" data-tab="inventory">📦 INVENTORY</button>
            <button class="tab-btn" data-tab="admin" id="adminTabBtn" style="display: none;">⚙️ ADMIN</button>
        </div>

        <!-- Roller tab -->
        <div id="rollerTab" class="panel active">
            <div class="odds-bar" id="oddsDisplay"></div>
            <div class="card-display" id="cardDisplay">
                <img id="cardImage" class="card-image" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png" alt="Card">
                <div class="card-name" id="cardName">Pikachu</div>
                <div class="card-rarity" id="cardRarity" style="background: #aaa;">Common</div>
            </div>
            <button class="roll-btn" id="rollBtn">🎲 ROLL CARD 🎲</button>
        </div>

        <!-- Inventory tab -->
        <div id="inventoryTab" class="panel" style="display: none;">
            <div id="inventoryList" class="inventory-grid"></div>
        </div>

        <!-- Admin tab (only for Owner-999) -->
        <div id="adminTab" class="panel" style="display: none;">
            <div class="admin-section">
                <h3 class="admin-title">⚖️ Rarity Weights (Higher = More Common)</h3>
                <div class="slider-group">
                    <label>Common Weight: <span id="commonWeightVal">10000000</span></label>
                    <input type="range" id="commonWeight" min="1" max="50000000" step="1000">
                </div>
                <div class="slider-group">
                    <label>Rare Weight: <span id="rareWeightVal">1000000</span></label>
                    <input type="range" id="rareWeight" min="1" max="10000000" step="1000">
                </div>
                <div class="slider-group">
                    <label>Epic Weight: <span id="epicWeightVal">100000</span></label>
                    <input type="range" id="epicWeight" min="1" max="5000000" step="1000">
                </div>
                <div class="slider-group">
                    <label>Legendary Weight: <span id="legendaryWeightVal">10000</span></label>
                    <input type="range" id="legendaryWeight" min="1" max="1000000" step="100">
                </div>
                <div class="slider-group">
                    <label>Mythical Weight: <span id="mythicalWeightVal">1</span></label>
                    <input type="range" id="mythicalWeight" min="1" max="10000" step="1">
                </div>
                <button class="save-rates" id="saveRatesBtn">💾 Save Weights</button>
            </div>
            <div class="admin-section">
                <h3 class="admin-title">🔮 Force Next Card (Override Rarity)</h3>
                <div class="force-select" id="forceButtons">
                    <button class="force-btn" data-rarity="Common">Common</button>
                    <button class="force-btn" data-rarity="Rare">Rare</button>
                    <button class="force-btn" data-rarity="Epic">Epic</button>
                    <button class="force-btn" data-rarity="Legendary">Legendary</button>
                    <button class="force-btn" data-rarity="Mythical">Mythical</button>
                    <button class="force-btn" data-rarity="None">Clear force</button>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
    // ---------- Pokémon card database ----------
    const cardsDB = {
        Common: [
            { name: "Bulbasaur", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png" },
            { name: "Charmander", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/4.png" },
            { name: "Squirtle", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png" },
            { name: "Pikachu", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png" },
            { name: "Jigglypuff", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/39.png" },
            { name: "Psyduck", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/54.png" },
            { name: "Growlithe", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/58.png" },
            { name: "Machop", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/66.png" }
        ],
        Rare: [
            { name: "Haunter", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/93.png" },
            { name: "Eevee", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/133.png" },
            { name: "Snorlax", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/143.png" },
            { name: "Dragonair", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/148.png" },
            { name: "Marill", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/183.png" },
            { name: "Lapras", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/131.png" }
        ],
        Epic: [
            { name: "Gengar", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/94.png" },
            { name: "Arcanine", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/59.png" },
            { name: "Vaporeon", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/134.png" },
            { name: "Jolteon", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/135.png" },
            { name: "Flareon", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/136.png" },
            { name: "Tyranitar", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/248.png" }
        ],
        Legendary: [
            { name: "Mewtwo", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/150.png" },
            { name: "Lugia", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/249.png" },
            { name: "Ho-Oh", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/250.png" },
            { name: "Rayquaza", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/384.png" },
            { name: "Dialga", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/483.png" },
            { name: "Palkia", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/484.png" }
        ],
        Mythical: [
            { name: "Mew", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/151.png" },
            { name: "Celebi", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/251.png" },
            { name: "Jirachi", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/385.png" },
            { name: "Darkrai", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/491.png" },
            { name: "Shaymin", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/492.png" },
            { name: "Arceus", img: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/493.png" }
        ]
    };

    const rarityColors = {
        Common: "#6c757d",
        Rare: "#007bff",
        Epic: "#9b59b6",
        Legendary: "#f39c12",
        Mythical: "#e84393"
    };

    const rarityList = ["Common", "Rare", "Epic", "Legendary", "Mythical"];

    // ---------- Weight-based system ----------
    let weights = {
        Common: 10000000,   // 10 million
        Rare: 1000000,      // 1 million
        Epic: 100000,       // 100k
        Legendary: 10000,   // 10k
        Mythical: 1         // 1 in ~ 11,110,001 total
    };

    function getTotalWeight() {
        return weights.Common + weights.Rare + weights.Epic + weights.Legendary + weights.Mythical;
    }

    function getOddsText(rarity) {
        const total = getTotalWeight();
        const w = weights[rarity];
        if (w === 0) return "0%";
        const chance = total / w;
        if (chance < 100) return `${(100 / chance).toFixed(2)}%`;
        else return `1 in ${Math.round(chance).toLocaleString()}`;
    }

    function updateOddsDisplay() {
        const oddsDiv = document.getElementById("oddsDisplay");
        if (!oddsDiv) return;
        oddsDiv.innerHTML = `
            <span class="odds-item">⚪ Common: <span class="odds-value">${getOddsText("Common")}</span></span>
            <span class="odds-item">🔵 Rare: <span class="odds-value">${getOddsText("Rare")}</span></span>
            <span class="odds-item">🟣 Epic: <span class="odds-value">${getOddsText("Epic")}</span></span>
            <span class="odds-item">🟠 Legendary: <span class="odds-value">${getOddsText("Legendary")}</span></span>
            <span class="odds-item">💖 Mythical: <span class="odds-value">${getOddsText("Mythical")}</span></span>
        `;
        // Update admin sliders if visible
        document.getElementById("commonWeightVal").innerText = weights.Common;
        document.getElementById("commonWeight").value = weights.Common;
        document.getElementById("rareWeightVal").innerText = weights.Rare;
        document.getElementById("rareWeight").value = weights.Rare;
        document.getElementById("epicWeightVal").innerText = weights.Epic;
        document.getElementById("epicWeight").value = weights.Epic;
        document.getElementById("legendaryWeightVal").innerText = weights.Legendary;
        document.getElementById("legendaryWeight").value = weights.Legendary;
        document.getElementById("mythicalWeightVal").innerText = weights.Mythical;
        document.getElementById("mythicalWeight").value = weights.Mythical;
    }

    function getRandomCard() {
        if (forcedNextRarity && forcedNextRarity !== "None") {
            const rarity = forcedNextRarity;
            forcedNextRarity = null;
            const pool = cardsDB[rarity];
            if (pool && pool.length) {
                const card = pool[Math.floor(Math.random() * pool.length)];
                return { rarity, card };
            }
        }
        const total = getTotalWeight();
        let rand = Math.random() * total;
        if (rand < weights.Common) return { rarity: "Common", card: cardsDB.Common[Math.floor(Math.random() * cardsDB.Common.length)] };
        rand -= weights.Common;
        if (rand < weights.Rare) return { rarity: "Rare", card: cardsDB.Rare[Math.floor(Math.random() * cardsDB.Rare.length)] };
        rand -= weights.Rare;
        if (rand < weights.Epic) return { rarity: "Epic", card: cardsDB.Epic[Math.floor(Math.random() * cardsDB.Epic.length)] };
        rand -= weights.Epic;
        if (rand < weights.Legendary) return { rarity: "Legendary", card: cardsDB.Legendary[Math.floor(Math.random() * cardsDB.Legendary.length)] };
        return { rarity: "Mythical", card: cardsDB.Mythical[Math.floor(Math.random() * cardsDB.Mythical.length)] };
    }

    // ---------- User management ----------
    let currentUser = null;
    let users = JSON.parse(localStorage.getItem("pokemon_users")) || {};
    let forcedNextRarity = null;
    const OWNER_USERNAME = "Owner-999";

    function saveUserData() {
        if (currentUser) {
            users[currentUser.username].inventory = currentUser.inventory;
            users[currentUser.username].weights = weights;
            localStorage.setItem("pokemon_users", JSON.stringify(users));
        }
    }

    function loadUserData() {
        if (!currentUser) return;
        const stored = users[currentUser.username];
        if (stored) {
            currentUser.inventory = stored.inventory || [];
            if (stored.weights) weights = stored.weights;
        } else {
            currentUser.inventory = [];
        }
        updateOddsDisplay();
        updateInventoryUI();
        const isOwner = (currentUser.username === OWNER_USERNAME);
        document.getElementById("adminTabBtn").style.display = isOwner ? "block" : "none";
    }

    async function rollCard() {
        const btn = document.getElementById("rollBtn");
        const img = document.getElementById("cardImage");
        const nameSpan = document.getElementById("cardName");
        const raritySpan = document.getElementById("cardRarity");
        const displayDiv = document.getElementById("cardDisplay");

        btn.disabled = true;
        btn.innerText = "🌀 ROLLING...";

        img.classList.add("rolling");
        const sparkle = document.createElement("div");
        sparkle.className = "sparkle";
        displayDiv.appendChild(sparkle);

        await new Promise(r => setTimeout(r, 600));

        const { rarity, card } = getRandomCard();
        img.src = card.img;
        nameSpan.innerText = card.name;
        raritySpan.innerText = rarity;
        raritySpan.style.background = rarityColors[rarity];

        img.classList.remove("rolling");
        sparkle.remove();

        currentUser.inventory.push({ name: card.name, img: card.img, rarity, timestamp: Date.now() });
        saveUserData();
        updateInventoryUI();

        btn.disabled = false;
        btn.innerText = "🎲 ROLL CARD 🎲";
    }

    function updateInventoryUI() {
        const container = document.getElementById("inventoryList");
        if (!container) return;
        container.innerHTML = "";
        const inv = [...currentUser.inventory].reverse();
        inv.forEach(item => {
            const cardDiv = document.createElement("div");
            cardDiv.className = "inventory-card";
            const img = document.createElement("img");
            img.src = item.img;
            const nameSpan = document.createElement("div");
            nameSpan.innerText = item.name;
            nameSpan.style.color = "white";
            nameSpan.style.fontSize = "0.7rem";
            const raritySpan = document.createElement("div");
            raritySpan.innerText = item.rarity;
            raritySpan.style.fontSize = "0.6rem";
            raritySpan.style.color = "#FFD966";
            cardDiv.appendChild(img);
            cardDiv.appendChild(nameSpan);
            cardDiv.appendChild(raritySpan);
            container.appendChild(cardDiv);
        });
    }

    // Admin functions
    function saveWeights() {
        weights.Common = parseInt(document.getElementById("commonWeight").value);
        weights.Rare = parseInt(document.getElementById("rareWeight").value);
        weights.Epic = parseInt(document.getElementById("epicWeight").value);
        weights.Legendary = parseInt(document.getElementById("legendaryWeight").value);
        weights.Mythical = parseInt(document.getElementById("mythicalWeight").value);
        // Ensure no zero weights (minimum 1)
        for (let r of rarityList) if (weights[r] < 1) weights[r] = 1;
        updateOddsDisplay();
        saveUserData();
        alert("Weights saved! New odds applied.");
    }

    function setupForceButtons() {
        const btns = document.querySelectorAll(".force-btn");
        btns.forEach(btn => {
            btn.addEventListener("click", () => {
                const rarity = btn.getAttribute("data-rarity");
                if (rarity === "None") forcedNextRarity = null;
                else forcedNextRarity = rarity;
                btns.forEach(b => b.classList.remove("active"));
                if (rarity !== "None") btn.classList.add("active");
                alert(`Next card forced to ${rarity || "random"}`);
            });
        });
    }

    // Auth functions
    function login() {
        const username = document.getElementById("loginUsername").value.trim();
        const password = document.getElementById("loginPassword").value;
        if (!username || !password) {
            document.getElementById("loginError").innerText = "Fill all fields";
            return;
        }
        const userData = users[username];
        if (!userData || userData.password !== password) {
            document.getElementById("loginError").innerText = "Invalid credentials";
            return;
        }
        currentUser = {
            username: username,
            password: userData.password,
            inventory: userData.inventory || [],
            isOwner: username === OWNER_USERNAME
        };
        if (userData.weights) weights = userData.weights;
        loadUserData();
        showMainApp();
    }

    function register() {
        const username = document.getElementById("regUsername").value.trim();
        const password = document.getElementById("regPassword").value;
        if (!username || !password) {
            document.getElementById("regError").innerText = "Fill all fields";
            return;
        }
        if (users[username]) {
            document.getElementById("regError").innerText = "Username already taken";
            return;
        }
        users[username] = { password: password, inventory: [], weights: { Common:10000000, Rare:1000000, Epic:100000, Legendary:10000, Mythical:1 } };
        localStorage.setItem("pokemon_users", JSON.stringify(users));
        document.getElementById("regError").innerText = "Account created! Please login.";
        document.getElementById("regUsername").value = "";
        document.getElementById("regPassword").value = "";
    }

    function logout() {
        currentUser = null;
        forcedNextRarity = null;
        document.getElementById("authPanel").style.display = "block";
        document.getElementById("mainPanel").style.display = "none";
        document.getElementById("usernameSpan").innerText = "Guest";
        document.getElementById("logoutBtn").style.display = "none";
        document.getElementById("loginUsername").value = "";
        document.getElementById("loginPassword").value = "";
        document.getElementById("regUsername").value = "";
        document.getElementById("regPassword").value = "";
    }

    function showMainApp() {
        document.getElementById("authPanel").style.display = "none";
        document.getElementById("mainPanel").style.display = "block";
        document.getElementById("usernameSpan").innerText = currentUser.username;
        document.getElementById("logoutBtn").style.display = "block";
        updateInventoryUI();
        updateOddsDisplay();
        // set a default card
        const defaultCard = cardsDB.Common[0];
        document.getElementById("cardName").innerText = defaultCard.name;
        document.getElementById("cardImage").src = defaultCard.img;
        document.getElementById("cardRarity").innerText = "Common";
        document.getElementById("cardRarity").style.background = rarityColors.Common;
    }

    function initTabs() {
        const tabs = document.querySelectorAll(".tab-btn");
        tabs.forEach(btn => {
            btn.addEventListener("click", () => {
                const tabName = btn.getAttribute("data-tab");
                document.querySelectorAll(".panel").forEach(panel => panel.classList.remove("active"));
                if (tabName === "roller") document.getElementById("rollerTab").classList.add("active");
                else if (tabName === "inventory") document.getElementById("inventoryTab").classList.add("active");
                else if (tabName === "admin") document.getElementById("adminTab").classList.add("active");
                tabs.forEach(b => b.classList.remove("active"));
                btn.classList.add("active");
            });
        });
    }

    // Event binding
    document.getElementById("doLogin").addEventListener("click", login);
    document.getElementById("doRegister").addEventListener("click", register);
    document.getElementById("logoutBtn").addEventListener("click", logout);
    document.getElementById("rollBtn").addEventListener("click", rollCard);
    if (document.getElementById("saveRatesBtn")) {
        document.getElementById("saveRatesBtn").addEventListener("click", saveWeights);
        setupForceButtons();
        // Slider live preview
        const sliders = ["commonWeight", "rareWeight", "epicWeight", "legendaryWeight", "mythicalWeight"];
        sliders.forEach(id => {
            const slider = document.getElementById(id);
            const span = document.getElementById(id + "Val");
            if (slider) {
                slider.addEventListener("input", () => {
                    span.innerText = slider.value;
                });
            }
        });
    }
    initTabs();
</script>
</body>
</html>
