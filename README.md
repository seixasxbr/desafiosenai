# Desafio Senai
#### Candidato: Mateus Seixas
## Descrição da Solução
O objetivo desse desafio é fazer com que o robô se desloque do local marcado como início do ambiente simulacional e alcance a região marcada como fim.
O robô escolhido para o desafio é o Pioneer 3-dx que conta com 16 sensores de distância, sendo 8 deles apontados para a frente e 8 apontados para trás.
Na região de chegada do robô existe uma fonte luminosa que será utilizada pelo robo para identificar que ele alcançou seu objetivo. Para isso será integrado ao robô
um sensor de luz no seu topo.
#### Controlador
O controlador utilizado para levar o robô da região de início para a região de chegada é um controlador que tem a função de fazer com que o robô se desloque por sua trajetória
evitando colidir com objetos em sua direção. Para isso ele utiliza os 8 sensores frontais. As informações sensoriais são processadas para calcular a distância dos obstáculos para 
cada sensor, em seguida são dados pesos para cada sensor para o cáculo de duas variáveis, uma referente aos sensores voltados para esquerda e uma para os sensores voltados 
para a direita, para avaliar a aproximação dos objetos na sua trajetória e calcular a decisão de continaur seguindo reto, virar para um lado ou para o outro.

O funcionamento do robô se baseia em uma máquina de estados. 

Ele se inicia no estado FOWARD, em que ele está andando para frente com determinada velocidade. Se o sensor de luz detectar um sinal a cima de um limete,
o robô entra no estado de PARA e começa a freiar. Se ele encontrar
um objeto na sua trajetória a sua esquerda, ele começa a girar no sentido horário e entra no estado RIGHT. Caso encontro um objeto a sua direita ele começa a rodar no sentido
anti-horário e entra noe stado LEFT. 

No estado RIGHT ele continua rodando no sentido horário até encontrar um trajeto livre e retorna para o estado FOWARD.

No estado LEFT ele continua rodando no sentido anti-horário até encontrar um trajeto livre e retorna para o estado FOWARD.

No estado de PARA ele continua freando até parar completamente. Se o sensor de luz voltar a nãod etectar sinais a cima do limite ele volta pro estado de FOWARD.
