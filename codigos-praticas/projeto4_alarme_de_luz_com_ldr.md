## 📄 Código - Projeto 4

```cpp
// Define os pinos do Arduino conectados aos componentes
#define buzzer 7       // Pino digital 7 controla o buzzer (som)
#define led 6          // Pino digital 6 controla o LED
#define fotosensor A5  // Pino analógico A5 conectado ao divisor de tensão com o LDR

void setup()
{
  // Configura os pinos de saída
  pinMode(led, OUTPUT);      // LED como saída
  pinMode(buzzer, OUTPUT);   // Buzzer como saída
  
  // O LDR (fotosensor) é lido com analogRead(), não precisa de pinMode como INPUT,
  // mas aqui foi configurado para clareza
  pinMode(fotosensor, INPUT);

  // Inicializa a comunicação serial para monitorar os valores do sensor no PC
  Serial.begin(9600);
}

void loop()
{
  // Faz a leitura analógica do sensor de luz (valor entre 0 e 1023)
  int valorSensorLuz = analogRead(fotosensor);
 
  // Se a luminosidade for maior ou igual a 500, acende o LED
  if(valorSensorLuz >= 500){
  	digitalWrite(led, HIGH);   // Liga LED
  } else {
    digitalWrite(led, LOW);    // Desliga LED
  }
  
  // Se a luminosidade for muito alta (>= 900), ativa o buzzer
  if(valorSensorLuz >= 900){
   digitalWrite(buzzer, HIGH); // Liga buzzer
  } else {
    digitalWrite(buzzer, LOW); // Desliga buzzer
  }
  
  // Envia o valor do sensor para o Serial Monitor (para observar no PC)
  Serial.println(valorSensorLuz);

  // Aguarda 300 ms antes da próxima leitura (para não "inundar" o monitor serial)
  delay(300);
}
```

---

## 📚 Explicação

1. **Leitura do sensor (entrada):**
   * O Arduino lê o valor do **LDR** no pino analógico A5.
   * Esse valor vai de **0 a 1023**:
     * **0 → escuridão total**
     * **1023 → claridade máxima**
2. **Processamento:**
   * O programa compara esse valor com dois limites:
     * **>= 500** → Acende o LED.
     * **>= 900** → Além do LED, liga também o buzzer.
3. **Saídas:**
   * O **LED** indica que a luz ambiente passou de um certo nível.
   * O **buzzer** serve como alerta extra quando a luminosidade é ainda mais intensa.
4. **Monitoramento:**
   * O valor do sensor é impresso no **Serial Monitor** (no computador) para acompanhar em tempo real como o LDR está reagindo à luz.

---

👉Em resumo: esse código funciona como um **alarme de luminosidade**.

* Luz moderada → LED acende.
* Luz muito forte → LED + buzzer ativados.
