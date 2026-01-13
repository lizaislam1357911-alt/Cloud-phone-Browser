
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cloud Phone BD Browser</title>
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0; padding: 0;
            background-color: #f8f9fa;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex; flex-direction: column; height: 100vh;
        }

        /* উপরের অংশ (Header) */
        header {
            background-color: #0056b3;
            color: white;
            text-align: center;
            padding: 12px;
            font-size: 20px;
            font-weight: bold;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        /* সার্চ এবং বুকমার্ক সেকশন */
        .search-section {
            padding: 15px;
            background: #fff;
            text-align: center;
        }

        .google-logo {
            font-size: 32px; font-weight: bold; margin-bottom: 15px;
        }

        .search-bar-container {
            display: flex;
            align-items: center;
            background: #f1f3f4;
            border-radius: 30px;
            padding: 5px 15px;
            max-width: 500px;
            margin: 0 auto;
            border: 1px solid #dfe1e5;
        }

        #urlInput {
            flex: 1;
            border: none;
            background: transparent;
            padding: 10px;
            font-size: 16px;
            outline: none;
        }

        .action-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 20px;
            padding: 5px;
            color: #5f6368;
            transition: color 0.2s;
        }

        .action-btn:hover { color: #000; }
        .add-btn { color: #28a745; font-size: 24px; font-weight: bold; }

        /* বুকমার্ক ডিসপ্লে গ্রিড */
        .bookmarks-grid {
            padding: 20px;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(70px, 1fr));
            gap: 20px;
            flex: 1;
            overflow-y: auto;
        }

        .bookmark-card {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: #3c4043;
            cursor: pointer;
        }

        .icon-circle {
            width: 50px;
            height: 50px;
            background-color: #fff;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
            font-weight: bold;
            color: #0056b3;
            box-shadow: 0 2px 6px rgba(0,0,0,0.1);
            margin-bottom: 8px;
            border: 1px solid #eee;
        }

        .bookmark-name {
            font-size: 12px;
            text-align: center;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            width: 100%;
        }

        /* ফুটার */
        footer {
            background-color: #202124;
            color: #3dfc03;
            text-align: center;
            padding: 10px;
            font-size: 12px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <header>Browser</header>

    <div class="search-section">
        <div class="google-logo">
            <span style="color: #4285F4">G</span><span style="color: #EA4335">o</span><span style="color: #FBBC05">o</span><span style="color: #4285F4">g</span><span style="color: #34A853">l</span><span style="color: #EA4335">e</span>
        </div>
        
        <div class="search-bar-container">
            <input type="text" id="urlInput" placeholder="Search or type URL">
            <button class="action-btn" onclick="googleSearch()" title="Search">🔍</button>
            <button class="action-btn add-btn" onclick="addBookmark()" title="Add Bookmark">+</button>
        </div>
    </div>

    <div class="bookmarks-grid" id="bookmarkContainer">
        </div>

    <footer>
        Owner By (Cloud Phone BD)
    </footer>

    <script>
        const urlInput = document.getElementById('urlInput');
        const container = document.getElementById('bookmarkContainer');

        // পেজ লোড হলে সেভ করা বুকমার্কগুলো দেখাবে
        window.onload = loadBookmarks;

        function googleSearch() {
            let val = urlInput.value.trim();
            if (val) {
                window.location.href = "https://www.google.com/search?q=" + encodeURIComponent(val);
            }
        }

        function addBookmark() {
            let name = urlInput.value.trim();
            if (!name) {
                alert("কিছু একটা লিখুন যা বুকমার্ক হিসেবে সেভ করবেন!");
                return;
            }

            let bookmarks = JSON.parse(localStorage.getItem('myLinks')) || [];
            bookmarks.push(name);
            localStorage.setItem('myLinks', JSON.stringify(bookmarks));
            
            urlInput.value = ""; // ইনপুট বক্স খালি করা
            loadBookmarks(); // নতুন তালিকা আপডেট করা
        }

        function loadBookmarks() {
            let bookmarks = JSON.parse(localStorage.getItem('myLinks')) || [];
            container.innerHTML = ""; // আগেরগুলো মুছে নতুন করে সাজানো

            bookmarks.forEach((item) => {
                let firstLetter = item.charAt(0).toUpperCase();
                
                let card = document.createElement('div');
                card.className = 'bookmark-card';
                card.onclick = () => {
                    window.location.href = "https://www.google.com/search?q=" + encodeURIComponent(item);
                };

                card.innerHTML = `
                    <div class="icon-circle">${firstLetter}</div>
                    <div class="bookmark-name">${item}</div>
                `;
                container.appendChild(card);
            });
        }

        // Enter চাপলে সার্চ হবে
        urlInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') googleSearch();
        });
    </script>

</body>
</html>
