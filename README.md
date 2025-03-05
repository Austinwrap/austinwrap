<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1, user-scalable=no">
    <title>AUSTINWRAP</title>
    <link href="https://fonts.googleapis.com/css2?family=Bungee+Shade&family=Comic+Neue:wght@700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Comic Neue', sans-serif;
            background: #F5F5F5 url('https://www.transparenttextures.com/patterns/confetti.png') repeat;
            color: #333;
            line-height: 1.6;
            font-size: 16px;
            overflow-x: hidden;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: #26A69A;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }
        nav .logo {
            font-family: 'Bungee Shade', cursive;
            font-size: 2.5em;
            color: #FFF;
            text-shadow: 2px 2px 4px rgba(205, 220, 57, 0.5);
        }
        nav ul {
            list-style: none;
            display: flex;
            gap: 20px;
        }
        nav ul li a {
            text-decoration: none;
            color: #FFF;
            font-weight: 700;
            font-size: 1em;
            transition: color 0.3s, transform 0.3s;
            cursor: pointer;
        }
        nav ul li a:hover {
            color: #CDDC39;
            transform: scale(1.1);
        }
        .hamburger { display: none; font-size: 1.5em; color: #FFF; cursor: pointer; }
        @media (max-width: 768px) {
            nav { padding: 10px 15px; }
            nav .logo { font-size: 1.8em; }
            nav ul {
                display: none;
                flex-direction: column;
                position: fixed;
                top: 50px;
                right: 0;
                background: #26A69A;
                padding: 15px;
                box-shadow: -5px 5px 15px rgba(0, 0, 0, 0.2);
                width: 100%;
            }
            nav ul.show { display: flex; }
            .hamburger { display: block; }
        }
        .landing {
            padding: 60px 10px;
            text-align: center;
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
            z-index: 1;
        }
        .landing h1 {
            font-family: 'Bungee Shade', cursive;
            font-size: 4em;
            color: #26A69A;
            text-shadow: 2px 2px 4px rgba(205, 220, 57, 0.5);
            margin-bottom: 15px;
        }
        .landing p {
            font-size: 1.5em;
            color: #333;
            max-width: 600px;
            margin-bottom: 20px;
        }
        .pinata {
            width: 150px;
            height: 150px;
            background: url('https://cdn-icons-png.flaticon.com/512/3069/3069171.png') no-repeat center/contain;
            cursor: pointer;
            transition: transform 0.3s;
            margin-bottom: 20px;
        }
        .pinata:hover { transform: scale(1.1) rotate(5deg); }
        .tiles {
            display: none;
            max-width: 100%;
            margin: 0 auto;
            padding: 10px;
            opacity: 0;
            transition: opacity 0.5s ease;
        }
        .tiles.active {
            display: block;
            opacity: 1;
        }
        .section {
            margin-bottom: 20px;
        }
        .section h2 {
            font-family: 'Bungee', cursive;
            font-size: 2em;
            color: #CDDC39;
            margin-bottom: 10px;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
            cursor: pointer;
        }
        .tile-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
            gap: 10px;
        }
        .tile {
            background: #CDDC39;
            border: 3px solid #26A69A;
            border-radius: 10px;
            padding: 15px;
            text-align: center;
            transition: transform 0.3s, background 0.3s;
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.2);
            animation: bounceIn 0.5s ease;
        }
        @keyframes bounceIn {
            0% { transform: scale(0); opacity: 0; }
            60% { transform: scale(1.1); opacity: 1; }
            100% { transform: scale(1); }
        }
        .tile a {
            color: #333;
            text-decoration: none;
            font-weight: 700;
            font-size: 1em;
            display: block;
        }
        .tile:hover {
            transform: scale(1.05) rotate(2deg);
            background: #26A69A;
        }
        .tile:hover a { color: #FFF; }
        footer {
            background: #26A69A;
            color: #FFF;
            text-align: center;
            padding: 15px;
            border-top: 4px solid #CDDC39;
            z-index: 1000;
        }
        footer p { font-size: 1em; margin: 5px 0; }
        footer a { color: #FFF; text-decoration: none; }
        footer a:hover { color: #CDDC39; }
        @media (max-width: 768px) {
            .landing h1 { font-size: 2.5em; }
            .landing p { font-size: 1.2em; }
            .pinata { width: 120px; height: 120px; }
            .section h2 { font-size: 1.5em; }
            .tile-grid { grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); }
            .tile { padding: 10px; }
            .tile a { font-size: 0.9em; }
        }
    </style>
</head>
<body>
    <nav>
        <div class="logo">AUSTINWRAP</div>
        <div class="hamburger" id="hamburger"><i class="fas fa-bars"></i></div>
        <ul id="nav-links">
            <li><a onclick="scrollToSection('services')">Services</a></li>
            <li><a onclick="scrollToSection('games')">Games</a></li>
            <li><a onclick="scrollToSection('shop')">Shop</a></li>
            <li><a onclick="scrollToSection('social')">Social</a></li>
            <li><a onclick="scrollToSection('contact')">Contact</a></li>
        </ul>
    </nav>

    <div class="landing" id="home">
        <h1>AUSTINWRAP</h1>
        <p>Bing bong! Smash the pinata for fun stuff!</p>
        <div class="pinata" id="pinata"></div>
        <div class="tiles" id="tiles">
            <div class="section" id="services">
                <h2>Services</h2>
                <div class="tile-grid">
                    <div class="tile"><a href="mailto:roundhouselandscape@gmail.com">Power Washing</a></div>
                    <div class="tile"><a href="mailto:roundhouselandscape@gmail.com">Hauling</a></div>
                    <div class="tile"><a href="mailto:roundhouselandscape@gmail.com">Seasonal Work</a></div>
                    <div class="tile"><a href="mailto:roundhouselandscape@gmail.com">Specialty Tasks</a></div>
                    <div class="tile"><a href="mailto:ctdraftbeer@gmail.com">Beer & Keg Services</a></div>
                </div>
            </div>
            <div class="section" id="games">
                <h2>Games</h2>
                <div class="tile-grid">
                    <div class="tile"><a href="https://austinwrap.github.io/Bartend/" target="_blank">Celebrity Bartender</a></div>
                    <div class="tile"><a href="https://austinwrap.github.io/FrostyFarms/" target="_blank">Chicken Farm</a></div>
                    <div class="tile"><a href="https://austinwrap.github.io/BristolTycoon/" target="_blank">Bristol Tycoon</a></div>
                    <div class="tile"><a href="https://austinwrap.github.io/bad-mailman/" target="_blank">Bad Mailman</a></div>
                    <div class="tile"><a href="https://austinwrap.github.io/feminine-stocks/" target="_blank">Feminine Stocks</a></div>
                </div>
            </div>
            <div class="section" id="shop">
                <h2>Shop</h2>
                <div class="tile-grid">
                    <div class="tile"><a href="https://austinwrap.github.io/BananaGram/" target="_blank">Mail a Banana</a></div>
                    <div class="tile"><a href="https://austinwrap.github.io/Mobile-Bartending/" target="_blank">Mobile Bartending</a></div>
                    <div class="tile"><a href="https://austinwrap.github.io/Powerwash/" target="_blank">Powerwash LLC</a></div>
                    <div class="tile"><a href="https://www.etsy.com/shop/MyFavoriteAlien/" target="_blank">Etsy Shop</a></div>
                    <div class="tile"><a href="https://www.amazon.com/dp/B0CPTDZZSW" target="_blank">Book on Amazon</a></div>
                    <div class="tile"><a href="https://www.amazon.com/dp/B0CQHBF7XJ" target="_blank">Affirmations Journal</a></div>
                    <div class="tile"><a href="http://www.ctdraft.com/" target="_blank">CT Draft</a></div>
                    <div class="tile"><a href="https://austinwrap.github.io/TREY/" target="_blank">Trey’s Music</a></div>
                </div>
            </div>
            <div class="section" id="social">
                <h2>Social</h2>
                <div class="tile-grid">
                    <div class="tile"><a href="https://www.youtube.com/@austinwrap" target="_blank">YouTube</a></div>
                    <div class="tile"><a href="https://www.instagram.com/austinwrap" target="_blank">Instagram</a></div>
                    <div class="tile"><a href="https://www.tiktok.com/@austinwrap" target="_blank">TikTok</a></div>
                    <div class="tile"><a href="https://www.twitch.tv/austinwrap_" target="_blank">Twitch</a></div>
                </div>
            </div>
            <div class="section" id="contact">
                <h2>Contact</h2>
                <div class="tile-grid">
                    <div class="tile"><a href="mailto:aytmout@gmail.com">General Inquiries</a></div>
                    <div class="tile"><a href="mailto:roundhouselandscape@gmail.com">Services</a></div>
                    <div class="tile"><a href="mailto:ctdraftbeer@gmail.com">Beer Line Work</a></div>
                    <div class="tile"><a href="tel:+18609066883">(860) 906-6883</a></div>
                </div>
            </div>
        </div>
    </div>

    <footer>
        <p>© 2025 AUSTINWRAP. All Rights Reserved.</p>
        <p>Bristol, CT • <a href="mailto:aytmout@gmail.com">aytmout@gmail.com</a></p>
    </footer>

    <script>
        function scrollToSection(id) {
            document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
            const tiles = document.getElementById('tiles');
            if (!tiles.classList.contains('active')) {
                document.getElementById('pinata').style.display = 'none';
                tiles.classList.add('active');
            }
        }

        document.getElementById('hamburger').addEventListener('click', () => {
            document.getElementById('nav-links').classList.toggle('show');
        });

        document.getElementById('pinata').addEventListener('click', () => {
            const pinata = document.getElementById('pinata');
            const tiles = document.getElementById('tiles');
            pinata.style.display = 'none';
            tiles.classList.add('active');
        });
    </script>
</body>
</html>
