<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<title>Geburtstags Abenteuer 🎉</title>

<style>

body{
font-family:Arial;
background:linear-gradient(120deg,#667eea,#764ba2);
margin:0;
text-align:center;
color:white;
}

.container{
max-width:800px;
margin:auto;
padding:40px;
}

.card{
background:white;
color:#333;
padding:30px;
border-radius:18px;
box-shadow:0 15px 40px rgba(0,0,0,0.2);
margin-top:20px;
}

button{
background:#667eea;
border:none;
color:white;
padding:12px 22px;
border-radius:10px;
font-size:16px;
cursor:pointer;
margin:10px;
}

input{
padding:10px;
width:80%;
margin:8px;
border-radius:8px;
border:1px solid #ddd;
}

table{
width:100%;
margin-top:20px;
border-collapse:collapse;
}

td,th{
padding:10px;
border-bottom:1px solid #ddd;
}

.step{
display:none;
}

.active{
display:block;
}

</style>

</head>

<body>

<div class="container">

<h1>🎂 Geburtstags Abenteuer</h1>

<div class="card step active" id="step1">

<h2>Mission Start</h2>

<p>
Zum Geburtstag schenken wir euch einen gemeinsamen Ausflug.
</p>

<button onclick="nextStep()">Mission starten</button>

</div>


<div class="card step" id="step2">

<h2>🌄 Ausflüge entdecken</h2>

<p>Ideen findet ihr hier:</p>

<a href="https://suissepartout.ch/de/" target="_blank">
<button>Ausflugsideen ansehen</button>
</a>

<br>

<button onclick="nextStep()">Weiter</button>

</div>


<div class="card step" id="step3">

<h2>🏆 Eure Top 3</h2>

<input id="name" placeholder="Name"><br>

<input id="p1" placeholder="🥇 Platz 1"><br>
<input id="p2" placeholder="🥈 Platz 2"><br>
<input id="p3" placeholder="🥉 Platz 3"><br>

<button onclick="saveVote()">Stimme speichern</button>

</div>


<div class="card step" id="step4">

<h2>📊 Aktuelles Ranking</h2>

<table id="ranking"></table>

<button onclick="nextStep()">Weiter</button>

</div>


<div class="card step" id="step5">

<h2>📅 Termin wählen</h2>

<a href="https://doodle.com">
<button>Termin abstimmen</button>
</a>

<br>

<button onclick="nextStep()">Weiter</button>

</div>


<div class="card step" id="step6">

<h2>📱 Mission abschließen</h2>

<button onclick="sendWhatsApp()">WhatsApp Nachricht senden</button>

<p>Mission abgeschlossen 🎉</p>

</div>

</div>


<script>

let step=1

function nextStep(){

document.getElementById("step"+step).classList.remove("active")

step++

document.getElementById("step"+step).classList.add("active")

}


function saveVote(){

let name=document.getElementById("name").value
let p1=document.getElementById("p1").value
let p2=document.getElementById("p2").value
let p3=document.getElementById("p3").value

let votes=JSON.parse(localStorage.getItem("votes")||"[]")

votes.push({name,p1,p2,p3})

localStorage.setItem("votes",JSON.stringify(votes))

calculateRanking()

nextStep()

}


function calculateRanking(){

let votes=JSON.parse(localStorage.getItem("votes")||"[]")

let points={}

votes.forEach(v=>{

points[v.p1]=(points[v.p1]||0)+3
points[v.p2]=(points[v.p2]||0)+2
points[v.p3]=(points[v.p3]||0)+1

})

let ranking=Object.entries(points).sort((a,b)=>b[1]-a[1])

let table="<tr><th>Ausflug</th><th>Punkte</th></tr>"

ranking.forEach(r=>{

table+="<tr><td>"+r[0]+"</td><td>"+r[1]+"</td></tr>"

})

document.getElementById("ranking").innerHTML=table

}


function sendWhatsApp(){

let text=
"🎉 Geburtstags-Ausflug Abstimmung abgeschlossen!%0A"+
"Ranking ansehen:"

window.open("https://wa.me/?text="+text)

}

</script>

</body>
</html>
