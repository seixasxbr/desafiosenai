# Desafio Senai
#### Candidato: Mateus Zarth Seixas
## Descrição da Solução
O objetivo desse desafio é fazer com que o robô se desloque do local marcado como início do ambiente simulacional e alcance a região marcada como fim.
O robô escolhido para o desafio é o Pioneer 3-dx que conta com 16 sensores de distância, sendo 8 deles apontados para a frente e 8 apontados para trás.
Na região de chegada do robô existe uma fonte de luz que será utilizada pelo robo para identificar que ele alcançou seu objetivo. Para isso será integrado ao robô
um sensor de luz no seu topo.
#### Controlador
O controlador utilizado para levar o robô da região de início para a região de chegada é baseado em uma máquina de estados e tem a função de fazer com que o robô se desloque pela sua trajetória evitando colidir com objetos em sua direção. Para isso ele utiliza os 8 sensores frontais. As informações sensoriais são processadas para calcular duas variáveis, uma referente aos sensores voltados para esquerda e uma para os sensores voltados para a direita, que são resultado da soma das informações referentes a cada sensor ponderadas pela sua posição (sensores mais voltados para a frente do robô tem mais peso). Essas variáveis servem para avaliar a proximidadade dos obstáculos com a trajetória do robô e fazer com que o robô decida seu estado.

Ele se inicia no estado FOWARD, em que ele está andando com determinada velocidade para a frente. Se o sensor de luz detectar um sinal acima de um limite, constatando a proximidade com a fonte de luz e sua chegada ao objetivo, ele começa a frear e entra no estado de PARA.
Se ele encontrar um objeto na sua trajetória a sua esquerda, detectado quando a variável referente aos sensores da esquerda estiver acima de um limite, ele começa a girar no sentido horário e entra no estado LEFT. Caso encontro um objeto a sua direita ele começa a rodar no sentido
anti-horário e entra no estado LEFT. 

No estado RIGHT ele continua rodando no sentido horário até encontrar um trajeto livre e retorna para o estado FOWARD.

No estado LEFT ele continua rodando no sentido anti-horário até encontrar um trajeto livre e retorna para o estado FOWARD.

No estado de PARA ele continua freando até parar completamente. Se ele voltar a não detectar a presença da fonte de luz com o sensor de luz ele volta pro estado de FOWARD.
