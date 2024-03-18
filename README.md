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
    <div class="apps-container" id="apps-container">
        <!-- Aplicativos serão adicionados aqui dinamicamente -->
    </div>
</div>

<div class="category">
    <div class="category-title">Jogos</div>
    <div class="apps-container" id="games-container">
        <!-- Jogos serão adicionados aqui dinamicamente -->
    </div>
</div>

<script>
    // Dados de exemplo (pode ser substituído por uma fonte de dados real)
    const aplicativos = [
        { name: "WhatsApp GB", description: "Description of WhatsApp GB." },
        { name: "WhatsApp", description: "Description of WhatsApp." }
    ];

    const jogos = [
        { name: "SpeedDr", description: "Description of SpeedDr." },
        { name: "Extrem Survival", description: "Description of Extrem Survival." }
    ];

    // Função para renderizar aplicativos na categoria de aplicativos
    function renderizarAplicativos(aplicativos) {
        const container = document.getElementById("apps-container");
        container.innerHTML = "";
        aplicativos.forEach(app => {
            const appElement = document.createElement("div");
            appElement.classList.add("app");
            appElement.innerHTML = `
                <img src="https://via.placeholder.com/150" alt="${app.name} Icon">
                <div class="app-title">${app.name}</div>
                <div class="app-description">${app.description}</div>
                <button class="app-button">Install</button>
            `;
            container.appendChild(appElement);
        });
    }

    // Função para renderizar jogos na categoria de jogos
    function renderizarJogos(jogos) {
        const container = document.getElementById("games-container");
        container.innerHTML = "";
        jogos.forEach(jogo => {
            const jogoElement = document.createElement("div");
            jogoElement.classList.add("app");
            jogoElement.innerHTML = `
                <img src="https://via.placeholder.com/150" alt="${jogo.name} Icon">
                <div class="app-title">${jogo.name}</div>
                <div class="app-description">${jogo.description}</div>
                <button class="app-button">Install</button>
            `;
            container.appendChild(jogoElement);
        });
    }

    // Função para filtrar aplicativos e jogos com base na pesquisa
    function pesquisar() {
        const searchTerm = document.querySelector(".search-input").value.toLowerCase();
        const aplicativosFiltrados = aplicativos.filter(app => app.name.toLowerCase().includes(searchTerm));
        const jogosFiltrados = jogos.filter(jogo => jogo.name.toLowerCase().includes(searchTerm));
        renderizarAplicativos(aplicativosFiltrados);
        renderizarJogos(jogosFiltrados);
    }

    // Renderizar os aplicativos e jogos iniciais
    renderizarAplicativos(aplicativos);
    renderizarJogos(jogos);

    // Adicionar evento de pesquisa à barra de pesquisa
    document.querySelector(".search-input").addEventListener("input", pesquisar);
</script>

</body>
</html>
