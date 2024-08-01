# Página de Vídeo YouTube em Tela Cheia

Este projeto cria uma página HTML que exibe um vídeo do YouTube em tela cheia com uma interface estilizada. O vídeo é configurado para iniciar automaticamente, ser reproduzido em loop, e ter controles visíveis.

## Funcionalidades

1. **Player em Tela Cheia:** O vídeo é exibido em tela cheia com um fundo escuro e uma sobreposição estilizada.
2. **Reprodução Automática:** O vídeo tenta iniciar automaticamente e é reproduzido em loop.
3. **Controles e Mute:** Os controles do vídeo são exibidos e o áudio é inicialmente mutado para evitar bloqueios de autoplay.
4. **Reinício do Vídeo:** O vídeo é reiniciado após 1 minuto de reprodução para garantir uma experiência contínua.

## Estrutura do Código

### HTML

- **`<head>`:** Inclui links para o CSS do Bootstrap e Font Awesome para ícones, e estilos personalizados para o layout e o player.
- **`<body>`:** Contém o contêiner do player e a sobreposição de texto.

### CSS

- **Estilo Geral:** Define a aparência da página, incluindo o layout de tela cheia e o fundo em gradiente.
- **Player Wrapper:** Define o estilo do contêiner do player com sombra e fundo escuro.
- **Overlay Text:** Configura o texto sobreposto que está oculto por padrão.

### JavaScript

- **API do YouTube:** Carrega a API do YouTube e cria um novo player para o vídeo.
- **Reprodução e Reinício:** Define o comportamento do player, incluindo a reprodução automática e o reinício do vídeo após 1 minuto.

## Código

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Assistir YouTube</title>
  <!-- Link para o CSS do Bootstrap e Font Awesome para ícones -->
  <link href="https://stackpath.bootstrapcdn.com/bootstrap/5.3.0/css/bootstrap.min.css" rel="stylesheet">
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
  <style>
    /* Estilos gerais */
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #0d1117, #1f2937);
      color: #ffffff;
      overflow: hidden;
    }
    .full-screen-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .player-wrapper {
      width: 100%;
      height: 100%;
      border-radius: 0; /* Sem bordas arredondadas para tela cheia */
      overflow: hidden; /* Esconde a parte que sai da borda */
      box-shadow: 0 8px 30px rgba(0, 0, 0, 0.8); /* Sombra para dar profundidade */
      background: rgba(0, 0, 0, 0.7); /* Fundo escuro com transparência */
      position: relative;
      transition: box-shadow 0.3s ease;
    }
    .player-wrapper:hover {
      box-shadow: 0 12px 50px rgba(0, 0, 0, 0.9); /* Sombra mais intensa ao passar o mouse */
    }
    #player {
      width: 100%;
      height: 100%;
    }
    .overlay-text {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      color: #ffffff;
      text-align: center;
      font-size: 2rem;
      font-weight: bold;
      z-index: 2;
      text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.6);
      display: none; /* Oculta o texto de sobreposição */
    }
    .footer {
      position: absolute;
      bottom: 10px;
      width: 100%;
      text-align: center;
      color: #ffffff;
      font-size: 0.9rem;
      z-index: 2;
    }
  </style>
</head>
<body>
  <div class="full-screen-container">
    <div class="player-wrapper">
      <div id="player"></div>
      <div class="overlay-text">Assistindo a Vídeo</div>
    </div>
  </div>

  <script>
    // Carrega a API do YouTube Player
    function onYouTubeIframeAPIReady() {
      new YT.Player('player', {
        height: '100%',
        width: '100%',
        videoId: 'mpkmNKRefxU', // ID do vídeo do YouTube
        playerVars: {
          'autoplay': 1, // Tenta iniciar a reprodução automaticamente
          'controls': 1, // Exibe controles do vídeo
          'mute': 1, // Muta o vídeo para evitar bloqueio de autoplay
          'playsinline': 1, // Permite reprodução em linha em dispositivos móveis
          'loop': 1, // Reproduz o vídeo em loop (opcional)
        },
        events: {
          'onReady': onPlayerReady
        }
      });
    }

    function onPlayerReady(event) {
      var player = event.target;
      player.playVideo(); // Inicia a reprodução do vídeo

      // Define um intervalo para monitorar e reiniciar o vídeo
      setInterval(function() {
        var currentTime = player.getCurrentTime();
        if (currentTime > 60) { // Assiste o vídeo por 1 minuto
          player.seekTo(0); // Reinicia o vídeo
          player.playVideo(); // Recomeça a reprodução
        }
      }, 70000); // Reexecuta a cada 1 minuto e 10 segundos
    }

    // Carrega a API do YouTube
    var tag = document.createElement('script');
    tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
  </script>

  <!-- Link para o JS do Bootstrap -->
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.6/dist/umd/popper.min.js"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/5.3.0/js/bootstrap.min.js"></script>
</body>
</html>
