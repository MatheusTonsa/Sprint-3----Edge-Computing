# Sistema de Registro e Pontuação de Jogadoras com LCD I2C

## Equipe

| Nome | Matrícula / ID |
|------|------------------|
| Seu Nome | Seu ID |

---

## Sobre o Projeto

Este projeto simula um sistema para registrar estatísticas de jogadoras (gols e assistências), exibir placar, e determinar a “craque da partida”, usando um display LCD I2C e botões.  
Ele foi implementado e testado no simulador **Wokwi** com Arduino (ou microcontrolador compatível).

---

## Arquitetura e Funcionamento

- **Hardware / Simulação**: Wokwi com LCD I2C (endereço 0x27, 20x4), botões definidos como entradas com `INPUT_PULLUP`.  
- **Estrutura de dados**:  
  - Array de jogadoras, cada uma com estatísticas de gol e assistência.  
  - Enumeração de telas: Registro, Placar, e Craque.  
- **Interação / Botões**:  
  - `BTN_A`, `BTN_B`, `BTN_C` para navegar e confirmar escolhas.  
  - `BTN_MENU` para alternar telas ou resetar as estatísticas se mantido pressionado por certo tempo.  
- **Telas**:  
  1. Tela de Registro: escolher jogadora e ação (gol ou assistência).  
  2. Tela de Placar: visualizar todos os placares com rolagem.  
  3. Tela Craque da Partida: calcula com base numa fórmula simples (2×gols + assistências) para escolher a melhor.

---

## Tecnologias / Bibliotecas

- Arduino / linguagem C++  
- Biblioteca `Wire.h`  
- Biblioteca `LiquidCrystal_I2C`  

---

## Como Executar

1. Clonar este repositório  
   ```bash
   git clone https://github.com/seu_usuario/seu_repositorio.git
