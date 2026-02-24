# 07 - Melhores Práticas

[← APE](06-ape.md) | [Próximo: Anti-Padrões →](08-anti-padroes.md)

---

## 1. ✅ Forneça Exemplos

**Recomendação:** 3-5 exemplos para few-shot

Modelos aprendem por padrão. Exemplos mostram exatamente o que você espera.

---

## 2. ✅ Design com Simplicidade

**Antes:**
> Estou visitando Nova York agora com meus dois filhos de 3 anos e gostaria de saber sobre ótimos locais para visitar...

**Depois:**
> Sugira 5 lugares em Nova York para visitar com crianças de 3 anos.

> Se está confuso para você, está confuso para o modelo.

---

## 3. ✅ Seja Específico sobre a Saída

| ❌ Vago | ✅ Específico |
|---------|---------------|
| "Resuma" | "Resuma em 3 bullets de máx. 20 palavras cada" |
| "Classifique" | "Classifique como A, B ou C. Retorne apenas a letra." |

---

## 4. ✅ Use Instruções Positivas

| ❌ Negativo | ✅ Positivo |
|-------------|-------------|
| "Não use jargões" | "Use linguagem simples" |
| "Não seja longo" | "Seja conciso (máx. 100 palavras)" |

---

## 5. ✅ Use Delimitadores

```
Analise o texto:

---TEXTO---
[texto aqui]
---FIM---

Identifique: tema, tom, público.
```

**Delimitadores comuns:** `---`, `"""`, ``` ``` ```, `<tags>`

---

## 6. ✅ Use Variáveis

```python
prompt = """
Você é um {papel}.
Tarefa: {tarefa}
Contexto: {contexto}
"""
```

---

## 7. ✅ Divida Tarefas Complexas

**Em vez de:**
```
Analise, identifique riscos, sugira melhorias, calcule...
```

**Divida:**
```
Prompt 1: Extraia cláusulas
Prompt 2: Analise riscos
Prompt 3: Sugira melhorias
```

---

## 8. ✅ Peça Auto-verificação

```
Antes de responder, verifique:
1. Formato está correto?
2. Todas as partes foram respondidas?
3. Há contradições?
```

---

## 9. ✅ Documente Iterações

| Versão | Prompt | Config | Resultado |
|--------|--------|--------|-----------|
| 1.0 | [texto] | temp=0.5 | 70% |
| 1.1 | [texto] | temp=0.3 | 85% |

---

## 10. ✅ Teste Edge Cases

- Entrada vazia
- Texto muito longo
- Caracteres especiais
- Informações ambíguas

---

## 11. ✅ Controle Alucinações

```
"Responda apenas com informações do texto."
"Se não souber, diga 'Não disponível'."
"Para cada afirmação, cite a frase exata."
```

---

## 12. ✅ Balanceie Classes em Few-shot

```
✅ Positivo, Negativo, Positivo, Negativo
❌ Positivo, Positivo, Positivo, Negativo
```

---

## 13. ✅ Adapte-se ao Modelo

| Modelo | Dica |
|--------|------|
| GPT-4 | Peça concisão |
| Claude | Ótimo para instruções longas |
| Gemini | Aproveite multimodalidade |

---

## 14. ✅ Teste Formatos de Saída

| Formato | Quando Usar |
|---------|-------------|
| JSON | APIs, integração |
| Markdown | Documentos |
| Lista | Leitura rápida |

---

## 15. ✅ Use CoT com Moderação

- ✅ Lógica, matemática, debugging
- ❌ Classificação simples, uma palavra

---

[Próximo: Anti-Padrões →](08-anti-padroes.md)
