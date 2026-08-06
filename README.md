<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sardor | Contact</title>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial,Helvetica,sans-serif;
}

body{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    background:linear-gradient(-45deg,#0f172a,#111827,#1e293b,#020617);
    background-size:400% 400%;
    animation:bg 10s ease infinite;
}

@keyframes bg{
    0%{background-position:0% 50%;}
    50%{background-position:100% 50%;}
    100%{background-position:0% 50%;}
}

.card{
    width:360px;
    padding:35px;
    border-radius:25px;
    text-align:center;
    background:rgba(255,255,255,.08);
    backdrop-filter:blur(18px);
    border:1px solid rgba(255,255,255,.15);
    box-shadow:0 0 35px rgba(0,255,255,.25);
    animation:card 1s ease;
}

@keyframes card{
    from{
        opacity:0;
        transform:translateY(40px);
    }
    to{
        opacity:1;
        transform:translateY(0);
    }
}

.avatar{
    width:110px;
    height:110px;
    border-radius:50%;
    margin:auto;
    background:linear-gradient(45deg,#00e5ff,#0066ff);
    display:flex;
    align-items:center;
    justify-content:center;
    color:white;
    font-size:48px;
    box-shadow:0 0 25px cyan;
    animation:rotateGlow 4s linear infinite;
}

@keyframes rotateGlow{
    50%{
        box-shadow:0 0 40px #00e5ff;
    }
}

h2{
    color:white;
    margin-top:18px;
}

p{
    color:#cbd5e1;
    margin:8px 0 30px;
}

.btn{
    display:flex;
    align-items:center;
    justify-content:center;
    gap:12px;
    text-decoration:none;
    color:white;
    padding:15px;
    margin:15px 0;
    border-radius:15px;
    font-size:18px;
    font-weight:bold;
    transition:.35s;
}

.instagram{
    background:linear-gradient(45deg,#833AB4,#E1306C,#FCAF45);
}

.telegram{
    background:linear-gradient(45deg,#0088cc,#00c6ff);
}

.phone{
    background:linear-gradient(45deg,#16a34a,#22c55e);
}

.btn:hover{
    transform:translateY(-6px) scale(1.04);
    box-shadow:0 15px 30px rgba(0,255,255,.35);
}

.footer{
    color:#94a3b8;
    margin-top:20px;
    font-size:13px;
}
</style>

</head>

<body>

<div class="card">

<div class="avatar">
<i class="fa-solid fa-user"></i>
</div>

<h2>Sardor</h2>
<p>Connect With Me</p>

<a class="btn instagram" href="https://instagram.com/_rs207" target="_blank">
<i class="fab fa-instagram"></i>
Instagram
</a>

<a class="btn telegram" href="https://t.me/loter_uz" target="_blank">
<i class="fab fa-telegram"></i>
Telegram
</a>

<a class="btn phone" href="tel:+998773811383">
<i class="fas fa-phone"></i>
Telefon
</a>

<div class="footer">
Made with ❤️
</div>

</div>

</body>
</html>
