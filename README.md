<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0; padding: 0;
            background-color: #f4f4f9;
            font-family: 'Segoe UI', Arial, sans-serif;
            display: flex; flex-direction: column; height: 100vh;
            overflow: hidden;
        }

        /* স্ট্যাটাস বার (ছবির মতো) */
        .status-bar {
            background-color: #007bff;
            color: white;
            padding: 5px 10px;
            display: flex;
            justify-content: space-between;
            font-size: 10px;
            font-weight: bold;
        }

        /* হেডার */
        header {
            background-color: #007bff;
            color: white;
            text-align: center;
            padding: 10px;
            font-size: 18px;
            font-weight: bold;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        /* সার্চ সেকশন */
        .search-container {
            padding: 15px 10px;
            background: white;
            text-align: center;
        }

        .search-bar {
            display: flex;
            align-items: center;
            background: #f1f3f4;
            border-radius: 25px;
            padding: 5px 12px;
            border: 1px solid #dfe1e5;
        }

        #urlInput {
            flex: 1; border: none; background: transparent;
            padding: 8px; font-size: 14px; outline: none;
        }

        .btn-action { background: none; border: none; cursor: pointer; font-size: 18px; padding: 0 5px; }

        /* কন্টেন্ট এরিয়া */
        .content {
            flex: 1; overflow-y: auto; padding: 10px;
        }

        h3 { 
            font-size: 12px; 
            color: #444; 
            margin: 10px 0; 
            padding-left: 5px;
            border-left: 3px solid #007bff;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }

        .item {
            text-align: center;
            text-decoration: none;
            color: #333;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* আইকন বক্স ডিজাইন */
        .icon-box {
            width: 45px;
            height: 45px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 18px;
            box-shadow: 0 3px 6px rgba(0,0,0,0.15);
            margin-bottom: 5px;
            transition: transform 0.2s;
        }

        .item:active .icon-box { transform: scale(0.9); }

        /* হাইলাইট কালার */
        .yt { background: linear-gradient(135deg, #ff0000, #b20000); }
        .gpt { background: linear-gradient(135deg, #10a37f, #0d7a5f); }
        .gemini { background: linear-gradient(135deg, #4285f4, #3367d6); }
        .fb { background: linear-gradient(135deg, #1877F2, #145dbf); }
        .user-added { background: linear-gradient(135deg, #6c757d, #495057); }

        .item span { font-size: 9px; font-weight: 600; white-space: nowrap; }

        /* ফুটার */
        footer {
            background-color: #212529;
            color: #3dfc03;
            text-align: center;
            padding: 8px;
            font-size: 10px;
            font-weight: bold;
            border-top: 1px solid #444;
        }
    </style>
</head>
<body>

    <div class="status-bar">
        <span>Cloud Phone BD</span>
        <span>4G LTE 🔋 98%</span>
    </div>

    <header>Browser</header>

    <div class="search-container">
        <div class="search-bar">
            <input type="text" id="urlInput" placeholder="Search Google...">
            <button class="btn-action" onclick="search()" title="Search">🔍</button>
            <button class="btn-action" style="color: #28a745;" onclick="add()" title="Add Bookmark">+</button>
        </div>
    </div>

    <div class="content">
        <h3>Highlights</h3>
        <div class="grid">
            <a href="https://www.youtube.com" class="item">
                <div class="icon-box yt">Y</div>
                <span>YouTube</span>
            </a>
            <a href="https://chat.openai.com" class="item">
                <div class="icon-box gpt">C</div>
                <span>ChatGPT</span>
            </a>
            <a href="https://gemini.google.com" class="item">
                <div class="icon-box gemini">G</div>
                <span>Gemini</span>
            </a>
            <a href="https://www.facebook.com" class="item">
                <div class="icon-box fb">F</div>
                <span>Facebook</span>
            </a>
        </div>

        <h3>Bookmarks</h3>
        <div id="myBookmarks" class="grid">
            </div>
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
                let list = JSON.parse(localStorage.getItem('cloudLinks')) || [];
                list.push(val);
                localStorage.setItem('cloudLinks', JSON.stringify(list));
                document.getElementById('urlInput').value = "";
                load();
            }
        }

        function load() {
            let list = JSON.parse(localStorage.getItem('cloudLinks')) || [];
            let box = document.getElementById('myBookmarks');
            box.innerHTML = "";
            list.forEach((item, index) => {
                box.innerHTML += `
                    <div class="item" onclick="window.location.href='https://www.google.com/search?q=${item}'">
                        <div class="icon-box user-added">${item[0].toUpperCase()}</div>
                        <span>${item}</span>
                    </div>
                `;
            });
        }

        document.getElementById('urlInput').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') search();
        });
    </script>

</body>
</html>
