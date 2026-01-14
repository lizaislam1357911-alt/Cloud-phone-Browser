<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0; padding: 0;
            background-color: #f1f3f4;
            font-family: 'Segoe UI', sans-serif;
            display: flex; flex-direction: column; height: 100vh;
            overflow: hidden;
        }

        /* স্ট্যাটাস বার */
        .status-bar {
            background-color: #007bff;
            color: white;
            padding: 5px 10px;
            display: flex;
            justify-content: space-between;
            font-size: 10px;
        }

        header {
            background-color: #007bff;
            color: white;
            text-align: center;
            padding: 8px; font-weight: bold; font-size: 16px;
        }

        /* সার্চ এরিয়া */
        .search-container {
            padding: 12px 10px;
            background: white;
            border-bottom: 1px solid #ddd;
        }

        .search-bar {
            display: flex;
            align-items: center;
            background: #f1f3f4;
            border-radius: 20px;
            padding: 2px 10px;
            border: 1px solid #dfe1e5;
        }

        #urlInput {
            flex: 1; border: none; background: transparent;
            padding: 8px; font-size: 13px; outline: none;
        }

        /* মেইন কন্টেন্ট */
        .content { flex: 1; overflow-y: auto; padding: 10px; }

        h3 { font-size: 11px; color: #555; margin: 10px 0 5px 0; text-transform: uppercase; }

        .grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
            margin-bottom: 20px;
        }

        .item {
            text-align: center;
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
            cursor: pointer;
        }

        /* লোগো ইমেজ স্টাইল */
        .logo-img {
            width: 45px; height: 45px;
            border-radius: 10px;
            object-fit: cover;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
            margin-bottom: 4px;
            background: white;
        }

        /* ডিলিট বাটন */
        .del-btn {
            position: absolute; top: -5px; right: -2px;
            background: #ff4d4d; color: white; border: none;
            border-radius: 50%; width: 16px; height: 16px;
            font-size: 10px; display: flex; align-items: center;
            justify-content: center; z-index: 10;
        }

        .label { font-size: 9px; font-weight: 600; color: #333; white-space: nowrap; overflow: hidden; width: 100%; text-overflow: ellipsis; }

        /* ফুটার */
        footer {
            background-color: #202124;
            color: #3dfc03;
            text-align: center;
            padding: 8px; font-size: 10px; font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="status-bar">
        <span>Cloud Phone BD</span>
        <span>4G 🔋 98%</span>
    </div>

    <header>Browser</header>

    <div class="search-container">
        <div class="search-bar">
            <input type="text" id="urlInput" placeholder="Search Google...">
            <button style="background:none; border:none;" onclick="search()">🔍</button>
            <button style="background:none; border:none; color:green; font-weight:bold; font-size:20px;" onclick="add()">+</button>
        </div>
    </div>

    <div class="content">
        <h3>Highlights</h3>
        <div class="grid">
            <div class="item" onclick="location.href='https://www.youtube.com'">
                <img src="https://cdn-icons-png.flaticon.com/128/1384/1384060.png" class="logo-img">
                <div class="label">YouTube</div>
            </div>
            <div class="item" onclick="location.href='https://chat.openai.com'">
                <img src="https://cdn-icons-png.flaticon.com/128/12222/12222588.png" class="logo-img">
                <div class="label">ChatGPT</div>
            </div>
            <div class="item" onclick="location.href='https://gemini.google.com'">
                <img src="https://cdn-icons-png.flaticon.com/128/15496/15496659.png" class="logo-img">
                <div class="label">Gemini</div>
            </div>
            <div class="item" onclick="location.href='https://www.facebook.com'">
                <img src="https://cdn-icons-png.flaticon.com/128/733/733547.png" class="logo-img">
                <div class="label">Facebook</div>
            </div>
        </div>

        <h3>My Bookmarks</h3>
        <div id="bookmarkGrid" class="grid"></div>
    </div>

    <footer>
        Owner By (Cloud Phone BD)
    </footer>

    <script>
        window.onload = load;

        function search() {
            let q = document.getElementById('urlInput').value.trim();
            if(q) window.location.href = "https://www.google.com/search?q=" + encodeURIComponent(q);
        }

        function add() {
            let val = document.getElementById('urlInput').value.trim();
            if(val) {
                let list = JSON.parse(localStorage.getItem('myLinks')) || [];
                list.push(val);
                localStorage.setItem('myLinks', JSON.stringify(list));
                document.getElementById('urlInput').value = "";
                load();
            }
        }

        function remove(index) {
            let list = JSON.parse(localStorage.getItem('myLinks')) || [];
            list.splice(index, 1);
            localStorage.setItem('myLinks', JSON.stringify(list));
            load();
        }

        function load() {
            let list = JSON.parse(localStorage.getItem('myLinks')) || [];
            let grid = document.getElementById('bookmarkGrid');
            grid.innerHTML = "";
            list.forEach((item, index) => {
                grid.innerHTML += `
                    <div class="item">
                        <button class="del-btn" onclick="remove(${index})">×</button>
                        <div onclick="location.href='https://www.google.com/search?q=${item}'">
                            <div style="width:45px; height:45px; background:#5f6368; color:white; border-radius:10px; display:flex; align-items:center; justify-content:center; font-weight:bold; font-size:20px;">${item[0].toUpperCase()}</div>
                            <div class="label">${item}</div>
                        </div>
                    </div>`;
            });
        }
    </script>
</body>
</html>
