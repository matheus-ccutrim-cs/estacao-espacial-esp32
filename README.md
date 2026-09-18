# Monitor de Temperatura com ESP32

Projeto desenvolvido com **VS Code + PlatformIO + Wokwi Simulator**, sem MQTT. A aplicação monitora a temperatura localmente e apresenta o resultado em um display LCD e no Monitor Serial.

## Objetivo

Criar um sistema embarcado capaz de ler a temperatura, classificar a situação e alertar o usuário quando o valor estiver fora dos limites definidos.

## Componentes

- ESP32 DevKit V1
- Sensor analógico de temperatura NTC
- Display LCD 16x2 I2C
- 3 LEDs: verde, amarelo e vermelho
- 3 resistores de 220 ohms
- Buzzer
- Botão de pressão

## Funcionamento

| Condição | Estado | Ação |
|---|---|---|
| Temperatura abaixo de 30 °C | Normal | LED verde |
| Temperatura entre 30 °C e 34,9 °C | Atenção | LED amarelo |
| Temperatura igual ou acima de 35 °C | Crítico | LED vermelho e buzzer |

O botão azul silencia o buzzer durante 30 segundos. As medições são atualizadas a cada 2 segundos. Nenhum dado é enviado para a internet.

## Pinos utilizados

| Componente | Pino do ESP32 |
|---|---:|
| Sensor NTC – saída analógica | GPIO 34 |
| LCD – SDA | GPIO 21 |
| LCD – SCL | GPIO 22 |
| LED verde | GPIO 25 |
| LED amarelo | GPIO 26 |
| LED vermelho | GPIO 27 |
| Buzzer | GPIO 14 |
| Botão | GPIO 13 |

## Como executar

1. Instale o VS Code.
2. No VS Code, instale as extensões **PlatformIO IDE** e **Wokwi Simulator**.
3. Extraia o arquivo ZIP deste projeto.
4. No PlatformIO, escolha **Open Project** e selecione a pasta `estacao-ambiental-esp32`.
5. Aguarde a instalação automática da biblioteca do LCD definida em `platformio.ini`.
6. Clique em **Build** na barra inferior do PlatformIO.
7. Abra a paleta de comandos com `Ctrl+Shift+P`.
8. Execute **Wokwi: Start Simulator**.
9. Clique no sensor NTC durante a simulação para mudar a temperatura.
10. Observe o LCD, os LEDs, o buzzer e o Monitor Serial.

## Testes sugeridos

1. Configure 27 °C: deve acender o LED verde.
2. Configure 32 °C: deve acender o LED amarelo.
3. Configure 38 °C: LED vermelho e buzzer devem ser ativados.
4. Em estado crítico, pressione o botão azul: o som deve parar por 30 segundos.

## Estrutura do projeto

```text
estacao-ambiental-esp32/
├── diagram.json       # circuito do Wokwi
├── platformio.ini     # configuração e bibliotecas
├── wokwi.toml         # firmware usado pelo simulador
├── src/
│   └── main.cpp       # código principal
└── README.md          # documentação
```

## Resumo do projeto

A aplicação é um monitor de temperatura baseado em ESP32. O sensor NTC realiza uma leitura analógica a cada dois segundos. O programa classifica a temperatura em normal, atenção ou crítico. O resultado aparece no LCD e é representado pelos LEDs. Em uma situação crítica, o buzzer é acionado, mas pode ser silenciado pelo botão por 30 segundos. O sistema não usa MQTT nem depende de conexão com a internet.
