
        <!DOCTYPE html>
        <html lang="my">
        <head>
            <meta charset="UTF-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0" />
            <title>MyLove.html</title>
            <style>
                @import url('https://fonts.googleapis.com/css2?family=Padauk:wght@400;700&display=swap');

                * { margin: 0; padding: 0; box-sizing: border-box; }

                body {
                    margin: 0;
                    font-family: 'Padauk', sans-serif;
                    min-height: 100vh;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    overflow: hidden;
                    position: relative;
                    /* CRISP & CLEAR background image — NO BLUR */
                    background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ5TIVuQSMY26uYfzgLTm4B4SXkKUI0lI4lzk-J_xekmg&s=10');
                    background-size: cover;
                    background-position: center;
                    background-attachment: fixed;
                }

                /* Dark overlay for readability — NO BLUR */
                body::before {
                    content: '';
                    position: fixed;
                    inset: 0;
                    background: rgba(0, 0, 0, 0.30);
                    /* only dark tint, no backdrop-filter */
                    z-index: 0;
                }

                .heart-container {
                    position: fixed;
                    top: 0; left: 0;
                    width: 100%; height: 100%;
                    pointer-events: none;
                    overflow: hidden;
                    z-index: 1;
                }
                .heart {
                    position: absolute;
                    bottom: -50px;
                    font-size: 2rem;
                    animation: floatUp linear infinite;
                    opacity: 0.6;
                }
                @keyframes floatUp {
                    0% { transform: translateY(0) rotate(0deg); opacity: 0.6; }
                    100% { transform: translateY(-110vh) rotate(360deg); opacity: 0; }
                }

                .glow-orb {
                    position: fixed;
                    border-radius: 50%;
                    filter: blur(45px);
                    opacity: 0.30;
                    pointer-events: none;
                    z-index: 0;
                    animation: orbDrift 9s ease-in-out infinite;
                }
                .glow-orb.o1 { width: 220px; height: 220px; background: #ffe29f; top: 8%; left: 8%; }
                .glow-orb.o2 { width: 170px; height: 170px; background: #ff9a9e; top: 62%; left: 80%; animation-delay: 2s; }
                .glow-orb.o3 { width: 190px; height: 190px; background: #ffd3a5; top: 72%; left: 10%; animation-delay: 4s; }
                @keyframes orbDrift {
                    0%, 100% { transform: translate(0,0) scale(1); }
                    50% { transform: translate(18px,-18px) scale(1.12); }
                }

                #app {
                    width: 100%;
                    max-width: 500px;
                    height: 90vh;
                    max-height: 800px;
                    background: rgba(255, 255, 255, 0.20);
                    /* NO backdrop-filter blur */
                    border-radius: 30px;
                    box-shadow: 0 20px 50px rgba(0,0,0,0.2), inset 0 0 0 1px rgba(255,255,255,0.35);
                    border: 1px solid rgba(255,255,255,0.2);
                    padding: 20px;
                    box-sizing: border-box;
                    display: flex;
                    flex-direction: column;
                    justify-content: center;
                    align-items: center;
                    text-align: center;
                    position: relative;
                    z-index: 2;
                    transition: all 0.5s ease;
                }

                .screen { display: none; flex-direction: column; align-items: center; width: 100%; height: 100%; justify-content: center; }
                .screen.active { display: flex; animation: fadeScale 0.6s ease; }
                @keyframes fadeScale {
                    0% { opacity: 0; transform: scale(0.95); }
                    100% { opacity: 1; transform: scale(1); }
                }

                h1 { color: #4A235A; margin-bottom: 10px; font-size: 2.2rem; text-shadow: 0 2px 4px rgba(255,255,255,0.5); }
                h2 { color: #333; font-size: 1.5rem; margin-bottom: 15px; }

                .question-badge {
                    background: rgba(255,255,255,0.7);
                    color: #6a3b7a;
                    font-weight: 700;
                    font-size: 0.95rem;
                    padding: 8px 20px;
                    border-radius: 30px;
                    margin-bottom: 15px;
                    box-shadow: 0 3px 10px rgba(0,0,0,0.08);
                    letter-spacing: 0.3px;
                }

                .bubble {
                    background: rgba(255, 182, 193, 0.80);
                    /* NO blur */
                    padding: 20px 30px;
                    border-radius: 30px;
                    border-bottom-left-radius: 5px;
                    margin: 20px 0;
                    font-size: 1.2rem;
                    color: #4a2040;
                    box-shadow: 0 5px 15px rgba(0,0,0,0.08);
                    max-width: 90%;
                }

                .btn-main {
                    background: #8E44AD;
                    color: white;
                    border: none;
                    padding: 15px 35px;
                    border-radius: 40px;
                    font-size: 1.2rem;
                    cursor: pointer;
                    font-weight: bold;
                    box-shadow: 0 4px 15px rgba(142, 68, 173, 0.4);
                    transition: all 0.2s;
                    margin-top: 10px;
                    position: relative;
                }
                .btn-main:hover { transform: scale(1.05); box-shadow: 0 6px 20px rgba(142, 68, 173, 0.5); }
                .btn-main:active { transform: scale(0.95); }

                .btn-next {
                    background: #2ECC71;
                    box-shadow: 0 4px 15px rgba(46, 204, 113, 0.4);
                }
                .btn-next:hover { box-shadow: 0 6px 20px rgba(46, 204, 113, 0.5); }

                #answer-overlay {
                    position: absolute;
                    top: 0; left: 0; width: 100%; height: 100%;
                    background: rgba(255, 255, 255, 0.25);
                    /* NO blur */
                    border-radius: 30px;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    z-index: 10;
                    opacity: 0;
                    pointer-events: none;
                    transition: opacity 0.4s ease;
                }
                #answer-overlay.open {
                    opacity: 1;
                    pointer-events: auto;
                }
                .answer-card {
                    background: rgba(255, 255, 255, 0.95);
                    /* NO blur */
                    padding: 30px;
                    border-radius: 20px;
                    max-width: 90%;
                    box-shadow: 0 10px 30px rgba(0,0,0,0.15);
                    transform: scale(0.9);
                    transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
                }
                #answer-overlay.open .answer-card {
                    transform: scale(1);
                }
                .answer-card {
                    padding-top: 0;
                    overflow: hidden;
                }
                .answer-header {
                    background: linear-gradient(135deg, #ffb6c1, #ff8fab);
                    color: #4a1942;
                    font-weight: 800;
                    font-size: 1.15rem;
                    padding: 16px 20px;
                    margin: 0 0 18px 0;
                    letter-spacing: 0.3px;
                }
                .answer-card p {
                    font-size: 1.2rem;
                    color: #333;
                    line-height: 1.5;
                }

                .confetti-piece {
                    position: fixed;
                    width: 10px;
                    height: 10px;
                    top: -10px;
                    z-index: 999;
                    pointer-events: none;
                    animation: fall linear forwards;
                }
                @keyframes fall {
                    to { transform: translateY(110vh) rotate(720deg); }
                }

                @media (max-width: 400px) {
                    #app { max-height: 90vh; padding: 15px; }
                    h1 { font-size: 1.8rem; }
                    .bubble { font-size: 1rem; padding: 15px; }
                }
            </style>
        </head>
        <body>
            <div class="heart-container" id="heart-container"></div>
            <div class="glow-orb o1"></div>
            <div class="glow-orb o2"></div>
            <div class="glow-orb o3"></div>

            <div id="app">
                <div id="intro-screen" class="screen active">
                    <h1>Hello ငယ်လေး! 💖</h1>
                    <div class="bubble">
                        <p>Your Boy မှာ သင့်အတွက် မေးခွန်းအချို့ ရှိပါတယ် 💕💕</p>
                    </div>
                    <button class="btn-main" onclick="startGame()">✨ ကြည့်ရန် ✨</button>
                </div>

                <div id="question-screen" class="screen">
                    <div class="question-badge">💌 Rizz Question <span id="q-num">1</span> of 5</div>
                    <div class="bubble" style="max-width:100%; padding:30px 20px;">
                        <p id="q-text" style="font-size:1.3rem; margin:0;">Loading...</p>
                    </div>
                    <button id="btn-choice" class="btn-main" onclick="revealAnswer()" style="background:#E67E22; box-shadow:0 4px 15px rgba(230,126,34,0.4);">Click Here</button>
                </div>

                <div id="answer-overlay">
                    <div class="answer-card">
                        <div class="answer-header">💖 Rizz Answer</div>
                        <p id="a-text">Answer Here...</p>
                        <button id="btn-next" class="btn-main btn-next" onclick="nextQuestion()">✨ Next ✨</button>
                    </div>
                </div>

                <div id="final-screen" class="screen">
                    <h1>🎉 Rizz Complete! 🎉</h1>
                    <div class="bubble" style="background:rgba(216,191,216,0.8);">
                        <p id="final-msg">ကြွေလောက်ပြီထင်တယ် အာဘွားလေးတော့ပေးခဲ့ပါအုံး😘</p>
                    </div>
                    <button id="btn-abwar" class="btn-main" style="background:#FF6B9D; box-shadow:0 4px 15px rgba(255,107,157,0.4); margin-top:10px;" onclick="giveAbwar()">💋 အာဘွား</button>
                    <div style="font-size:5rem; margin-top:20px; animation:float 2s infinite;">💖</div>
                </div>
            </div>

            <script>
                const questions = [{"q":"မင်း မှာ မြေပုံရှိလား ဗျ? 🤔","b":"မရှိဘူး 😅","a":"ငါ နှလုံးသားထဲမှာ မင်း အချစ်တွေ ပျောက်ဆုံးသွားလို့ ဗျ။ 🥰💖"},{"q":"မင်း က မှော်အတတ်တွေ သုံးတတ်တာလား ဗျ? 🪄✨","b":"မသုံးတတ်ပါဘူး 😶","a":"ဒါဆိုရင် ငါ က မင်း ကို မြင်ရင် အခြားဘယ်သူ့ကိုမှ မမြင်ရတော့လို့ပါ 👀🤭"},{"q":"မင်း ကို ကြည့်ရတာ လမ်းခဏခဏ ပျောက်တတ်သလိုပဲနော် 🗺️💫","b":"ဘာလို့လဲ? 🤨","a":"လမ်းမှားပြီး ငါ နှလုံးသားထဲ ဝင်လာလို့လေ 😉💕"},{"q":"မင်း က သူခိုးမှန်း ငါ မသိခဲ့ဘူးနော် 🥷💸","b":"ဘာလို့လဲ? 🧐","a":"ငါ ရဲ့ နှလုံးသားလေးကို ခိုးသွားလို့လေ 👀💘"},{"q":"မင်း က ငါ ကို မျက်လုံးပြပြီး လှည့်စားနေတာလား ဗျ? 😜","b":"ဟုတ်တယ် 😄","a":"ဟုတ်တယ်... ငါ အသက်တွေတောင် ရပ်သွားပါပြီနော် ချစ်တော့မယ်နော် 😍😍😍"}];
                let currentQuestion = 0;

                function startGame() {
                    document.getElementById('intro-screen').classList.remove('active');
                    document.getElementById('question-screen').classList.add('active');
                    updateQuestion();
                }

                function updateQuestion() {
                    const data = questions[currentQuestion];
                    document.getElementById('q-num').innerText = currentQuestion + 1;
                    document.getElementById('q-text').innerText = data.q;
                    document.getElementById('btn-choice').innerText = data.b;
                    document.getElementById('answer-overlay').classList.remove('open');
                }

                function revealAnswer() {
                    const data = questions[currentQuestion];
                    document.getElementById('a-text').innerHTML = data.a;
                    document.getElementById('answer-overlay').classList.add('open');
                    fireConfetti();
                }

                function nextQuestion() {
                    currentQuestion++;
                    if (currentQuestion < questions.length) {
                        updateQuestion();
                    } else {
                        document.getElementById('question-screen').classList.remove('active');
                        document.getElementById('answer-overlay').classList.remove('open');
                        document.getElementById('final-screen').classList.add('active');
                        fireConfetti();
                        fireConfetti();
                    }
                }

                function giveAbwar() {
                    document.getElementById('final-msg').innerHTML = 'အရမ်းချစ်တယ်နော ❤❤';
                    document.getElementById('btn-abwar').style.display = 'none';
                    fireConfetti();
                }

                function fireConfetti() {
                    const colors = ['#ff6b6b','#ffa94d','#ffd93d','#6bcb77','#4d96ff','#9b59b6','#ff9ff3','#feca57'];
                    for(let i=0; i<70; i++){
                        const c = document.createElement('div');
                        c.className = 'confetti-piece';
                        c.style.left = Math.random() * 100 + 'vw';
                        c.style.width = Math.random() * 8 + 4 + 'px';
                        c.style.height = Math.random() * 8 + 4 + 'px';
                        c.style.background = colors[Math.floor(Math.random() * colors.length)];
                        c.style.borderRadius = Math.random() > 0.5 ? '50%' : '2px';
                        c.style.animationDuration = Math.random() * 3 + 2 + 's';
                        document.body.appendChild(c);
                        setTimeout(() => c.remove(), 5000);
                    }
                }

                function createHeart() {
                    const h = document.createElement('div');
                    h.className = 'heart';
                    h.innerHTML = ['❤️','🧡','💛','💚','💙','💜','💖','💗'][Math.floor(Math.random()*8)];
                    h.style.left = Math.random() * 100 + 'vw';
                    h.style.animationDuration = Math.random() * 8 + 5 + 's';
                    h.style.fontSize = Math.random() * 1.5 + 1 + 'rem';
                    document.getElementById('heart-container').appendChild(h);
                    setTimeout(() => h.remove(), 15000);
                }
                setInterval(createHeart, 1000);
            </script>
        </body>
        </html>
