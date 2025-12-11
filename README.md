<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minecraft Server TW | 純生存伺服器</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;700;900&family=Poppins:wght@400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        :root {
            --primary-color: #00ff88; /* 螢光綠 (MC風格) */
            --accent-color: #7000ff; /* 賽博龐克紫 */
            --bg-dark: #0f1014;
            --glass-bg: rgba(255, 255, 255, 0.05);
            --glass-border: rgba(255, 255, 255, 0.1);
            --text-main: #ffffff;
            --text-dim: #a0a0a0;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', 'Noto Sans TC', sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-main);
            overflow-x: hidden;
        }

        /* 背景動態光暈 */
        .ambient-light {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 10% 20%, rgba(0, 255, 136, 0.05) 0%, transparent 40%),
                        radial-gradient(circle at 90% 80%, rgba(112, 0, 255, 0.05) 0%, transparent 40%);
            z-index: -1;
            pointer-events: none;
        }

        /* 導航欄 */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            padding: 1.5rem 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(15, 16, 20, 0.8);
            backdrop-filter: blur(10px);
            z-index: 1000;
            border-bottom: 1px solid var(--glass-border);
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 900;
            letter-spacing: 1px;
            color: var(--text-main);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo span {
            color: var(--primary-color);
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
        }

        .nav-links a {
            color: var(--text-dim);
            text-decoration: none;
            font-weight: 600;
            transition: 0.3s;
            position: relative;
        }

        .nav-links a:hover {
            color: var(--text-main);
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--primary-color);
            transition: 0.3s;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .cta-btn {
            padding: 0.6rem 1.5rem;
            background: linear-gradient(45deg, var(--accent-color), #4c00b0);
            border-radius: 50px;
            color: white;
            text-decoration: none;
            font-weight: 700;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .cta-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(112, 0, 255, 0.4);
        }

        /* Hero 區域 */
        .hero {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 0 5%;
            position: relative;
            /* **請更換此處的圖片！** 使用你伺服器的生存模式截圖，讓網站更有真實感。 */
            background: linear-gradient(to bottom, rgba(15, 16, 20, 0.3), var(--bg-dark)), 
                        url('https://images.unsplash.com/photo-1587573089734-09cb69c0f2b4?q=80&w=2070&auto=format&fit=crop') no-repeat center center/cover;
        }

        .hero h1 {
            font-size: 4rem;
            font-weight: 900;
            line-height: 1.1;
            margin-bottom: 1rem;
            background: linear-gradient(to right, #fff, #ccc);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .hero p {
            font-size: 1.2rem;
            color: var(--text-dim);
            margin-bottom: 2.5rem;
            max-width: 600px;
        }

        .server-ip-box {
            background: var(--glass-bg);
            border: 1px solid var(--glass-border);
            padding: 1rem 2rem;
            border-radius: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            backdrop-filter: blur(10px);
            transition: 0.3s;
            cursor: pointer;
        }

        .server-ip-box:hover {
            border-color: var(--primary-color);
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.2);
        }

        .ip-text {
            font-family: 'Poppins', monospace;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-color);
        }

        .copy-hint {
            font-size: 0.8rem;
            color: var(--text-dim);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        /* 特色區塊 */
        .features {
            padding: 5rem 10%;
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            margin-bottom: 3rem;
            font-weight: 800;
        }
        
        .section-title span {
            color: var(--primary-color);
        }

        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        .card {
            background: var(--glass-bg);
            border: 1px solid var(--glass-border);
            padding: 2.5rem;
            border-radius: 20px;
            transition: 0.3s;
            position: relative;
            overflow: hidden;
        }

        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: var(--primary-color);
            transform: scaleX(0);
            transform-origin: left;
            transition: 0.3s;
        }

        .card:hover {
            transform: translateY(-10px);
            background: rgba(255, 255, 255, 0.08);
        }

        .card:hover::before {
            transform: scaleX(1);
        }

        .card i {
            font-size: 2.5rem;
            color: var(--primary-color);
            margin-bottom: 1.5rem;
        }

        .card h3 {
            font-size: 1.5rem;
            margin-bottom: 1rem;
        }

        .card p {
            color: var(--text-dim);
            line-height: 1.6;
        }

        /* 頁腳 */
        footer {
            text-align: center;
            padding: 3rem;
            border-top: 1px solid var(--glass-border);
            color: var(--text-dim);
        }

        /* RWD 適配 */
        @media (max-width: 768px) {
            .nav-links {
                display: none; /* 簡單隱藏，實際開發可用漢堡選單 */
            }
            .hero h1 {
                font-size: 2.5rem;
            }
            .server-ip-box {
                flex-direction: column;
                gap: 5px;
            }
        }
    </style>
</head>
<body>

    <div class="ambient-light"></div>

    <nav>
        <div class="logo">
            <i class="fas fa-cube"></i> MC Server<span>TW</span>
        </div>
        <ul class="nav-links">
            <li>首頁</li>
            <li>關於純生存</li>
            <li>社群規定</li>
            <li>贊助/支持</li>
        </ul>
        
    </nav>

    <section class="hero">
        <span style="color: var(--primary-color); font-weight: 600; letter-spacing: 2px; margin-bottom: 10px;">PURE SURVIVAL</span>
        <h1>歡迎來到<br>純粹的生存世界</h1>
        <p>一個追求原版體驗、高社群互動的伺服器。沒有複雜的插件，只有你和朋友創造無限可能的方塊旅程。</p >
        
        <div class="server-ip-box" onclick="copyIP()" id="ipBox">
            <div class="ip-icon"><i class="fas fa-gamepad"></i></div>
            <div class="ip-text" id="ipText">PLAY.MCSERVER.TW</div>
            <div class="copy-hint" id="copyHint"><i class="far fa-copy"></i> 點擊複製 IP</div>
        </div>
    </section>

    <section class="features">
        <h2 class="section-title">我們的 <span>生存哲學</span></h2>
        <div class="card-grid">
            <div class="card">
                <i class="fas fa-gem"></i>
                <h3>原味核心體驗</h3>
                <p>我們極力保持原版 Minecraft 的核心玩法。沒有影響平衡的指令，享受最原始的探索與挑戰。</p >
            </div>
            <div class="card">
                <i class="fas fa-users"></i>
                <h3>社群共建家園</h3>
                <p>在和諧的社群中建立屬於你的城市、進行跨越世界的貿易。真正的樂趣來自於共同創造與分享。</p >
            </div>
            <div class="card">
                <i class="fas fa-lock"></i>
                <h3>公平與安全</h3>
                <p>雖然純淨，但我們有基礎的領地保護與反作弊機制，確保你的努力成果不會被惡意破壞。</p >
            </div>
        </div>
    </section>

    <footer>
        <p>&copy; 2024 Minecraft Server TW. Not affiliated with Mojang AB.</p >
        <div style="margin-top: 10px; font-size: 1.5rem;">
            
            <i class="fab fa-facebook" style="margin: 0 10px; cursor: pointer;"></i>
            <i class="fab fa-youtube" style="margin: 0 10px; cursor: pointer;"></i>
        </div>
    </footer>

    <script>
        function copyIP() {
            const ipText = document.getElementById('ipText').innerText;
            const hint = document.getElementById('copyHint');
            const box = document.getElementById('ipBox');

            // 執行複製
            navigator.clipboard.writeText(ipText).then(() => {
                // 視覺回饋
                hint.innerHTML = '<i class="fas fa-check"></i> 已複製！';
                hint.style.color = '#00ff88';
                box.style.borderColor = '#00ff88';
                
                // 2秒後恢復原狀
                setTimeout(() => {
                    hint.innerHTML = '<i class="far fa-copy"></i> 點擊複製 IP';
                    hint.style.color = '#a0a0a0';
                    box.style.borderColor = 'rgba(255, 255, 255, 0.1)';
                }, 2000);
            });
        }
    </script>
</body>
</html>
