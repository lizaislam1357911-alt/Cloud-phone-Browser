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
        }

        /* হেডার */
        header {
            background-color: #007bff;
            color: white;
            text-align: center;
            padding: 12px; font-weight: bold; font-size: 18px;
        }

        /* সার্চ সেকশন */
        .search-container {
            padding: 20px 10px;
            background: white;
            text-align: center;
            border-bottom: 1px solid #ddd;
        }

        .search-bar {
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

        .btn-action { background: none; border: none; cursor: pointer; font-size: 20px; padding: 0 5px; }

        /* কন্টেন্ট এরিয়া */
        .content {
            flex: 1; overflow-y: auto; padding: 15px;
        }

        h3 { font-size: 14px; color: #666; margin-bottom: 12px; border-bottom: 2px solid #007bff; width: fit-content; }

        .grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px; margin-bottom: 30px;
        }

        .item {
            text-align: center; text-decoration: none; color: #333;
            display: flex; flex-direction: column; align-items: center;
        }

        /* আইকন বক্স স্টাইল */
        .icon-box {
            width: 50px; height: 50px;
            border-radius: 12px;
            display: flex; align-items: center; justify-content: center;
            color: white; font-weight: bold; font-size: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            margin-bottom: 6px;
        }

        .yt { background: #FF0000; } /* YouTube Red */
        .gpt { background: #10a37f; } /* ChatGPT Green */
        .gemini { background: #4285f4; } /* Gemini Blue */
        .fb { background: #1877F2; } /* Facebook Blue */
        .user-added { background: #6c757d; } /* Default Grey for user bookmarks */

        .item span { font-size: 11px; font-weight: 500; }

        /* ফুটার */
        footer {
            background-color: #212529;
            color: #3dfc03;
            text-align: center;
            padding: 10px; font-size: 11px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <header>Browser</header>

    <div class="search-container">
        <div class="search-bar">
            <input type="text" id="urlInput" placeholder="Search Google...">
            <button class="btn-action" onclick="search()">🔍</button>
            <button class="btn-action" style="color: #28a745;" onclick="add()">+</button>
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

        <h3>My Bookmarks</h3>
        <div class="grid" id="myBookmarks">
            </div>
    </div>

    <footer>
        Owner By (Cloud Phone BD)
    </footer>

    <script>
        // পেজ লোড হলে বুকমার্ক দেখাবে
        window.onload = load;

        function search() {
            let q = document.getElementById('urlInput').value.trim();
            if(q) window.location.href = "https://www.google.com/search?q=" + encodeURIComponent(q);
        }

        function add() {
            let val = document.getElementById('urlInput').value.trim();
            if(val) {
                let list = JSON.parse(localStorage.getItem('savedLinks')) || [];
                list.push(val);
                localStorage.setItem('savedLinks', JSON.stringify(list));
                document.getElementById('urlInput').value = "";
                load();
            }
        }

        function load() {
            let list = JSON.parse(localStorage.getItem('savedLinks')) || [];
            let box = document.getElementById('myBookmarks');
            box.innerHTML = "";
            list.forEach(item => {
                box.innerHTML += `
                    <div class="item" onclick="window.location.href='https://www.google.com/search?q=${item}'">
                        <div class="icon-box user-added">${item[0].toUpperCase()}</div>
                        <span>${item}</span>
                    </div>
                `;
            });
        }
    </script>

</body>
</html>
