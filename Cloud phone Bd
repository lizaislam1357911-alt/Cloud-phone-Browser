<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=320, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Cloud Phone Browser</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body {
      height:100vh;
      font-family: Arial, Helvetica, sans-serif;
      background:#1e3a8a; /* ডার্ক ব্লু - কম আই স্ট্রেইন */
      color:#ffffff;
      display:flex;
      flex-direction:column;
      overflow:hidden;
    }
    header {
      padding:12px;
      text-align:center;
      background:#111827;
      font-size:20px;
      font-weight:bold;
    }
    main {
      flex:1;
      display:flex;
      flex-direction:column;
      align-items:center;
      justify-content:center;
      padding:10px;
    }
    .search-container {
      width:100%;
      max-width:300px;
      margin:20px 0;
    }
    .search-box {
      width:100%;
      padding:14px;
      font-size:18px;
      border:none;
      border-radius:30px;
      background:#374151;
      color:#ffffff;
      outline:none;
      text-align:center;
    }
    .search-box::placeholder { color:#9ca3af; }
    .bookmarks {
      display:grid;
      grid-template-columns:repeat(3, 1fr); /* ৩টা করে আইকন — ছোট স্ক্রিনে ফিট */
      gap:16px;
      width:100%;
      max-width:300px;
    }
    .bookmark {
      text-align:center;
      text-decoration:none;
      color:#ffffff;
    }
    .bookmark img {
      width:64px;
      height:64px;
      border-radius:16px;
      background:#4b5563;
      padding:8px;
    }
    .bookmark span {
      font-size:14px;
      margin-top:6px;
      display:block;
    }
    footer {
      padding:10px;
      text-align:center;
      background:#111827;
      font-size:14px;
    }
  </style>
</head>
<body>

  <header>Cloud Phone Browser</header>

  <main>
    <!-- সার্চ বার -->
    <div class="search-container">
      <form action="https://www.google.com/search" method="get" target="_blank">
        <input type="text" name="q" class="search-box" placeholder="সার্চ করুন..." autofocus>
      </form>
    </div>

    <!-- বুকমার্ক — বড় + কম স্পেস -->
    <div class="bookmarks">
      <a href="https://www.cloudemulator.net/" class="bookmark" target="_blank">
        <img src="https://www.google.com/s2/favicons?domain=cloudemulator.net&sz=64" alt="Redfinger">
        <span>Redfinger</span>
      </a>
      <a href="https://www.ldcloud.net/" class="bookmark" target="_blank">
        <img src="https://www.google.com/s2/favicons?domain=ldcloud.net&sz=64" alt="LDCloud">
        <span>LDCloud</span>
      </a>
      <a href="https://www.geelark.com/" class="bookmark" target="_blank">
        <img src="https://www.google.com/s2/favicons?domain=geelark.com&sz=64" alt="GeeLark">
        <span>GeeLark</span>
      </a>
      <!-- আরও যোগ করলে grid auto-adjust হবে -->
    </div>
  </main>

  <footer>Owned By (Cloudphonebd)</footer>

</body>
</html>
