# 04 - Walkthrough: Resumidor de Chamadas

[← Processo](03-processo.md) | [Próximo: Bot de Suporte →](05-bot-suporte.md)

---

Vamos construir um prompt para **resumir chamadas de atendimento ao cliente**.

## Cenário

**Objetivo:** Resumir transcrições de chamadas de suporte para:
- Documentação rápida
- Handoff entre agentes
- Análise de qualidade

**Requisitos:**
- Identificar problema e solução
- Extrair dados do cliente
- Máximo 200 palavras
- Formato estruturado

---

## Versão 1: Básico

```
Resuma a chamada abaixo:

{transcricao}
```

**Problemas:**
- ❌ Sem estrutura
- ❌ Pode ser muito longo
- ❌ Não extrai informações específicas

---

## Versão 2: Com Estrutura

```
Resuma a chamada de atendimento abaixo no seguinte formato:

PROBLEMA: [descrição]
SOLUÇÃO: [descrição]
PRÓXIMO PASSO: [descrição]

Transcrição:
{transcricao}
```

**Melhorias:**
- ✅ Estrutura básica
- ❌ Sem limite de tamanho
- ❌ Não extrai dados do cliente

---

## Versão 3: Completa

```
# Papel
Você é um especialista em resumir chamadas de atendimento ao cliente.

# Tarefa
Analise a transcrição da chamada e crie um resumo estruturado.

# Informações a Extrair
1. Dados do cliente (nome, conta, contato)
2. Motivo da chamada
3. Problema relatado
4. Solução aplicada
5. Próximos passos
6. Sentimento do cliente (positivo/negativo/neutro)

# Formato de Saída

## 📋 Resumo da Chamada

### Dados do Cliente
- Nome: [nome ou "Não informado"]
- Conta: [número ou "Não informado"]
- Contato: [email/telefone ou "Não informado"]

### Motivo
[1 frase descrevendo o motivo principal]

### Problema
[Descrição detalhada do problema em 2-3 frases]

### Solução
[O que foi feito para resolver, em 2-3 frases]

### Próximos Passos
- [Ação 1]
- [Ação 2]

### Sentimento do Cliente
[POSITIVO/NEGATIVO/NEUTRO] - [breve justificativa]

---
📊 Tempo estimado da chamada: [X minutos]
🏷️ Categoria: [Dúvida/Problema técnico/Reclamação/Outro]

# Restrições
- Máximo 200 palavras no total
- Se informação não estiver na transcrição, usar "Não informado"
- Não invente informações
- Seja objetivo e factual

# Transcrição
{transcricao}
```

---

## Exemplo de Entrada

```
Agente: Bom dia, atendimento da Empresa X. Meu nome é João.
Cliente: Oi, bom dia. É o Carlos da Silva.
Agente: Opa, Carlos! Como posso ajudar?
Cliente: Tô com problema no meu plano. Tava vendo a fatura aqui, 
        veio cobrando o dobro do valor normal.
Agente: Entendi. Deixa eu verificar aqui. Qual seu CPF?
Cliente: 123.456.789-00
Agente: Ok, encontrei. Você tem o plano Premium, né? O valor 
        normal é R$ 99,90. Deixou vir R$ 199,80?
Cliente: Isso mesmo! O dobro!
Agente: Vou verificar aqui... Ah, encontrei o problema. Houve uma 
        cobrança duplicada no sistema. Vou estornar a diferença 
        agora mesmo.
Cliente: Ah, perfeito! Quando entra?
Agente: Em até 3 dias úteis na sua fatura. Você recebe 
        confirmação por email.
Cliente: Show, obrigado!
Agente: De nada! Precisando, é só chamar. Até mais!
Cliente: Até!
```

---

## Exemplo de Saída

```markdown
## 📋 Resumo da Chamada

### Dados do Cliente
- Nome: Carlos da Silva
- Conta: CPF 123.456.789-00
- Contato: Não informado

### Motivo
Cliente questionou cobrança duplicada na fatura do plano Premium.

### Problema
Cliente identificou que a fatura veio com valor dobrado 
(R$ 199,80 ao invés de R$ 99,90). Cobrança duplicada no sistema.

### Solução
Agente identificou o erro no sistema e iniciou estorno da 
diferença (R$ 99,90). Prazo de até 3 dias úteis.

### Próximos Passos
- Aguardar estorno em até 3 dias úteis
- Cliente receberá confirmação por email

### Sentimento do Cliente
POSITIVO - Cliente satisfeito com a resolução rápida

---
📊 Tempo estimado da chamada: 2-3 minutos
🏷️ Categoria: Problema técnico
```

---

## Variações do Prompt

### Versão Curtíssima (para dashboards)

```
Resuma em 1 frase (máx. 50 palavras):
PROBLEMA → SOLUÇÃO → PRÓXIMO PASSO

{transcricao}
```

### Versão com Análise de Qualidade

```
[Adicionar ao prompt anterior]

### Avaliação de Qualidade
- Saudação: [✅ Correta / ❌ Incorreta / ⚠️ Ausente]
- Verificação de segurança: [✅ Feita / ❌ Não feita]
- Solução: [✅ Completa / ⚠️ Parcial / ❌ Não resuelta]
- Nota geral: [1-5]
```

---

## Lições Aprendidas

| Aspecto | Aprendizado |
|---------|-------------|
| **Formato** | Estrutura consistente facilita consumo |
| **Dados** | Separar dados em campos específicos |
| **Valores nulos** | Definir comportamento para "não informado" |
| **Flexibilidade** | Ter versões para diferentes necessidades |

---

[Próximo: Bot de Suporte →](05-bot-suporte.md)
