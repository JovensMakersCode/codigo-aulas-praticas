# 📘 Documentação do Código – Controle de Servo Motor com LEDs

---

## 🔹 O que o código faz?

Esse programa controla um **servo motor** para que ele fique se movendo continuamente de um lado para o outro (0° → 180° e depois 180° → 0°).

* Enquanto o **servo abre (0° → 180°)**, o **LED verde** fica aceso.
* Enquanto o **servo fecha (180° → 0°)**, o **LED vermelho** fica aceso.

Assim, os LEDs funcionam como indicadores visuais da direção do movimento do servo.

---

## 🔹 Estrutura do Código

### 1. **Inclusão da Biblioteca**

```cpp
#include <Servo.h>
```

* Aqui estamos incluindo a biblioteca `Servo.h`.
* **Biblioteca no Arduino:** é um conjunto de funções prontas que expandem as capacidades da linguagem.
  * Em vez de ter que programar todos os sinais elétricos que controlam um servo, a biblioteca já traz funções como `attach()` e `write()` que simplificam o trabalho.
  * É como se fosse um "pacote de ferramentas" que você importa para o seu código.

---

### 2. **Definição de Pinos**

```cpp
#define meuServo 7
#define led_verm 6
#define led_verd 5
```

* O pino **7** controla o **servo motor**.
* O pino **6** controla o **LED vermelho**.
* O pino **5** controla o **LED verde**.

> Isso facilita caso queira mudar os pinos depois — basta alterar aqui, não no código inteiro.

---

### 3. **Declarações de Variáveis**

```cpp
Servo servo;      // Cria um objeto "servo"
int posicao = 0;  // Armazena a posição atual do servo
bool indoDireita = true; // Indica a direção do movimento
```

* `Servo servo;` cria um objeto chamado **servo** para controlar o motor.
* `posicao` guarda o ângulo atual do servo (0 a 180).
* `indoDireita` funciona como uma "bandeira" que indica se o servo está indo para a direita (abrindo) ou para a esquerda (fechando).

---

### 4. **Setup**

```cpp
void setup() {
  pinMode(led_verm, OUTPUT);
  pinMode(led_verd, OUTPUT);

  servo.attach(meuServo);
  servo.write(0); // começa fechado
}
```

* Configura os pinos dos LEDs como **saída**.
* Conecta o objeto `servo` ao **pino 7**.
* Define a posição inicial do servo em **0 graus** (posição fechada).

---

### 5. **Loop Principal**

```cpp
void loop() {
  if (indoDireita) {
    // Move servo de 0 até 180 graus
    for (posicao = 0; posicao <= 180; posicao++) {
      servo.write(posicao);
      digitalWrite(led_verd, HIGH);
      digitalWrite(led_verm, LOW);
      delay(15); // velocidade do movimento
    }
    indoDireita = false;
  } else {
    // Move servo de 180 até 0 graus
    for (posicao = 180; posicao >= 0; posicao--) {
      servo.write(posicao);
      digitalWrite(led_verd, LOW);
      digitalWrite(led_verm, HIGH);
      delay(15);
    }
    indoDireita = true;
  }
}
```

🔎 **Explicação passo a passo:**

* **Se `indoDireita == true`:**
  * O servo gira de **0° até 180°**.
  * Enquanto isso:
    * O **LED verde acende**.
    * O **LED vermelho apaga**.
  * No final, `indoDireita` passa a ser **false** (mudando a direção).
* **Se `indoDireita == false`:**
  * O servo gira de **180° até 0°**.
  * Enquanto isso:
    * O **LED vermelho acende**.
    * O **LED verde apaga**.
  * No final, `indoDireita` volta a ser **true** (mudando a direção de novo).

⚡ O `delay(15)` controla a **velocidade do movimento**:

* Quanto menor o delay, mais rápido o servo se move.
* Quanto maior, mais lento e suave fica o movimento.

---

## 🔹 Resumindo

* O servo oscila continuamente entre 0° e 180°.
* O LED verde indica movimento de abertura.
* O LED vermelho indica movimento de fechamento.
* A biblioteca `Servo.h` simplifica o controle do motor, evitando código complexo de geração de sinais PWM.
