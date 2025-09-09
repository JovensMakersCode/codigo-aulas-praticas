# 🚦 Projeto: Semáforo com 3 LEDs

## 📄 Código 1 — Versão **sem `for()`**

Esse é o jeito mais direto: escrevemos cada comando “na mão”.

```cpp
int led_verde = 11;
int led_amarelo = 10;
int led_vermelho = 9;

void setup()
{
  pinMode(led_verde, OUTPUT);    // Configura LED verde como saída
  pinMode(led_amarelo, OUTPUT);  // Configura LED amarelo como saída
  pinMode(led_vermelho, OUTPUT); // Configura LED vermelho como saída
}

void loop()
{
  // Acende o verde
  digitalWrite(led_verde, HIGH);
  delay(2000); // espera 2 segundos
  digitalWrite(led_verde, LOW);

  // Acende o amarelo
  digitalWrite(led_amarelo, HIGH);
  delay(2000);
  digitalWrite(led_amarelo, LOW);

  // Acende o vermelho
  digitalWrite(led_vermelho, HIGH);
  delay(2000);
  digitalWrite(led_vermelho, LOW);
}
```

---

## 📄 Código 2 — Versão **com `for()`**

Aqui usamos **array + laço de repetição** para simplificar e evitar repetição de código.

```cpp
int led_verde = 11;
int led_amarelo = 10;
int led_vermelho = 9;

// Lista que guarda todos os LEDs
int lista_leds[3];

void setup()
{
  // Colocamos cada LED dentro da lista
  lista_leds[0] = led_verde;
  lista_leds[1] = led_amarelo;
  lista_leds[2] = led_vermelho;

  // Configura todos os LEDs como saída usando for
  for (int i = 0; i < 3; i++) {
    pinMode(lista_leds[i], OUTPUT);
  }
}

void loop()
{
  // Percorre cada LED da lista e acende em sequência
  for (int i = 0; i < 3; i++) {
    digitalWrite(lista_leds[i], HIGH); // Acende LED atual
    delay(2000);                       // Espera 2 segundos
    digitalWrite(lista_leds[i], LOW);  // Apaga LED atual
  }
}
```

---

## 📌 Diferença entre os dois códigos

* **Versão sem `for()`**: mais fácil de entender no começo, mas fica **muito repetitiva**. Se tivéssemos 10 LEDs, teríamos que escrever **30 linhas** só para ligar e desligar.
* **Versão com `for()`**: aproveita o **poder dos arrays e laços de repetição** → o código fica **curto, limpo e fácil de expandir**.

---

## 🎯 Em resumo

* Ambos os códigos fazem a mesma coisa: **simulam um semáforo simples** (verde → amarelo → vermelho).
* O primeiro jeito é bom para aprender.
* O segundo é mais **profissional e escalável**.
