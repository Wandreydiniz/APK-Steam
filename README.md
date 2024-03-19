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
            display: flex;
            align-items: center;
        }
        .app img {
            max-width: 100px;
            max-height: 100px;
            width: auto;
            height: auto;
            margin-right: 20px;
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
        .details-container {
            margin-top: 20px;
            text-align: left;
        }
        .details-label {
            font-weight: bold;
        }
        .trailer-container {
            margin-top: 20px;
            text-align: center;
        }
        .trailer-video {
            width: 100%;
            height: 315px;
        }
    </style>
</head>
<body>

<div class="search-bar">
    <input type="text" class="search-input" placeholder="Search for apps/games...">
</div>

<div class="category" id="aplicativos">
    <!-- Categoria de Aplicativos -->
</div>

<div class="category" id="jogos">
    <!-- Categoria de Jogos -->
</div>

<div class="category" id="filmes">
    <!-- Categoria de Aplicativos de Filmes -->
</div>

<div class="category" id="Recomendados">
    <!-- Categoria de Aplicativos de Recomendados -->
</div>
<div class="fullscreen-overlay" id="fullscreen-overlay">
    <div class="fullscreen-content" id="fullscreen-content">
        <button class="close-button" onclick="closeFullscreen()">X</button>
        <button class="back-button" onclick="closeFullscreen()">Back</button>
        <h2 id="fullscreen-title"></h2>
        <div class="app">
            <img src="" alt="App Icon" id="fullscreen-icon">
            <div>
                <p id="fullscreen-description"></p>
                <div class="details-container">
                    <span class="details-label">Downloads:</span> <span id="fullscreen-downloads"></span><br>
                    <span class="details-label">Company:</span> <span id="fullscreen-company"></span>
                </div>
            </div>
        </div>
        <button class="app-button" onclick="downloadApp()">Install</button>
        <div class="trailer-container" id="trailer-container">
            <!-- Vídeo do YouTube será adicionado aqui dinamicamente -->
        </div>
    </div>
</div>

<script>
    // Dados de exemplo (pode ser substituído por uma fonte de dados real)
    const aplicativos = [
        { name: "WhatsApp GB", description: "Descrição do WhatsApp GB.", downloads: "1B+", company: "Facebook", downloadLink: "", iconLink: "https://play-lh.googleusercontent.com/jSok_1-X-LMKajCRR8lcnM951R898YWrmDat-Qrk94slj2dTJDee5LhYzaEZjGH6je8" },
        
        { name: "WhatsApp", description: "Descrição do WhatsApp.", downloads: "5B+", company: "Facebook", downloadLink: "https://download2279.mediafire.com/aq3fjydpq5vgp2atm90tvzSKvkWvU-j6FAQn_Gdjgpkdu3EURY7fXYE0dzBaQrH9tuFHpoj-JVY-3PNXL1XGQ_ybApEleRJQhaYY65NIPV9InBwUSyZWfNX3WEEKoo1mMhT5wcIRspWKY7dSNxORYXDafcg_ojTolJX8NPyaCHjO1oWg/5a4ti64j56ucdu3/base.apk", iconLink: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTBoumtAmE3rz6Sb5u2yAIqHaZMQuj2lBJiLqdPvG5NhA&s" }
    ];

    const jogos = [
        { name: "Free fire", description: "Free Fire é um jogo de tiro e sobrevivência mundialmente famoso disponível no celular. Cada partida dura cerca de 10 minutos e te coloca em uma ilha para enfrentar 49 jogadores na luta pela sobrevivência. Os jogadores chegam ao mapa de avião e podem escolher quando saltar de paraquedas.", downloads: "100M+", company: "SpeedDev", downloadLink: "#", iconLink: "https://t.ctcdn.com.br/ywCdsUfbWpqLdzYMQo1gtLLhCbk=/48x27:931x524/768x432/smart/i371015.jpeg" },
        { name: "SpeedDr", description: "Descrição do SpeedDr.", downloads: "100M+", company: "SpeedDev", downloadLink: "#", iconLink: "https://via.placeholder.com/150" },
        { name: "Extrem Survival", description: "Descrição do Extrem Survival.", downloads: "50M+", company: "Extreme Games", downloadLink: "https://gbwhatsapp.downgamespc.com/br/download/gb-whatsapp-pro/latest/", iconLink: "https://via.placeholder.com/150" }
    ];

const Recomendados = [
    { name: "MEGA FILME - Filmes Online", description: "Licença Grátis Versão1.0", downloads: "6K", company: "Torang App", downloadLink: "#", iconLink: "https://images.sftcdn.net/images/t_app-icon-m/p/d08bcdb5-134d-4cbe-afb6-66eafe78141c/3543653762/mega-filme-filmes-online-logo" },
    { name: "Filme 1", description: "Descrição do Filme 1.", downloads: "10M+", company: "Empresa A", downloadLink: "#", iconLink: "https://via.placeholder.com/150" },
    { name: "Filme 2", description: "Descrição do Filme 2.", downloads: "5M+", company: "Empresa B", downloadLink: "#", iconLink: "https://via.placeholder.com/150" }
];


const filmes = [ //filmes
    { name: "Cine Filmes", description: "Cine Filmes", downloads: "10M+", company: "Cine Filmes", downloadLink: "#", iconLink: "https://yt3.googleusercontent.com/ytc/AIdro_lf1IEeEbw-xnJZXcRa6XGFKHIpkZBRlK24nBFH=s900-c-k-c0x00ffffff-no-rj" },
    { name: "MEGA FILME - Filmes Online", description: "Licença Grátis Versão1.0", downloads: "6K", company: "Torang App", downloadLink: "#", iconLink: "https://images.sftcdn.net/images/t_app-icon-m/p/d08bcdb5-134d-4cbe-afb6-66eafe78141c/3543653762/mega-filme-filmes-online-logo" }
]

function criarCategoriaRecomendados() {
    const container = document.createElement("div");
    container.classList.add("category");
    container.id = "Recomendados";
    
    const titleElement = document.createElement("div");
    titleElement.classList.add("category-title");
    titleElement.textContent = "Recomendados";
    container.appendChild(titleElement);

    const appsContainer = document.createElement("div");
    appsContainer.classList.add("apps-container");
    container.appendChild(appsContainer);

    document.body.appendChild(container);

    renderizarApps(Recomendados, appsContainer);
}

function criarCategoriaFilmes() {
    const container = document.createElement("div");
    container.classList.add("category");
    container.id = "filmes";
    
    const titleElement = document.createElement("div");
    titleElement.classList.add("category-title");
    titleElement.textContent = "Filmes";
    container.appendChild(titleElement);

    const appsContainer = document.createElement("div");
    appsContainer.classList.add("apps-container");
    container.appendChild(appsContainer);

    document.body.appendChild(container);

    renderizarApps(filmes, appsContainer);
}


    // Função para criar e renderizar uma categoria
    function criarCategoria(id, title, data) {
        const container = document.createElement("div");
        container.classList.add("category");
        container.id = id;
        
        const titleElement = document.createElement("div");
        titleElement.classList.add("category-title");
        titleElement.textContent = title;
        container.appendChild(titleElement);

        const appsContainer = document.createElement("div");
        appsContainer.classList.add("apps-container");
        container.appendChild(appsContainer);

        document.body.appendChild(container);

        renderizarApps(data, appsContainer);
    }

    // Função para renderizar aplicativos ou jogos em uma categoria
    function renderizarApps(data, container) {
        container.innerHTML = "";
        data.forEach(item => {
            const appElement = document.createElement("div");
            appElement.classList.add("app");
            appElement.innerHTML = `
                <img src="${item.iconLink}" alt="${item.name} Icon">
                <div>
                    <div class="app-title">${item.name}</div>
                    <div class="app-description">${item.description}</div>
                </div>
                <a href="${item.downloadLink}" class="app-button">Download</a>
            `;
            appElement.addEventListener("click", function() {
                openFullscreen(item);
            });
            container.appendChild(appElement);
        });
    }

    // Função para abrir o modo de tela cheia com detalhes do aplicativo ou jogo
    function openFullscreen(item) {
        const fullscreenOverlay = document.getElementById("fullscreen-overlay");
        const fullscreenContent = document.getElementById("fullscreen-content");
        const fullscreenTitle = document.getElementById("fullscreen-title");
        const fullscreenDescription = document.getElementById("fullscreen-description");
        const fullscreenDownloads = document.getElementById("fullscreen-downloads");
        const fullscreenCompany = document.getElementById("fullscreen-company");
        const fullscreenIcon = document.getElementById("fullscreen-icon");

        fullscreenTitle.textContent = item.name;
        fullscreenDescription.textContent = item.description;
        fullscreenDownloads.textContent = item.downloads;
        fullscreenCompany.textContent = item.company;
        fullscreenIcon.src = item.iconLink;

        fullscreenOverlay.style.display = "flex";
    }

    // Função pasra fechar o modo de tela cheia
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
    const filmesFiltrados = filmes.filter(filme => filme.name.toLowerCase().includes(searchTerm));
    const recomendadosFiltrados = Recomendados.filter(recomendado => recomendado.name.toLowerCase().includes(searchTerm));

    renderizarApps(aplicativosFiltrados, document.getElementById("aplicativos")); // Correção aqui
    renderizarApps(jogosFiltrados, document.getElementById("jogos")); // Correção aqui
    renderizarApps(filmesFiltrados, document.getElementById("filmes")); // Correção aqui
    renderizarApps(recomendadosFiltrados, document.getElementById("Recomendados")); // Correção aqui
}

    //============================================RENDERIDADORES DE CATEGORIAS==========================================================
    // Renderizar as categorias iniciais
    criarCategoriaRecomendados()
    criarCategoria("aplicativos", "Aplicativos", aplicativos);
    criarCategoria("jogos", "Jogos", jogos);
    criarCategoriaFilmes();
    
    // Adicionar evento de pesquisa à barra de pesquisa
    document.querySelector(".search-input").addEventListener("input", pesquisar);
</script>

</body>
</html>
