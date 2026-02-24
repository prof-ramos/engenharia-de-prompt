# 03 - Configurações de Saída

[← Voltar ao Sumário](00-sumario.md)

---

Depois de escolher seu modelo, você precisa definir as configurações. A engenharia de prompt eficaz requer ajuste fino desses parâmetros.

## Comprimento da Saída

Controla quantos tokens o modelo pode gerar.

> ⚠️ **Importante:** Reduzir o limite NÃO faz o modelo mais sucinto — apenas corta a resposta quando atinge o limite.

**Quando ajustar:**
- APIs com custo por token → limite menor
- Tarefas longas (relatórios, código) → limite maior
- ReAct/agentes → limite generoso (evita cortes em cadeias de raciocínio)

---

## Temperatura

Controla a **aleatoriedade** na seleção de tokens.

| Valor | Comportamento | Uso Ideal |
|-------|---------------|-----------|
| **0** | Determinístico | Código, matemática, fatos |
| **0.1 - 0.3** | Baixa variação | Classificação, extração |
| **0.4 - 0.7** | Equilibrado | Conversação, escrita geral |
| **0.8 - 1.0** | Alta variação | Criatividade, brainstorming |
| **> 1.0** | Muito aleatório | Experimental |

**Analogia:** Temperatura é como a "temperatura softmax" em ML:
- Baixa = alta certeza, poucas opções consideradas
- Alta = mais incerteza, mais opções consideradas

---

## Top-K

Seleciona apenas os **K tokens mais prováveis**.

- **Top-K = 1**: Sempre o mais provável (decodificação gananciosa)
- **Top-K = 40**: Considera os 40 mais prováveis
- **Top-K alto** (100+): Praticamente sem restrição

---

## Top-P (Amostragem Nuclear)

Seleciona tokens até atingir **probabilidade acumulada P**.

- **Top-P = 0.1**: Muito restritivo
- **Top-P = 0.9**: Padrão comum
- **Top-P = 1.0**: Sem restrição

---

## Como as Configurações Interagem

Se temperatura, top-K e top-P estiverem disponíveis:

```
1. Top-K filtra para os K tokens mais prováveis
2. Top-P filtra para tokens com prob. acumulada ≤ P
3. Temperatura aplica softmax aos candidatos restantes
4. Amostra um token da distribuição resultante
```

### Configurações Extremas

| Configuração | Efeito |
|--------------|--------|
| Temperatura = 0 | Top-K e Top-P ignorados |
| Top-K = 1 | Temperatura e Top-P ignorados |
| Top-P ≈ 0 | Praticamente determinístico |

---

## Guia Rápido de Configurações

| Cenário | Temperatura | Top-P | Top-K | Max Tokens |
|---------|-------------|-------|-------|------------|
| **Código/Debug** | 0 | 0.9 | 20 | 2000 |
| **Matemática/Lógica** | 0 | 0.9 | 20 | 500 |
| **Classificação** | 0.1 | 0.9 | 20 | 100 |
| **Resumo** | 0.2 | 0.95 | 30 | 500 |
| **Conversação** | 0.5 | 0.95 | 40 | 1000 |
| **Escrita Criativa** | 0.8 | 0.99 | 50 | 2000 |
| **Brainstorming** | 0.9 | 0.99 | 60 | 1500 |

---

## Bug do Loop de Repetição

> ⚠️ O modelo pode ficar preso repetindo a mesma palavra/frase.

**Causas:**
- Temperatura muito baixa (determinismo excessivo)
- Temperatura muito alta (aleatoriedade excessiva)

**Solução:** Ajuste temperatura para valores intermediários (0.2 - 0.7)

---

## Próximo Passo

- [Zero-shot](tecnicas/01-zero-shot.md) - Primeira técnica de prompting
