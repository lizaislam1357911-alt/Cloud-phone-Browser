<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cloud Phone BD Browser</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', sans-serif;
            display: flex;
            flex-direction: column;
            height: 100vh;
        }

        /* হেডার */
        header {
            background-color: #0044cc;
            color: white;
            text-align: center;
            padding: 10px 0;
            font-size: 18px;
            font-weight: bold;
        }

        /* টুলবার */
        .toolbar {
            display: flex;
            align-items: center;
            background: #f1f1f1;
            padding: 8px;
            gap: 8px;
            border-bottom: 1px solid #ccc;
        }

        .toolbar input {
            flex: 1;
            padding: 10px;
            border: 1px solid #bbb;
            border-radius: 20px;
            outline: none;
        }

        .btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 20px;
            display: flex;
            align-items: center;
        }

        /* গুগল সার্চ রেজাল্ট দেখানোর ফ্রেম */
        #browser-viewport {
            flex: 1;
            width: 100%;
            border: none;
        }

        /* ফুটার */
        footer {
            background-color: #1a1a1a;
            color: #3dfc03;
            text-align: center;
            padding: 8px 0;
            font-size: 12px;
        }
    </style>
</head>
<body>

    <header>Browser</header>

    <div class="toolbar">
        <input type="text" id="urlInput" placeholder="Search Google or type URL...">
        <button class="btn" onclick="performSearch()">🔍</button>
        <button class="btn" onclick="alert('Bookmarked!')">⭐</button>
        <button class="btn">⋮</button>
    </div>

    <iframe id="browser-viewport" src="https://www.google.com/search?igu=1"></iframe>

    <footer>
        Owner By (Cloud Phone BD)
    </footer>

    <script>
        const urlInput = document.getElementById('urlInput');
        const viewport = document.getElementById('browser-viewport');

        function performSearch() {
            const query = urlInput.value;
            if (query) {
                // যদি সরাসরি URL না হয়, তবে গুগলে সার্চ হবে
                if (query.includes('.') && !query.includes(' ')) {
                    viewport.src = query.startsWith('http') ? query : 'https://' + query;
                } else {
                    viewport.src = 'https://www.google.com/search?q=' + encodeURIComponent(query) + '&igu=1';
                }
            }
        }

        // এন্টার চাপলে সার্চ হবে
        urlInput.addEventListener('keypress', function (e) {
            if (e.key === 'Enter') {
                performSearch();
            }
        });
    </script>

</body>
</html>
