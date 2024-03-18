<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Play Store Simulation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f0f0;
        }
        .search-bar {
            padding: 20px;
            background-color: #ffffff;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .search-input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
            box-sizing: border-box;
        }
        .category {
            margin-bottom: 30px;
        }
        .category-title {
            font-size: 24px;
            margin-bottom: 10px;
        }
        .apps-container {
            display: flex;
            overflow-x: auto;
            padding-bottom: 10px; /* Adicionando margem inferior para a rolagem horizontal */
        }
        .app {
            flex: 0 0 auto; /* Forçando a largura automática para os aplicativos */
            background-color: #ffffff;
            border-radius: 5px;
            padding: 20px;
            margin-right: 10px; /* Adicionando margem direita entre os aplicativos */
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .app img {
            max-width: 100%;
            height: auto;
        }
        .app-title {
            font-size: 16px;
            margin: 10px 0;
        }
        .app-description {
            color: #555555;
            margin-bottom: 10px;
        }
        .app-button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 3px;
            cursor: pointer;
            font-size: 14px;
            text-transform: uppercase;
        }
    </style>
</head>
<body>

<div class="search-bar">
    <input type="text" class="search-input" placeholder="Search for apps/games...">
</div>

<div class="category">
    <div class="category-title">Aplicativos</div>
    <div class="apps-container">
        <div class="app">
            <img src="https://via.placeholder.com/150" alt="App Icon">
            <div class="app-title">Whatsapp GB</div>
            <div class="app-description">Description of App 1.</div>
            <button class="app-button">Install</button>
        </div>
        <div class="app">
            <img src="https://via.placeholder.com/150" alt="App Icon">
            <div class="app-title">Whatsapp</div>
            <div class="app-description">Description of App 2.</div>
            <button class="app-button">Install</button>
        </div>
        <!-- Adicione mais aplicativos aqui -->
    </div>
</div>

<div class="category">
    <div class="category-title">Jogos Recomendados</div>
    <div class="apps-container">
        <div class="app">
            <img src="https://via.placeholder.com/150" alt="Game Icon">
            <div class="app-title">SpeedDr</div>
            <div class="app-description">Description of Game 1.</div>
            <button class="app-button">Install</button>
        </div>
        <div class="app">
            <img src="https://via.placeholder.com/150" alt="Game Icon">
            <div class="app-title">Extrem Survival</div>
            <div class="app-description">Description of Game 2.</div>
            <button class="app-button">Install</button>
        </div>
        <div class="app">
            <img src="https://via.placeholder.com/150" alt="Game Icon">
            <div class="app-title">Free Fire</div>
            <div class="app-description">Description of Game 3.</div>
            <button class="app-button">Install</button>
        </div>
        <!-- Adicione mais jogos aqui -->
    </div>
</div>

<div class="category">
    <div class="category-title">Jogos de Sobrevivência</div>
    <div class="apps-container">
        <div class="app">
            <img src="https://via.placeholder.com/150" alt="Game Icon">
            <div class="app-title">D.O.Z survival</div>
            <div class="app-description">Description of Game 1.</div>
            <button class="app-button">Install</button>
        </div>
        <div class="app">
            <img src="https://via.placeholder.com/150" alt="Game Icon">
            <div class="app-title">Extrem Survival</div>
            <div class="app-description">Description of Game 2.</div>
            <button class="app-button">Install</button>
        </div>
        <div class="app">
            <img src="https://via.placeholder.com/150" alt="Game Icon">
            <div class="app-title">Last Day on Earth Survival</div>
            <div class="app-description">Description of Game 3.</div>
            <button class="app-button">Install</button>
        </div>
        <!-- Adicione mais jogos aqui -->
    </div>
</div>

<!-- Adicione mais categorias e aplicativos/jogos conforme necessário -->

</body>
</html>
