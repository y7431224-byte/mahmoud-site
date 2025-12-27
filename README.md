<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>موقع المبرمج محمود 🚀</title>
    <style>
        body { background-color: #0f172a; color: white; font-family: 'Segoe UI', sans-serif; text-align: center; padding: 20px; margin: 0; }
        
        /* تصميم الساعة وعداد الزوار في الجنب */
        .sidebar-info { 
            position: fixed; 
            top: 20px; 
            left: 20px; 
            z-index: 1000;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        #digital-clock, .visitor-counter { 
            background: rgba(30, 41, 59, 0.9); 
            padding: 10px 15px; 
            border-radius: 10px; 
            border: 1px solid #38bdf8; 
            font-family: monospace; 
            font-size: 1.1rem; 
            color: #38bdf8;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }

        .visitor-counter { border-color: #fbbf24; color: #fbbf24; font-size: 0.9rem; }

        .container { display: flex; flex-wrap: wrap; justify-content: center; gap: 20px; margin-top: 80px; }
        .app-card { background-color: #1e293b; border-radius: 12px; padding: 20px; width: 300px; border: 1px solid #334155; }
        
        .xo-grid { display: grid; grid-template-columns: repeat(3, 100px); gap: 5px; justify-content: center; margin: 20px 0; }
        .xo-cell { width: 100px; height: 100px; background: #334155; border: none; font-size: 2rem; color: white; cursor: pointer; border-radius: 8px; }
        
        .whatsapp-btn { background-color: #25d366; color: white; padding: 12px 25px; text-decoration: none; border-radius: 50px; font-weight: bold; display: inline-block; margin-top: 15px; transition: 0.3s; }
        .whatsapp-btn:hover { transform: scale(1.05); background-color: #128c7e; }

        select, button { padding: 10px; margin: 10px; border-radius: 5px; border: none; cursor: pointer; }
    </style>
</head>
<body>

    <div class="sidebar-info">
        <div id="digital-clock">00:00:00</div>
        <div class="visitor-counter">👥 الزوار: <span id="count">جارِ التحميل..</span></div>
    </div>

    <h1>موقع المبرمج محمود 🚀</h1>

    <div class="container">
        <div class="app-card">
            <h3>لعبة XO الذكية 🎮</h3>
            <select id="difficulty">
                <option value="easy">مستوى سهل 😊</option>
                <option value="medium">مستوى متوسط 😐</option>
                <option value="hard">مستوى مستحيل 💀</option>
            </select>
            <div class="xo-grid" id="board">
                <button class="xo-cell" onclick="makeMove(0)"></button>
                <button class="xo-cell" onclick="makeMove(1)"></button>
                <button class="xo-cell" onclick="makeMove(2)"></button>
                <button class="xo-cell" onclick="makeMove(3)"></button>
                <button class="xo-cell" onclick="makeMove(4)"></button>
                <button class="xo-cell" onclick="makeMove(5)"></button>
                <button class="xo-cell" onclick="makeMove(6)"></button>
                <button class="xo-cell" onclick="makeMove(7)"></button>
                <button class="xo-cell" onclick="makeMove(8)"></button>
            </div>
            <button onclick="resetGame()" style="background: #ef4444; color: white;">إعادة اللعب</button>
        </div>

        <div class="app-card" style="border: 1px solid #25d366;">
            <h3 style="color: #25d366;">الشكاوى والاقتراحات 💬</h3>
            <p>للتواصل مع المبرمج محمود عبر واتساب</p>
            <a href="https://wa.me/201113832312?text=أهلاً%20المبرمج%20محمود%20عندي%20استفسار" target="_blank" class="whatsapp-btn">
                واتساب مباشر
            </a>
        </div>
    </div>

    <script>
        // ساعة
        function updateClock() {
            const now = new Date();
            document.getElementById('digital-clock').innerText = now.toLocaleTimeString('ar-EG');
        }
        setInterval(updateClock, 1000);
        updateClock();

        // عداد زوار (باستخدام خدمة GoatCounter البسيطة أو محاكاة برمجية)
        let visits = localStorage.getItem('visitorCount') || 0;
        visits++;
        localStorage.setItem('visitorCount', visits);
        document.getElementById('count').innerText = visits;

        // منطق لعبة XO (كما هو)
        let board = ["", "", "", "", "", "", "", "", ""];
        let gameOver = false;
        function makeMove(i) {
            if (board[i] === "" && !gameOver) {
                board[i] = "X";
                document.getElementsByClassName('xo-cell')[i].innerText = "X";
                checkWinner();
                if (!gameOver) setTimeout(computerMove, 500);
            }
        }
        function computerMove() {
            let available = board.map((v, i) => v === "" ? i : null).filter(v => v !== null);
            if (available.length > 0) {
                let move = available[Math.floor(Math.random() * available.length)];
                board[move] = "O";
                document.getElementsByClassName('xo-cell')[move].innerText = "O";
                checkWinner();
            }
        }
        function checkWinner() {
            const wins = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
            for (let s of wins) {
                if (board[s[0]] && board[s[0]] === board[s[1]] && board[s[0]] === board[s[2]]) {
                    alert(board[s[0]] === "X" ? "كسبت!" : "الكمبيوتر كسب!");
                    gameOver = true; return;
                }
            }
            if (!board.includes("")) { alert("تعادل!"); gameOver = true; }
        }
        function resetGame() {
            board = ["", "", "", "", "", "", "", "", ""]; gameOver = false;
            Array.from(document.getElementsByClassName('xo-cell')).forEach(c => c.innerText = "");
        }
    </script>
</body>
</html>
