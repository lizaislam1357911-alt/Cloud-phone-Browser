<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0; padding: 0;
            background-color: #f0f3f5;
            font-family: 'Segoe UI', sans-serif;
            display: flex; flex-direction: column; height: 100vh;
        }

        /* হেডার */
        header {
            background-color: #0056b3;
            color: white;
            text-align: center;
            padding: 12px; font-weight: bold; font-size: 18px;
        }

        /* গুগল সার্চ সেকশন */
        .search-area {
            padding: 20px 10px;
            background: white;
            text-align: center;
        }

        .search-box {
            display: flex;
            align-items: center;
            background: #f1f3f4;
            border-radius: 25px;
            padding: 5px 15px;
            max-width: 400px;
            margin: 0 auto;
            border: 1px solid #dfe1e5;
        }

        #urlInput {
            flex: 1; border: none; background: transparent;
            padding: 10px; font-size: 14px; outline: none;
        }

        .btn { background: none; border: none; cursor: pointer; font-size: 20px; }

        /* হাইলাইট ও বুকমার্ক সেকশন */
        .container {
            flex: 1; overflow-y: auto; padding: 15px;
        }

        h3 { font-size: 14px; color: #555; margin-bottom: 10px; border-bottom: 1px solid #ddd; padding-bottom: 5px; }

        .grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px; margin-bottom: 25px;
        }

        .item {
            text-align: center; text-decoration: none; color: #333;
        }

        .item img, .item .icon-circle {
            width: 45px; height: 45px;
            border-radius: 12px;
            background: white;
            display: flex; align-items: center; justify-content: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            margin: 0 auto 5px;
        }

        .item span { font-size: 11px; display: block; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }

        /* ফুটার */
        footer {
            background-color: #1a1a1a;
            color: #3dfc03;
            text-align: center;
            padding: 8px; font-size: 11px;
        }
    </style>
</head>
<body>

    <header>Browser</header>

    <div class="search-area">
        <div class="search-box">
            <input type="text" id="urlInput" placeholder="Search Google...">
            <button class="btn" onclick="search()">🔍</button>
            <button class="btn" style="color: green; font-weight: bold;" onclick="add()">+</button>
        </div>
    </div>

    <div class="container">
        <h3>Highlights</h3>
        <div class="grid">
            <a href="https://www.youtube.com" class="item">
                <img src="https://cdn-icons-png.flaticon.com/128/1384/1384060.png" alt="YT">
                <span>YouTube</span>
            </a>
            <a href="https://chat.openai.com" class="item">
                <img src="https://cdn-icons-png.flaticon.com/128/12222/12222588.png" alt="ChatGPT">
                <span>ChatGPT</span>
            </a>
            <a href="https://gemini.google.com" class="item">
                <img src="https://cdn-icons-png.flaticon.com/128/15496/15496659.png" alt="Gemini">
                <span>Gemini</span>
            </a>
            <a href="https://www.facebook.com" class="item">
                <img src="https://cdn-icons-png.flaticon.com/128/733/733547.png" alt="FB">
                <span>Facebook</span>
            </a>
        </div>

        <h3>My Bookmarks</h3>
        <div class="grid" id="myBookmarks"></div>
    </div>

    <footer>
        Owner By (Cloud Phone BD)
    </footer>

    <script>
        window.onload = load;

        function search() {
            let q = document.getElementById('urlInput').value;
            if(q) window.location.href = "https://www.google.com/search?q=" + encodeURIComponent(q);
        }

        function add() {
            let val = document.getElementById('urlInput').value.trim();
            if(val) {
                let list = JSON.parse(localStorage.getItem('saved')) || [];
                list.push(val);
                localStorage.setItem('saved', JSON.stringify(list));
                document.getElementById('urlInput').value = "";
                load();
            }
        }

        function load() {
            let list = JSON.parse(localStorage.getItem('saved')) || [];
            let box = document.getElementById('myBookmarks');
            box.innerHTML = "";
            list.forEach(item => {
                box.innerHTML += `
                    <div class="item" onclick="window.location.href='https://www.google.com/search?q=${item}'">
                        <div class="icon-circle" style="background:#0056b3; color:white; font-weight:bold;">${item[0].toUpperCase()}</div>
                        <span>${item}</span>
                    </div>
                `;
            });
        }
    </script>

</body>
</html>
