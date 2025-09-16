🎮 Contador de Pontos para Jogo com ESP32 e LCD I2C

📝 Descrição do Projeto

Este projeto implementa um sistema de contagem de pontos para um jogo, utilizando um microcontrolador ESP32, um display LCD I2C de 20x4 caracteres e quatro botões de pressão. O sistema foi desenvolvido para ser uma ferramenta simples e eficaz para registrar e acompanhar o desempenho de jogadoras em tempo real. Ele permite registrar gols e assistências para até 7 jogadoras, exibir o placar geral e identificar a "Craque do Jogo" com base nas estatísticas.

🏛️ Arquitetura Proposta

A arquitetura do projeto é baseada em um sistema embarcado simples, onde o ESP32 DevKitC V4 atua como o cérebro central, processando a lógica do jogo e gerenciando as interações com o usuário. O display LCD I2C é a interface de saída para exibir as informações, enquanto os quatro botões de pressão servem como interface de entrada para a navegação e registro de eventos.

Diagrama de Conexão (Wokwi)

O projeto foi simulado na plataforma Wokwi, e o arquivo diagram.json descreve a montagem do hardware e as conexões elétricas. O ESP32 se comunica com o LCD via protocolo I2C, e os botões são conectados a pinos GPIO específicos, configurados com INPUT_PULLUP para simplificar o circuito.

•
ESP32 DevKitC V4: Microcontrolador principal.

•
Display LCD 20x4 I2C: Conectado aos pinos SDA (GPIO21) e SCL (GPIO22) do ESP32.

•
Botões de Pressão:

•
🟡 Amarelo (BTN_A): Conectado ao pino GPIO13 do ESP32.

•
🔵 Azul (BTN_B): Conectado ao pino GPIO14 do ESP32.

•
🔴 Vermelho (BTN_C): Conectado ao pino GPIO12 do ESP32.

•
⚪ Cinza (BTN_MENU): Conectado ao pino GPIO32 do ESP32.



Todos os botões são conectados ao GND através do outro terminal.

📦 Recursos Necessários

Hardware

•
ESP32 DevKitC V4

•
Display LCD 20x4 I2C

•
4 Botões de Pressão (Amarelo, Azul, Vermelho, Cinza)

•
Fios de conexão (jumpers)

Software

•
Arduino IDE (ou ambiente de desenvolvimento compatível com ESP32)

•
Biblioteca LiquidCrystal I2C

•
Plataforma de simulação Wokwi (opcional, para simulação online)

🚀 Instruções de Uso

1. Configuração do Ambiente

1.
Certifique-se de ter a Arduino IDE instalada e configurada para o ESP32.

2.
Instale a biblioteca LiquidCrystal I2C através do Gerenciador de Bibliotecas da Arduino IDE.

2. Carregando o Código

1.
Abra o arquivo sketch.ino na Arduino IDE.

2.
Conecte seu ESP32 ao computador.

3.
Selecione a placa e a porta COM corretas na Arduino IDE.

4.
Faça o upload do código para o ESP32.

3. Simulação no Wokwi (Alternativa)

1.
Acesse o projeto no Wokwi: https://wokwi.com/projects/442264817239768065

2.
Clique no botão verde "Iniciar Simulação" (ícone de play ▶️).

3.
Utilize os botões virtuais no diagrama para interagir com o sistema:

•
🟡 BTN_A (Amarelo): Seleciona uma jogadora ou confirma a ação (gol/assistência).

•
🔵 BTN_B (Azul): Move o cursor para cima na lista de jogadoras ou alterna entre as opções de ação (Gol/Assistência).

•
🔴 BTN_C (Vermelho): Move o cursor para baixo na lista de jogadoras ou alterna entre as opções de ação (Gol/Assistência).

•
⚪ BTN_MENU (Cinza): Troca as telas do menu (Registro, Placar, Craque do Jogo). Uma pressão longa (aproximadamente 3 segundos) neste botão reinicia todas as estatísticas do jogo.



💻 Código-Fonte

O código-fonte principal do projeto está no arquivo sketch.ino, que gerencia toda a lógica do contador de pontos, a interação com os botões e a exibição no LCD.

👥 Alunos

Nome CompletoRM[Seu Nome Aqui][Seu RM Aqui][Nome do Aluno 2][RM do Aluno 2][Nome do Aluno 3][RM do Aluno 3][Nome do Aluno 4][RM do Aluno 4][Nome do Aluno 5][RM do Aluno 5]

