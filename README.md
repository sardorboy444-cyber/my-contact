```html
<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Bahora ❤️</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html, body {
    width: 100%;
    height: 100%;
    overflow: hidden;
    background: #02030a;
    font-family: Arial, sans-serif;
}

canvas {
    position: fixed;
    inset: 0;
    width: 100%;
    height: 100%;
}

.title {
    position: fixed;
    top: 8%;
    left: 50%;
    transform: translateX(-50%);
    color: rgba(255,255,255,0.85);
    font-size: 18px;
    letter-spacing: 5px;
    text-transform: uppercase;
    text-shadow: 0 0 15px #ff3b70;
    z-index: 5;
    animation: fade 3s ease-in-out infinite alternate;
}

@keyframes fade {
    from { opacity: .5; }
    to { opacity: 1; }
}
</style>
</head>

<body>

<div class="title">For Bahora ❤️</div>

<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

let W, H;
let particles = [];
let stars = [];

function resize() {
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
}

resize();
window.addEventListener("resize", resize);

// ----------------------
// YULDUZLAR
// ----------------------
for (let i = 0; i < 220; i++) {
    stars.push({
        x: Math.random(),
        y: Math.random(),
        r: Math.random() * 1.5 + 0.2,
        a: Math.random(),
        speed: Math.random() * 0.02 + 0.005
    });
}

// ----------------------
// YURAK FORMULASI
// ----------------------
function heart(t) {
    const x = 16 * Math.pow(Math.sin(t), 3);
    const y = -(13 * Math.cos(t)
        - 5 * Math.cos(2*t)
        - 2 * Math.cos(3*t)
        - Math.cos(4*t));

    return { x, y };
}

// Yurak zarrachalari
for (let i = 0; i < 1800; i++) {

    const t = Math.random() * Math.PI * 2;
    const scale = Math.sqrt(Math.random());

    const p = heart(t);

    particles.push({
        baseX: p.x * scale,
        baseY: p.y * scale,

        x: 0,
        y: 0,

        size: Math.random() * 1.8 + 0.5,
        phase: Math.random() * Math.PI * 2,
        speed: Math.random() * 0.02 + 0.005
    });
}

// ----------------------
// TASHQARIDAGI ZARRACHALAR
// ----------------------
let floating = [];

for (let i = 0; i < 500; i++) {
    floating.push({
        x: Math.random(),
        y: Math.random(),
        vx: (Math.random() - .5) * .0005,
        vy: (Math.random() - .5) * .0005,
        size: Math.random() * 2 + .3,
        alpha: Math.random()
    });
}

// ----------------------
// TEXT YARATISH
// ----------------------
const textCanvas = document.createElement("canvas");
const textCtx = textCanvas.getContext("2d");

textCanvas.width = 700;
textCanvas.height = 180;

textCtx.font = "bold 80px Arial";
textCtx.textAlign = "center";
textCtx.textBaseline = "middle";
textCtx.fillStyle = "white";
textCtx.shadowColor = "#ff3b70";
textCtx.shadowBlur = 25;

textCtx.fillText("Bahora ❤️", 350, 90);

const textData = textCtx.getImageData(
    0, 0,
    textCanvas.width,
    textCanvas.height
).data;

let textParticles = [];

for (let y = 0; y < textCanvas.height; y += 3) {
    for (let x = 0; x < textCanvas.width; x += 3) {

        const index = (y * textCanvas.width + x) * 4;

        if (textData[index + 3] > 100) {
            textParticles.push({
                x: x - 350,
                y: y - 90,
                offset: Math.random() * Math.PI * 2
            });
        }
    }
}

// ----------------------
// DRAW
// ----------------------
let time = 0;

function draw() {

    time += 0.01;

    // Fon
    const gradient = ctx.createRadialGradient(
        W/2, H/2, 50,
        W/2, H/2, Math.max(W,H)
    );

    gradient.addColorStop(0, "#16030d");
    gradient.addColorStop(.45, "#060611");
    gradient.addColorStop(1, "#010208");

    ctx.fillStyle = gradient;
    ctx.fillRect(0,0,W,H);

    // ------------------
    // YULDUZLAR
    // ------------------
    stars.forEach(s => {

        s.a += s.speed;

        const alpha =
            0.25 +
            Math.abs(Math.sin(s.a)) * 0.75;

        ctx.beginPath();
        ctx.arc(
            s.x * W,
            s.y * H,
            s.r,
            0,
            Math.PI * 2
        );

        ctx.fillStyle =
            `rgba(255,255,255,${alpha})`;

        ctx.fill();
    });

    // ------------------
    // UCHUVCHI ZARRACHALAR
    // ------------------
    floating.forEach(p => {

        p.x += p.vx;
        p.y += p.vy;

        if (p.x < 0 || p.x > 1) p.vx *= -1;
        if (p.y < 0 || p.y > 1) p.vy *= -1;

        ctx.beginPath();

        ctx.arc(
            p.x * W,
            p.y * H,
            p.size,
            0,
            Math.PI * 2
        );

        ctx.fillStyle =
            `rgba(255,70,130,${p.alpha})`;

        ctx.shadowColor = "#ff174f";
        ctx.shadowBlur = 10;

        ctx.fill();

        ctx.shadowBlur = 0;
    });

    // ------------------
    // YURAK
    // ------------------

    const scale =
        Math.min(W,H) / 38;

    const centerX = W/2;
    const centerY = H/2;

    particles.forEach(p => {

        const wave =
            Math.sin(time * 2 + p.phase) * 1.5;

        const x =
            centerX +
            p.baseX * scale +
            wave;

        const y =
            centerY +
            p.baseY * scale +
            wave;

        const glow =
            0.6 +
            Math.sin(time * 3 + p.phase) * .3;

        ctx.beginPath();

        ctx.arc(
            x,
            y,
            p.size,
            0,
            Math.PI * 2
        );

        ctx.fillStyle =
            `rgba(255,${30 + Math.random()*70},${90 + Math.random()*90},${glow})`;

        ctx.shadowColor = "#ff174f";
        ctx.shadowBlur = 12;

        ctx.fill();

        ctx.shadowBlur = 0;
    });

    // ------------------
    // BAHORA YOZUVI
    // ------------------

    const textScale =
        Math.min(W,H) / 750;

    textParticles.forEach(p => {

        const x =
            centerX +
            p.x * textScale;

        const y =
            centerY +
            p.y * textScale;

        const pulse =
            1 +
            Math.sin(time * 4 + p.offset) * .05;

        ctx.beginPath();

        ctx.arc(
            x,
            y,
            1.4 * pulse,
            0,
            Math.PI * 2
        );

        ctx.fillStyle =
            "rgba(255,255,255,.95)";

        ctx.shadowColor = "#ff4d88";
        ctx.shadowBlur = 8;

        ctx.fill();

        ctx.shadowBlur = 0;
    });

    // ------------------
    // MARKAZIY YORUG'LIK
    // ------------------

    const glow = ctx.createRadialGradient(
        centerX,
        centerY,
        0,
        centerX,
        centerY,
        scale * 15
    );

    glow.addColorStop(0, "rgba(255,30,90,.08)");
    glow.addColorStop(1, "rgba(255,30,90,0)");

    ctx.fillStyle = glow;

    ctx.fillRect(
        centerX - scale*15,
        centerY - scale*15,
        scale*30,
        scale*30
    );

    requestAnimationFrame(draw);
}

draw();
</script>

</body>
</html>
```
