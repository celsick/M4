## Projeto de Monitoramento Contínuo de Intensidade de Sinal Wi-Fi (RSSI) usando ESP32 e MQTT

### Objetivo Geral

O objetivo principal deste projeto foi desenvolver e validar um sistema de **Internet das Coisas (IoT)** capaz de **monitorar dinamicamente a potência do sinal Wi-Fi (RSSI)**, expressa em dBm, utilizando o microcontrolador **ESP32**. A demonstração prática buscou registrar em tempo real a influência de um ambiente com blindagem eletromagnética (simulação de gaiola de Faraday) na conectividade e na força do sinal.

---

### 🔗 Demonstração em Vídeo

[Assista ao vídeo completo da atividade](https://drive.google.com/)

---

### Configuração de Materiais e Métodos

#### 1. Hardware Utilizado

| Componente | Função no Projeto |
| :--- | :--- |
| **Microcontrolador** | ESP32 |
| **Ponto de Acesso** | Hotspot móvel (Celular) em 2.4 GHz |
| **Ambiente de Teste** | Elevador (Simulação de Gaiola de Faraday) |
| **Interface** | Notebook com Arduino IDE |

#### 2. Software e Serviços

* **Ambiente de Desenvolvimento:** Arduino IDE.
* **Protocolo de Comunicação:** Biblioteca **PubSubClient** (MQTT).
* **Plataforma Cloud:** **Adafruit IO**, configurada com um *broker* MQTT e uma *dashboard* para visualização gráfica.

#### 3. Princípio de Funcionamento

O firmware do ESP32 realiza as seguintes ações a cada segundo:

1.  Estabelece conexão com o ponto de acesso Wi-Fi.
2.  Obtém o valor da intensidade do sinal (**RSSI**) utilizando a função `WiFi.RSSI()`.
3.  Publica o valor lido no *feed* MQTT correspondente na Adafruit IO.
4.  Permite a exibição em tempo real do gráfico na *dashboard*.

---

### Resultados da Demonstração Prática

O vídeo documenta a jornada de teste, confirmando o sucesso do sistema em registrar as variações ambientais.

#### 1. Inicialização do Sistema e Conexão

O **Monitor Serial** valida o início da comunicação, exibindo valores típicos e confirmando a atividade: