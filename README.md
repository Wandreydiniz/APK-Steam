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
            cursor: pointer; /* Alteração para o cursor indicar interatividade */
        }
        .app img {
            max-width: 100%;
            max-height: 100%;
            width: auto;
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
        .app-details {
            font-size: 14px;
            color: #777777;
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
        .fullscreen-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 9999;
        }
        .fullscreen-content {
            background-color: #ffffff;
            border-radius: 5px;
            padding: 20px;
            max-width: 80%;
            max-height: 80%;
            overflow: auto;
            position: relative; /* Adicionado */
            text-align: center; /* Adicionado */
        }
        .close-button {
            position: absolute;
            top: 10px;
            right: 10px;
            background: none;
            border: none;
            font-size: 24px;
            color: #ffffff;
            cursor: pointer;
        }
        .back-button {
            position: absolute;
            top: 10px;
            left: 10px;
            background: none;
            border: none;
            font-size: 18px;
            color: #007bff;
            cursor: pointer;
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

<div class="fullscreen-overlay" id="fullscreen-overlay">
    <div class="fullscreen-content" id="fullscreen-content">
        <button class="close-button" onclick="closeFullscreen()">X</button>
        <button class="back-button" onclick="closeFullscreen()">Back</button>
        <h2 id="fullscreen-title"></h2>
        <p id="fullscreen-description"></p>
        <p id="fullscreen-details"></p>
        <button class="app-button" onclick="downloadApp()">Install</button>
    </div>
</div>

<script>
    // Dados de exemplo (pode ser substituído por uma fonte de dados real)
    const aplicativos = [
        { name: "WhatsApp GB", description: "Descrição do WhatsApp GB.", downloads: "1B+", company: "Facebook", downloadLink: "https://download1527.mediafire.com/y5d91mtemvhgi0_q5b2Ih_1POFZSceg6YWglVnfiM3e6loQNNB-r_RxArDYcDX0_JhKrKRyuSBQMePu1Jcka8Wjanlw9v-oLkEvkXylqXeSK6oc3xGtdNegcPbqQDOSfj9vrC39RYVJfv1aSYNYEqgM2k6I-GDC3NJjdA9DvrZDA51g/5a4ti64j56ucdu3/base.apk" },

        
        { name: "WhatsApp", description: "Descrição do WhatsApp.", downloads: "5B+", company: "Facebook", downloadLink: "https://download1527.mediafire.com/y5d91mtemvhgi0_q5b2Ih_1POFZSceg6YWglVnfiM3e6loQNNB-r_RxArDYcDX0_JhKrKRyuSBQMePu1Jcka8Wjanlw9v-oLkEvkXylqXeSK6oc3xGtdNegcPbqQDOSfj9vrC39RYVJfv1aSYNYEqgM2k6I-GDC3NJjdA9DvrZDA51g/5a4ti64j56ucdu3/base.apk" }
        
        { name: "WhatsApp", description: "Descrição do WhatsApp.", downloads: "5B+", company: "Facebook", downloadLink: "https://download1527.mediafire.com/y5d91mtemvhgi0_q5b2Ih_1POFZSceg6YWglVnfiM3e6loQNNB-r_RxArDYcDX0_JhKrKRyuSBQMePu1Jcka8Wjanlw9v-oLkEvkXylqXeSK6oc3xGtdNegcPbqQDOSfj9vrC39RYVJfv1aSYNYEqgM2k6I-GDC3NJjdA9DvrZDA51g/5a4ti64j56ucdu3/base.apk" }
    ];

    const jogos = [
        { name: "SpeedDr", description: "Descrição do SpeedDr.", downloads: "100M+", company: "SpeedDev", downloadLink: "#" },
        { name: "Extrem Survival", description: "Descrição do Extrem Survival.", downloads: "50M+", company: "Extreme Games", downloadLink: "https://gbwhatsapp.downgamespc.com/br/download/gb-whatsapp-pro/latest/" }
    ];

    // Função para renderizar aplicativos na categoria de aplicativos
    function renderizarAplicativos(aplicativos) {
        const container = document.getElementById("apps-container");
        container.innerHTML = "";
        aplicativos.forEach(app => {
            const appElement = document.createElement("div");
            appElement.classList.add("app");
            appElement.innerHTML = `
                <img src="https://t.ctcdn.com.br/qpEUCT2UXKOK2-JrsqjvFvbd1A4=/i618809.png" alt="${app.name} Icon" style="max-width: 100px; max-height: 100px;"> <!-- Ajustado o tamanho máximo da imagem -->
                <div class="app-title">${app.name}</div>
                <div class="app-description">${app.description}</div>
                <a href="${app.downloadLink}" class="app-button">Download</a> <!-- Adicionado o link de download -->
            `;
            appElement.addEventListener("click", function() {
                openFullscreen(app.name, app.description, app.downloads, app.company);
            });
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
                <a href="${jogo.downloadLink}" class="app-button">Download</a> <!-- Adicionado o link de download -->
            `;
            jogoElement.addEventListener("click", function() {
                openFullscreen(jogo.name, jogo.description, jogo.downloads, jogo.company);
            });
            container.appendChild(jogoElement);
        });
    }

    // Função para abrir o modo de tela cheia com detalhes do aplicativo ou jogo
    function openFullscreen(name, description, downloads, company) {
        const fullscreenOverlay = document.getElementById("fullscreen-overlay");
        const fullscreenContent = document.getElementById("fullscreen-content");
        const fullscreenTitle = document.getElementById("fullscreen-title");
        const fullscreenDescription = document.getElementById("fullscreen-description");
        const fullscreenDetails = document.getElementById("fullscreen-details");

        fullscreenTitle.textContent = name;
        fullscreenDescription.textContent = description;
        fullscreenDetails.innerHTML = `
            <p><strong>Downloads:</strong> ${downloads}</p>
            <p><strong>Company:</strong> ${company}</p>
        `;

        fullscreenOverlay.style.display = "flex";
    }

    // Função para fechar o modo de tela cheia
    function closeFullscreen() {
        const fullscreenOverlay = document.getElementById("fullscreen-overlay");
        fullscreenOverlay.style.display = "none";
    }

    // Função para simular o download do aplicativo ou jogo
    function downloadApp() {
        alert("Download initiated.");
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
