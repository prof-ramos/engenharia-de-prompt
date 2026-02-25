---
title: "Cadeia de Pensamento (CoT)"
weight: 7
description: "Raciocínio explícito passo a passo"
---

# Cadeia de Pensamento (CoT)

Faz o modelo **explicitar o raciocínio** passo a passo.

## A Frase Mágica

```
"Vamos pensar passo a passo."
```

## Por Que Funciona

- Modelos não "pensam" internamente
- Ao explicitar etapas, o raciocínio se torna mais confiável
- Reduz erros em problemas multi-passo

## Vantagens e Desvantagens

| ✅ Vantagens | ❌ Desvantagens |
|-------------|-----------------|
| Baixo esforço | Mais tokens = mais custo |
| Muito eficaz | Respostas mais longas |
| Interpretabilidade | |

## Quando Usar

| ✅ Ideal para | ❌ Evitar quando |
|--------------|------------------|
| Matemática e lógica | Classificação simples |
| Problemas multi-passo | Custo crítico |
| Debugging de código | |

## Melhores Práticas

1. Combine com Temperatura Baixa (0-0.3)
2. Peça Verificação
3. Estruture a Saída

---

[Próximo: Auto-consistência →](/tecnicas/auto-consistencia/)
