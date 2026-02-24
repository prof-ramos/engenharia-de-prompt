# 08 - Anti-Padrões ⚠️

[← Melhores Práticas](07-melhores-praticas.md) | [Próximo: Checklist →](09-checklist.md)

---

## 1. ❌ Prompts Vagos

```
"Fale sobre marketing"
```

**Problema:** Sem direção, escopo ou formato.

**Correção:**
```
"Explique 5 estratégias de marketing digital para pequenas empresas 
em 200 palavras, usando bullet points."
```

---

## 2. ❌ Instruções Conflitantes

```
"Seja breve mas cubra todos os detalhes importantes"
```

**Problema:** Impossível satisfazer ambas.

**Correção:**
```
"Resuma os 3 pontos mais importantes em 100 palavras."
```

---

## 3. ❌ Ambiguidade

```
"O prêmio foi de 1000 reais. Quanto João recebeu?"
```

**Problema:** Não diz como foi dividido.

**Correção:**
```
"O prêmio de 1000 reais foi dividido igualmente entre João e Maria. 
Quanto João recebeu?"
```

---

## 4. ❌ Sobrecarga de Instruções

```
"Seja formal mas amigável, técnico mas simples, 
conciso mas detalhado, humorístico mas profissional..."
```

**Problema:** Muitas restrições conflitantes.

**Correção:**
```
Escolha 2-3 características principais.
"Use tom profissional mas acessível, com exemplos práticos."
```

---

## 5. ❌ Assumir Conhecimento

```
"Use a metodologia XYZ para analisar."
```

**Problema:** Modelo pode não conhecer ou ter definição diferente.

**Correção:**
```
"Use a metodologia XYZ (descrita abaixo) para analisar..."

[Método XYZ: 1. Identificar... 2. Avaliar... 3. Priorizar...]
```

---

## 6. ❌ Exemplos Inconsistentes

```
EXEMPLO 1: Saída = "Positivo"
EXEMPLO 2: A resposta é: Negativo
EXEMPLO 3: POSITIVO
```

**Problema:** Formatos diferentes confundem o modelo.

**Correção:**
```
EXEMPLO 1: "Positivo"
EXEMPLO 2: "Negativo"
EXEMPLO 3: "Positivo"
```

---

## Resumo

| Anti-Padrão | Solução |
|-------------|---------|
| Vago | Seja específico |
| Conflitante | Priorize |
| Ambíguo | Explicitar |
| Sobrecarregado | Simplificar |
| Assumir conhecimento | Explicar |
| Inconsistente | Padronizar |

---

[Próximo: Checklist →](09-checklist.md)
