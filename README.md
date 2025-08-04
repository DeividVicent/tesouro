<!DOCTYPE html>
<html lang="PT-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tesouros de Itanhaém</title>
  <style>
    /* Estilos globais e de layout */
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;800;900&display=swap');
    body {
      font-family: 'Inter', sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #e0f2fe, #c7d2fe);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      color: #1f2937;
    }
    .container {
      position: relative;
      background: rgba(255, 255, 255, 0.7);
      backdrop-filter: blur(10px);
      border-radius: 2rem;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
      padding: 2rem;
      max-width: 32rem;
      width: 100%;
      text-align: center;
      animation: fadeIn 0.5s ease-in-out;
    }
    .hidden {
      display: none;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    /* Estilos para o layout do jogo */
    .game-layout {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
      align-items: center;
      transition: all 0.5s ease-in-out;
    }
    .game-element {
      width: 100%;
    }
    
    /* Estilos para os ícones principais (início e fim) */
    .icon {
      width: 6rem;
      height: 6rem;
      margin-bottom: 1rem;
    }
    .icon.bounce-slow {
      animation: bounceSlow 2s infinite ease-in-out;
    }
    @keyframes bounceSlow {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }
    
    /* Novo estilo para o ícone de 'certo' */
    .correct-icon {
      color: #10b981; /* Verde */
      animation: bounceSlow 1.5s infinite ease-in-out;
    }
    
    /* Estilos para o ícone dentro da charada (agora menor e inline) */
    .riddle-icon {
      width: 2rem;
      height: 2rem;
      margin-right: 0.5rem;
      vertical-align: middle;
      color: #3b82f6;
    }

    /* Estilos de tipografia e elementos de texto */
    h1 {
      font-size: 2.25rem;
      font-weight: 900;
      color: #1f2937;
      margin-bottom: 1rem;
    }
    h2 {
      font-size: 1.5rem;
      font-weight: 700;
      color: #1f2937;
      margin-bottom: 0.5rem;
    }
    h3 {
      font-size: 1.875rem;
      font-weight: 800;
      color: #2563eb;
      margin-bottom: 1rem;
    }
    p {
      font-size: 1rem;
      color: #4b5563;
      margin-bottom: 1.5rem;
    }
    /* Estilos para imagens */
    .game-image {
      border-radius: 0.5rem;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
      width: 100%;
    }
    /* Estilos para botões */
    .btn {
      width: 100%;
      padding: 0.75rem 1.5rem;
      border: none;
      border-radius: 9999px;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.3s ease-in-out;
      transform: scale(1);
      box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    }
    .btn:hover {
      transform: scale(1.05);
    }
    .btn-primary {
      background-color: #2563eb;
      color: white;
    }
    .btn-primary:hover {
      background-color: #1d4ed8;
    }
    .btn-option {
      background-color: #e5e7eb;
      color: #1f2937;
      margin-bottom: 0.75rem;
    }
    .btn-option.selected {
      background-color: #3b82f6;
      color: white;
    }
    .btn-option:hover {
      background-color: #d1d5db;
    }
    .btn-success {
      background-color: #10b981;
      color: white;
    }
    .btn-success:hover {
      background-color: #059669;
    }
    .btn:disabled {
      background-color: #9ca3af;
      cursor: not-allowed;
      transform: none;
      box-shadow: none;
    }
    .btn-container {
      display: flex;
      flex-direction: column;
      width: 100%;
    }
    .link {
      margin-top: 1rem;
      color: #2563eb;
      font-weight: 600;
      text-decoration: none;
      transition: color 0.2s;
    }
    .link:hover {
      color: #1e40af;
    }
    /* Estilos da tela final */
    .final-score {
      font-size: 1.5rem;
      font-weight: 700;
      color: #2563eb;
      margin-bottom: 1rem;
    }
    /* Efeitos de feedback */
    .correct-message {
      color: #10b981;
      font-weight: 700;
      margin-top: 1rem;
      animation: pulse 1s infinite;
    }
    .incorrect-message {
      color: #ef4444;
      font-weight: 600;
      margin-top: 1rem;
      animation: fadeIn 0.3s;
    }
    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }
    /* Ícones SVG para Lucide-React */
    .lucide-icon {
      display: inline-block;
      vertical-align: middle;
      stroke-width: 2;
      stroke: currentColor;
      fill: none;
      line-height: 1;
    }
    .lucide-icon.map-pin {
      color: #3b82f6;
    }
    .lucide-icon.arrow-right {
      width: 1.5rem;
      height: 1.5rem;
      color: #fff;
      margin-right: 0.5rem;
    }
    
    /* Estilo do confete */
    #confetti-canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 999;
      pointer-events: none;
    }

    /* Estilo da estrela de conclusão */
    .star-icon {
      width: 4rem;
      height: 4rem;
      color: #fde047; /* Amarelo/Dourado */
      margin-bottom: 1rem;
      animation: sparkle 1s infinite alternate;
      stroke: #fde047;
      fill: #fde047;
    }

    @keyframes sparkle {
      0% { transform: scale(1) rotate(0deg); opacity: 1; }
      100% { transform: scale(1.1) rotate(15deg); opacity: 0.9; }
    }
  </style>
</head>
<body>

  <!-- Container principal do aplicativo -->
  <div class="container">
    
    <!-- Tela de início -->
    <div id="start-screen">
      <h1>Tesouros de Itanhaém</h1>
      <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQEeWjRGY3RHlTwGHOBDFwurOvhGLtnZ0cx0CrCJgkaqCZ_cE1blY9itAjkVUR-oN49uB8&usqp=CAU" alt="Uma imagem da cidade de Itanhaém" class="game-image">
      <p>Uma caça ao tesouro digital para explorar a rica história e os patrimônios culturais da segunda cidade mais antiga do Brasil.</p>
      <button class="btn btn-primary" onclick="startGame()">
        <svg class="lucide-icon arrow-right" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
        Iniciar Aventura
      </button>
      <a href="https://www.itanhaem.sp.gov.br/" target="_blank" rel="noopener noreferrer" class="link">Saiba mais sobre Itanhaém</a>
    </div>

    <!-- Tela do jogo (escondida por padrão) -->
    <div id="game-screen" class="hidden">
      <h2 id="step-title"></h2>
      <svg class="lucide-icon map-pin icon bounce-slow" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 21.7c-4.4-4.4-8-7-8-10.7C4 6 7.6 2 12 2s8 4 8 9c0 3.7-3.6 6.3-8 10.7z"/><circle cx="12" cy="11" r="3"/></svg>
      <div id="game-content" class="game-layout">
        <div id="riddle-container" class="game-element">
          <h3 id="riddle-title">Qual o nome deste patrimônio?</h3>
          <p id="riddle-text"></p>
        </div>

        <div id="image-container" class="game-element">
          <img id="patrimonio-image" src="" alt="Imagem do patrimônio" class="game-image">
        </div>
        
        <div id="options-container" class="game-element btn-container"></div>
      </div>
      <button id="check-button" class="btn btn-primary" disabled>Verificar Resposta</button>
      
      <div id="correct-answer" class="hidden">
        <svg class="lucide-icon icon correct-icon" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6 9 17l-5-5"/></svg>
        <h4 class="correct-message">Resposta Correta!</h4>
        <p id="patrimonio-description" class="text-left"></p>
        <button class="btn btn-success" onclick="nextStep()">
          <svg class="lucide-icon arrow-right" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
          Próximo Patrimônio
        </button>
      </div>
    </div>

    <!-- Tela final com o novo ícone de estrela -->
    <div id="end-screen" class="hidden">
      <h1>Caça ao Tesouro Concluída!</h1>
      <svg class="lucide-icon star-icon" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
      <p>Parabéns, explorador! Você desvendou os segredos dos principais patrimônios históricos de Itanhaém.</p>
      <div id="final-score" class="final-score"></div>
      <button class="btn btn-primary" onclick="startGame()">Reiniciar Aventura</button>
    </div>

  </div>

  <script>
    // Dados do jogo - Lista com 5 perguntas.
    const originalPatrimonios = [
      {
        id: 1,
        name: "Igreja Matriz de Sant'Anna",
        riddle: "Onde a fé de séculos se encontra no coração de Itanhaém, em uma igreja construída no século XVIII. Qual o nome deste lugar sagrado?",
        answer: "Igreja Matriz de Sant'Anna",
        options: ["Igreja Matriz de Sant'Anna", "Santuário Nossa Senhora do Sion", "Igreja Nossa Senhora da Candelária", "Igreja São Benedito"],
        description: "A Igreja Matriz de Sant'Anna, concluída em 1761, é um marco da arquitetura colonial portuguesa e um dos pontos mais antigos e significativos da cidade. O seu interior, de estilo maneirista, abriga importantes peças de arte sacra, incluindo uma obra do famoso pintor Benedito Calixto.",
        imageUrl: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRZjCDnvFGdJcfLszT2hA73y7NA3XYvR7dFI6PxxvFzhjhlEbHjRu90r06fACxfwVqflbY&usqp=CAU",
      },
      {
        id: 2,
        name: "Convento de Nossa Senhora da Conceição",
        riddle: "Suba o morro e encontre um lugar que abençoa a paisagem. Um antigo convento, fundado no início do século XVIII, que foi o primeiro templo dedicado à padroeira da cidade. Qual o nome deste local?",
        answer: "Convento de Nossa Senhora da Conceição",
        options: ["Convento de Nossa Senhora da Conceição", "Convento Santo Antônio", "Mosteiro de São Bento", "Santuário de Santa Edwiges"],
        description: "Construído sobre a primeira ermida de Itanhaém, o convento oferece uma vista panorâmica deslumbrante da cidade, do rio e do mar. É um local de grande importância histórica e religiosa, sendo um dos patrimônios tombados pelo IPHAN.",
        imageUrl: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRwPuPtksOxTl_L50pC4ZpMW-8G4uh0MtK3zQ&s",
      },
      {
        id: 3,
        name: "Cama de Anchieta",
        riddle: "Entre rochas e a beira-mar, um lendário poeta jesuíta encontrava paz e inspiração. Que formação rochosa, frequentada no século XVI, leva o nome do santo?",
        answer: "Cama de Anchieta",
        options: ["Cama de Anchieta", "Pedra da Baleia", "Pedra do Índio", "Praia do Sonho"],
        description: "Segundo a lenda, esta formação rochosa peculiar era o local favorito do Padre José de Anchieta para descansar e compor seus poemas. O local, acessível por uma passarela de madeira, é um dos mais visitados e pitorescos de Itanhaém.",
        imageUrl: "https://i.ytimg.com/vi/FEEUqQhMnsk/maxresdefault.jpg",
      },
      {
        id: 4,
        name: "Gruta de Nossa Senhora de Lourdes",
        riddle: "Um refúgio de paz, construído na década de 1960. Fica na beira-mar, perto de uma passarela, e abriga a imagem de uma santa. Qual é o nome deste local de fé?",
        answer: "Gruta de Nossa Senhora de Lourdes",
        options: ["Gruta de Nossa Senhora de Lourdes", "Caverna da Serpente", "Toca do Saci", "Gruta de Santo Antônio"],
        description: "Inspirada na gruta de Lourdes, na França, este local de devoção foi construído em uma formação rochosa natural. É um ponto de peregrinação e oração, que atrai muitos visitantes em busca de paz e milagres.",
        imageUrl: "https://www2.itanhaem.sp.gov.br/wp-content/uploads/2018/12/gruta_nossa_senhora_de_lourdes.jpg",
      },
      {
        id: 5,
        name: "Casa da Câmara e Cadeia",
        riddle: "Um edifício histórico que unia a justiça e o poder político. Já serviu como câmara e como prisão. Que prédio é este?",
        answer: "Casa da Câmara e Cadeia",
        options: ["Casa da Câmara e Cadeia", "Fórum de Itanhaém", "Paço Municipal", "Palácio dos Esportes"],
        description: "Construída no século XVII, este prédio histórico foi o centro do poder político e judiciário da vila. Sua arquitetura colonial é um dos destaques do Centro Histórico.",
        imageUrl: "https://www.cidadeecultura.com/wp-content/webp-express/webp-images/doc-root/wp-content/uploads/2016/08/itanhaem-museus-conceicao-de-itanhaem-IMG_6505-bx-1024x683.jpg.webp",
      },
    ];

    // Variáveis de estado do jogo
    let currentStep = 0;
    let score = 0;
    let selectedOption = '';
    let patrimonios = []; 
    
    // Funções para manipular a tela e o jogo
    const startScreen = document.getElementById('start-screen');
    const gameScreen = document.getElementById('game-screen');
    const endScreen = document.getElementById('end-screen');

    const stepTitle = document.getElementById('step-title');
    const riddleTitle = document.getElementById('riddle-title');
    const riddleText = document.getElementById('riddle-text');
    const patrimonioImage = document.getElementById('patrimonio-image');
    const optionsContainer = document.getElementById('options-container');
    const checkButton = document.getElementById('check-button');
    const finalScoreDisplay = document.getElementById('final-score');
    const correctMessageContainer = document.getElementById('correct-answer');
    const gameContentContainer = document.getElementById('game-content');
    const patrimonioDescription = document.getElementById('patrimonio-description');

    // Função para misturar um array (Algoritmo de Fisher-Yates)
    const shuffleArray = (array) => {
      const shuffledArray = [...array];
      for (let i = shuffledArray.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [shuffledArray[i], shuffledArray[j]] = [shuffledArray[j], shuffledArray[i]];
      }
      return shuffledArray;
    };
    
    const startGame = () => {
      currentStep = 1;
      score = 0;
      // Mantém a ordem original das perguntas
      patrimonios = [...originalPatrimonios];
      startScreen.classList.add('hidden');
      endScreen.classList.add('hidden'); 
      gameScreen.classList.remove('hidden');
      renderGameStep();
    };

    const renderGameStep = () => {
      correctMessageContainer.classList.add('hidden');
      gameContentContainer.classList.remove('hidden');
      
      const currentPatrimonio = patrimonios[currentStep - 1];
      stepTitle.textContent = `Desafio ${currentStep} de ${patrimonios.length}`;
      riddleTitle.textContent = "Qual o nome deste patrimônio?";
      riddleText.textContent = currentPatrimonio.riddle;
      patrimonioImage.src = currentPatrimonio.imageUrl;
      patrimonioImage.alt = `Imagem de ${currentPatrimonio.name}`;
      
      // Mistura a ordem das opções de resposta e renderiza os botões
      const shuffledOptions = shuffleArray([...currentPatrimonio.options]);
      optionsContainer.innerHTML = '';
      shuffledOptions.forEach(option => {
        const button = document.createElement('button');
        button.className = 'btn btn-option';
        button.textContent = option;
        button.onclick = (event) => selectOption(option, event.target);
        optionsContainer.appendChild(button);
      });
      
      selectedOption = '';
      checkButton.disabled = true;
      checkButton.textContent = 'Verificar Resposta';
      gameContentContainer.classList.remove('hidden');
    };

    const selectOption = (option, target) => {
      selectedOption = option;
      checkButton.disabled = false;
      
      // Remove a classe 'selected' de todos os botões e adiciona ao selecionado
      document.querySelectorAll('.btn-option').forEach(btn => btn.classList.remove('selected'));
      target.classList.add('selected');
    };

    const checkAnswer = () => {
      checkButton.disabled = true;
      checkButton.textContent = 'Verificando...';

      setTimeout(() => {
        const currentPatrimonio = patrimonios[currentStep - 1];
        if (selectedOption.toLowerCase() === currentPatrimonio.answer.toLowerCase()) {
          score += 2;
          patrimonioDescription.textContent = currentPatrimonio.description;
          gameContentContainer.classList.add('hidden');
          correctMessageContainer.classList.remove('hidden');
          createConfetti();
        } else {
          checkButton.disabled = false;
          checkButton.textContent = 'Verificar Resposta';
          const feedback = document.createElement('p');
          feedback.className = 'incorrect-message';
          feedback.textContent = 'Resposta incorreta. Tente novamente!';
          gameContentContainer.appendChild(feedback);
          setTimeout(() => feedback.remove(), 2000);
        }
      }, 500);
    };

    const nextStep = () => {
      if (currentStep < patrimonios.length) {
        currentStep++;
        renderGameStep();
      } else {
        renderEndScreen();
      }
    };
    
    const renderEndScreen = () => {
      gameScreen.classList.add('hidden');
      endScreen.classList.remove('hidden');
      finalScoreDisplay.textContent = `Sua Pontuação Final: ${score}`;
      createConfetti();
    };

    checkButton.addEventListener('click', checkAnswer);

    const createConfetti = () => {
      const existingCanvas = document.getElementById('confetti-canvas');
      if (existingCanvas) existingCanvas.remove();
      
      const canvas = document.createElement('canvas');
      canvas.id = 'confetti-canvas';
      document.body.appendChild(canvas);
      
      const ctx = canvas.getContext('2d');
      const particles = [];
      const particleCount = 200;
      const colors = ['#f44336', '#e91e63', '#9c27b0', '#673ab7', '#3f51b5', '#2196f3', '#03a9f4', '#00bcd4', '#009688', '#4caf50', '#8bc34a', '#cddc39', '#ffeb3b', '#ffc107', '#ff9800', '#ff5722'];
    
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    
      function Particle() {
        this.x = Math.random() * canvas.width;
        this.y = Math.random() * canvas.height - canvas.height;
        this.radius = Math.random() * 5 + 2;
        this.color = colors[Math.floor(Math.random() * colors.length)];
        this.velocity = {
          x: Math.random() * 3 - 1.5,
          y: Math.random() * 3 + 1
        };
        this.rotation = Math.random() * 360;
        this.rotationSpeed = Math.random() * 10 - 5;
    
        this.draw = function() {
          ctx.beginPath();
          ctx.fillStyle = this.color;
          ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
          ctx.fill();
          ctx.closePath();
        };
    
        this.update = function() {
          if (this.y > canvas.height) {
            this.y = -20;
            this.x = Math.random() * canvas.width;
          }
    
          this.x += this.velocity.x;
          this.y += this.velocity.y;
          this.rotation += this.rotationSpeed;
        };
      }
    
      for (let i = 0; i < particleCount; i++) {
        particles.push(new Particle());
      }
    
      function animate() {
        if (!canvas) return;
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        for (let i = 0; i < particles.length; i++) {
          particles[i].update();
          particles[i].draw();
        }
        requestAnimationFrame(animate);
      }
      
      animate();
    
      const handleResize = () => {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
      };
    
      window.addEventListener('resize', handleResize);
      
      setTimeout(() => {
        if (document.body.contains(canvas)) {
          document.body.removeChild(canvas);
        }
      }, 5000); 
    };
  </script>

</body>
</html>
