<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sistema de Carregamento</title>
<style>
    body {
        background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQcBe1zZREzbdTAgkjOTfwF6tNjdfqOjxiN6ffdHN9V1FSS_bSJ62gb4sGz&s=10');
        background-size: cover;
        background-repeat: no-repeat;
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        height: 100vh;
        position: relative;
    }
    #progress-bar {
        width: 80%;
        height: 10px; /* Reduzi a altura da barra de progresso */
        background-color: rgba(255, 255, 255, 0.5); /* Defini a barra de progresso como transparente */
        border-radius: 5px;
        overflow: hidden;
        margin: auto; /* Centralizei a barra de progresso */
        position: absolute;
        bottom: 70px;
        left: 50%;
        transform: translateX(-50%);
    }
    #progress {
        width: 0%;
        height: 100%;
        background-color: #708090; /* Alterei a cor da barra de carregamento */
        transition: width 2s ease; /* Aumentei a duração da transição para 2 segundos */
    }
    #btn-container {
        text-align: center; /* Centraliza o botão */
        position: absolute;
        bottom: 20px;
        left: 0;
        right: 0;
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
    #name {
        position: absolute;
        bottom: 10px;
        left: 10px;
        color: white;
        font-size: 12px; /* Reduzi o tamanho da fonte */
    }
</style>
</head>
<body>

<div id="progress-bar">
    <div id="progress"></div>
</div>
<div id="btn-container">
    <button onclick="startLoading()">Carregar</button>
</div>
<div id="name">Criptografado;@wandrecydiniz</div>

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
        }, 20); // Reduzi o intervalo para aumentar a velocidade do carregamento
    }
</script>

</body>
</html>
