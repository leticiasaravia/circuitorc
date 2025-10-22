## 🔌 TinkerCad  
[🔗 Acesse o circuito no TinkerCad](https://www.tinkercad.com/things/56l0xUr2CtW/editel?returnTo=%2Fdashboard%2Fdesigns%2Fcircuits&sharecode=gkkSldykQaZ8YRJdrQm6zkrcdCo3B7IxjZjaIHMSPcM)
<img width="1906" height="638" alt="image" src="https://github.com/user-attachments/assets/4d0176eb-72bd-4dcb-a889-85b9add3c7bb" />



## 🧩 Estrutura dos Dados

| Tempo (ms) | V_capacitor (V) | V_resistor (V) |
|-------------|-----------------|----------------|
| 10          | 0.00            | 5.00           |
| 2411        | 0.05            | 4.95           |
| 2813        | 0.05            | 4.95           |
| ...         | ...             | ...            |
| 25744       | 0.05            | 4.95           |

---



###  Código do Arduino (Para o Tinkercad)

Este código é inserido na aba **"Código"** do Tinkercad.  
Ele é idêntico ao usado no Arduino físico.

```cpp
// Código para o simulador do Tinkercad

int pinoNoRC = 0;
int valorLido = 0;
float tensaoResistor = 0;
float tensaoCapacitor = 0;
unsigned long time;

void setup() {
  Serial.begin(9600);
}

void loop() {
  time = millis();
  valorLido = analogRead(pinoNoRC);
  tensaoResistor = (valorLido * 5.0 / 1023.0);
  tensaoCapacitor = 5.0 - tensaoResistor;

  Serial.print(time);
  Serial.print(" ");
  Serial.print(tensaoResistor);
  Serial.print(" ");
  Serial.println(tensaoCapacitor);

  delay(400); // No Tinkercad, o tempo de simulação pode não ser real. O delay ainda é útil.
}
```

##  Código Python (Para Análise dos Dados)

Este script lê o arquivo de texto com os dados copiados do Tinkercad e gera os gráficos.  
Não há conexão em tempo real.

---

### **Nome do arquivo:** `analisar_dados_tinkercad.py`

```python
import pandas as pd
import matplotlib.pyplot as plt

# O nome do arquivo que você salvou com os dados do Tinkercad
arquivo_de_dados = 'dados_tinkercad.txt' 

try:
    # Lê os dados do arquivo de texto
    df = pd.read_csv(
        arquivo_de_dados,
        sep='\\s+',
        header=None,
        names=['Tempo_ms', 'TensaoResistor', 'TensaoCapacitor']
    )

    # Converte o tempo para segundos
    df['Tempo_s'] = df['Tempo_ms'] / 1000

    # --- Gráfico 1: Lado a Lado ---
    fig1, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 6))
    fig1.suptitle('Análise do Circuito RC (Gráficos Separados)', fontsize=16)
    ax1.plot(df['Tempo_s'], df['TensaoCapacitor'], color='blue', marker='o', linestyle='-', markersize=4)
    ax1.set_title('Curva de Carga do Capacitor')
    ax1.set_xlabel('Tempo Simulado (s)')
    ax1.set_ylabel('Tensão (V)')
    ax1.grid(True)

    ax2.plot(df['Tempo_s'], df['TensaoResistor'], color='red', marker='x', linestyle='--', markersize=4)
    ax2.set_title('Curva de Tensão no Resistor')
    ax2.set_xlabel('Tempo Simulado (s)')
    ax2.set_ylabel('Tensão (V)')
    ax2.grid(True)
    
    # --- Gráfico 2: Comparativo ---
    fig2, ax_comp = plt.subplots(figsize=(12, 8))
    ax_comp.plot(df['Tempo_s'], df['TensaoCapacitor'], color='blue', marker='o', markersize=4, label='Tensão no Capacitor (Carga)')
    ax_comp.plot(df['Tempo_s'], df['TensaoResistor'], color='red', marker='x', markersize=4, linestyle='--', label='Tensão no Resistor (Descarga)')
    ax_comp.set_title('Gráfico Comparativo: Tensão no Resistor vs. Capacitor', fontsize=16)
    ax_comp.set_xlabel('Tempo Simulado (s)')
    ax_comp.set_ylabel('Tensão (V)')
    ax_comp.legend()
    ax_comp.grid(True)

    # Exibe todas as figuras
    plt.show()

except FileNotFoundError:
    print(f"ERRO: O arquivo '{arquivo_de_dados}' não foi encontrado.")
```
## Execução e Resultados

O fluxo de trabalho consiste em gerar os dados na nuvem (**Tinkercad**) e analisá-los localmente (**Python**).

---

### 🖼️ Gráficos
<img width="1979" height="1180" alt="image" src="https://github.com/user-attachments/assets/8ddc374a-1d33-4a14-bf2c-7a4ddd381b72" />
<img width="1979" height="1180" alt="image" src="https://github.com/user-attachments/assets/2eab9bab-4211-408c-b697-0038787e43a0" />
<img width="1979" height="1180" alt="image" src="https://github.com/user-attachments/assets/9a9ab293-d5ba-481f-b214-9234fc9e9d49" />

---
### Montagem física
![Foto da Montagem físicA](https://github.com/user-attachments/assets/408d5396-e415-4109-b4f3-03c0fd41410b)
