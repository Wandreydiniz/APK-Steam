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
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }
    #video-background {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: -1;
    }
    #btn-container {
        margin-top: 20px;
        text-align: center; /* Centraliza o botão na horizontal */
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

<iframe id="video-background" src="https://www.youtube.com/embed/aq8uOeYE2Xk?autoplay=1&loop=1&controls=0&mute=1&playlist=aq8uOeYE2Xk&modestbranding=1&showinfo=0&autohide=1&disablekb=1" frameborder="0" allowfullscreen></iframe>

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
