# SD-ControleConcorrenciaJava-

### 1. Carro.java
No arquivo Carro.java, o controle de vagas é feito com um objeto. Isso significa que existe um contador global de vagas, e esse valor corresponde a quantos carros podem acessar o estacionamento ao mesmo tempo.

Características principais:
* **O Semaphore(10) permite até 10 carros simultaneamente.

As threads chamam:
* **acquire() → ocupa vaga
* **release() → libera vaga
O semáforo é estático, então todos os carros compartilham o mesmo estacionamento.

### Comportamento observado
* **Máximo de 10 carros “ocupando vaga” ao mesmo tempo.
* **Os outros carros ficam bloqueados e esperando, sem travar o programa.
* **A lógica simula corretamente um estacionamento real.

### 2. CarroLock.java
Já no arquivo CarroLock.java, existe um erro conceitual importante. Esse lock não é estatico.
Consequência:
Cada CarroLock tem o seu próprio lock, ou seja, as threads NÃO compartilham a mesma trava.
Todas as threads entram no estacionamento sem restrição, porque cada uma tem seu próprio lock.
Na prática, o programa não controla concorrência entre carros, apenas “tranca” cada carro consigo mesmo, pois não existe limite de vagas, mesmo que a intenção fosse simular um.

### 3. Conclusão
A implementação Carro.java está correta para modelar um estacionamento com número limitado de vagas. O uso de Semaforo(10) garante que somente 10 carros entrem simultaneamente, e que os demais aguardem, representando uma política realista de controle.
Já em CarroLock.java, apesar de utilizar ReentrantLock, a implementação não cria um recurso compartilhado entre as threads. Como o lock não é estático, cada carro possui sua própria trava, eliminando a concorrência e tornando a sincronização ineficaz para esse problema.
Isso impede a simulação de um estacionamento limitado e faz com que todas as threads entrem simultaneamente, quebrando a lógica original.
