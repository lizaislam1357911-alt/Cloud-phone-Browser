<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0; padding: 0;
            background-color: #f4f7f6;
            font-family: 'Segoe UI', sans-serif;
            display: flex; flex-direction: column; height: 100vh;
        }

        /* হেডার */
        header {
            background-color: #0088cc;
            color: white;
            text-align: center;
            padding: 10px; font-weight: bold; font-size: 18px;
        }

        /* সার্চ ও অ্যাড সেকশন */
        .controls {
            padding: 10px;
            background: #fff;
            display: flex; gap: 5px;
            border-bottom: 1px solid #ddd;
        }
        #urlInput {
            flex: 1; padding: 10px;
            border: 2px solid #0088cc;
            border-radius: 5px; outline: none;
        }
        .btn {
            background: #0088cc; color: white;
            border: none; border-radius: 5px;
            padding: 0 12px; cursor: pointer; font-size: 18px;
        }
        .btn-add { background: #28a745; } /* সবুজ রঙের প্লাস বাটন */

        /* বুকমার্ক গ্রিড */
        .bookmarks-grid {
            padding: 15px;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px; flex: 1;
            overflow-y: auto;
            align-content: start;
        }
        .bookmark-item {
            text-align: center; font-size: 11px; text-decoration: none; color: #333;
        }
        .bookmark-item div.icon-box {
            width: 45px; height: 45px;
            margin: 0 auto 5px;
            background: #0088cc; color: white;
            display: flex; align-items: center; justify-content: center;
            border-radius: 10px; font-size: 20px; font-weight: bold;
            box-shadow: 0 3px 6px rgba(0,0,0,0.1);
        }

        /* ফুটার */
        footer {
            background-color: #1a1a1a;
            color: #3dfc03;
            text-align: center;
            padding: 8px; font-size: 11px;
            letter-spacing: 1px;
        }
    </style>
</head>
<body>

    <header>Browser</header>

    <div class="controls">
        <input type="text" id="urlInput" placeholder="Search or Website name">
        <button class="btn" onclick="googleSearch()">🔍</button>
        <button class="btn btn-add" title="Add Bookmark" onclick="addBookmark()">+</button>
    </div>

    <div class="bookmarks-grid" id="bookmarkList">
        </div>

    <footer>
        Owner By (Cloud Phone BD)
    </footer>

    <script>
        const urlInput = document.getElementById('urlInput');
        const bookmarkList = document.getElementById('bookmarkList');

        // লোড হওয়ার সময় আগের বুকমার্কগুলো দেখানো
        window.onload = displayBookmarks;

        // গুগল সার্চ ফাংশন
        function googleSearch() {
            let query = urlInput.value;
            if(query) {
                window.location.href = "https://www.google.com/search?q=" + encodeURIComponent(query);
            }
        }

        // বুকমার্ক অ্যাড করার ফাংশন
        function addBookmark() {
            let name = urlInput.value;
            if(!name) {
                alert("Please enter a name first!");
                return;
            }

            let bookmarks = JSON.parse(localStorage.getItem('myBookmarks')) || [];
            bookmarks.push(name);
            localStorage.setItem('myBookmarks', JSON.stringify(bookmarks));
            
            urlInput.value = ""; // বক্স খালি করা
            displayBookmarks(); // লিস্ট আপডেট করা
        }

        // বুকমার্ক প্রদর্শন করার ফাংশন
        function displayBookmarks() {
            let bookmarks = JSON.parse(localStorage.getItem('myBookmarks')) || [];
            bookmarkList.innerHTML = ""; // আগের লিস্ট মোছা

            bookmarks.forEach((name, index) => {
                let firstLetter = name.charAt(0).toUpperCase();
                bookmarkList.innerHTML += `
                    <div class="bookmark-item" onclick="window.location.href='https://www.google.com/search?q=${name}'">
                        <div class="icon-box">${firstLetter}</div>
                        <div>${name}</div>
                    </div>
                `;
            });
        }

        // এন্টার চাপলে সার্চ
        urlInput.addEventListener('keypress', (e) => { if (e.key === 'Enter') googleSearch(); });
    </script>

</body>
</html>
