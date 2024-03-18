<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vídeo de Fundo</title>
<style>
    body {
        margin: 0;
        padding: 0;
        overflow: hidden;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    #video-background {
        position: fixed;
        top: 0;
        left: 0;
        min-width: 100%;
        min-height: 100%;
        width: auto;
        height: auto;
        z-index: -1;
    }
    #btn-container {
        margin-top: 20px;
    }
    #progress-bar {
        width: 80%;
        height: 10px;
        background-color: #f2f2f2;
        border-radius: 5px;
        overflow: hidden;
        margin-top: auto;
    }
    #progress {
        width: 0%;
        height: 100%;
        background-color: #4caf50;
        transition: width 2s ease;
    }
    button {
        padding: 10px 20px;
        font-size: 16px;
        background-color: #4caf50;
        color: white;
        border: none;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    button:hover {
        background-color: #45a049;
    }
</style>
</head>
<body>

<video id="video-background" autoplay loop muted playsinline>
    <source src="https://firebasestorage.googleapis.com/v0/b/teste-275ea.appspot.com/o/Mini%20DAYZ%20-%20Launch%20Trailer(720P_60FPS).mp4?alt=media&token=1a1eb028-70cb-4426-b2a9-69cf5cc702c0" type="video/mp4">
    Your browser does not support the video tag.
</video>

<div id="btn-container">
    <button onclick="startLoading()">Carregar</button>
</div>

<div id="progress-bar">
    <div id="progress"></div>
</div>

<script>
    function startLoading() {
        var progressBar = document.getElementById('progress');
        var width = 1;
        var interval = setInterval(function() {
            if (width >= 100) {
                clearInterval(interval);
                window.open("https://tanklesscamp658.github.io/mdzplus1.2.0/", "_blank");
            } else {
                width++;
                progressBar.style.width = width + '%';
            }
        }, 20);
    }
</script>

</body>
</html>
