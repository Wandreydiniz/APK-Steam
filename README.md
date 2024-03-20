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
            flex: 0 0 auto; 
            background-color: #ffffff;
            border-radius: 5px;
            padding: 20px;
            margin-right: 10px; 
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            cursor: pointer; 
            display: flex;
            align-items: center;
            justify-content: space-between; /* Adicionando espaço entre os elementos */
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
            margin-bottom: 5px; /* Adicionando margem inferior entre o nome do aplicativo e a quantidade de downloads */
        }
        .app-downloads {
            color: #555555;
            margin-bottom: 5px; /* Adicionando margem inferior entre a quantidade de downloads e o botão de download */
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
        .download-progress-container {
            width: 100%;
            height: 10px;
            background-color: #ddd;
            margin-top: 10px;
        }
        .download-progress-bar {
            height: 100%;
            background-color: #4CAF50;
            width: 0;
            transition: width 0.5s ease;
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
            <iframe class="trailer-video" id="trailer-video" width="560" height="315" src="" frameborder="0" allowfullscreen></iframe>
        </div>
        <div class="download-progress-container">
            <div class="download-progress-bar" id="download-progress-bar"></div>
        </div>
    </div>
</div>

<script>
    // Seu código JavaScript aqui

    // Dados de exemplo (pode ser substituído por uma fonte de dados real)
    const aplicativos = [
        { 
            name: "WhatsApp",
            description: "Descrição do WhatsApp GB.",
            downloads: "1B+",
            company: "Facebook",
            downloadLink: "https://d.apkpure.net/b/APK/com.whatsapp?version=latest",
            iconLink: "https://play-lh.googleusercontent.com/jSok_1-X-LMKajCRR8lcnM951R898YWrmDat-Qrk94slj2dTJDee5LhYzaEZjGH6je8",
            videoLink: "https://youtu.be/Fwk7bPOUHM4?si=f6McD_I7GBLmxZLM"
        },
        // Outros aplicativos
    ];

    const jogos = [
        { 
            name: "Free fire",
            description: "Free Fire é um jogo de tiro e sobrevivência mundialmente famoso disponível no celular.",
            downloads: "100M+",
            company: "Garena",
            downloadLink: "https://d.apkpure.net/b/XAPK/com.dts.freefireth?version=latest",
            iconLink: "https://i.scdn.co/image/ab67616d0000b273c72fc87f92c0e770bcc25ce7",
            videoLink: "https://tm.ibxk.com.br/2023/11/07/07164428263318.jpg"
        },
    { 
        name: "Survival Legends",
        description: "'Survival Legends' is an intense multiplayer game that pits two teams of three players against each other in a fight for survival in a post-apocalyptic world overrun by zombies. During the day, players must venture out into the dangerous and zombie-infested wastelands in search of food, weapons, and other supplies needed to stay alive.",
        downloads: "12K",
        company: "FreakGames",
        downloadLink: "https://d.apkpure.net/b/APK/com.FreakGames.ZombieLegends?version=latest",
        iconLink: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRsb-IVzgxj24-qBL3Q9hTARFHGCKQ3JzEvJs4dOmned0MYDzlgaiFRbyTtCLfmPM31o9w&usqp=CAU",
        videoLink: "https://firebasestorage.googleapis.com/v0/b/uninexus-game-store.appspot.com/o/Survival%20Legends(360P).mp4?alt=media&token=6a301166-fe7f-4222-ba21-9b0935ad240a"
    },

    { 
        name: "Minecraft Original",
        description: "'Survival Legends' is an intense multiplayer game that pits two teams of three players against each other in a fight for survival in a post-apocalyptic world overrun by zombies. During the day, players must venture out into the dangerous and zombie-infested wastelands in search of food, weapons, and other supplies needed to stay alive.",
        downloads: "12K",
        company: "Mojang",
        downloadLink: "https://d.apkpure.net/b/APK/com.minecraftpe.minecraft.original.free?version=latest",
        iconLink: "https://image.winudf.com/v2/user/admin/YWRtaW5fQmVGdW5reS1jb2xsYWdlLmpwZ18xNjY1OTc2NjY4NDAz/icon.webp?w=106&fakeurl=1&type=.webp",
        videoLink: ""
    }
        // Outros jogos
    ];

    const Recomendados = [
        { 
            name: "MEGA FILME - Filmes Online",
            description: "Licença Grátis Versão1.0",
            downloads: "6K",
            company: "Torang App",
            downloadLink: "https://d.apkpure.net/b/APK/me.filmeshd.mega?version=latest",
            iconLink: "https://images.sftcdn.net/images/t_app-icon-m/p/d08bcdb5-134d-4cbe-afb6-66eafe78141c/3543653762/mega-filme-filmes-online-logo",
            videoLink: ""
        },
        // Outros recomendados
    ];

    const filmes = [
        { 
            name: "Cine Filmes",
            description: "Cine Filmes",
            downloads: "10M+",
            company: "Cine Filmes",
            downloadLink: "https://d.apkpure.net/b/APK/com.filme.cine?version=latest",
            iconLink: "https://image.winudf.com/v2/image/Y29tLmZpbG1lLmNpbmVfaWNvbl8xNTM0OTgyNzk1XzA2Mg/icon.webp?w=140&fakeurl=1&type=.webp",
            videoLink: ""
        },
      { 
            name: "Cine Flix Play V2 ",
            description: "Cine Filmes",
            downloads: "10M+",
            company: "Cine Filmes",
            downloadLink: "https://d.apkpure.net/b/APK/com.cineflixplayv2?version=latest",
            iconLink: "https://image.winudf.com/v2/image1/Y29tLmNpbmVmbGl4cGxheXYyX2ljb25fMTY1MjU3NzYyNF8wMjk/icon.webp?w=140&fakeurl=1&type=.webp",
            videoLink: "https://image.winudf.com/v2/image1/Y29tLmNpbmVmbGl4cGxheXYyX3NjcmVlbl8wXzE2NTI1Nzc2MjRfMDA3/screen-0.webp?h=200&fakeurl=1&type=.webp"
        },
        
    ];

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
                    <div class="app-downloads">${item.downloads}</div>
                    <button class="app-button" onclick="downloadApp('${item.downloadLink}')">Download</button>
                </div>
            `;
            appElement.addEventListener("click", function() {
                openFullscreen(item);
            });
            container.appendChild(appElement);
        });
    }

    // Função para abrir o modo de tela cheia
    function openFullscreen(item) {
        const fullscreenOverlay = document.getElementById("fullscreen-overlay");
        const fullscreenContent = document.getElementById("fullscreen-content");
        const fullscreenTitle = document.getElementById("fullscreen-title");
        const fullscreenDescription = document.getElementById("fullscreen-description");
        const fullscreenDownloads = document.getElementById("fullscreen-downloads");
        const fullscreenCompany = document.getElementById("fullscreen-company");
        const fullscreenIcon = document.getElementById("fullscreen-icon");
        const trailerVideo = document.getElementById("trailer-video");

        fullscreenTitle.textContent = item.name;
        fullscreenDescription.textContent = item.description;
        fullscreenDownloads.textContent = item.downloads;
        fullscreenCompany.textContent = item.company;
        fullscreenIcon.src = item.iconLink;

        // Armazena o URL de download do aplicativo
        fullscreenContent.dataset.downloadLink = item.downloadLink;

        if (item.videoLink) {
            trailerVideo.src = item.videoLink;
            document.getElementById("trailer-container").style.display = "block";
        } else {
            trailerVideo.src = "";
            document.getElementById("trailer-container").style.display = "none";
        }

        fullscreenOverlay.style.display = "flex";
    }

    // Função para fechar o modo de tela cheia
    function closeFullscreen() {
        const fullscreenOverlay = document.getElementById("fullscreen-overlay");
        document.getElementById("trailer-video").src = ""; // Parar o vídeo quando o modo de tela cheia é fechado
        fullscreenOverlay.style.display = "none";
    }

// Função para simular o download do aplicativo ou jogo
function downloadApp(downloadLink) {
    const progressBar = document.getElementById("download-progress-bar");

    // Inicia a simulação do download
    let progress = 0;
    const interval = setInterval(() => {
        progress += Math.random() * 10;
        if (progress >= 100) {
            clearInterval(interval);
            progressBar.style.width = "100%";
            setTimeout(() => {
                // Simula o redirecionamento para o link de download real
                window.open(downloadLink, "_self");
            }, 500);
        } else {
            progressBar.style.width = `${progress}%`;
            document.getElementById("fullscreen-downloads").textContent = `${Math.round(progress)}%`; // Atualiza o texto de porcentagem
        }
    }, 500);
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

    criarCategoria("Recomendados", "Recomendados", Recomendados);
    // Renderizar as categorias iniciais
    criarCategoria("aplicativos", "Aplicativos", aplicativos);
    criarCategoria("jogos", "Jogos", jogos);
    criarCategoria("filmes", "Filmes", filmes);
 
    
    // Adicionar evento de pesquisa à barra de pesquisa
    document.querySelector(".search-input").addEventListener("input", pesquisar);
</script>

</body>
</html>

