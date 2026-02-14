<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Special Valentine</title>

<style>
body{
    margin:0;
    font-family: 'Poppins', sans-serif;
    text-align:center;
    background: linear-gradient(135deg,#ff9ec4,#ffcce6);
    overflow:hidden;
}

/* Common */
.screen{
    display:none;
    padding-top:120px;
}

button{
    padding:15px 30px;
    font-size:22px;
    border:none;
    border-radius:30px;
    cursor:pointer;
    margin:20px;
    transition:.3s;
}

/* Intro */
#intro{
    display:block;
    color:white;
}

input{
    padding:12px;
    font-size:18px;
    border-radius:20px;
    border:none;
    text-align:center;
}

/* Question */
#no{
    position:absolute;
    background:gray;
    color:white;
}

#yes{
    background:#ff4d88;
    color:white;
}

/* Final */
#final{
    color:white;
}

.heart{
    position:absolute;
    animation: float 5s linear infinite;
}

@keyframes float{
    0%{transform:translateY(100vh);opacity:1;}
    100%{transform:translateY(-10vh);opacity:0;}
}
</style>
</head>

<body>

<!-- Screen 1 -->
<div id="intro" class="screen">
    <h1>Welcome 💌</h1>
    <p>Enter your name first...</p>
    <input type="text" id="name" placeholder="Your Name">
    <br>
    <button onclick="start()">Continue 💖</button>
</div>

<!-- Screen 2 Loading -->
<div id="loading" class="screen">
    <h1>Checking Compatibility... 💞</h1>
    <h2 id="percent">0%</h2>
</div>

<!-- Screen 3 Question -->
<div id="question" class="screen">
    <h1 id="questionText"></h1>
    <button id="yes">Yes 💘</button>
    <button id="no">No 😜</button>
</div>

<!-- Screen 4 Final -->
<div id="final" class="screen">
    <h1 id="finalText"></h1>
    <img src="https://media.giphy.com/media/l0MYt5jPR6QX5pnqM/giphy.gif" width="250">
</div>

<script>

let nameInput = document.getElementById("name");

function start(){
    if(nameInput.value == ""){
        alert("Please enter your name 😏");
        return;
    }

    document.getElementById("intro").style.display="none";
    document.getElementById("loading").style.display="block";

    let percent = 0;
    let interval = setInterval(()=>{
        percent++;
        document.getElementById("percent").innerText = percent + "%";

        if(percent >= 100){
            clearInterval(interval);
            showQuestion();
        }
    },30);
}

function showQuestion(){
    document.getElementById("loading").style.display="none";
    document.getElementById("question").style.display="block";

    document.getElementById("questionText").innerText =
    nameInput.value + ", Will you be my Valentine? 💖";
}

let noBtn = document.getElementById("no");
let yesBtn = document.getElementById("yes");
let size = 22;

noBtn.addEventListener("mouseover", function(){
    let x = Math.random()*(window.innerWidth-100);
    let y = Math.random()*(window.innerHeight-50);
    noBtn.style.left = x+"px";
    noBtn.style.top = y+"px";

    size += 5;
    yesBtn.style.fontSize = size+"px";
});

yesBtn.addEventListener("click", function(){
    document.getElementById("question").style.display="none";
    document.getElementById("final").style.display="block";

    document.getElementById("finalText").innerText =
    "Yea! Good choice " + nameInput.value + " 😍💞";

    launchHearts();
});

function launchHearts(){
    for(let i=0;i<40;i++){
        let heart=document.createElement("div");
        heart.classList.add("heart");
        heart.innerHTML="💖";
        heart.style.left=Math.random()*100+"vw";
        heart.style.fontSize=(20+Math.random()*30)+"px";
        document.body.appendChild(heart);
        setTimeout(()=>heart.remove(),5000);
    }
}

</script>

</body>
</html>
