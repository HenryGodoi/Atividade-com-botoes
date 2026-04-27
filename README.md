
● O que o sistema precisa fazer e lista de passos:
O sistema irá receber a entrada de um dos 4 Botões e irá processar os dados e enviar o sinal para um ou mais, dos 6 LEDS, irei explicar oque cada Botão e Led irá fazer:
**Pino digital 1 - Botão 1 (Abre o Portão Esquerdo)**
**Pino digital 2 - Botão 2 (Abre o Portão Direito)**
**Pino digital 3 - Botão 3 (Abre os dois Portões)**
**Pino digital 4 - Botão 4 (Fecha os Portões)**

**Pino digital 5 - Portão Esquerdo 
Pino digital 6 - Led Verde Esquerdo (Ficará acesso caso o Portão Esquerdo esteja aberto)
Pino Digital 7 - Led Vermelho Esquerdo (Ficará acesso caso o Portão Esquerdo esteja fechado)**

**Pino digital 8 - Led Amarelo (Ficará acesso enquanto um ou os dois Portões estiverem se movimentando)
Pino digital 9 - Led Azul (Ficará acesso quando os dois Portões estiverem abertos)**

**Pino Digital 11 - Led Verde Direito (Ficará acesso caso o Portão Direito esteja aberto)
Pino digital 12 - Led Vermelho Direito (Ficará acesso caso o Portão Direito esteja fechado)
Pino digital 13 - Portão direito**
 
● Montagem do circuito:
De inicio, defini que no inicio os servos (Portões) no pino 5 e pino 13, ficaram em 0 graus;
Defini que os Led Vermelho Esquerdo e Direito (Pino 7 e pino 12) ficaram como ALTO (Ligados).

Depois disso, defini 4 variaveis sendo elas: botao1(1), botao2(2), botao3(3) e botao4(4)
Logo após isso, comecei a montar o que o **botao1** irá fazer ao ser apertado:
botao1 = ALTO;
irá definir o Led Amarelo (Pino 8) como Alto e definir o Led Vermelho Esquerdo (Pino 7) como Baixo.
Após isso o portão no pino 5 irá começar a girar em 180 graus, porém ao invés dele girar na velocidade normal,
eu coloquei um resistor no fio negativo dele para que ele gire devagar, após 2.5 segundos o Led Amarelo (Pino 8) irá ficar como Baixo (pois é o tempo exato que o portão se fecha)
e o Led Verde Esquerdo (Pino 6) ficará como Alto.

montagem do **botao2** ao ser apertado:
botao2 = ALTO;
irá definir o Led Amarelo como Alto e definirá o Led Vermelho Direito (Pino 12) como Baixo.
O portão no pino 13 começará a girar em 180 graus, o mesmo possui a mesma velocidade que o Portão Esquerdo e logo após 2.5 segundos
o pino 8 irá ficar como Baixo (pois é o tempo exato que o portão se fecha), e o Led Verde Direito (Pino 11) ficará como Alto.

Montagem do **botao3** ao ser apertado:
botao3 = ALTO;
O mesmo ao ser apertado irá começar a girar os dois Portões (Pino 5 e Pino 13) em 180 graus, com isso irá definir os Pinos 7 e 12 como Baixos
e definir o pino 8 como Alto, como de costume após 2.5 segundos o Pino 8 ficará como Baixo e juntamente dele os Pinos 11, 6 e 9 ficarão como Alto.

Montagem do **botao4** ao ser apertado:
botao4 = ALTO;
O mesmo começará a girar os Portões (Pino 5 e 13) em 0 graus, assim retornando eles para a posição de origem.
Definirá o Pino 8 como Alto e os Pinos 6, 9 e 11 como Baixos.
Aguardando 2,5 segundos, o Pino 8 ficará como Baixo e os Pinos 12 e 7 ficarão como Alto.

Observação:
Na montagem foi adicionado uma parte final que irá fazer a seguinte coisa:
Temos 1 IF AND, a primeira condição do IF está lendo se o Portão Esquerdo (Pino 5) é igual a 180 graus, se for verdadeiro irá ler se a segunda condição que é se o Portão Direito (Pino 13) também é igual a 180 Graus, 
se as duas condições forem verdadeieras, irá definir a LED Azul (Pino 9) como Alto

<img width="397" height="50" alt="image" src="https://github.com/user-attachments/assets/d769bbd4-a1a4-428d-bb9c-f353251cf9b3" />


● Print do código:

<img width="864" height="709" alt="image" src="https://github.com/user-attachments/assets/65ad6fc4-39c3-4c32-ae58-c27bb683465d" />

<img width="279" height="215" alt="image" src="https://github.com/user-attachments/assets/1de21475-1bc8-4d2f-ba64-dff7f5b7e75d" />

<img width="300" height="665" alt="image" src="https://github.com/user-attachments/assets/fe79cb49-f347-446d-801e-ebafba9cba5d" />
<img width="289" height="721" alt="image" src="https://github.com/user-attachments/assets/551435b3-9781-40b4-982d-40bd60d66d65" />
<img width="412" height="104" alt="image" src="https://github.com/user-attachments/assets/4d4a0da7-b2e9-4312-b158-df182d0cc542" />

```bash
// C++ code
//
#include <Servo.h>

int botao1 = 0;

int botao2 = 0;

int botao3 = 0;

int botao4 = 0;

Servo servo_5;

Servo servo_13;

void setup()
{
  servo_5.attach(5);

  servo_13.attach(13);

  pinMode(7, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(1, INPUT);
  pinMode(2, INPUT);
  pinMode(3, INPUT);
  pinMode(4, INPUT);
  pinMode(8, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(9, OUTPUT);

  servo_5.write(0);
  servo_13.write(0);
  digitalWrite(7, HIGH);
  digitalWrite(12, HIGH);
}

void loop()
{
  botao1 = digitalRead(1);
  botao2 = digitalRead(2);
  botao3 = digitalRead(3);
  botao4 = digitalRead(4);
  if (botao1 == HIGH) {
    digitalWrite(8, HIGH);
    digitalWrite(7, LOW);
    servo_5.write(180);
    delay(2500); // Wait for 2500 millisecond(s)
    digitalWrite(8, LOW);
    digitalWrite(6, HIGH);
  }
  if (botao2 == HIGH) {
    digitalWrite(8, HIGH);
    digitalWrite(12, LOW);
    servo_13.write(180);
    delay(2500); // Wait for 2500 millisecond(s)
    digitalWrite(8, LOW);
    digitalWrite(11, HIGH);
  }
  if (botao3 == HIGH) {
    servo_5.write(180);
    servo_13.write(180);
    digitalWrite(7, LOW);
    digitalWrite(12, LOW);
    digitalWrite(8, HIGH);
    delay(2500); // Wait for 2500 millisecond(s)
    digitalWrite(8, LOW);
    digitalWrite(11, HIGH);
    digitalWrite(6, HIGH);
    digitalWrite(9, HIGH);
  }
  if (botao4 == HIGH) {
    servo_5.write(0);
    servo_13.write(0);
    digitalWrite(8, HIGH);
    digitalWrite(6, LOW);
    digitalWrite(9, LOW);
    digitalWrite(11, LOW);
    delay(2500); // Wait for 2500 millisecond(s)
    digitalWrite(8, LOW);
    digitalWrite(12, HIGH);
    digitalWrite(7, HIGH);
  }
  if (servo_5.read() == 180 && servo_13.read() == 180) {
    digitalWrite(9, HIGH);
  }
}
```
