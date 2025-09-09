# Projeto 5

### **Versão 1: Código sem `for` e sem `array`**:

```cpp
#define pinBotao 6   // Pino do botão
#define pinLed1 13    // Pino do primeiro LED
#define pinLed2 12    // Pino do segundo LED
#define pinLed3 11    // Pino do terceiro LED
#define pinLed4 10    // Pino do quarto LED
#define pinLed5 9     // Pino do quinto LED
#define pinLed6 8     // Pino do sexto LED

int contador = 0;  // Contador para controlar o número de LEDs acesos
int tamanho = 6;   // Número total de LEDs

void setup()
{
  // Configura os pinos dos LEDs como OUTPUT
  pinMode(pinLed1, OUTPUT);
  pinMode(pinLed2, OUTPUT);
  pinMode(pinLed3, OUTPUT);
  pinMode(pinLed4, OUTPUT);
  pinMode(pinLed5, OUTPUT);
  pinMode(pinLed6, OUTPUT);
  
  pinMode(pinBotao, INPUT);  // Configura o pino do botão como INPUT
}

void loop()
{
  // Lê o estado do botão
  bool botao_clicado = digitalRead(pinBotao);

  if(botao_clicado == HIGH){  // Se o botão for pressionado
    contador++;  // Aumenta o contador
    delay(100);  // Delay de 100ms para evitar múltiplos cliques acidentais
    if(contador > tamanho){  // Se o contador ultrapassar o número de LEDs
      contador = 0;  // Reseta o contador para 0
    }
  }

  // Controla os LEDs conforme o valor do contador
  if(contador >= 1) digitalWrite(pinLed1, HIGH); else digitalWrite(pinLed1, LOW);
  if(contador >= 2) digitalWrite(pinLed2, HIGH); else digitalWrite(pinLed2, LOW);
  if(contador >= 3) digitalWrite(pinLed3, HIGH); else digitalWrite(pinLed3, LOW);
  if(contador >= 4) digitalWrite(pinLed4, HIGH); else digitalWrite(pinLed4, LOW);
  if(contador >= 5) digitalWrite(pinLed5, HIGH); else digitalWrite(pinLed5, LOW);
  if(contador >= 6) digitalWrite(pinLed6, HIGH); else digitalWrite(pinLed6, LOW);
}
```

#### Explicação da versão sem `for` e sem `array`:

1. **Definições de pinos:**
   * Cada pino de LED é definido individualmente. `pinLed1`, `pinLed2`, etc., são usados para os LEDs, e `pinBotao` é usado para o botão.
2. **Função `setup()`:**
   * Cada pino de LED é configurado como saída (`OUTPUT`) individualmente, sem o uso de um loop. O pino do botão é configurado como entrada (`INPUT`).
3. **Função `loop()`:**
   * A leitura do botão é feita com `digitalRead()`, e se o botão for pressionado, o contador é incrementado.
   * O código verifica o estado do botão com um `if` e, dependendo do valor do contador, acende ou apaga os LEDs utilizando múltiplos `if`. Cada `if` controla um LED específico, verificando se o contador é maior ou igual ao número do LED.
4. **Vantagens:**
   * Simples e direto.
   * Não há o uso de arrays ou loops, como solicitado.
5. **Desvantagens:**
   * Não é escalável. Se você quiser adicionar mais LEDs, precisará escrever mais `if` e mais configurações de pinos manualmente.
   * O código fica mais longo e difícil de manter com o aumento do número de LEDs.

---

### **Versão 2: Código com `for` e com `array`**:

```cpp
#define pinBotao 6   // Pino do botão
int lista_leds[] = {13, 12, 11, 10, 9, 8}; // Define os pinos dos LEDs
int contador = 0;  // Variável para contar o número de LEDs acesos
int tamanho = sizeof(lista_leds) / sizeof(lista_leds[0]); // Calcula a quantidade de LEDs

void setup()
{
  // Configura os pinos dos LEDs como OUTPUT usando um loop
  for(int i = 0; i < tamanho; i++){
    pinMode(lista_leds[i], OUTPUT); // Configura cada pino de LED como saída
  }
  pinMode(pinBotao, INPUT);  // Configura o pino do botão como entrada
}

void loop()
{
  // Lê o estado do botão
  bool botao_clicado = digitalRead(pinBotao);

  if(botao_clicado == HIGH){  // Se o botão for pressionado
    contador++;  // Aumenta o contador
    delay(100);  // Delay de 100ms para evitar múltiplos cliques acidentais
    if(contador > tamanho){  // Se o contador ultrapassar o número de LEDs
      contador = 0;  // Reseta o contador para 0
    }
  }

  // Acende os LEDs de acordo com o contador usando um loop
  for(int i = 0; i < tamanho; i++){
    if(contador >= (i + 1)){  // Se o contador for maior ou igual ao índice do LED
      digitalWrite(lista_leds[i], HIGH);  // Acende o LED
    } else {
      digitalWrite(lista_leds[i], LOW);  // Apaga o LED
    }
  }
}
```

#### Explicação da versão com `for` e com `array`:

1. **Definições de pinos:**
   * O vetor `lista_leds[]` contém os pinos dos LEDs, o que permite que o código seja mais flexível, pois qualquer número de LEDs pode ser facilmente manipulado adicionando ou removendo pinos do vetor.
2. **Função `setup()`:**
   * O loop `for` percorre todos os pinos de LEDs (definidos no vetor `lista_leds[]`) e os configura como saídas usando `pinMode()`.
   * O pino do botão é configurado como entrada com `pinMode(pinBotao, INPUT)`.
3. **Função `loop()`:**
   * A leitura do botão é feita com `digitalRead()`, e se o botão for pressionado, o contador é incrementado.
   * Se o contador ultrapassar o número de LEDs, ele é reiniciado para 0.
   * O loop `for` percorre o vetor `lista_leds[]` e acende ou apaga os LEDs com base no valor do contador:
     * Se o contador for maior ou igual ao índice do LED (baseado no valor do vetor), o LED é aceso.
     * Caso contrário, o LED é apagado.
4. **Vantagens:**
   * O código é **mais compacto e escalável**. Adicionar ou remover LEDs é fácil, basta modificar o vetor `lista_leds[]`.
   * Utiliza um **loop** que evita a repetição de código, tornando-o mais limpo e legível.
5. **Desvantagens:**
   * Precisa de arrays para armazenar os pinos dos LEDs.
   * A utilização de `for` e `array` pode ser mais difícil de entender para iniciantes, embora seja mais eficiente e flexível.

---

### **Comparação entre as duas versões:**

1. **Simplicidade vs. Escalabilidade:**
   * **Versão sem `for`**: É simples e direta, mas não escalável. Para adicionar mais LEDs, você precisaria adicionar mais linhas de código manualmente.
   * **Versão com `for`**: É mais escalável e reutilizável. Você pode facilmente adicionar ou remover LEDs no vetor `lista_leds[]` sem precisar reescrever várias linhas de código.
2. **Legibilidade e Manutenção:**
   * A versão com `for` é mais legível e fácil de manter, especialmente quando há mais LEDs.
   * A versão sem `for` e sem arrays é mais difícil de manter à medida que o número de LEDs cresce, pois você teria que adicionar manualmente mais verificações `if` e mais configurações de pinos.
