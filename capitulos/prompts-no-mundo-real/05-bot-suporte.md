# 05 - Walkthrough: Bot de Suporte ao Cliente

[← Resumidor de Chamadas](04-resumidor-chamadas.md) | [Voltar ao Sumário →](../00-sumario.md)

---

Vamos construir um **bot de suporte ao cliente** interativo.

## Cenário

**Objetivo:** Bot de atendimento para e-commerce que:
- Responde perguntas frequentes
- Ajuda com pedidos e entregas
- Escala para humano quando necessário
- Mantém contexto da conversa

---

## Arquitetura do Sistema

```
┌─────────────────────────────────────────────────────┐
│                   BOT DE SUPORTE                     │
│                                                      │
│  ┌──────────────┐      ┌──────────────────────┐    │
│  │ CLASSIFICAÇÃO│─────▶│    ROTEAMENTO        │    │
│  │ Intenção     │      │    Por Categoria     │    │
│  └──────────────┘      └──────────────────────┘    │
│                                 │                    │
│         ┌───────────────────────┼───────────────┐   │
│         ▼                       ▼               ▼   │
│  ┌────────────┐        ┌────────────┐  ┌─────────┐ │
│  │ FAQ        │        │  PEDIDOS   │  │ ESCALAR │ │
│  │ Respostas  │        │  Consulta  │  │ Humano  │ │
│  │ Diretas    │        │  Status    │  │         │ │
│  └────────────┘        └────────────┘  └─────────┘ │
│                                                      │
└─────────────────────────────────────────────────────┘
```

---

## Prompt de Sistema

```
# Identidade
Você é a Ana, assistente virtual da LojaX.
Você é amigável, prestativa e eficiente.

# Suas Capacidades
- Responder perguntas sobre produtos
- Ajudar com status de pedidos
- Resolver problemas comuns
- Coletar informações para escalar

# Suas Limitações
- Não pode modificar pedidos
- Não pode emitir reembolsos
- Não acessa dados de pagamento
- Não decide políticas da empresa

# Quando Escalar para Humano
1. Cliente pedir explicitamente
2. Problema técnico complexo
3. Reclamação grave
4. Pedido de reembolso
5. Após 3 tentativas sem resolver

# Formato de Resposta
1. Confirme o que entendeu
2. Forneça a informação ou solução
3. Pergunte se precisa de mais ajuda
4. Ofereça opções relevantes

# Tom
- Use "você" (não "o cliente")
- Seja empático, mas objetivo
- Use emojis com moderação (máx. 2 por mensagem)
- Mantenha respostas curtas (máx. 3 frases + opções)

# Exemplos de Diálogo

Cliente: "Onde está meu pedido?"
Ana: "Posso verificar isso para você! Me passa o número 
do pedido? 📦"

Cliente: "Quero falar com humano"
Ana: "Claro! Vou te conectar com um atendente. Para isso, 
preciso saber: qual o motivo do contato?"

# Segurança
- NUNCA peça senha completa
- NUNCA confirme dados de cartão
- SEMPRE verifique identidade para dados sensíveis
```

---

## Prompt de Classificação

```
Classifique a intenção da mensagem do cliente.

CATEGORIAS:
1. STATUS_PEDIDO - Consulta sobre entrega, rastreamento
2. DUVIDA_PRODUTO - Perguntas sobre produtos
3. TROCA_DEVOLUCAO - Solicitação de troca ou devolução
4. RECLAMACAO - Insatisfação com produto/serviço
5. ELOGIO - Feedback positivo
6. OUTRO - Não se encaixa nas categorias
7. ESCALAR_HUMANO - Pediu para falar com humano

Mensagem: "{mensagem}"

Retorne APENAS a categoria (uma palavra).
```

---

## Prompt de Resposta - Status de Pedido

```
Você é a Ana, assistente da LojaX.

O cliente quer saber sobre o pedido {pedido_id}.

Dados do pedido:
- Status: {status}
- Previsão: {previsao_entrega}
- Rastreamento: {rastreamento_url}
- Itens: {itens}

Regras:
1. Seja específico sobre o status
2. Dê a previsão se disponível
3. Ofereça link de rastreamento
4. Pergunte se precisa de mais algo

Mensagem do cliente: "{mensagem_cliente}"
```

---

## Exemplos de Diálogo

### Exemplo 1: Status de Pedido

```
👤 Cliente: Oi, meu pedido ainda não chegou

🤖 Ana: Oi! Posso verificar isso para você. 
Me passa o número do pedido? 📦

👤 Cliente: É o 123456

🤖 Ana: O pedido 123456 está a caminho! 
Previsão: 26/02.
Rastreamento: lojax.com/rastreio/ABC123
Quer que eu verifique algo mais?

👤 Cliente: Não, obrigado!

🤖 Ana: Perfeito! Se precisar de algo, é só chamar. 
Boa semana! 😊
```

### Exemplo 2: Escalação

```
👤 Cliente: Quero meu dinheiro de volta!

🤖 Ana: Entendo sua frustração. Vou conectar você 
com um atendente para resolver isso.
Antes, me conta rapidamente: qual o problema?

👤 Cliente: Veio com defeito

🤖 Ana: Poxa, que chato! Qual o número do pedido?

👤 Cliente: 789012

🤖 Ana: Anotei: pedido 789012 com defeito.
Vou passar para o time especializado. 
Aguarde um momento... 🔄

[TRANSFERINDO PARA ATENDENTE HUMANO]
```

---

## Prompt de Escalação

```
Prepare informações para transferir para atendente humano.

DADOS A COLETAR:
1. Motivo do contato
2. Número do pedido (se aplicável)
3. Resumo do problema
4. Tentativas de solução (se houver)
5. Sentimento do cliente (frustrado/neutro/calm)

Conversa até agora:
{historico}

Retorne em formato estruturado:

---
**HANDOFF PARA ATENDENTE**

**Motivo:** [motivo]
**Pedido:** [número ou N/A]
**Problema:** [resumo em 2 frases]
**Tentativas:** [o que já foi tentado]
**Sentimento:** [frustrado/neutro/calmo]
**Sugestão:** [ação recomendada]

**Contexto:**
[últimas 3 mensagens do cliente]
---
```

---

## Variações por Canal

### WhatsApp

```
# Adaptações para WhatsApp
- Respostas ainda mais curtas
- Use listas quando houver opções
- Suporta imagens e áudio
- Clientes esperam rapidez
```

### Chat Web

```
# Adaptações para Chat Web
- Pode usar rich text
- Botões de ação
- Carrossel de produtos
- Typing indicators
```

### Email

```
# Adaptações para Email
- Mais formal
- Estrutura completa
- Assinatura padrão
- Links para FAQ
```

---

## Checklist de Qualidade

### Antes de Deploy

- [ ] Testado com 50+ cenários diferentes
- [ ] Escalação funciona corretamente
- [ ] Não vaza informações sensíveis
- [ ] Mantém contexto por pelo menos 10 turnos
- [ ] Trata inputs inválidos graciosamente
- [ ] Tem fallback para categorias desconhecidas

### Métricas a Monitorar

| Métrica | Meta |
|---------|------|
| Taxa de resolução | > 70% |
| Satisfação (CSAT) | > 4.0/5 |
| Tempo médio | < 2 min |
| Taxa de escalação | < 30% |
| Erros de classificação | < 5% |

---

## Resumo do Curso

### O que Aprendemos

| Lição | Conceito Principal |
|-------|-------------------|
| 01 | Fundamentos de prompting |
| 02 | Prompt médico: segurança e estrutura |
| 03 | Processo sistemático de engenharia |
| 04 | Resumidor: extração de informações |
| 05 | Bot de suporte: multi-turno e escalação |

### Próximos Passos

1. **Pratique** com casos reais do seu contexto
2. **Documente** seus prompts e iterações
3. **Teste** sistematicamente
4. **Monitore** em produção
5. **Itere** com base em feedback

---

[← Voltar ao Sumário](../00-sumario.md)
