## 📄 Código com explicação

```cpp
int pot = A0;   // Pino do potenciômetro (entrada analógica)
int led = 6;    // Pino do LED (saída PWM)

void setup() {
  pinMode(led, OUTPUT);   // Configura o LED como saída
}

void loop() {
  // 1. Lê o valor do potenciômetro (0 a 1023)
  int valorPot = analogRead(pot);   

  // 2. Converte esse valor para a faixa do PWM (0 a 255)
  int brilho = map(valorPot, 0, 1023, 0, 255); 

  // 3. Ajusta o brilho do LED de acordo com o valor convertido
  analogWrite(led, brilho);   
}
```

## 📝 Explicação passo a passo

### 1. **Declaração das variáveis globais**

* `int pot = A0;` → define que o potenciômetro está conectado no pino analógico **A0**.
* `int led = 6;` → define que o LED está no pino digital **6**, que tem suporte a **PWM**.

---

### 2. **Função `setup()`**

* Aqui só aparece:

  ```cpp
  pinMode(led, OUTPUT);
  ```

  Isso porque o **LED precisa ser configurado como saída**.
* Mas o **potenciômetro não aparece aqui**.
  👉 Motivo: os pinos analógicos do Arduino **não precisam ser configurados com `pinMode()`** quando usados com `analogRead()`. Eles já são automaticamente tratados como entradas analógicas.

---

### 3. **Função `loop()`**

Essa função roda para sempre. Dentro dela:

1. **Leitura do potenciômetro**:

   ```cpp
   int valorPot = analogRead(pot);
   ```

   * O Arduino lê a tensão no pino A0.
   * Essa tensão varia de **0V a 5V**, convertida para um número de **0 a 1023** (conversor ADC de 10 bits).

   Exemplo:

   * Potenciômetro no mínimo → `valorPot = 0`
   * Potenciômetro no meio → `valorPot ≈ 512`
   * Potenciômetro no máximo → `valorPot = 1023`

---

2. **Conversão de faixa (escala)**:

   ```cpp
   int brilho = map(valorPot, 0, 1023, 0, 255);
   ```

   * A função `map()` pega um número em uma faixa e converte para outra.
   * Como o **PWM do Arduino vai de 0 a 255**, precisamos converter o valor lido do potenciômetro (0 a 1023) para essa faixa. É como regra de três.

   👉 Exemplo prático:

   * `valorPot = 0` → `brilho = 0` (LED apagado)
   * `valorPot = 512` → `brilho ≈ 127` (LED com meia intensidade)
   * `valorPot = 1023` → `brilho = 255` (LED brilho máximo)

---

3. **Controle do LED via PWM**:

   ```cpp
   analogWrite(led, brilho);
   ```

   * O pino 6 gera um sinal PWM correspondente ao valor de `brilho`.
   * Quanto maior o valor, maior o tempo que o LED fica “ligado” dentro do ciclo, e mais forte ele brilha.

---

## 📌 Por que o potenciômetro não precisa estar no `setup()`?

* Diferente dos pinos digitais, **pinos analógicos são automaticamente configurados como entrada pelo Arduino** quando você usa `analogRead()`.
* Ou seja, você **não precisa de `pinMode(pot, INPUT);`**.
* Se colocasse, não daria erro, mas também não teria efeito.

👉 Isso acontece porque `analogRead()` já instrui o microcontrolador a usar o ADC (conversor analógico-digital) no pino correspondente.

---

## 🎯 Em resumo:

Esse código lê o valor analógico do **potenciômetro**, converte para a faixa do **PWM** e usa isso para controlar o **brilho do LED**.

* O LED é inicializado como **saída** no `setup()`.
* O potenciômetro **não precisa de inicialização**, porque o `analogRead()` já trata o pino analógico como entrada.
