## 📄 Código com explicação

```cpp
// Define os pinos que vamos usar
#define led 6       // LED conectado ao pino digital 6
#define botao 5     // Botão conectado ao pino digital 5

// Variável para armazenar o estado do botão (pressionado ou não)
bool botao_pressionado = false;

void setup()
{
  // Configura os pinos
  pinMode(led, OUTPUT);   // Define o pino do LED como saída
  pinMode(botao, INPUT);  // Define o pino do botão como entrada
}

void loop()
{
  // Lê o estado do botão (HIGH = 1 = pressionado | LOW = 0 = solto)
  botao_pressionado = digitalRead(botao);
  
  // Se o botão estiver pressionado
  if(botao_pressionado){
    digitalWrite(led, HIGH);  // Liga o LED
  } 
  // Caso contrário
  else {
    digitalWrite(led, LOW);   // Desliga o LED
  }
  
  // Pequena pausa para evitar leituras muito rápidas (100 ms)
  delay(100);
}
```

---

## 📌 Explicação didática por partes

1. **Definição dos pinos**

   * `#define led 6` → o LED será controlado pelo **pino 6** do Arduino.
   * `#define botao 5` → o botão será lido pelo **pino 5** do Arduino.

   🔎 Usar `#define` facilita caso queira mudar os pinos depois (só altera o número em um lugar).

---

2. **Variável de controle**
   * `bool botao_pressionado = false;`
     Uma variável do tipo **booleano** (`true` ou `false`) que guarda se o botão está pressionado ou não.

---

3. **Função `setup()`**
   * Executa **uma vez** no início do programa.
   * `pinMode(led, OUTPUT);` → o pino do LED funciona como saída (Arduino envia energia).
   * `pinMode(botao, INPUT);` → o pino do botão funciona como entrada (Arduino lê se tem energia ou não).

---

4. **Função `loop()`**
   * Repete **para sempre** enquanto o Arduino está ligado.
   * `digitalRead(botao)` → lê o estado do botão:
     * `HIGH (1)` se está pressionado.
     * `LOW (0)` se está solto.
   * Esse valor é guardado na variável `botao_pressionado`.
   * O **if** decide o que fazer:
     * Se o botão está pressionado → acende o LED (`digitalWrite(led, HIGH)`).
     * Se não está pressionado → apaga o LED (`digitalWrite(led, LOW)`).
   * `delay(100);` → o Arduino espera **100 milissegundos** antes de repetir a leitura.
     Isso evita leituras muito rápidas e também reduz o efeito de "ruído" do botão.

---

## 📖 Em resumo:

Esse programa faz o **LED acender quando o botão está pressionado** e apagar quando o botão é solto.
É um exemplo clássico de **entrada (botão) e saída (LED)** no Arduino.
