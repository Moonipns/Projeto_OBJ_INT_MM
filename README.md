# Projeto_OBJ_INT_MM
Objetos Inteligentes Conectados - Luminária reativa a música

## Resumo
O presente projeto consiste no desenvolvimento de uma luminária reativa a música com o uso de um hardware denominado Arduino. A luminária é composta por microfones e LEDs RGB que respondem aos sons do ambiente, criando um efeito visual dinâmico e único. O projeto envolve a conexão do circuito, o processamento de áudio, o controle dos LEDs, a construção da luminária e ajustes para garantir um bom desempenho e a conexão wifi via MQTT. Além de ser uma opção interessante para decoração de festas e eventos, a criação de uma luminária reativa à música pode ser uma forma divertida e educativa para quem deseja aprender mais sobre eletrônica, programação e a integração de tecnologias em objetos do cotidiano.

## Introdução
A tecnologia tem possibilitado a criação de diversas soluções criativas e inovadoras, e uma dessas soluções é a criação de luminárias reativas a música com o uso do Arduino (ARAUJO, 2018; KOUICI et al., 2021). Com o avanço dos dispositivos eletrônicos, tornou-se possível integrar microfones e LEDs RGB em uma luminária para que ela possa responder aos sons do ambiente em que está inserida, criando um efeito visual único e dinâmico (JUNIOR, 2010; PARREIRA et al., 2017). Nesse contexto, a criação de uma luminária de mesa reativa a música com Arduino pode ser um projeto interessante para quem busca unir eletrônica, programação e design (FERREIRA, 2015; BANZI; SHILLOV, 2015). A luminária reativa à música pode ser uma opção para decoração de festas e eventos, bem como para uso doméstico, tornando-se um elemento diferenciado e interativo em diferentes espaços (MENDONÇA et al., 2019). Além disso, esse tipo de projeto pode ser uma forma divertida e educativa para quem deseja aprender mais sobre eletrônica, programação e a integração de tecnologias em objetos do cotidiano.

## Materiais e Métodos
O desenvolvimento de uma luminária reativa a música é composto por componentes de hardware e software.
### Como componentes de hardware forão utilizados:
•	Arduino Nano (REV3.0): é uma placa de desenvolvimento eletrônico compacta e versátil baseada no microcontrolador ATmega328P. Ele possui 22 pinos de entrada/saída digitais, 8 pinos de entrada analógica, 14 pinos PWM (Pulse Width Modulation) e uma frequência de clock de 16 MHz. Além disso, também possui um microcontrolador USB-serial integrado que permite a comunicação com um computador por meio de uma porta USB. Essa comunicação permite que o usuário envie programas para o Arduino e receba dados de sensores conectados à placa. A placa também inclui um regulador de tensão de 5V e 3.3V, o que permite que ela seja alimentada por meio de uma fonte de alimentação externa ou por meio da porta USB (ELETROGATE, 2022).  
•	Placa com ESP8266 (nodeMCU): placa microcontroladora que realiza comunicação WiFi (LOCATELLI, 2020).
•	Módulo detector de som (LM393): é o componente que capta o sinal de áudio e o envia para o Arduino. Pode ser um microfone ou uma entrada de áudio (INSTRUCATABLES, 2017).
•	Tiras de LED endereçáveis (WS2812B) individualmente 60 leds por metro: são fitas de LED compostas por vários LEDs individuais controláveis, comumente utilizadas em projetos de iluminação. As tiras de LED são conectadas ao Arduino e programadas para mudar de cor de acordo com o sinal de áudio (INSTRUCATABLES, 2017).
•	Fonte de alimentação de 5 volts: é responsável por fornecer energia para o Arduino e para as tiras de LED (INSTRUCATABLES, 2017).
•	Pequeno pedaço de tubo de PVC: neste material serão envolvidas as tiras de LED a serem colocadas na luminária (INSTRUCATABLES, 2017).
•	Recipiente de vidro ou plástico redondo 600ml: estrutura da luminária (INSTRUCATABLES, 2017).
### Como componentes de software forão utilizados:
•	Arduino IDE: é o ambiente de desenvolvimento integrado (IDE) utilizado para programar o Arduino. Permite escrever e compilar o código, enviar o programa para a placa e monitorar a execução (QUINTINO, 2021). Nele será construído o código que irá definir o comportamento da luminária, realizando a leitura do sinal de áudio e a alteração da cor dos LEDs com a biblioteca FastLED que controla as tiras de LED endereçáveis, possui funções para ajustar a cor e a intensidade dos LEDs, bem como para animar as mudanças de cores. Além disso, nele será realizada a programação para conexão MQTT com a instalação das bibliotecas PubSubClient e WiFiClient.
•	CloudMQTT: Servidor broker responsável por receber as mensagens dos dispositivos, roteá-las para os destinatários corretos e manter um registro das mensagens enviadas e recebidas. Atua como um canal de comunicação para dispositivos IoT (Internet das Coisas) que utilizam o protocolo MQTT (SOUZA, 2018).

### Os métodos para o desenvolvimento deste projeto podem ser divididos em três etapas:

1. Conexão dos componentes
O módulo de som deve ser conectado ao Arduino através de um pino de entrada analógica: o VIN é conectado no Arduino e na placa do detector de som à entrada positiva. Em seguida, é conectado o GND no Arduino e o detector ao negativo. É preciso conectar a entrada positiva e negativa na faixa de LED à fonte de alimentação (INSTRUCATABLES, 2017).
Após conectar as três partes à energia, é necessário conectá-las umas às outras. O módulo detector de som se comunicará com o Arduino através dos pinos de entrada analógica, será utilizado o pino de número 0 (INSTRUCATABLES, 2017).
A placa ESP8266 tem alguns pinos que precisam ser conectados ao Arduino Nano para que as duas placas possam se comunicar. Esses pinos são (CURVELLO, 2015):
•	RX (Receber): Este pino é usado para receber dados do Arduino Nano e deve ser conectado ao pino TX do Arduino Nano.
•	TX (Transmitir): Este pino é usado para transmitir dados para o Arduino Nano e deve ser conectado ao pino RX do Arduino Nano.
•	GND: Este pino é usado para fornecer um ponto de referência comum para os sinais entre as duas placas e deve ser conectado ao GND do Arduino Nano.
•	VCC: Este pino é usado para fornecer energia à placa ESP8266. O Arduino Nano não é capaz de fornecer energia suficiente para alimentar a placa ESP8266, portanto, é necessário fornecer energia externa a partir de uma fonte de alimentação USB ou outra fonte externa.
Para conectar a placa ESP8266 ao Arduino Nano, é utilizado um cabo jumper (fios) para fazer as conexões adequadas entre as duas placas. O cabo jumper deve ser conectado ao pino RX do ESP8266 e ao pino TX do Arduino Nano, e ao pino TX do ESP8266 e ao pino RX do Arduino Nano. O GND da placa ESP8266 deve ser conectado ao GND do Arduino Nano também (SOUZA, 2018).
As fitas de LED precisam de um pulso digital para poder entender qual LED é desejado abordar. Portanto, é necessário conectar um pino de saída digital ao Arduino nano, será utilizado o pino de número 6. Desta forma, a parte eletrônica estará finalizada (INSTRUCATABLES, 2017).

2. Programação do Arduino
Depois de conectar os componentes, o próximo passo é programar o Arduino, a programação será realizada no software Arduino IDE e enviada para o Arduino. Nesta etapa, o princípio principal é mapear o valor analógico que é obtido do sensor para uma quantidade de LEDs a serem exibidos. Para isso, será utilizada a função map, que permitirá exibir uma certa quantidade de LEDs dada uma entrada. É realizado um rastreamento mais avançado da intensidade da música/som com base em médias, para permitir que a luz mude de cor quando a música entra em um pico (INSTRUCATABLES, 2017).
Para acionamento da luminária, é necessário configurar um broker MQTT, no projeto será utilizado o CloudMQTT que gerencia um servidor Mosquitto na nuvem, nele será criada uma instância para registro das informações necessárias para conexão com o Broker: Server, User, Password e Port, essas informações serão utilizadas no código do ESP8266 (SOUZA, 2018).
Por fim, é construído o código apropriado para a placa ESP8266 na IDE do Arduino e carrega-se na placa contendo as informações do CloudMQTT. No software Arduino IDE é necessário importar as bibliotecas PubSubClient e WiFiClient para utilização do módulo (CURVELLO, 2015).

3. Montagem da estrutura
Com todo o código e os componentes prontos será iniciada a etapa de montagem da luminária. O cano de PVC é oco e serão inseridos componentes eletrônicos por dentro. Será realizada uma fenda no tubo de PVC para permitir deslizar a tira sem obstruir a superfície nivelada do orifício do PVC. Posteriormente, será colada a fita de LED no tubo de PVC (INSTRUCATABLES, 2017). Na base do recipiente utilizado como estrutura da luminária serão inseridos os componentes eletrônicos e assim a luminária estará pronta para utilização (INSTRUCATABLES, 2017).


