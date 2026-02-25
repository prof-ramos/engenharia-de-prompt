---
title: "15 Melhores Práticas"
weight: 1
description: "Práticas essenciais para prompts eficazes"
---

# 15 Melhores Práticas

## 1. Forneça Exemplos

3-5 exemplos para few-shot. Modelos aprendem por padrão.

## 2. Design com Simplicidade

```
❌ "Estou visitando Nova York agora com meus dois filhos de 3 anos..."

✅ "Sugira 5 lugares em Nova York para visitar com crianças de 3 anos."
```

## 3. Seja Específico sobre a Saída

```
❌ "Resuma"
✅ "Resuma em 3 bullets de máx. 20 palavras cada"
```

## 4. Use Instruções Positivas

```
❌ "Não use jargões"
✅ "Use linguagem simples"
```

## 5. Use Delimitadores

```
---TEXTO---
[texto aqui]
---
```

## 6. Use Variáveis

```python
prompt = f"""
Tarefa: {tarefa}
Contexto: {contexto}
"""
```

## 7. Divida Tarefas Complexas

Prompt 1 → Prompt 2 → Prompt 3

## 8. Peça Auto-verificação

```
Antes de responder, verifique:
1. Formato está correto?
2. Todas as partes foram respondidas?
```

## 9. Documente Iterações

| Versão | Prompt | Resultado |
|--------|--------|-----------|
| 1.0 | ... | 70% |
| 1.1 | ... | 85% |

## 10. Teste Edge Cases

- Entrada vazia
- Texto muito longo
- Caracteres especiais

## 11. Controle Alucinações

```
"Responda apenas com informações do texto."
"Se não souber, diga 'Não disponível'."
```

## 12. Balanceie Classes em Few-shot

Positivo, Negativo, Positivo, Negativo...

## 13. Adapte-se ao Modelo

Cada modelo tem características diferentes.

## 14. Teste Formatos de Saída

JSON, Markdown, Lista, etc.

## 15. Use CoT com Moderação

- ✅ Lógica, matemática
- ❌ Classificação simples
