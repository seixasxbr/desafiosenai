# Desafio Robótica
#### Candidato: Mateus Zarth Seixas
## Descrição da Solução
# ![image](https://github.com/seixasxbr/desafiosenai/blob/main/banner.png)
O objetivo desse desafio é fazer com que o robô se desloque do local marcado como início do ambiente simulacional e alcance a região marcada como stop em 2 minutos.
O robô escolhido para o desafio é o Pioneer 3-dx que conta com 16 sensores de distância, sendo 8 deles apontados para a frente e 8 apontados para trás.
Na região de chegada do robô existe uma fonte de luz que será utilizada pelo robô para identificar que ele alcançou seu objetivo. Para isso, será integrado ao topo do robô
um sensor de luz.
#### Controlador
O controlador utilizado para levar o robô da região de início para a região de chegada é baseado em uma máquina de estados e tem a função de fazer com que o robô se desloque pela sua trajetória evitando colidir com objetos em sua direção. Para isso ele utiliza os 8 sensores frontais. As informações sensoriais são processadas para calcular duas variáveis, uma referente aos sensores voltados para esquerda (wheel_weight_total[0]) e uma para os sensores voltados para a direita (wheel_weight_total[1]), que são resultado da soma das informações referentes a cada sensor ponderadas pela sua posição (sensores mais voltados para a frente do robô tem mais peso). Essas variáveis servem para avaliar a proximidadade dos obstáculos com a trajetória do robô e fazer com que o robô decida seu estado.

# ![image](https://github.com/seixasxbr/desafiosenai/blob/main/MACHINE.PNG)
Ele se inicia no estado FOWARD, em que ele está andando com determinada velocidade para a frente. Se o sensor de luz detectar um sinal acima de um limite, constatando a proximidade da fonte de luz e sua chegada ao objetivo, ele começa a frear e entra no estado de PARA.
Se ele encontrar um objeto na sua trajetória a sua esquerda, detectado quando wheel_weight_total[0] estiver acima de um limite, ele começa a girar no sentido horário e entra no estado LEFT. Caso encontre um objeto a sua direita, detectado quando wheel_weight_total[1] estiver acima de um limite, ele começa a rodar no sentido anti-horário e entra no estado LEFT. 

No estado RIGHT ele continua rodando no sentido horário até encontrar um trajeto livre, começa a andar para a frente e retorna para o estado FOWARD.

No estado LEFT ele continua rodando no sentido anti-horário até encontrar um trajeto livre, começa a andar para a frente e retorna para o estado FOWARD.

No estado de PARA ele continua freando até parar completamente. Se ele voltar a não detectar a presença da fonte de luz com o sensor de luz ele volta pro estado de FOWARD.

#### Resultado
O robô conseguiu alcançar o seu objetivo em 1 minuto e 4 segundos, como mostrado no vídeo contído nesse repositório.

##### OBS : É necessário iniciar o controlador no world que está neste repositório, pois é necessária adicionar o sensor de luz.
