[index.html](https://github.com/user-attachments/files/25726619/index.html)
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Seni Seviyorum 💖 - Multilingual Responsive</title>
<style>
body, html {
    margin: 0;
    height: 100%;
    overflow: hidden;
    background: #000;
    font-family: Arial, sans-serif;
}

/* Ortadaki büyük kalp */
.container {
    position: relative;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 2;
}
.heart {
    width: 120px;
    height: 120px;
    background: red;
    transform: rotate(-45deg);
    position: relative;
    cursor: pointer;
    z-index: 3;
}
.heart::before,
.heart::after {
    content: "";
    width: 120px;
    height: 120px;
    background: red;
    border-radius: 50%;
    position: absolute;
}
.heart::before { top: -60px; left: 0; }
.heart::after { left: 60px; top: 0; }

/* Patlayan kalpler */
.burst-heart {
    position: absolute;
    width: 20px;
    height: 20px;
    background: red;
    transform: rotate(-45deg);
    border-radius: 50%;
    pointer-events: none;
    animation: burst 0.7s forwards;
}
.burst-heart::before,
.burst-heart::after {
    content: "";
    width: 20px;
    height: 20px;
    background: red;
    border-radius: 50%;
    position: absolute;
}
.burst-heart::before { top: -10px; left: 0; }
.burst-heart::after { left: 10px; top: 0; }
@keyframes burst {
    0% { transform: scale(1) rotate(-45deg); opacity:1; }
    100% { transform: scale(3) rotate(-45deg); opacity:0; }
}

/* Küçük uçan kalpler */
.small-heart {
    width: 10px;
    height: 10px;
    background: pink;
    position: absolute;
    transform: rotate(-45deg);
    border-radius: 50%;
    pointer-events: none;
    animation: floatUp linear infinite;
}
.small-heart::before,
.small-heart::after {
    content: "";
    width: 10px;
    height: 10px;
    background: pink;
    border-radius: 50%;
    position: absolute;
}
.small-heart::before { top: -5px; left: 0; }
.small-heart::after { left: 5px; top: 0; }
@keyframes floatUp {
    0% { transform: translateY(0) scale(1) rotate(-45deg); opacity:1; }
    100% { transform: translateY(-700px) scale(0.5) rotate(-45deg); opacity:0; }
}

/* Yazılar */
.random-message {
    position: absolute;
    font-size: 16px;
    color: #ff1a75;
    pointer-events: none;
    opacity: 0.8;
    user-select: none;
}
</style>
</head>
<body>
<div class="container">
    <div class="heart" id="heart"></div>
</div>

<script>
const heart = document.getElementById('heart');
const body = document.body;

// 15 dilde “Seni Seviyorum”
const loveTexts = [
    "Seni Seviyorum 💖","I Love You 💖","Je t'aime 💖","Te quiero 💖","Ich liebe dich 💖",
    "Ti amo 💖","Eu te amo 💖","Я тебя люблю 💖","我爱你 💖","愛してる 💖",
    "사랑해 💖","أنا أحبك 💖","मैं तुमसे प्यार करता हूँ 💖","Jeg elsker dig 💖","Te iubesc 💖"
];

// Küçük kalpler sürekli
setInterval(() => {
    const sh = document.createElement('div');
    sh.className = 'small-heart';
    sh.style.left = Math.random() * window.innerWidth + 'px';
    sh.style.top = window.innerHeight + 'px';
    sh.style.background = randomColor();
    sh.style.animationDuration = (3 + Math.random()*3) + 's';
    body.appendChild(sh);
    setTimeout(() => body.removeChild(sh), 7000);
}, 120);

// Kalbin üzerine gelince patlama ve yazılar
heart.addEventListener('mouseenter', (e) => {
    for(let i=0;i<40;i++){
        createBurst(e.clientX, e.clientY);
        if(i % 4 === 0) createRandomMessage();
    }
});

// Patlayan kalp
function createBurst(x, y){
    const burst = document.createElement('div');
    burst.className = 'burst-heart';
    burst.style.left = (x - 10) + 'px';
    burst.style.top = (y - 10) + 'px';
    burst.style.background = randomColor();
    body.appendChild(burst);
    setTimeout(() => body.removeChild(burst), 700);
}

// Rastgele dilde yazı
function createRandomMessage(){
    const msg = document.createElement('div');
    msg.className = 'random-message';
    msg.innerText = loveTexts[Math.floor(Math.random() * loveTexts.length)];
    msg.style.left = Math.random() * (window.innerWidth - 100) + 'px';
    msg.style.top = Math.random() * (window.innerHeight - 40) + 'px';
    msg.style.fontSize = (14 + Math.random()*14) + 'px';
    msg.style.color = randomColor();
    body.appendChild(msg);
    setTimeout(() => body.removeChild(msg), 4000);
}

// Rastgele renk
function randomColor(){
    const colors = ['#ff99cc','#ff66b3','#ff3399','#ff1a75','#ff4d94','#ff0000','#ff4d4d','#ff80bf'];
    return colors[Math.floor(Math.random()*colors.length)];
}
</script>
</body>
</html>
