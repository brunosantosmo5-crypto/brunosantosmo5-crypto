<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bruno Santos · IA e automação</title>
    <link rel="stylesheet" href="assets/fonts.css">

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #0b0512;
            background-image: 
                radial-gradient(rgba(255, 42, 133, 0.12) 1px, transparent 1px),
                linear-gradient(rgba(18, 7, 28, 0.95), rgba(8, 3, 14, 0.98));
            background-size: 16px 16px, 100% 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            font-family: 'Rajdhani', sans-serif;
            color: #fce8f3;
            overflow: hidden;
        }

        /* --- CONTENEDOR PRINCIPAL --- */
        .banner-container {
            position: relative;
            width: 1000px;
            height: 560px;
            background: rgba(22, 9, 34, 0.94);
            border: 2px solid #ff2a85;
            overflow: hidden;
            box-shadow: 0 0 35px rgba(255, 42, 133, 0.3), 0 0 15px rgba(0, 245, 212, 0.25), inset 0 0 25px rgba(255, 42, 133, 0.15);
            backdrop-filter: blur(10px);
        }

        /* Fondo Grid Neón */
        .cyber-grid {
            position: absolute;
            width: 200%;
            height: 200%;
            top: -50%;
            left: -50%;
            background-image: 
                linear-gradient(to right, rgba(0, 245, 212, 0.06) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 42, 133, 0.06) 1px, transparent 1px);
            background-size: 32px 32px;
            animation: gridMove 20s linear infinite;
            pointer-events: none;
        }

        @keyframes gridMove {
            0% { transform: translateY(0) rotate(0deg); }
            100% { transform: translateY(32px) rotate(0deg); }
        }

        /* Destello ambiental flotante */
        .ambient-glow {
            position: absolute;
            width: 350px;
            height: 350px;
            background: radial-gradient(circle, rgba(255, 42, 133, 0.25) 0%, rgba(212, 178, 255, 0.1) 40%, transparent 70%);
            top: -50px;
            left: -50px;
            pointer-events: none;
            z-index: 1;
            animation: pulseGlow 6s ease-in-out infinite alternate;
        }

        @keyframes pulseGlow {
            0% { transform: scale(1); opacity: 0.6; }
            100% { transform: scale(1.2); opacity: 0.9; }
        }

        .scanline {
            position: absolute;
            width: 100%;
            height: 100%;
            background: linear-gradient(
                to bottom,
                rgba(255,255,255,0),
                rgba(255,255,255,0) 50%,
                rgba(0, 0, 0, 0.25) 50%,
                rgba(0, 0, 0, 0.25)
            );
            background-size: 100% 4px;
            pointer-events: none;
            z-index: 10;
            opacity: 0.5;
        }

        /* --- HEADER Y TITULARES --- */
        .header-box {
            position: absolute;
            left: 45px;
            top: 35px;
            z-index: 5;
        }

        .subtitle-cyber-id {
            font-family: 'Orbitron', sans-serif;
            font-weight: 800;
            font-size: 13px;
            letter-spacing: 4px;
            color: #00f5d4;
            text-transform: uppercase;
            text-shadow: 0 0 10px rgba(0, 245, 212, 0.8), 0 0 18px rgba(0, 245, 212, 0.4);
            margin-bottom: 2px;
        }

        .alias-script {
            font-family: 'Playfair Display', serif;
            font-style: italic;
            font-size: 15px;
            color: #d4b2ff;
            letter-spacing: 1.5px;
            margin-bottom: 4px;
            text-shadow: 0 0 8px rgba(212, 178, 255, 0.5);
        }

        .main-title {
            font-family: 'Oxanium', sans-serif;
            font-weight: 800;
            font-size: 72px;
            letter-spacing: 6px;
            line-height: 0.9;
            color: #ffffff;
            text-transform: uppercase;
            position: relative;
            text-shadow: 
                3px 3px 0px #ff2a85,
                -2px -2px 0px #00f5d4,
                0 0 20px rgba(255, 42, 133, 0.5);
            animation: floatText 4s ease-in-out infinite alternate;
        }

        @keyframes floatText {
            0% { transform: translateY(0px); }
            100% { transform: translateY(-4px); }
        }

        /* --- DETALLES DE CORAZÓN Y ETIQUETAS HUD --- */
        .hud-status-tag {
            position: absolute;
            left: 45px;
            top: 155px;
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(255, 42, 133, 0.12);
            border: 1px solid #ff2a85;
            padding: 4px 12px;
            font-family: 'Share Tech Mono', monospace;
            font-size: 11px;
            color: #ff94c2;
            z-index: 5;
            box-shadow: 0 0 12px rgba(255, 42, 133, 0.2);
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background-color: #00f5d4;
            border-radius: 50%;
            box-shadow: 0 0 10px #00f5d4;
            animation: pulseDot 1.5s infinite alternate;
        }

        @keyframes pulseDot {
            0% { opacity: 0.3; scale: 0.8; }
            100% { opacity: 1; scale: 1.2; }
        }

        /* --- STATS Y CARACTERÍSTICAS (LLENADO DE ESPACIO) --- */
        .stats-hud-box {
            position: absolute;
            left: 45px;
            top: 195px;
            width: 480px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            z-index: 5;
        }

        .stat-card {
            background: rgba(30, 12, 46, 0.7);
            border: 1px solid rgba(212, 178, 255, 0.3);
            border-left: 3px solid #ff2a85;
            padding: 6px 10px;
            font-family: 'Share Tech Mono', monospace;
        }

        .stat-label {
            font-size: 9px;
            color: #d4b2ff;
            letter-spacing: 1px;
            text-transform: uppercase;
        }

        .stat-value {
            font-family: 'Orbitron', sans-serif;
            font-size: 11px;
            font-weight: 800;
            color: #ffffff;
            margin-top: 2px;
            text-shadow: 0 0 5px rgba(255, 42, 133, 0.6);
        }

        /* CITA FEMENINA Y ELEGANTE */
        .cyber-quote {
            position: absolute;
            left: 45px;
            top: 260px;
            width: 480px;
            font-family: 'Share Tech Mono', monospace;
            font-size: 11.5px;
            line-height: 1.5;
            color: #fce8f3;
            background: rgba(22, 9, 34, 0.85);
            border-left: 3px solid #00f5d4;
            border-right: 1px solid rgba(255, 42, 133, 0.3);
            padding: 10px 14px;
            z-index: 5;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.4);
        }

        .cyber-quote span {
            color: #ff94c2;
            font-weight: bold;
        }

        /* --- MARCOS DE GIFS --- */
        .gif-frame-primary {
            position: absolute;
            right: 45px;
            top: 35px;
            width: 380px;
            height: 220px;
            border: 2px solid #ff2a85;
            background: #000;
            overflow: hidden;
            z-index: 4;
            box-shadow: 0 0 20px rgba(255, 42, 133, 0.3);
            clip-path: polygon(0 0, 100% 0, 100% 88%, 92% 100%, 0 100%);
        }

        .gif-frame-secondary {
            position: absolute;
            right: 45px;
            bottom: 35px;
            width: 380px;
            height: 220px;
            border: 2px solid #00f5d4;
            background: #000;
            overflow: hidden;
            z-index: 4;
            box-shadow: 0 0 20px rgba(0, 245, 212, 0.3);
            clip-path: polygon(8% 0, 100% 0, 100% 100%, 0 100%, 0 15%);
        }

        .gif-content {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: contrast(105%) brightness(98%);
        }

        .cam-label {
            position: absolute;
            top: 8px;
            left: 10px;
            font-family: 'Share Tech Mono', monospace;
            font-size: 10px;
            background: rgba(11, 5, 18, 0.85);
            padding: 2px 8px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            z-index: 5;
            letter-spacing: 1px;
        }

        /* --- REPRODUCTOR DE MÚSICA FEMENINO --- */
        .music-widget-single {
            position: absolute;
            left: 45px;
            bottom: 35px;
            width: 480px;
            background: rgba(28, 11, 42, 0.92);
            border: 2px solid #ff2a85;
            padding: 14px 16px;
            z-index: 6;
            box-shadow: 0 0 25px rgba(255, 42, 133, 0.25);
            clip-path: polygon(0 0, 95% 0, 100% 22%, 100% 100%, 0 100%);
        }

        .player-top-row {
            display: flex;
            align-items: center;
            gap: 14px;
            margin-bottom: 10px;
        }

        .disc-icon {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            background: radial-gradient(circle, #00f5d4 15%, #ff2a85 40%, #0b0512 75%);
            border: 2px solid #ff94c2;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-shrink: 0;
            box-shadow: 0 0 12px rgba(255, 42, 133, 0.5);
        }

        .disc-icon.playing {
            animation: spinDisc 4s linear infinite;
        }

        @keyframes spinDisc {
            100% { transform: rotate(360deg); }
        }

        .disc-center {
            width: 10px;
            height: 10px;
            background: #ffffff;
            border-radius: 50%;
        }

        .track-meta {
            overflow: hidden;
            width: 100%;
        }

        .track-title {
            font-family: 'Oxanium', sans-serif;
            font-weight: 800;
            font-size: 13px;
            color: #ffffff;
            letter-spacing: 1px;
            text-transform: uppercase;
            text-shadow: 0 0 6px rgba(255, 42, 133, 0.4);
        }

        .track-sub {
            font-family: 'Share Tech Mono', monospace;
            font-size: 10.5px;
            color: #00f5d4;
            margin-top: 2px;
        }

        .progress-bar-container {
            width: 100%;
            height: 6px;
            background: rgba(11, 5, 18, 0.8);
            border: 1px solid #ff2a85;
            position: relative;
            margin-bottom: 10px;
            cursor: pointer;
            border-radius: 2px;
        }

        .progress-current {
            position: absolute;
            top: 0;
            left: 0;
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, #ff2a85, #d4b2ff, #00f5d4);
            box-shadow: 0 0 10px #ff2a85;
        }

        .player-controls-single {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .btn-cyber {
            background: rgba(11, 5, 18, 0.85);
            border: 1px solid #ff2a85;
            color: #ffffff;
            padding: 5px 16px;
            font-family: 'Orbitron', sans-serif;
            font-size: 10.5px;
            font-weight: 800;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 0 8px rgba(255, 42, 133, 0.2);
        }

        .btn-cyber:hover {
            background: #ff2a85;
            color: #ffffff;
            box-shadow: 0 0 15px #ff2a85;
        }

        .btn-mute {
            border-color: #00f5d4;
            color: #00f5d4;
            box-shadow: 0 0 8px rgba(0, 245, 212, 0.2);
        }

        .btn-mute:hover {
            background: #00f5d4;
            color: #0b0512;
            box-shadow: 0 0 15px #00f5d4;
        }

        /* Sello en la esquina inferior */
        .corner-tag {
            position: absolute;
            bottom: 10px;
            left: 45px;
            font-family: 'Share Tech Mono', monospace;
            font-size: 9px;
            color: #d4b2ff;
            letter-spacing: 2px;
            opacity: 0.6;
        }
    
body{display:block;overflow:auto;padding:clamp(12px,3vw,44px);font-family:Rajdhani,system-ui,sans-serif}
main{max-width:1080px;margin:auto}.banner-container{width:100%;height:auto;padding:clamp(18px,3.5vw,44px);display:grid;grid-template-columns:1.22fr 1fr;gap:32px;isolation:isolate}
.copy,.feeds{position:relative;z-index:4;min-width:0;display:grid;align-content:center;gap:18px}.feeds{gap:20px}
.header-box,.stats-hud-box,.hud-status-tag,.cyber-quote,.music-widget-single,.gif-frame-primary,.gif-frame-secondary{position:relative;inset:auto;width:auto}
.main-title{font-size:clamp(44px,5.6vw,78px);letter-spacing:-.035em;line-height:1.03}.alias-script{margin:10px 0}.subtitle-cyber-id,.stat-label,.cam-label,.track-sub{font-size:12px}.cam-label{left:auto;right:12px}.cyber-quote{font-size:16px}.hud-status-tag{justify-self:start;font-size:13px}.stat-value,.track-title,.btn-cyber{font-size:14px}
.gif-frame-primary,.gif-frame-secondary{height:auto;aspect-ratio:1.85;background-size:cover;background-position:center}.gif-frame-primary{background-image:url(assets/camera-01.webp)}.gif-frame-secondary{background-image:url(assets/camera-02.webp)}.gif-content{display:block}.scanline{inset:0;opacity:.21}
.disc-icon{background:conic-gradient(#ff2a85,#321738,#00f5d4,#391039,#ff2a85)}input[type=range]{width:100%;accent-color:#00f5d4;margin:8px 0 14px}.music-widget-single{padding:16px}
nav,.lower{background:#160e22;border:1px solid #62335d}nav{display:flex;gap:24px;align-items:center;flex-wrap:wrap;padding:14px 20px;margin-bottom:15px}a{color:#67fbe8;text-underline-offset:4px}nav a{font-weight:700;text-decoration:none}nav b{color:#ff9bc7;margin-right:auto}.lower{padding:clamp(20px,4vw,44px);margin-top:20px}.lower h2{font:700 clamp(32px,4vw,52px)/1.1 Oxanium,system-ui,sans-serif;color:#ffb6d5;margin-bottom:20px}.projects{display:grid;grid-template-columns:1fr 1fr;gap:15px}.projects details{background:#22152f;padding:18px;border-left:2px solid #00f5d4}.projects summary{cursor:pointer;color:#bbfff4;font-weight:bold;font-size:20px}.lower p{font-size:18px;line-height:1.5;margin:10px 0}.lower small{color:#dabfff;font:14px/1.6 monospace}.links{display:flex;flex-wrap:wrap;gap:22px}button,a,input,summary{touch-action:manipulation}:focus-visible{outline:2px solid #00f5d4;outline-offset:3px}
@media(max-width:740px){.banner-container,.projects{grid-template-columns:1fr}.feeds{grid-template-columns:1fr 1fr;gap:8px}.cam-label{font-size:10px;right:4px;top:4px}.banner-container{gap:18px}nav{gap:12px}.stat-card{padding:7px 5px}.stats-hud-box{gap:5px}.progress-bar-container{min-height:12px}}
@media(prefers-reduced-motion:reduce){*,*::before,*::after{animation:none!important;scroll-behavior:auto!important}.feeds .gif-content{display:none}.gif-frame-primary{background-image:url(assets/camera-01.webp)}.gif-frame-secondary{background-image:url(assets/camera-02.webp)}}
body{padding:0}main{max-width:1055px}.banner-container{padding:40px 3% 16px;gap:4%;border-width:2px 0 0}.copy{gap:22px}.feeds{gap:26px}.header-box{margin-bottom:12px}.subtitle-cyber-id,.stat-label,.cam-label,.track-sub{font-size:14px}.alias-script{font-size:20px}.main-title{font-size:clamp(44px,6.3vw,66px)}.hud-status-tag{font-size:16px}.cyber-quote{font-size:20px;padding:13px 18px}.stat-value,.track-title,.btn-cyber{font-size:18px}.music-widget-single{padding:20px}.disc-icon{width:52px;height:52px}.music-widget-single input{margin:13px 0 19px}nav{margin:18px 0 0}.lower{scroll-margin:16px}
@media(max-width:740px){.banner-container{padding:24px 16px;gap:24px}.feeds{grid-template-columns:1fr;gap:12px}.header-box{margin-bottom:0}.copy{gap:16px}.cyber-quote{font-size:17px}.hud-status-tag{font-size:14px}.stat-value{font-size:15px}}
.btn-cyber{min-height:38px}select{font-size:16px}.stat-card{padding:8px 14px}.music-widget-single input{margin:18px 0 20px}
</style>
</head>
<body><main>
<section class="banner-container"><div class="cyber-grid"></div><div class="ambient-glow"></div><div class="scanline"></div><div class="copy"><header class="header-box"><p class="subtitle-cyber-id">INTELIGÊNCIA ARTIFICIAL</p><p class="alias-script">Agentes &amp; automação</p><h1 class="main-title">Bruno Santos</h1></header><div class="hud-status-tag"><i class="status-dot"></i> Em busca de estágio ou vaga júnior</div><div class="stats-hud-box"><div class="stat-card"><div class="stat-label">Linguagem</div><div class="stat-value">Python</div></div><div class="stat-card"><div class="stat-label">Fluxos</div><div class="stat-value">n8n</div></div><div class="stat-card"><div class="stat-label">Dados</div><div class="stat-value">PostgreSQL</div></div></div>
<p class="cyber-quote">Desenvolvo <span>agentes de IA</span> que consultam dados, atendem clientes e confirmam pedidos. Conecto APIs e bancos de dados para automatizar essas tarefas.</p>
<div class="music-widget-single"><div class="player-top-row"><div class="disc-icon" id="disc"><i class="disc-center"></i></div><div><div class="track-title">Trilha cyberpunk</div><label class="track-sub" for="choice">FAIXA </label><select id="choice"><option value="assets/pulso.wav">Pulso neon</option><option value="assets/original.m4a">Original do modelo</option></select><span class="track-sub" role="status" id="track"></span></div></div><input id="seek" type="range" min="0" max="100" step=".1" value="0" aria-label="Posição na trilha"><div class="player-controls-single"><button class="btn-cyber" id="play">Reproduzir</button><button class="btn-cyber btn-mute" id="mute" aria-pressed="false">Silenciar</button></div><audio id="audio" preload="none"></audio></div></div>
<div class="feeds"><div class="gif-frame-primary"><span class="cam-label">CAM / 01</span><img class="gif-content" src="assets/camera-01.gif" alt="Mulher-robô de cabelo rosa sentada diante de um painel azul" onerror="this.hidden=true;this.style.display='none'"></div><div class="gif-frame-secondary"><span class="cam-label">CAM / 02</span><img class="gif-content" src="assets/camera-02.gif" alt="Detalhe do braço articulado da mulher-robô em movimento" onerror="this.hidden=true;this.style.display='none'"></div></div></section><nav><b>BS / PORTFÓLIO</b><a href="#projetos">Projetos</a><a href="#perfil">Sobre mim</a><a href="#contato">Contato</a></nav><section class="lower" id="projetos"><h2>Projetos.</h2><div class="projects"><details open><summary>RAG híbrido</summary><p>Consulta uma base vetorial local e recorre à busca na web quando precisa de outra fonte. A resposta chega ao usuário pela interface Streamlit.</p><small>Python · ChromaDB · Pandas · Streamlit · OpenRouter</small></details><details ><summary>Agente de pré-venda</summary><p>Atende pelo WhatsApp, consulta preços e estoque de materiais de construção e confirma pedidos. Regras no PostgreSQL validam os dados e o fluxo permite encaminhar a conversa a um atendente.</p><small>n8n · PostgreSQL · Python · Docker Compose</small></details><details ><summary>Instagram Caption Agent</summary><p>Gera legendas e publica conteúdo pela Meta Graph API, com acompanhamento de cada execução.</p><small>n8n · Python · Meta Graph API</small></details><details ><summary>Mini-CRM com IA</summary><p>Captura e qualifica leads, organiza os contatos e gera relatórios de acompanhamento.</p><small>Python · Pandas · n8n · Supabase</small></details></div></section><section class="lower" id="perfil"><h2>Sobre mim.</h2><p>Sou Bruno dos Santos de Morais, de Morro Agudo, SP. Minha trajetória inclui atendimento e rotinas de escritório. Hoje aplico essa experiência no desenvolvimento de agentes conversacionais e integrações.</p><small>Em andamento · Gestão da Tecnologia da Informação na Estácio e Dados com Python e IA na Aceleração Santander.</small></section><section class="lower" id="contato"><h2>Vamos conversar?</h2><p class="links"><a href="mailto:brunosantosmo5@gmail.com">Enviar e-mail</a><a href="https://github.com/brunosantosmo5-crypto">GitHub</a><a href="https://www.linkedin.com/in/bruno-santos-717a761a1/">LinkedIn</a></p></section></main><script>
const audio=document.querySelector('audio'), play=document.querySelector('#play'), mute=document.querySelector('#mute'), seek=document.querySelector('#seek'), disc=document.querySelector('#disc');
audio.preload='metadata';audio.src='assets/pulso.wav';
const choice=document.querySelector('#choice'), message=document.querySelector('#track');
choice.onchange=()=>{audio.pause();seek.value=0;message.textContent='';audio.src=choice.value;audio.load()};
audio.onerror=()=>{if(choice.selectedIndex===1){choice.selectedIndex=0;audio.src=choice.value;message.textContent=' · Original indisponível. Pulso neon selecionada.'}};
play.onclick=()=>{if(audio.paused)audio.play().catch(()=>document.querySelector('#track').textContent='Falha ao reproduzir áudio');else audio.pause()};
function sync(){play.textContent=audio.paused?'Reproduzir':'Pausar';disc.classList.toggle('playing',!audio.paused)}
audio.onplay=audio.onpause=sync;audio.onended=()=>{seek.value=0;sync()};
mute.onclick=()=>{audio.muted=!audio.muted;mute.setAttribute('aria-pressed',audio.muted);mute.textContent=audio.muted?'Ativar som':'Silenciar'};
audio.ontimeupdate=()=>{if(audio.duration)seek.value=100*audio.currentTime/audio.duration};seek.oninput=()=>{if(audio.duration)audio.currentTime=audio.duration*seek.value/100};
</script><script type="module">import { mountAutoSiteWidget } from "/_sites/dispatch-assets/sites-widget.js";mountAutoSiteWidget({"kind":"auto","toolbarOrigin":null,"viewerRemixEnabled":false,"invitationBanner":true,"mobileEnabled":false,"environment":"production","chatgptOrigin":"https://chatgpt.com","locale":"pt-BR","accountId":"personal","projectId":"appgprj_6aff3bbbeccc8191b4f3dbd9b7f52ac5","projectTitle":"Bruno Santos · Portfólio"});</script></body></html>
