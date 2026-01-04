<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<title>Sürpriz</title>
<style>
    body {
        margin: 0;
        overflow: hidden;
        background: black;
        font-family: Arial, sans-serif;
    }

    canvas {
        position: absolute;
        top: 0;
        left: 0;
    }

    .kalp {
        position: absolute;
        color: pink;
        font-size: 24px;
        animation: yukari 6s linear forwards;
    }

    @keyframes yukari {
        from {
            transform: translateY(0);
            opacity: 1;
        }
        to {
            transform: translateY(-800px);
            opacity: 0;
        }
    }

    #yazi {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        color: #ff4d6d;
        font-size: 48px;
        display: none;
        text-align: center;
        animation: ortaya 2s ease-in-out forwards;
    }

    @keyframes ortaya {
        from {
            opacity: 0;
            transform: translate(-50%, -60%) scale(0.5);
        }
        to {
            opacity: 1;
            transform: translate(-50%, -50%) scale(1);
        }
    }
</style>
</head>
<body>

<canvas id="canvas"></canvas>
<div id="yazi">Seni çok seviyorum ❤️</div>

<script>
/* Havai fişek (basit) */
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let patlamalar = [];

function patlama() {
    const x = Math.random() * canvas.width;
    const y = Math.random() * canvas.height / 2;
    for (let i = 0; i < 50; i++) {
        patlamalar.push({
            x, y,
            dx: (Math.random() - 0.5) * 6,
            dy: (Math.random() - 0.5) * 6,
            life: 60
        });
    }
}

function animasyon() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    patlamalar.forEach((p, i) => {
        ctx.fillStyle = "yellow";
        ctx.fillRect(p.x, p.y, 3, 3);
        p.x += p.dx;
        p.y += p.dy;
        p.life--;
        if (p.life <= 0) patlamalar.splice(i, 1);
    });
    requestAnimationFrame(animasyon);
}

animasyon();
setInterval(patlama, 800);

/* Kalpler */
function kalpUcur() {
    const kalp = document.createElement("div");
    kalp.className = "kalp";
    kalp.innerHTML = "💖";
    kalp.style.left = Math.random() * window.innerWidth + "px";
    kalp.style.bottom = "0px";
    document.body.appendChild(kalp);

    setTimeout(() => kalp.remove(), 6000);
}

setTimeout(() => {
    setInterval(kalpUcur, 300);
}, 3000);

/* Yazı */
setTimeout(() => {
    document.getElementById("yazi").style.display = "block";
}, 5000);
</script>

</body>
</html>
