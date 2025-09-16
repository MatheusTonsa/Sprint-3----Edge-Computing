# Sprint-3----Edge-Computing

🎮 Contador de Pontos para Jogo com ESP32 e LCD I2C

Este projeto inovador oferece um sistema completo para gerenciar pontos em jogos, ideal para competições amigáveis ou acompanhamento de desempenho. Desenvolvido com um ESP32 DevKitC V4, um display LCD I2C de 20x4 e quatro botões intuitivos, ele permite registrar gols e assistências para até 7 jogadoras, exibir placares em tempo real e destacar a "Craque do Jogo" de forma dinâmica.

✨ Funcionalidades Principais

•
Registro Detalhado: Adicione gols e assistências com facilidade para cada jogadora.

•
Placar Abrangente: Acompanhe o desempenho de todas as participantes em um placar geral claro.

•
Destaque da Craque: Identificação automática da jogadora com mais gols e da jogadora com mais assistências.

•
Navegação Intuitiva: Alterne entre as telas de registro, placar e craque do jogo com botões dedicados.

•
Reinício Rápido: Opção de resetar todas as estatísticas do jogo com uma pressão longa no botão de menu.

⚙️ Componentes de Hardware

O coração deste projeto é o ESP32 DevKitC V4, complementado pelos seguintes componentes:

ComponenteDescriçãoESP32 DevKitC V4Microcontrolador principal que gerencia toda a lógica do contador de pontos.Display LCD 20x4 I2CExibe as informações do jogo, menus de navegação e estatísticas das jogadoras.Botão Amarelo (BTN_A)Utilizado para selecionar jogadoras e confirmar ações (registrar gol ou assistência).Botão Azul (BTN_B)Navega para cima nos menus e alterna entre as opções de ação (gol/assistência).Botão Vermelho (BTN_C)Navega para baixo nos menus e alterna entre as opções de ação (gol/assistência).Botão Cinza (BTN_MENU)Alterna entre as diferentes telas (Registro, Placar, Craque do Jogo). Uma pressão longa reinicia o jogo.

🔌 Diagrama de Conexão (Wokwi)

Este projeto foi concebido e simulado na plataforma Wokwi. O arquivo diagram.json detalha a montagem do hardware e as conexões:

•
Display LCD I2C: Conectado aos pinos SDA (GPIO21) e SCL (GPIO22) do ESP32.

•
Botões de Controle:

•
BTN_A (Amarelo): Conectado ao pino GPIO13 do ESP32.

•
BTN_B (Azul): Conectado ao pino GPIO14 do ESP32.

•
BTN_C (Vermelho): Conectado ao pino GPIO12 do ESP32.

•
BTN_MENU (Cinza): Conectado ao pino GPIO32 do ESP32.



Todos os botões são configurados com INPUT_PULLUP no código e conectados ao GND através do outro terminal, garantindo um acionamento por nível baixo.

📚 Bibliotecas Essenciais

Para o funcionamento do display LCD, utilizamos a biblioteca:

•
LiquidCrystal I2C: Essencial para a comunicação do ESP32 com o display LCD via protocolo I2C, facilitando a exibição de texto e controle do backlight.

▶️ Como Simular no Wokwi

Para experimentar o contador de pontos, siga os passos abaixo:

1.
Acesse o Projeto: Navegue até o projeto no Wokwi: https://wokwi.com/projects/442264817239768065

2.
Inicie a Simulação: Clique no botão verde "Iniciar Simulação" (ícone de play ▶️) localizado na parte superior da interface do Wokwi.

3.
Interaja com os Botões: Utilize os botões virtuais no diagrama para controlar o sistema:

•
🟡 BTN_A (Amarelo): Seleciona uma jogadora ou confirma a ação (gol/assistência).

•
🔵 BTN_B (Azul): Move o cursor para cima na lista de jogadoras ou alterna entre as opções de ação (Gol/Assistência).

•
🔴 BTN_C (Vermelho): Move o cursor para baixo na lista de jogadoras ou alterna entre as opções de ação (Gol/Assistência).

•
⚪ BTN_MENU (Cinza): Troca as telas do menu (Registro, Placar, Craque do Jogo). Uma pressão longa (aproximadamente 3 segundos) neste botão reinicia todas as estatísticas do jogo.



💻 Estrutura do Código (sketch.ino)

O código-fonte (sketch.ino) é cuidadosamente organizado para clareza e manutenção, dividido nas seguintes seções:

•
Configuração Inicial: Define os pinos dos botões, inicializa o objeto LiquidCrystal_I2C para o LCD e configura as variáveis globais.

•
Estruturas de Dados: Declara a struct StatsJogadora para armazenar assistencias e gols, além de arrays para nomesJogadoras e nomesAcoes.

•
Funções de Utilidade:

•
debounceRead(int pino, unsigned long &ultimoTempo): Implementa um mecanismo de debounce para os botões, garantindo leituras precisas e evitando múltiplos acionamentos.

•
resetGame(): Reinicia todas as estatísticas das jogadoras, o cursor de seleção e a tela atual para o estado inicial.



•
Gerenciamento de Telas: Um conjunto de funções (exibirTelaRegistro, exibirTelaPlacar, exibirTelaCraque, exibirSelecaoAcao) que são responsáveis por renderizar o conteúdo específico de cada tela no display LCD.

•
atualizarDisplay(): Função central que limpa o LCD e chama a função de exibição da tela atual.

•
setup(): Função de inicialização do Arduino, onde o LCD é configurado, os pinos dos botões são definidos como INPUT_PULLUP e o jogo é resetado e o display atualizado pela primeira vez.

•
loop(): A função principal que executa continuamente. Ela monitora o estado dos botões, processa as interações do usuário (seleção de jogadoras, registro de pontos, troca de telas) e atualiza o display conforme a lógica do jogo.

