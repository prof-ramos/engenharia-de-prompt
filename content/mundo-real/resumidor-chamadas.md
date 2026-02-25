---
title: "Walkthrough: Resumidor de Chamadas"
weight: 4
description: "Exemplo completo: resumo de atendimentos"
---

# Resumidor de Chamadas

Vamos construir um prompt para **resumir chamadas de atendimento**.

## Cenário

- Documentação rápida
- Handoff entre agentes
- Análise de qualidade
- Máximo 200 palavras

## Prompt Completo

```
# Papel
Você é especialista em resumir chamadas de atendimento.

# Tarefa
Analise a transcrição e crie um resumo estruturado.

# Informações a Extrair
1. Dados do cliente (nome, conta)
2. Motivo da chamada
3. Problema relatado
4. Solução aplicada
5. Próximos passos
6. Sentimento do cliente

# Formato de Saída

## 📋 Resumo da Chamada

### Dados do Cliente
- Nome: [ou "Não informado"]
- Conta: [ou "Não informado"]

### Motivo
[1 frase]

### Problema
[2-3 frases]

### Solução
[2-3 frases]

### Próximos Passos
- [Ação 1]
- [Ação 2]

### Sentimento
[POSITIVO/NEGATIVO/NEUTRO]

---
📊 Tempo: [X min]
🏷️ Categoria: [Dúvida/Problema/Reclamação]

# Restrições
- Máximo 200 palavras
- Não invente informações
- Seja objetivo

# Transcrição
{transcricao}
```

## Exemplo de Saída

```markdown
## 📋 Resumo da Chamada

### Dados do Cliente
- Nome: Carlos da Silva
- Conta: CPF 123.456.789-00

### Motivo
Cliente questionou cobrança duplicada na fatura.

### Problema
Fatura veio com valor dobrado (R$ 199,80 ao invés de R$ 99,90).

### Solução
Identificado erro no sistema. Estorno iniciado.

### Próximos Passos
- Aguardar estorno em até 3 dias úteis

### Sentimento
POSITIVO

---
📊 Tempo: 2-3 min
🏷️ Categoria: Problema técnico
```
