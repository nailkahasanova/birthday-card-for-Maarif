<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Открытка</title>
<style>
body {
margin: 0;
font-family: Arial, sans-serif;
background: linear-gradient(135deg,#ffdde1,#ee9ca7);
overflow: hidden;
text-align: center;
}

/* ссылка */
#startBtn {
margin-top: 20%;
padding: 15px 25px;
font-size: 18px;
border: none;
border-radius: 20px;
cursor: pointer;
background: white;
}

/* конверт */
#envelope {
display: none;
margin-top: 15%;
font-size: 80px;
cursor: pointer;
animation: pop 0.6s ease;
}

@keyframes pop {
from { transform: scale(0); }
to { transform: scale(1); }
}

/* окно текста */
#card {
display: none;
background: white;
padding: 20px;
width: 80%;
margin: auto;
border-radius: 20px;
margin-top: 10%;
}

/* торт */
#cake {
font-size: 80px;
margin-top: 20px;
display: none;
}

.candle {
font-size: 40px;
}

/* кнопка микрофона */
#micBtn {
margin-top: 15px;
padding: 10px;
border-radius: 10px;
border: none;
cursor: pointer;
}
</style>
</head>
<body>

<button id="startBtn">🔗 Açmaq üçün kliklə</button>

<div id="envelope">💌</div>

<div id="card">
<h3>Ad günün mübarək, əziz Maarif! 🎉🎂</h3>
<p>
Sənə can sağlığı, xoşbəxtlik, uğur və bütün arzularının həyata keçməsini arzulayıram. Həyatın həmişə sevinc, gülüş və gözəl insanlarla dolu olsun.
</p>

<p>
Həm də sənə bir dost kimi təşəkkür etmək istəyirəm. Hər zaman yanımda olduğun, çətin anlarda mənə dəstək verdiyin, köməyini və diqqətini əsirgəmədiyin üçün çox sağ ol.
</p>

<p>
Ümid edirəm ki, dostluğumuz uzun illər davam edəcək və birlikdə daha çox gözəl xatirələr yaşayacağıq.
</p>

<p>Bir daha ad günün mübarək! 🤍</p>

<div id="cake">
🎂<br>
<span class="candle">🕯️🕯️🕯️</span>
</div>

<button id="micBtn">🎤 Şamları üfür</button>
</div>

<!-- музыка -->
<audio id="music" loop>
<!-- Buraya Count on me və ya başqa musiqi linki qoy -->
<source src="" type="audio/mpeg">
</audio>

<script>
const startBtn = document.getElementById("startBtn");
const envelope = document.getElementById("envelope");
const card = document.getElementById("card");
const cake = document.getElementById("cake");
const micBtn = document.getElementById("micBtn");
const music = document.getElementById("music");

startBtn.onclick = () => {
startBtn.style.display = "none";
envelope.style.display = "block";
};

envelope.onclick = () => {
envelope.style.display = "none";
card.style.display = "block";
cake.style.display = "block";
music.play();
};

/* микрофон эффект (обнаружение громкого звука) */
micBtn.onclick = async () => {
const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
const audioCtx = new AudioContext();
const mic = audioCtx.createMediaStreamSource(stream);
const analyser = audioCtx.createAnalyser();
mic.connect(analyser);

const data = new Uint8Array(analyser.fftSize);

function checkSound() {
analyser.getByteTimeDomainData(data);
let volume = data.reduce((a,b)=>a+b)/data.length;

if (volume > 130) {
document.querySelector(".candle").innerText = " ";
alert("🎉 Şamlar söndü! Ad günün mübarək!");
} else {
requestAnimationFrame(checkSound);
}
}

checkSound();
};
</script>

</body>
</html>
