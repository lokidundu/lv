<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>A Special Message | Shobhit Dev</title>
    <style>
        * { box-sizing: border-box; }

        body {
            margin: 0;
            display: flex;
            min-height: 100dvh;
            perspective: 1000px;
            font: 1em/1.4 "Poppins", sans-serif;
            overflow: hidden;
            background: linear-gradient(to right, #ff7eb9, #ff65a3, #ff165d);
            background-size: 400% 400%;
            animation: gradientAnimation 10s ease infinite;
        }

        @keyframes gradientAnimation {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* 3D Book Core */
        .book {
            position: relative;
            display: flex;
            margin: auto;
            width: 42cqmin;
            pointer-events: none;
            transform-style: preserve-3d;
            transition: translate 1s;
            translate: calc(min(var(--c), 1) * 50%) 0%;
            rotate: 1 0 0 30deg;
        }

        .page {
            --thickness: 4;
            flex: none;
            display: flex;
            width: 100%;
            font-size: 2cqmin;
            pointer-events: all;
            user-select: none;
            transform-style: preserve-3d;
            transform-origin: left center;
            transition: transform 1s, rotate 1s ease-in calc((min(var(--i), var(--c)) - max(var(--i), var(--c))) * 50ms);
            translate: calc(var(--i) * -100%) 0px 0px;
            transform: translateZ(calc((var(--c) - var(--i) - 0.5) * calc(var(--thickness) * 0.23cqmin)));
            rotate: 0 1 0 calc(clamp(0, var(--c) - var(--i), 1) * -180deg);
        }

        .front, .back {
            position: relative;
            flex: none;
            width: 100%;
            backface-visibility: hidden;
            overflow: hidden;
            background-color: #fff;
            display: flex;
            flex-flow: column nowrap;
            padding: 1.5em;
            border: 1px solid #0002;
            color: hsl(0, 100%, 30%);
        }

        .back {
            translate: -100% 0;
            rotate: 0 1 0 180deg;
            background-image: linear-gradient(to right, #f7f7f7 80%, #eee 100%);
        }

        .front {
            background: linear-gradient(to left, #f7f7f7 80%, #eee 100%);
        }

        .cover {
            background: hsl(231, 32%, 29%) url("./cover.jpg") 50% / cover;
            color: white !important;
        }

        img { width: 100%; height: 100%; object-fit: cover; }

        /* Valentine Form Styling */
        .question-container {
            text-align: left;
            font-size: 0.8em;
            overflow-y: auto;
            max-height: 80%;
        }

        textarea {
            width: 100%;
            margin: 5px 0;
            border: 1px solid #ffccd5;
            border-radius: 5px;
            font-family: inherit;
            resize: none;
        }

        .btn-group {
            position: relative;
            height: 60px;
            margin-top: 10px;
        }

        button {
            padding: 8px 15px;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
        }

        #yesBtn { background: #ff165d; color: white; }
        #noBtn { background: #eee; color: #333; position: absolute; transition: 0.2s; }

        .saveBtn {
            background: #ff165d;
            color: white;
            width: 100%;
            margin-top: 10px;
        }

        /* Emojis */
        .emoji {
            position: absolute;
            font-size: 2rem;
            opacity: 0;
            bottom: -50px;
            animation: floatEmojis 6s linear infinite;
        }

        @keyframes floatEmojis {
            0% { transform: translateY(0); opacity: 0; }
            20% { opacity: 1; }
            100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body>

    <audio id="loveMusic" loop>
        <source src="love.mp3" type="audio/mpeg">
    </audio>

    <div class="book">
        <div class="page">
            <div class="front cover">
                <h1 style="text-shadow: 2px 2px 5px black;">A Message for You🤍</h1>
                <p style="text-shadow: 2px 2px 5px black;">2025.<br />SHOBHIT Special Edition</p>
            </div>
            <div class="back">
                <h2>A Special Beginning ❤️</h2>
                <p>Some people come into our lives unexpectedly, yet leave a lasting impact. You are one of those rare souls who make every moment feel special.</p>
                <p>Click the pages to keep reading...</p>
            </div>
        </div>

        <div class="page">
            <div class="front">
                <h2>The Magic of You ✨</h2>
                <p>There’s a charm about you that words can hardly capture. It’s in the sparkle of your eyes and the warmth of your smile.</p>
            </div>
            <div class="back">
                <img src="./1.jpg" alt="Memory 1" />
            </div>
        </div>

        <div class="page">
            <div class="front">
                <h2>A Question... ❤️</h2>
                <p>From the moment we started talking, you’ve been on my mind. You make my world brighter and my heart fuller.</p>
                <p>So, straight from my heart...</p>
                <h3 style="text-align: center;">Will you be my Valentine?</h3>
                
                <div class="btn-group">
                    <button id="yesBtn" onclick="showLetterForm()">Yes 💕</button>
                    <button id="noBtn" onmouseover="moveNo()">No 🙈</button>
                </div>
            </div>
            <div class="back" id="letterPage">
                <h2>My Love Letter 💖</h2>
                <div class="question-container" id="formContent">
                    <p style="font-style: italic;">(Please click "Yes" on the other page first!)</p>
                </div>
            </div>
        </div>

        <div class="page">
            <div class="front">
                <img src="./4.png" alt="Ending" />
            </div>
            <div class="back cover" style="text-align: center;">
                <h3>Cutest Queen</h3>
                <p>Forever Yours,<br>Shobhit Dev</p>
            </div>
        </div>
    </div>

    <script>
        const emojis = ['❤️', '💖', '✨', '🌸', '🥰', '💘'];
        for (let i = 0; i < 15; i++) {
            let div = document.createElement('div');
            div.className = 'emoji';
            div.innerHTML = emojis[Math.floor(Math.random() * emojis.length)];
            div.style.left = Math.random() * 100 + 'vw';
            div.style.animationDelay = Math.random() * 5 + 's';
            document.body.appendChild(div);
        }

        const flipBook = (elBook) => {
            elBook.style.setProperty("--c", 0);
            elBook.querySelectorAll(".page").forEach((page, idx) => {
                page.style.setProperty("--i", idx);
                page.addEventListener("click", (evt) => {
                    if (evt.target.closest("button") || evt.target.closest("textarea")) return;
                    const curr = evt.target.closest(".back") ? idx : idx + 1;
                    elBook.style.setProperty("--c", curr);
                });
            });
        };
        document.querySelectorAll(".book").forEach(flipBook);

        function moveNo() {
            const btn = document.getElementById('noBtn');
            const x = Math.random() * 100 - 50;
            const y = Math.random() * 60 - 30;
            btn.style.transform = `translate(${x}px, ${y}px)`;
        }

        function showLetterForm() {
            document.getElementById("loveMusic").play();
            const form = document.getElementById("formContent");
            const questions = [
                "What's your favorite memory of us?",
                "What little thing about me makes you smile?",
                "If we could go anywhere right now, where?",
                "What song reminds you of us?"
            ];
            
            let html = `<p>Answer these for me:</p>`;
            questions.forEach((q, i) => {
                html += `<div><strong>${q}</strong><textarea id="q${i}" rows="1"></textarea></div>`;
            });
            html += `<button class="saveBtn" onclick="saveLetter()">Save Letter 💌</button>`;
            
            form.innerHTML = html;
            alert("Yay! You made me the happiest! Now check the next page to fill out our letter. 💕");
        }

        function saveLetter() {
            let text = "💌 Our Valentine Memories\n\n";
            const questions = ["Memory:", "What makes you smile:", "Travel destination:", "Our Song:"];
            for(let i=0; i<4; i++) {
                text += questions[i] + " " + document.getElementById(`q${i}`).value + "\n";
            }
            const blob = new Blob([text], {type: "text/plain"});
            const a = document.createElement("a");
            a.href = URL.createObjectURL(blob);
            a.download = "Love_Letter.txt";
            a.click();
        }
    </script>
</body>
</html>
