## 🔌 TinkerCad  
[🔗 Acesse o circuito no TinkerCad](https://www.tinkercad.com/things/56l0xUr2CtW/editel?returnTo=%2Fdashboard%2Fdesigns%2Fcircuits&sharecode=gkkSldykQaZ8YRJdrQm6zkrcdCo3B7IxjZjaIHMSPcM)

### 🖼️ Montagem do Circuito
<img width="756" height="488" alt="image" src="https://github.com/user-attachments/assets/4d2faa90-84db-447c-98b7-2e3c1b74adf7" />
<img width="775" height="489" alt="image" src="https://github.com/user-attachments/assets/d96be6a2-83ae-4762-8115-f762f458cd68" />
<img width="873" height="571" alt="image" src="https://github.com/user-attachments/assets/0b62bcca-1550-40c8-af39-9f9fb5b0830c" />

---

## 🧩 Estrutura dos Dados

| Tempo (ms) | V_capacitor (V) | V_resistor (V) |
|-------------|-----------------|----------------|
| 10          | 0.00            | 5.00           |
| 2411        | 0.05            | 4.95           |
| 2813        | 0.05            | 4.95           |
| ...         | ...             | ...            |
| 25744       | 0.05            | 4.95           |

---

## 📊 Código Python — Gerar Gráfico RC

Salve o código abaixo como **`grafico_rc.py`** e execute para visualizar o comportamento do circuito RC com os dados coletados do Arduino.

```python
import pandas as pd
import matplotlib.pyplot as plt
from io import StringIO

# --- Dados coletados do Arduino ---
dados_txt = """10 0.00 5.00
2411 0.05 4.95
2813 0.05 4.95
3216 0.05 4.95
3618 0.05 4.95
4021 0.05 4.95
4422 0.05 4.95
4825 0.05 4.95
5227 0.05 4.95
5629 0.05 4.95
6031 0.05 4.95
6433 0.05 4.95
6836 0.05 4.95
7238 0.05 4.95
7641 0.05 4.95
8042 0.05 4.95
8444 0.05 4.95
8847 0.05 4.95
9249 0.05 4.95
9651 0.05 4.95
10053 0.05 4.95
10456 0.05 4.95
10858 0.05 4.95
11260 0.05 4.95
11663 0.05 4.95
12065 0.05 4.95
12468 0.05 4.95
12870 0.05 4.95
13272 0.05 4.95
13674 0.05 4.95
14076 0.05 4.95
14479 0.05 4.95
14881 0.05 4.95
15284 0.05 4.95
15686 0.05 4.95
16089 0.05 4.95
16491 0.05 4.95
16893 0.05 4.95
17295 0.05 4.95
17697 0.05 4.95
18100 0.05 4.95
18502 0.05 4.95
18905 0.05 4.95
19307 0.05 4.95
19709 0.05 4.95
20112 0.05 4.95
20514 0.05 4.95
20917 0.05 4.95
21318 0.05 4.95
21721 0.05 4.95
22123 0.05 4.95
22525 0.05 4.95
22928 0.05 4.95
23330 0.05 4.95
23733 0.05 4.95
24135 0.05 4.95
24538 0.05 4.95
24940 0.05 4.95
25341 0.05 4.95
25744 0.05 4.95
```

# --- Conversão para DataFrame ---
dados = pd.read_csv(StringIO(dados_txt), sep=" ", names=["tempo_ms", "tensao_capacitor", "tensao_resistor"])

# --- Plotagem ---
plt.figure(figsize=(10,6))
plt.plot(dados["tempo_ms"], dados["tensao_capacitor"], label="Tensão no Capacitor (V)", marker="o")
plt.plot(dados["tempo_ms"], dados["tensao_resistor"], label="Tensão no Resistor (V)", linestyle="--")

plt.title("Comportamento do Circuito RC (dados experimentais)")
plt.xlabel("Tempo (ms)")
plt.ylabel("Tensão (V)")
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
