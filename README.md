# find-and-get-web
A premium, interactive landing page for Find &amp; Get—a digital agency utilizing AI scouting mechanics to discover offline local businesses and transition them into high-conversion web ecosystems. Features a custom neon-themed responsive interface and an interactive canvas framework.freelance-portfolio • ai-finder • interactive-design • neon-theme 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Find & Get | AI Business Scouting & Web Design</title>
    <style>
        /* --- Design System Tokens --- */
        :root {
            --bg-color: #090412;
            --bg-card: rgba(25, 12, 43, 0.4);
            --pink-neon: #ff2a85;
            --purple-neon: #bd00ff;
            --text-main: #f3e8ff;
            --text-muted: #a494be;
            --purple-glow: drop-shadow(0 0 15px rgba(189, 0, 255, 0.5));
        }

        /* --- Reset & Base Styles --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background-color: var(--bg-color);
            background-image: radial-gradient(circle at 50% 50%, #1a0933 0%, #090412 100%);
            color: var(--text-main);
            overflow-x: hidden;
            min-height: 100vh;
            position: relative;
        }

        /* --- Ambient Corner Spider Webs --- */
        .corner-web {
            position: fixed;
            width: 300px;
            height: 300px;
            z-index: 1;
            opacity: 0.15;
            pointer-events: none;
            stroke: var(--pink-neon);
            filter: drop-shadow(0 0 3px var(--pink-neon));
        }
        .top-left { top: 0; left: 0; }
        .top-right { top: 0; right: 0; transform: scaleX(-1); }
        .bottom-left { bottom: 0; left: 0; transform: scaleY(-1); }
        .bottom-right { bottom: 0; right: 0; transform: scale(-1); }

        /* --- Navigation Layout --- */
        header {
            position: relative;
            z-index: 10;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 2rem 4rem;
            max-width: 1400px;
            margin: 0 auto;
        }

        .logo {
            font-size: 1.6rem;
            font-weight: 900;
            letter-spacing: 1.5px;
            color: #fff;
            text-shadow: 0 0 10px var(--pink-neon), 0 0 20px var(--purple-neon);
            text-transform: uppercase;
        }

        nav {
            display: flex;
            align-items: center;
        }

        nav a {
            color: var(--text-muted);
            text-decoration: none;
            margin-left: 2.5rem;
            transition: all 0.3s ease;
            font-size: 1rem;
            font-weight: 500;
            letter-spacing: 0.5px;
        }

        nav a:hover {
            color: var(--pink-neon);
            text-shadow: 0 0 8px var(--pink-neon);
        }

        .admin-trigger {
            cursor: pointer;
            border: 1px solid var(--purple-neon);
            padding: 0.6rem 1.2rem;
            border-radius: 4px;
            box-shadow: inset 0 0 8px rgba(189, 0, 255, 0.2), 0 0 8px rgba(189, 0, 255, 0.2);
        }

        .admin-trigger:hover {
            background: var(--purple-neon);
            color: #fff;
            box-shadow: 0 0 15px var(--purple-neon);
        }

        /* --- Layout Grid --- */
        main {
            position: relative;
            z-index: 10;
            max-width: 1300px;
            margin: 0 auto;
            padding: 2rem;
        }

        section {
            padding: 5rem 0;
        }

        .hero-section {
            display: grid;
            grid-template-columns: 1.2fr 1fr;
            align-items: center;
            gap: 4rem;
            min-height: 70vh;
        }

        @media (max-width: 968px) {
            .hero-section {
                grid-template-columns: 1fr;
                text-align: center;
                gap: 2rem;
            }
            .hero-right { order: -1; }
            header { padding: 2rem; flex-direction: column; gap: 1.5rem; }
        }

        /* --- Hero Typography & Buttons --- */
        .hero-left h1 {
            font-size: 4rem;
            font-weight: 800;
            line-height: 1.1;
            margin-bottom: 1.5rem;
            text-transform: uppercase;
            background: linear-gradient(135deg, #ffffff 30%, var(--text-muted) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero-left p {
            font-size: 1.2rem;
            color: var(--text-muted);
            line-height: 1.7;
            margin-bottom: 2.5rem;
            max-width: 540px;
        }

        .cta-btn {
            background: linear-gradient(135deg, var(--pink-neon) 0%, var(--purple-neon) 100%);
            color: #fff;
            padding: 1rem 2.5rem;
            font-weight: 700;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-size: 1.1rem;
            letter-spacing: 1px;
            text-transform: uppercase;
            box-shadow: 0 0 20px rgba(255, 42, 133, 0.4);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .cta-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 0 30px rgba(255, 42, 133, 0.8), 0 0 15px rgba(189, 0, 255, 0.5);
        }

        /* --- Interactive Rotating Spider Net --- */
        .hero-right {
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .web-interactive-wrapper {
            position: relative;
            width: 400px;
            height: 400px;
            cursor: pointer;
            user-select: none;
        }

        .spider-net-svg-container {
            width: 100%;
            height: 100%;
            transition: transform 1.6s cubic-bezier(0.1, 0.8, 0.2, 1);
            filter: var(--purple-glow);
        }

        .spider-net-svg-container svg {
            width: 100%;
            height: 100%;
            animation: webPulse 4s ease-in-out infinite alternate;
        }

        @keyframes webPulse {
            0% { filter: drop-shadow(0 0 8px rgba(189, 0, 255, 0.4)); }
            100% { filter: drop-shadow(0 0 22px rgba(255, 42, 133, 0.6)); }
        }

        .spinning-blur {
            filter: blur(2px) contrast(1.2) var(--purple-glow) !important;
        }

        /* --- About Us Section --- */
        .section-title {
            font-size: 2.5rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            text-align: center;
            margin-bottom: 3rem;
            color: #fff;
            text-shadow: 0 0 10px rgba(189, 0, 255, 0.3);
        }

        .section-title span {
            color: var(--pink-neon);
        }

        .about-container {
            background: var(--bg-card);
            border: 1px solid rgba(189, 0, 255, 0.2);
            border-radius: 16px;
            padding: 3.5rem;
            max-width: 900px;
            margin: 0 auto;
            text-align: center;
            backdrop-filter: blur(10px);
        }

        .about-container p {
            font-size: 1.2rem;
            line-height: 1.8;
            color: var(--text-main);
            margin-bottom: 1.5rem;
        }

        .about-container p:last-child {
            margin-bottom: 0;
            color: var(--text-muted);
        }

        /* --- AI Finder Section --- */
        .finder-container {
            background: rgba(15, 7, 28, 0.7);
            border: 1px solid rgba(255, 42, 133, 0.2);
            border-radius: 16px;
            padding: 3rem;
            max-width: 800px;
            margin: 0 auto;
            box-shadow: 0 15px 35px rgba(0,0,0,0.4);
        }

        .finder-search-bar {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
        }

        @media (max-width: 600px) {
            .finder-search-bar { flex-direction: column; }
        }

        .finder-input {
            flex: 1;
            padding: 1rem 1.5rem;
            background: #090412;
            border: 1px solid rgba(189, 0, 255, 0.4);
            border-radius: 30px;
            color: #fff;
            font-size: 1rem;
            transition: all 0.3s;
        }

        .finder-input:focus {
            outline: none;
            border-color: var(--pink-neon);
            box-shadow: 0 0 15px rgba(255, 42, 133, 0.3);
        }

        .scan-btn {
            background: linear-gradient(135deg, var(--purple-neon), #7b00ff);
            color: white;
            border: none;
            padding: 1rem 2rem;
            border-radius: 30px;
            font-weight: 700;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            transition: all 0.3s;
        }

        .scan-btn:hover {
            box-shadow: 0 0 20px var(--purple-neon);
            transform: scale(1.02);
        }

        .results-box {
            background: #06020a;
            border-radius: 12px;
            padding: 1.5rem;
            border: 1px solid rgba(255, 42, 133, 0.1);
            min-height: 150px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .status-placeholder {
            text-align: center;
            color: var(--text-muted);
            font-style: italic;
        }

        .shop-card {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem;
            border-bottom: 1px solid rgba(164, 148, 190, 0.1);
            animation: fadeIn 0.5s ease forwards;
        }

        .shop-card:last-child { border-bottom: none; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .shop-info h4 { color: #fff; font-size: 1.1rem; margin-bottom: 0.2rem;}
        .shop-info p { color: var(--text-muted); font-size: 0.85rem; }
        
        .status-tag {
            background: rgba(255, 42, 133, 0.15);
            color: var(--pink-neon);
            padding: 0.4rem 0.8rem;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: 700;
            text-transform: uppercase;
            border: 1px solid rgba(255, 42, 133, 0.3);
        }

        /* --- Feature Card Layout --- */
        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        .card {
            background: var(--bg-card);
            border: 1px solid rgba(255, 42, 133, 0.15);
            padding: 2.5rem 2rem;
            border-radius: 12px;
            backdrop-filter: blur(8px);
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
        }

        .card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 3px;
            background: linear-gradient(90deg, var(--pink-neon), var(--purple-neon));
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        .card:hover {
            transform: translateY(-5px);
            border-color: rgba(255, 42, 133, 0.4);
            box-shadow: 0 10px 25px rgba(13, 5, 26, 0.5);
        }

        .card:hover::before { opacity: 1; }
        .card h3 { font-size: 1.5rem; text-transform: uppercase; margin-bottom: 1rem; color: #fff; }
        .card p { color: var(--text-muted); line-height: 1.6; font-size: 0.95rem; }

        /* --- Secure Admin Modal --- */
        .admin-modal {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(6, 3, 13, 0.96);
            z-index: 100;
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s ease;
        }

        .admin-modal.active { opacity: 1; pointer-events: auto; }

        .login-box {
            background: #140b24;
            padding: 3rem;
            border-radius: 12px;
            border: 1px solid rgba(189, 0, 255, 0.3);
            width: 100%;
            max-width: 420px;
        }

        .login-box h2 { margin-bottom: 1.5rem; color: #fff; text-transform: uppercase; text-align: center; }
        .form-group { margin-bottom: 1.5rem; }
        .form-group label { display: block; margin-bottom: 0.5rem; color: var(--text-muted); font-size: 0.85rem; }
        .form-group input { width: 100%; padding: 0.8rem 1rem; background: #090412; border: 1px solid rgba(255, 42, 133, 0.2); border-radius: 6px; color: #fff; }
        .form-group input:focus { outline: none; border-color: var(--pink-neon); }
        .login-actions { display: flex; justify-content: space-between; align-items: center; margin-top: 2rem; }
        .cancel-btn { background: transparent; color: var(--text-muted); border: none; cursor: pointer; font-weight: 600; }
        .error-msg { color: var(--pink-neon); font-size: 0.85rem; margin-top: 0.5rem; display: none; text-align: center; }
    </style>
</head>
<body>

    <!-- SVG Background Corner Pieces -->
    <svg class="corner-web top-left" viewBox="0 0 100 100" preserveAspectRatio="none"><path d="M0,0 L100,0 M0,0 L0,100 M0,0 L100,100 M0,25 Q25,25 25,0 M0,50 Q50,50 50,0 M0,75 Q75,75 75,0 M0,100 Q100,100 100,0" fill="none" stroke-width="0.5"/></svg>
    <svg class="corner-web top-right" viewBox="0 0 100 100" preserveAspectRatio="none"><path d="M0,0 L100,0 M0,0 L0,100 M0,0 L100,100 M0,25 Q25,25 25,0 M0,50 Q50,50 50,0 M0,75 Q75,75 75,0 M0,100 Q100,100 100,0" fill="none" stroke-width="0.5"/></svg>
    <svg class="corner-web bottom-left" viewBox="0 0 100 100" preserveAspectRatio="none"><path d="M0,0 L100,0 M0,0 L0,100 M0,0 L100,100 M0,25 Q25,25 25,0 M0,50 Q50,50 50,0 M0,75 Q75,75 75,0 M0,100 Q100,100 100,0" fill="none" stroke-width="0.5"/></svg>
    <svg class="corner-web bottom-right" viewBox="0 0 100 100" preserveAspectRatio="none"><path d="M0,0 L100,0 M0,0 L0,100 M0,0 L100,100 M0,25 Q25,25 25,0 M0,50 Q50,50 50,0 M0,75 Q75,75 75,0 M0,100 Q100,100 100,0" fill="none" stroke-width="0.5"/></svg>

    <!-- Header -->
    <header>
        <div class="logo">Find & Get</div>
        <nav>
            <a href="#about">About Us</a>
            <a href="#ai-finder">AI Finder</a>
            <a href="#services">Services</a>
            <a href="#" class="admin-trigger" id="open-admin">Admin Portal</a>
        </nav>
    </header>

    <!-- Main Workspace -->
    <main>
        
        <!-- Hero Section -->
        <section class="hero-section">
            <div class="hero-left">
                <h1>We Find Offline Shops.<br>We Get Them Online.</h1>
                <p>Using proprietary automation to track local businesses without a digital presence, crafting premium web frameworks to catch their target clients.</p>
                <button class="cta-btn" onclick="location.href='#ai-finder'">Try AI Finder</button>
            </div>
            
            <div class="hero-right">
                <div class="web-interactive-wrapper" id="web-wrapper" title="Click to spin the net!">
                    <div class="spider-net-svg-container" id="spinning-net">
                        <svg viewBox="0 0 400 400">
                            <g transform="translate(200,200)">
                                <!-- Axes -->
                                <line x1="0" y1="0" x2="0" y2="-180" stroke="#bd00ff" stroke-width="1.5" />
                                <line x1="0" y1="0" x2="127" y2="-127" stroke="#bd00ff" stroke-width="1.5" />
                                <line x1="0" y1="0" x2="180" y2="0" stroke="#bd00ff" stroke-width="1.5" />
                                <line x1="0" y1="0" x2="127" y2="127" stroke="#bd00ff" stroke-width="1.5" />
                                <line x1="0" y1="0" x2="0" y2="180" stroke="#bd00ff" stroke-width="1.5" />
                                <line x1="0" y1="0" x2="-127" y2="127" stroke="#bd00ff" stroke-width="1.5" />
                                <line x1="0" y1="0" x2="-180" y2="0" stroke="#bd00ff" stroke-width="1.5" />
                                <line x1="0" y1="0" x2="-127" y2="-127" stroke="#bd00ff" stroke-width="1.5" />
                                <!-- Concentric Strings -->
                                <polygon points="0,-50 35,-35 50,0 35,35 0,50 -35,35 -50,0 -35,-35" fill="none" stroke="#ff2a85" stroke-width="1" opacity="0.5"/>
                                <polygon points="0,-90 64,-64 90,0 64,64 0,90 -64,64 -90,0 -64,-64" fill="none" stroke="#ff2a85" stroke-width="1" opacity="0.6"/>
                                <polygon points="0,-130 92,-92 130,0 92,92 0,130 -92,92 -130,0 -92,-92" fill="none" stroke="#ff2a85" stroke-width="1.2" opacity="0.7"/>
                                <polygon points="0,-170 120,-120 170,0 120,120 0,170 -120,120 -170,0 -120,-120" fill="none" stroke="#ff2a85" stroke-width="1.5" opacity="0.9"/>
                                <!-- Nodes -->
                                <circle cx="0" cy="-170" r="6" fill="#fff" filter="drop-shadow(0 0 5px #ff2a85)"/>
                                <circle cx="120" cy="-120" r="6" fill="#fff" filter="drop-shadow(0 0 5px #ff2a85)"/>
                                <circle cx="170" cy="0" r="6" fill="#fff" filter="drop-shadow(0 0 5px #ff2a85)"/>
                                <circle cx="120" cy="120" r="6" fill="#fff" filter="drop-shadow(0 0 5px #ff2a85)"/>
                                <circle cx="0" cy="170" r="6" fill="#fff" filter="drop-shadow(0 0 5px #ff2a85)"/>
                                <circle cx="-120" cy="120" r="6" fill="#fff" filter="drop-shadow(0 0 5px #ff2a85)"/>
                                <circle cx="-170" cy="0" r="6" fill="#fff" filter="drop-shadow(0 0 5px #ff2a85)"/>
                                <circle cx="-120" cy="-120" r="6" fill="#fff" filter="drop-shadow(0 0 5px #ff2a85)"/>
                                <circle cx="0" cy="0" r="8" fill="#fff" filter="drop-shadow(0 0 8px #bd00ff)"/>
                            </g>
                        </svg>
                    </div>
                </div>
            </div>
        </section>

        <!-- About Us Section -->
        <section id="about">
            <h2 class="section-title">About <span>Us</span></h2>
            <div class="about-container">
                <p><strong>Find & Get</strong> was built to solve a massive real-world gap. Millions of incredible brick-and-mortar shops, local boutiques, and service providers have flawless physical reputations but are completely invisible online.</p>
                <p>We are a dual-force digital agency. First, we use automation algorithms to map cities and identify shops operating entirely offline or with critically outdated landing pages. Second, we spin elite, high-conversion web frameworks to deploy them directly into the modern web ecosystem, turning hidden local businesses into visible digital anchors.</p>
            </div>
        </section>

        <!-- AI Finder Section -->
        <section id="ai-finder">
            <h2 class="section-title">AI Shop <span>Finder</span></h2>
            <div class="finder-container">
                <div class="finder-search-bar">
                    <input type="text" id="location-input" class="finder-input" placeholder="Enter target city or zip code (e.g., New York, London)...">
                    <button class="scan-btn" id="scan-btn">Scan Area</button>
                </div>
                <div class="results-box" id="results-box">
                    <p class="status-placeholder" id="status-placeholder">Ready to hunt. Enter a location and execute AI scan...</p>
                </div>
            </div>
        </section>

        <!-- Services/Features Section -->
        <section id="services" class="features-grid">
            <div class="card">
                <h3>1. Find</h3>
                <p>We continuously crawl localized coordinates to catalog physical businesses lacking domain authorities or active responsive pages.</p>
            </div>
            <div class="card">
                <h3>2. Design</h3>
                <p>We deploy premium tailored user experiences wrapped in interactive, lightweight code bases optimized to convert traffic instantly.</p>
            </div>
            <div class="card">
                <h3>3. Get Results</h3>
                <p>By connecting custom domains, launching search ranking setups, and providing modern UI layers, we hand over complete client hooks.</p>
            </div>
        </section>
    </main>

    <!-- Secure Admin Panel Modal -->
    <div class="admin-modal" id="admin-modal">
        <div class="login-box">
            <h2>Access Control</h2>
            <form id="admin-form">
                <div class="form-group">
                    <label for="username">Admin Identifier</label>
                    <input type="text" id="username" autocomplete="off" required>
                </div>
                <div class="form-group">
                    <label for="password">Passkey</label>
                    <input type="password" id="password" required>
                </div>
                <div class="error-msg" id="error-msg">Invalid verification credentials.</div>
                <div class="login-actions">
                    <button type="button" class="cancel-btn" id="close-admin">Cancel</button>
                    <button type="submit" class="cta-btn" style="padding: 0.6rem 1.5rem; font-size: 0.9rem;">Verify</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Scripting Infrastructure -->
    <script>
        /* --- Interactive Net Spinning System --- */
        const webWrapper = document.getElementById('web-wrapper');
        const spinningNet = document.getElementById('spinning-net');
        let targetRotation = 0;
        let isSpinning = false;

        webWrapper.addEventListener('click', () => {
            targetRotation += 720; 
            spinningNet.style.transform = `rotate(${targetRotation}deg)`;
            if (!isSpinning) {
                isSpinning = true;
                spinningNet.classList.add('spinning-blur');
            }
        });

        spinningNet.addEventListener('transitionend', () => {
            spinningNet.classList.remove('spinning-blur');
            isSpinning = false;
        });

        /* --- Simulated AI Finder System Logic --- */
        const scanBtn = document.getElementById('scan-btn');
        const locationInput = document.getElementById('location-input');
        const resultsBox = document.getElementById('results-box');

        const mockShops = [
            { name: "Downtown Vintage & Denim", type: "Boutique Apparel", status: "No Website Found" },
            { name: "Silverline Auto Mechanical", type: "Automotive Repair", status: "Outdated (2012 Layout)" },
            { name: "The Wooden Whisk Cafe", type: "Artisanal Bakery", status: "Missing Mobile UI" }
        ];

        scanBtn.addEventListener('click', () => {
            const loc = locationInput.value.trim();
            if (!loc) {
                alert("Please provide a city or coordinate area to scan.");
                return;
            }

            // Enter active processing mode
            scanBtn.textContent = "Scanning...";
            scanBtn.disabled = true;
            resultsBox.innerHTML = `<p class="status-placeholder" style="color: var(--pink-neon);">AI crawler deployed to ${loc}... analyzing regional map directories...</p>`;

            setTimeout(() => {
                resultsBox.innerHTML = ""; // Flush template strings
                
                mockShops.forEach((shop, index) => {
                    setTimeout(() => {
                        const card = document.createElement('div');
                        card.className = 'shop-card';
                        card.innerHTML = `
                            <div class="shop-info">
                                <h4>${shop.name}</h4>
                                <p>${shop.type} • Target Candidate</p>
                            </div>
                            <span class="status-tag">${shop.status}</span>
                        `;
                        resultsBox.appendChild(card);
                    }, index * 400); // Stagger animations nicely
                });

                scanBtn.textContent = "Scan Area";
                scanBtn.disabled = false;
            }, 1800);
        });

        /* --- Admin Portal Overlay Controls --- */
        const openBtn = document.getElementById('open-admin');
        const closeBtn = document.getElementById('close-admin');
        const modal = document.getElementById('admin-modal');
        const form = document.getElementById('admin-form');
        const errMsg = document.getElementById('error-msg');

        openBtn.addEventListener('click', (e) => { e.preventDefault(); modal.classList.add('active'); });
        closeBtn.addEventListener('click', () => { modal.classList.remove('active'); form.reset(); errMsg.style.display = 'none'; });

        form.addEventListener('submit', (e) => {
            e.preventDefault();
            if (document.getElementById('username').value === "admin" && document.getElementById('password').value === "securepass") {
                alert("Access approved. Loading central directory routing layout.");
                modal.classList.remove('active');
                form.reset();
            } else {
                errMsg.style.display = 'block';
            }
        });
    </script>
</body>
</html>