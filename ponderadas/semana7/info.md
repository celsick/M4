# Informações gerais da ponderada realizada em sala

## Resumo

Este documento descreve um projeto de Internet das Coisas (IoT) focado na **aquisição e visualização em tempo real** da Intensidade do Sinal Recebido (RSSI, *Received Signal Strength Indicator*) de uma rede Wi-Fi. Utilizando o microcontrolador **ESP32**, os dados são coletados e transmitidos via protocolo **MQTT** para o serviço de nuvem Adafruit IO, onde são apresentados em um painel dinâmico. O sistema foi validado através de testes práticos que simulam a atenuação do sinal em um ambiente blindado (Efeito Gaiola de Faraday).

---

## Detalhes da Implementação Técnica

### I. Plataformas e Protocolos Chave

| Elemento | Descrição e Função |
| :--- | :--- |
| **Hardware Principal** | ESP32 (Microcontrolador com WiFi Integrado) |
| **Protocolo de Transporte** | MQTT (Message Queuing Telemetry Transport) |
| **Serviço de Nuvem (Cloud)** | Adafruit IO (Broker MQTT e Dashboard) |
| **Variável Monitorada** | RSSI (Medido em **dBm**) |

### II. Roteiro Operacional

O ciclo de funcionamento do sistema compreende três etapas principais executadas continuamente:

1.  **Conectividade:** O módulo ESP32 estabelece a comunicação com o ponto de acesso Wi-Fi configurado.
2.  **Captura de Dados:** Uma rotina interna mede a força do sinal (*RSSI*) em intervalos de tempo pré-definidos (tipicamente a cada segundo).
3.  **Publicação:** O dado de RSSI é empacotado e enviado de forma assíncrona para o *feed* MQTT da Adafruit IO.

---

## Validação e Resultados Práticos

O sistema foi submetido a um teste de campo para comprovar sua capacidade de registrar mudanças ambientais abruptas na propagação do sinal eletromagnético.

### Cenário de Teste: Gaiola de Faraday

O experimento utilizou um elevador como **ambiente de blindagem metálica**, simulando uma gaiola de Faraday para induzir a máxima atenuação do sinal.

* **Status Inicial:** O ESP32 inicia a operação mostrando conectividade estável com a rede (ex: RSSI em torno de -65 dBm).
* **Indução de Atenuação (Entrada no Elevador):** Ao entrar na cabine do elevador, a blindagem metálica causa uma **queda abrupta e significativa** na potência do sinal. Isso é imediatamente refletido no painel de controle (*Dashboard*), onde a linha do gráfico despenca.
* **Perda/Restauração:** Durante o período dentro do elevador, pode haver uma perda temporária da conexão MQTT devido ao RSSI cair para níveis não operacionais (ex: abaixo de -90 dBm).
* **Recuperação (Saída do Elevador):** Ao sair do ambiente blindado, o sinal de rádio é **instantaneamente restaurado**. O ESP32 retoma a publicação no MQTT, e o gráfico online registra o retorno do RSSI aos níveis normais de operação.

### Visualização dos Dados

A **Dashboard da Adafruit IO** serve como a interface de análise, apresentando o gráfico **Tempo × RSSI**. Este gráfico registra de forma visual e inconfundível o "vale" ou interrupção durante o período de atenuação no elevador, confirmando o registro bem-sucedido do evento.