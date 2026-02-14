<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Be My Valentine?</title>
<style>
    body {
        text-align: center;
        font-family: Arial, sans-serif;
        background-color: #ffe6f0;
        margin-top: 100px;
    }

    h1 {
        font-size: 40px;
        color: #ff3366;
    }

    .btn {
        padding: 15px 30px;
        font-size: 20px;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        margin: 20px;
        position: absolute;
    }

    #yes {
        background-color: #ff4d88;
        color: white;
        position: static;
    }

    #no {
        background-color: #666;
        color: white;
    }

    #result {
        margin-top: 50px;
        font-size: 28px;
        color: green;
        display: none;
    }

    img {
        width: 250px;
        margin-top: 20px;
    }
</style>
</head>
<body>

<h1>Will you be my Valentine Papi?💖</h1>

<button id="yes" class="btn">Yes</button>
<button id="no" class="btn">No</button>

<h6>No! Button is a bit say....☺️</h6>

<div id="result">
    <p>Yea! Good choice 😍</p>
    <img src="https://media.giphy.com/media/MDJ9IbxxvDUQM/giphy.gif" alt="Love GIF">
</div>

<script>
    const noBtn = document.getElementById("no");

    noBtn.addEventListener("mouseover", function() {
        const x = Math.random() * (window.innerWidth - 100);
        const y = Math.random() * (window.innerHeight - 50);
        noBtn.style.left = x + "px";
        noBtn.style.top = y + "px";
    });

    document.getElementById("yes").addEventListener("click", function() {
        document.getElementById("result").style.display = "block";
    });
</script>

</body>
</html>
