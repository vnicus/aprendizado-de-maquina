# Matriz de Confusão

## O que é a Matriz de Confusão?

A **matriz de confusão** é uma ferramenta fundamental em aprendizado de máquina, utilizada para avaliar o desempenho de modelos de classificação.

Mais do que simplesmente mostrar o número total de acertos, ela permite **visualizar exatamente onde o modelo está acertando e que tipos de erros está cometendo**.

Em um problema de **classificação binária** — onde existem apenas duas classes, geralmente chamadas de *Positiva* e *Negativa* — a matriz é formada por uma tabela **2×2** dividida em quatro quadrantes:

|                      | **Previsão: Negativo**      | **Previsão: Positivo**      |
|----------------------|-----------------------------|-----------------------------|
| **Real: Negativo**   | Verdadeiro Negativo (VN)    | Falso Positivo (FP)         |
| **Real: Positivo**   | Falso Negativo (FN)         | Verdadeiro Positivo (VP)    |

---

## Os Quatro Quadrantes

### ✅ Verdadeiro Positivo (VP)
- O modelo previu **Positivo** e o valor real era **Positivo**.
- **Exemplo:** O modelo disse que um paciente tinha a doença, e ele realmente tinha. *(Acerto)*

### ✅ Verdadeiro Negativo (VN)
- O modelo previu **Negativo** e o valor real era **Negativo**.
- **Exemplo:** O modelo disse que um paciente era saudável, e ele realmente era. *(Acerto)*

### ❌ Falso Positivo (FP)
- O modelo previu **Positivo**, mas o valor real era **Negativo**.
- **Exemplo:** O modelo deu um alarme falso. Disse que um paciente tinha a doença, mas ele era saudável. Isso pode gerar custos e estresse desnecessários.

### ❌ Falso Negativo (FN)
- O modelo previu **Negativo**, mas o valor real era **Positivo**.
- **Exemplo:** O modelo não detectou o problema. Disse que um paciente era saudável, mas ele tinha a doença. Em contextos médicos, este é frequentemente o **erro mais perigoso**.

---

## Métricas da Matriz de Confusão

A partir dos quatro valores (VP, VN, FP, FN), é possível calcular diversas métricas para entender o comportamento do modelo sob diferentes perspectivas.

---

### 1. Acurácia (Accuracy)

Indica a **proporção geral de previsões corretas** em relação ao total de previsões realizadas.

$$
Acurácia = \frac{VP + VN}{VP + VN + FP + FN}
$$

> É uma boa métrica quando o conjunto de dados é **balanceado** (número semelhante de exemplos em ambas as classes) e os custos de Falsos Positivos e Falsos Negativos são equivalentes.

---

### 2. Precisão (Precision)

Mede a proporção de **previsões positivas que estavam corretas**. Responde à pergunta: *"De todos os casos que o modelo classificou como positivos, quantos realmente eram?"*

$$
Precisão = \frac{VP}{VP + FP}
$$

> Fundamental quando o **custo de um Falso Positivo é alto**. Exemplo: em um filtro de spam, é preferível deixar passar um spam (FN) do que classificar um e-mail importante como spam (FP).

---

### 3. Revocação / Sensibilidade (Recall / Sensitivity)

Mede a proporção de **positivos reais que foram identificados corretamente** pelo modelo. Responde à pergunta: *"De todos os casos que realmente são positivos, quantos o modelo conseguiu detectar?"*

$$
Revocação = \frac{VP}{VP + FN}
$$

> Essencial quando o **custo de um Falso Negativo é alto**. Exemplo: na detecção de câncer, é preferível dar um alarme falso em um paciente saudável (FP) do que não detectar a doença em alguém que está doente (FN).

---

### 4. Especificidade (Specificity)

Mede a proporção de **negativos reais que foram identificados corretamente**.

$$
Especificidade = \frac{VN}{VN + FP}
$$

> Útil para avaliar a capacidade do modelo de **evitar alarmes falsos**. Muito utilizada na área médica em conjunto com a Sensibilidade (Revocação).

---

### 5. F1-Score (F-Measure)

É a **média harmônica entre a Precisão e a Revocação**. O F1-Score busca um equilíbrio entre essas duas métricas, penalizando severamente modelos que tenham um valor muito baixo em uma delas.

$$
F1\text{-}Score = 2 \times \frac{Precisão \times Revocação}{Precisão + Revocação}
$$

> É a métrica ideal quando o conjunto de dados é **desbalanceado** (por exemplo, detecção de fraudes, onde as fraudes são raras) e você precisa de um único número que pondere adequadamente o balanço entre Falsos Positivos e Falsos Negativos.

---

## Exemplo Prático — Calculando na Mão

### Dataset (recorte do Titanic)

| Nome                   | Real (y) | Previsto (ŷ) | Avaliação                        |
|------------------------|----------|--------------|----------------------------------|
| Kelly, Mr. James       | 0        | 0            | Verdadeiro Negativo (VN)         |
| Wilkes, Mrs. James     | 1        | 1            | Verdadeiro Positivo (VP)         |
| Myles, Mr. Thomas      | 0        | 1            | **Falso Positivo (FP)**          |
| Wirz, Mr. Albert       | 0        | 0            | Verdadeiro Negativo (VN)         |
| Hirvonen, Mrs. Alex    | 1        | 0            | **Falso Negativo (FN)**          |
| Svensson, Mr. Johan    | 0        | 0            | Verdadeiro Negativo (VN)         |
| Connolly, Miss. Kate   | 1        | 1            | Verdadeiro Positivo (VP)         |

### Matriz resultante

|                       | Previsto: Positivo (1) | Previsto: Negativo (0) |
|-----------------------|------------------------|------------------------|
| **Real: Positivo (1)**| 2 (VP)                 | 1 (FN)                 |
| **Real: Negativo (0)**| 1 (FP)                 | 3 (VN)                 |

Ou seja: **VP = 2, VN = 3, FP = 1, FN = 1**

---

## Cálculos

### **Acurácia:**
Das 7 previsões que o modelo fez, quantas ele acertou no total?
$$
Acurácia = \frac{2 + 3}{2 + 3 + 1 + 1} = \frac{5}{7} \approx 71{,}4\%
$$

---

### **Precisão:**
• Das 3 pessoas que o modelo disse que sobreviveriam (𝑉𝑃 + 𝐹𝑃), quantas realmente sobreviveram?
$$
Precisão = \frac{2}{2 + 1} = \frac{2}{3} \approx 66{,}7\%
$$

---

### **Revocação:**
Das 3 pessoas que realmente sobreviveram no dataset (𝑉𝑃 + 𝐹𝑁), quantas o modelo conseguiu salvar/detectar?
$$
Revocação = \frac{2}{2 + 1} = \frac{2}{3} \approx 66{,}7\%
$$

---

### **Especificidade:**
Das 4 pessoas que realmente morreram no dataset (𝑉𝑁 + 𝐹𝑃), quantas o modelo identificou corretamente?
$$
Especificidade = \frac{3}{3 + 1} = \frac{3}{4} = 75\%
$$

---

### **F1-Score:**
A média harmônica para balancear Precisão e Revocação. É uma visão geral sobre como foi o “desempenho” do modelo.
$$
F1\text{-}Score = 2 \times \frac{0{,}667 \times 0{,}667}{0{,}667 + 0{,}667} \approx 66{,}7\%
$$

---

## Quando usar cada métrica?

| Situação                                      | Métrica prioritária  |
|-----------------------------------------------|----------------------|
| Dataset balanceado, erros equivalentes        | Acurácia             |
| Custo alto de Falso Positivo (ex: spam)       | Precisão             |
| Custo alto de Falso Negativo (ex: diagnóstico)| Revocação            |
| Avaliar detecção de negativos reais           | Especificidade       |
| Dataset desbalanceado (ex: fraude)            | F1-Score             |

> **Atenção:** a acurácia sozinha pode ser enganosa. Em datasets desbalanceados, um modelo que sempre prevê a classe majoritária pode ter alta acurácia, mas ser completamente inútil na prática.

---

*Material baseado na aula 8 — Matriz de Confusão | Prof. Me. Tiago A. Silva | FATEC Jahu*