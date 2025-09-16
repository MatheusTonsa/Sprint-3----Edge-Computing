Projeto Wokwi: Sistema de Registro de Gols e Assistências


Nome: [Seu Nome Completo]
RM: [Seu RM]




Este repositório contém o código e o diagrama de um projeto desenvolvido no Wokwi, que simula um sistema para registrar gols e assistências de jogadoras utilizando um ESP32, botões e um display LCD I2C.

Visão Geral do Projeto

O projeto simula um placar interativo onde é possível registrar assistências e gols para diferentes jogadoras. Ele utiliza um ESP32 como microcontrolador, um display LCD 20x4 para exibir as informações e quatro botões para interação (seleção de jogadora, seleção de ação e registro).

Componentes Utilizados

•
ESP32 DevKitC V4

•
Display LCD 20x4 (I2C)

•
4x Botões Pushbutton (Amarelo, Azul, Vermelho, Cinza)

Diagrama de Conexão

Abaixo está o diagrama de conexão do projeto, conforme visualizado no Wokwi:







Como Usar no Wokwi

1.
Acesse o projeto no Wokwi: https://wokwi.com/projects/442264817239768065

2.
Inicie a simulação.

3.
Utilize os botões para interagir com o sistema:

•
Botão Cinza (BTN_MENU): Alterna entre as telas (Registro, Placar, Craque).

•
Botão Amarelo (BTN_A): Na tela de Registro, seleciona a jogadora. Na tela de Placar, rola a lista de jogadoras.

•
Botão Azul (BTN_B): Na tela de Registro, alterna entre registrar 'Assistência' e 'Gol' para a jogadora selecionada.

•
Botão Vermelho (BTN_C): Na tela de Registro, registra a ação (Assistência ou Gol) para a jogadora selecionada.



Código Fonte

#include <Wire.h>
#include <LiquidCrystal_I2C.h>
// --- CONFIGURAÇÃO ---
LiquidCrystal_I2C lcd(0x27, 20, 4);
#define BTN_A 12
#define BTN_B 13
#define BTN_C 14
#define BTN_MENU 32
// --- ESTRUTURAS E VARIÁVEIS (PARA 7 JOGADORAS) ---
const int NUM_JOGADORAS = 7;
struct StatsJogadora {
  int assistencias;
  int gols;
};
StatsJogadora jogadoras[NUM_JOGADORAS];
const char* nomesJogadoras[] = {
  "JOGADORA A", "JOGADORA B", "JOGADORA C", "JOGADORA D",
  "JOGADORA E", "JOGADORA F", "JOGADORA G"
};
const char* nomesAcoes[] = {"ASSISTENCIA", "GOL"};
enum Tela { TELA_REGISTRO, TELA_PLACAR, TELA_CRAQUE };
Tela telaAtual = TELA_REGISTRO;
// Variáveis para o menu de seleção com rolagem
int cursorSelecao = 0;       // Posição do cursor na lista inteira (0 a 6)
int scrollOffset = 0;        // Qual jogadora está no topo da tela
bool emSelecaoDeAcao = false;
int jogadoraDaVez = -1;
// Variáveis de debounce e reset
unsigned long ultimoTempoBtnA = 0, ultimoTempoBtnB = 0, ultimoTempoBtnC = 0, ultimoTempoBtnMenu = 0;
unsigned long tempoMenuPressionado = 0;
const long intervaloDebounce = 250;
const long tempoParaReset = 3000;
// --- FUNÇÕES BÁSICAS ---
bool debounceRead(int pino, unsigned long &ultimoTempo) {
  if (digitalRead(pino) == LOW && (millis() - ultimoTempo) > intervaloDebounce) {
    ultimoTempo = millis();
    return true;
  }
  return false;
}
void setup() {
  Serial.begin(115200);
  Serial.println("Iniciando...");
  lcd.init();
  lcd.backlight();
  pinMode(BTN_A, INPUT_PULLUP);
  pinMode(BTN_B, INPUT_PULLUP);
  pinMode(BTN_C, INPUT_PULLUP);
  pinMode(BTN_MENU, INPUT_PULLUP);
  // Inicializa as estatísticas das jogadoras
  for (int i = 0; i < NUM_JOGADORAS; i++) {
    jogadoras[i].assistencias = 0;
    jogadoras[i].gols = 0;
  }
  exibirTela(telaAtual);
}
void loop() {
  if (debounceRead(BTN_MENU, ultimoTempoBtnMenu)) {
    if (telaAtual == TELA_REGISTRO) {
      telaAtual = TELA_PLACAR;
    } else if (telaAtual == TELA_PLACAR) {
      telaAtual = TELA_CRAQUE;
    } else {
      telaAtual = TELA_REGISTRO;
    }
    exibirTela(telaAtual);
  }
  if (telaAtual == TELA_REGISTRO) {
    handleRegistro();
  } else if (telaAtual == TELA_PLACAR) {
    handlePlacar();
  } else if (telaAtual == TELA_CRAQUE) {
    handleCraque();
  }
}
void exibirTela(Tela tela) {
  lcd.clear();
  switch (tela) {
    case TELA_REGISTRO:
      lcd.setCursor(0, 0);
      lcd.print("REGISTRO");
      break;
    case TELA_PLACAR:
      lcd.setCursor(0, 0);
      lcd.print("PLACAR");
      break;
    case TELA_CRAQUE:
      lcd.setCursor(0, 0);
      lcd.print("CRAQUE");
      break;
  }
}
void handleRegistro() {
  // Lógica para registrar assistências e gols
  if (debounceRead(BTN_A, ultimoTempoBtnA)) {
    // Seleciona jogadora
    emSelecaoDeAcao = false;
    jogadoraDaVez = (jogadoraDaVez + 1) % NUM_JOGADORAS;
    exibirJogadoraRegistro(jogadoraDaVez);
  }
  if (jogadoraDaVez != -1) {
    if (debounceRead(BTN_B, ultimoTempoBtnB)) {
      // Seleciona ação (assistência/gol)
      emSelecaoDeAcao = !emSelecaoDeAcao;
      exibirJogadoraRegistro(jogadoraDaVez);
    }
    if (debounceRead(BTN_C, ultimoTempoBtnC)) {
      // Registra ação
      if (emSelecaoDeAcao) {
        jogadoras[jogadoraDaVez].gols++;
      } else {
        jogadoras[jogadoraDaVez].assistencias++;
      }
      exibirJogadoraRegistro(jogadoraDaVez);
    }
  }
}
void exibirJogadoraRegistro(int index) {
  lcd.setCursor(0, 1);
  lcd.print("                "); // Limpa a linha
  lcd.setCursor(0, 1);
  lcd.print(nomesJogadoras[index]);
  lcd.setCursor(0, 2);
  lcd.print("A: ");
  lcd.print(jogadoras[index].assistencias);
  lcd.print(" G: ");
  lcd.print(jogadoras[index].gols);
  lcd.setCursor(0, 3);
  lcd.print(emSelecaoDeAcao ? "GOL" : "ASSISTENCIA");
}
void handlePlacar() {
  // Exibe o placar atual
  // Lógica de rolagem
  if (debounceRead(BTN_A, ultimoTempoBtnA)) {
    scrollOffset = (scrollOffset + 1) % NUM_JOGADORAS;
  }
  exibirPlacar(scrollOffset);
}
void exibirPlacar(int offset) {
  lcd.setCursor(0, 1);
  lcd.print("                ");
  lcd.setCursor(0, 1);
  lcd.print(nomesJogadoras[offset]);
  lcd.setCursor(0, 2);
  lcd.print("A: ");
  lcd.print(jogadoras[offset].assistencias);
  lcd.print(" G: ");
  lcd.print(jogadoras[offset].gols);
}
void handleCraque() {
  // Encontra a jogadora com mais gols
  int craqueIndex = 0;
  for (int i = 1; i < NUM_JOGADORAS; i++) {
    if (jogadoras[i].gols > jogadoras[craqueIndex].gols) {
      craqueIndex = i;
    }
  }
  lcd.setCursor(0, 1);
  lcd.print("                ");
  lcd.setCursor(0, 1);
  lcd.print("CRAQUE: ");
  lcd.print(nomesJogadoras[craqueIndex]);
  lcd.setCursor(0, 2);
  lcd.print("Gols: ");
  lcd.print(jogadoras[craqueIndex].gols);
}



O código-fonte principal (sketch.ino) está incluído neste repositório e pode ser visualizado abaixo:

