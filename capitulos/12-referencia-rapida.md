# 12 - Referência Rápida

[← Troubleshooting](11-troubleshooting.md) | [Voltar ao Sumário →](00-sumario.md)

---

## Técnicas por Tarefa

| Tarefa | Técnicas |
|--------|----------|
| Classificação | Zero-shot, Few-shot |
| Extração | Few-shot, JSON |
| Resumo | Sistema, Contexto |
| Raciocínio | CoT, Step-back |
| Criatividade | Papel, Temperatura alta |
| Código | Sistema, CoT |
| Análise | Papel, CoT, Step-back |
| Conversação | Sistema, Papel, Contexto |

---

## Configurações por Tarefa

| Tarefa | Temperatura | Top-P | Top-K |
|--------|-------------|-------|-------|
| Fatos/Código | 0 | 0.9 | 20 |
| Classificação | 0.1 | 0.9 | 20 |
| Resumo | 0.2 | 0.95 | 30 |
| Conversação | 0.5 | 0.95 | 40 |
| Criatividade | 0.8 | 0.99 | 50 |

---

## Frases Mágicas

| Objetivo | Frase |
|----------|-------|
| Ativar CoT | `"Vamos pensar passo a passo."` |
| Evitar alucinação | `"Se não estiver no texto, responda 'Não disponível'."` |
| Garantir formato | `"Retorne APENAS o JSON, sem texto adicional."` |
| Melhor raciocínio | `"Pense cuidadosamente antes de responder."` |
| Auto-verificação | `"Verifique sua resposta antes de finalizar."` |
| Ser conciso | `"Seja conciso. Máximo 100 palavras."` |
| Formato específico | `"Responda no formato: [exemplo]"` |

---

## Estrutura de Prompt

```
[PAPEL - opcional]
Você é um {papel}.

[CONTEXTO]
{informações relevantes}

[TAREFA]
{descrição clara do que fazer}

[FORMATO]
{como deve ser a saída}

[RESTRIÇÕES - opcional]
{limitações}

[EXEMPLOS - opcional]
{few-shot examples}
```

---

## Delimitadores

| Tipo | Uso |
|------|-----|
| `---` | Separar seções |
| `"""` | Texto longo |
| ``` ``` ``` | Código |
| `<tag></tag>` | Estrutura XML |
| `###` | Cabeçalhos |

---

## Checklist Rápido

```
✅ Tarefa clara?
✅ Formato especificado?
✅ Contexto suficiente?
✅ Exemplos (se necessário)?
✅ Temperatura adequada?
```

---

## Links Rápidos

- [Introdução](01-introducao.md)
- [Configurações](03-configuracoes.md)
- [Zero-shot](tecnicas/01-zero-shot.md)
- [CoT](tecnicas/07-cot.md)
- [Templates](10-templates.md)
- [Troubleshooting](11-troubleshooting.md)

---

[← Voltar ao Sumário](00-sumario.md)
