---
title: "Auto-consistência"
weight: 8
description: "Votação majoritária"
---

# Auto-consistência

Gera **múltiplas respostas** e escolhe a mais frequente (votação).

## Processo

```
1. Execute o mesmo prompt N vezes (temperatura alta)
2. Extraia a resposta de cada execução
3. Conte a frequência de cada resposta
4. Retorne a mais comum
```

## Configuração

| Parâmetro | Valor Recomendado |
|-----------|-------------------|
| Temperatura | 0.7 - 1.0 (alta) |
| N execuções | 3 - 10 |
| Método de seleção | Votação majoritária |

## Trade-offs

| ✅ Vantagens | ❌ Desvantagens |
|-------------|-----------------|
| Maior precisão | Custo N× maior |
| Robustez | Mais tempo |

## Quando Usar

- Classificações ambíguas
- Decisões críticas
- Alta precisão necessária

---

[Próximo: Árvore de Pensamentos →](/tecnicas/tot/)
