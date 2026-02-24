# 🎯 Engenharia de Prompt - Guia Completo

**Autor original:** Lee Boonstra (Google)  
**Versão:** 2.0 | **Atualização:** Fevereiro 2025  
**Idioma:** Português (Brasil)

---

## 📑 Índice

1. [Introdução](#introdução)
2. [Como LLMs Funcionam](#como-llms-funcionam)
3. [Configurações de Saída](#configurações-de-saída)
   - [Comprimento da Saída](#comprimento-da-saída)
   - [Temperatura](#temperatura)
   - [Top-K e Top-P](#top-k-e-top-p)
   - [Guia Rápido de Configurações](#guia-rápido-de-configurações)
4. [Técnicas de Prompting](#técnicas-de-prompting)
   - [Zero-shot](#1-zero-shot)
   - [One-shot e Few-shot](#2-one-shot-e-few-shot)
   - [Prompt de Sistema](#3-prompt-de-sistema)
   - [Prompt de Papel (Role)](#4-prompt-de-papel-role)
   - [Prompt Contextual](#5-prompt-contextual)
   - [Step-back (Recuo)](#6-step-back-recuo)
   - [Cadeia de Pensamento (CoT)](#7-cadeia-de-pensamento-cot)
   - [Auto-consistência](#8-auto-consistência)
   - [Árvore de Pensamentos (ToT)](#9-árvore-de-pensamentos-tot)
   - [ReAct (Raciocinar e Agir)](#10-react-raciocinar-e-agir)
5. [Prompting para Código](#prompting-para-código)
6. [Engenharia Automática de Prompts](#engenharia-automática-de-prompts-ape)
7. [Melhores Práticas](#melhores-práticas)
8. [Anti-Padrões](#anti-padrões--o-que-evitar)
9. [Checklist de Revisão](#checklist-de-revisão-de-prompt)
10. [Templates Prontos](#templates-prontos-para-usar)
11. [Troubleshooting](#troubleshooting-comum)
12. [Referência Rápida](#referência-rápida)

---

## Introdução

Um **prompt** é a entrada que um modelo de linguagem grande (LLM) usa para prever uma saída específica. Você não precisa ser cientista de dados ou engenheiro de ML — **qualquer pessoa pode escrever um prompt**.

No entanto, criar prompts eficazes requer prática. Muitos aspectos afetam a qualidade da resposta:

- O modelo escolhido (GPT, Claude, Gemini, LLaMA, etc.)
- As configurações do modelo (temperatura, top-K, top-P)
- A escolha de palavras, estilo e tom
- A estrutura e o contexto fornecido

> **Engenharia de Prompt** é o processo iterativo de projetar entradas de alta qualidade que guiam LLMs a produzir saídas precisas e úteis.

### Este Guia Vai Te Ajudar a:

✅ Entender como LLMs funcionam "por baixo do capô"  
✅ Dominar as principais técnicas de prompting  
✅ Escolher as configurações certas para cada tarefa  
✅ Evitar armadilhas comuns  
✅ Criar prompts robustos e reutilizáveis  

---

## Como LLMs Funcionam

LLMs são **mecanismos de previsão de tokens**:

1. Recebem texto sequencial como entrada
2. Preveem qual deve ser o próximo token (baseado em treinamento)
3. Adicionam o token previsto ao final do texto
4. Repetem o processo

A previsão é baseada na relação entre tokens anteriores e o que o LLM viu durante treinamento.

### O Que Isso Significa na Prática?

| Conceito | Implicação |
|----------|------------|
| **Previsão probabilística** | O modelo não "pensa" — prevê o mais provável |
| **Contexto importa** | Tokens anteriores influenciam os próximos |
| **Treinamento define limites** | O modelo só sabe o que viu no treinamento |
| **Sem memória entre sessões** | Cada conversa começa do zero |

---

## Configurações de Saída

### Comprimento da Saída

Controla quantos tokens o modelo pode gerar.

> ⚠️ **Importante:** Reduzir o limite NÃO faz o modelo mais sucinto — apenas corta a resposta quando atinge o limite. Se precisar de respostas curtas, **ajuste também o prompt**.

**Quando ajustar:**
- APIs com custo por token → limite menor
- Tarefas longas (relatórios, código) → limite maior
- ReAct/agentes → limite generoso (evita cortes em cadeias de raciocínio)

---

### Temperatura

Controla a **aleatoriedade** na seleção de tokens.

| Valor | Comportamento | Uso Ideal |
|-------|---------------|-----------|
| **0** | Determinístico (sempre o token mais provável) | Código, matemática, fatos |
| **0.1 - 0.3** | Baixa variação | Classificação, extração, resumo |
| **0.4 - 0.7** | Equilibrado | Conversação, escrita geral |
| **0.8 - 1.0** | Alta variação | Criatividade, brainstorming |
| **> 1.0** | Muito aleatório | Experimental, surpreendente |

**Analogia:** Temperatura é como a "temperatura softmax" em ML:
- Baixa = alta certeza, poucas opções consideradas
- Alta = mais incerteza, mais opções consideradas

---

### Top-K e Top-P

Restringem quais tokens são candidatos a serem selecionados.

#### Top-K
Seleciona apenas os **K tokens mais prováveis**.

- **Top-K = 1**: Sempre o mais provável (decodificação gananciosa)
- **Top-K = 40**: Considera os 40 mais prováveis
- **Top-K alto** (100+): Praticamente sem restrição

#### Top-P (Amostragem Nuclear)
Seleciona tokens até atingir **probabilidade acumulada P**.

- **Top-P = 0.1**: Muito restritivo
- **Top-P = 0.9**: Padrão comum
- **Top-P = 1.0**: Sem restrição

---

### Guia Rápido de Configurações

| Cenário | Temperatura | Top-P | Top-K | Max Tokens |
|---------|-------------|-------|-------|------------|
| **Código/Debug** | 0 | 0.9 | 20 | 2000 |
| **Matemática/Lógica** | 0 | 0.9 | 20 | 500 |
| **Classificação** | 0.1 | 0.9 | 20 | 100 |
| **Resumo** | 0.2 | 0.95 | 30 | 500 |
| **Conversação** | 0.5 | 0.95 | 40 | 1000 |
| **Escrita Criativa** | 0.8 | 0.99 | 50 | 2000 |
| **Brainstorming** | 0.9 | 0.99 | 60 | 1500 |

> 🔧 **Dica:** Se temperatura = 0, Top-K e Top-P são ignorados. Se Top-K = 1, temperatura é ignorada.

---

## Técnicas de Prompting

### 1. Zero-shot

O prompt mais simples: **sem exemplos**, apenas a instrução.

**Estrutura:**
```
[Instrução clara]
[Contexto/dados de entrada]
[Formato esperado da saída]
```

**Exemplo - Classificação:**

```
Classifique a avaliação abaixo como POSITIVO, NEGATIVO ou NEUTRO.

Avaliação: "O produto chegou antes do prazo, mas a qualidade deixou a desejar."

Classificação:
```

**Saída:** `NEUTRO`

**Quando usar:**
- ✅ Tarefas simples e bem definidas
- ✅ Modelo já treinado para o tipo de tarefa
- ✅ Poucos tokens disponíveis

**Quando evitar:**
- ❌ Tarefas complexas ou ambíguas
- ❌ Formato de saída específico necessário
- ❌ Modelo menos capaz ou desconhecido

---

### 2. One-shot e Few-shot

Fornece **exemplos** para o modelo imitar o padrão.

**One-shot** = 1 exemplo  
**Few-shot** = 3-5 exemplos (recomendado)

**Estrutura:**
```
[Instrução]

EXEMPLO 1:
Entrada: [exemplo de entrada]
Saída: [exemplo de saída]

EXEMPLO 2:
Entrada: [exemplo de entrada]
Saída: [exemplo de saída]

EXEMPLO 3:
Entrada: [exemplo de entrada]
Saída: [exemplo de saída]

Agora faça:
Entrada: [entrada real]
Saída:
```

**Exemplo - Extração de Entidades:**

```
Extraia nomes de pessoas e locais do texto.

EXEMPLO 1:
Texto: "Maria foi a Paris visitar o Louvre."
Saída: {"pessoas": ["Maria"], "locais": ["Paris", "Louvre"]}

EXEMPLO 2:
Texto: "João e Ana se encontraram no café central de São Paulo."
Saída: {"pessoas": ["João", "Ana"], "locais": ["São Paulo", "café central"]}

Texto: "Carlos viajou de Brasília para Rio de Janeiro com sua esposa."
Saída:
```

**Saída:**
```json
{"pessoas": ["Carlos"], "locais": ["Brasília", "Rio de Janeiro"]}
```

> 💡 **Dicas para Few-shot:**
> - Use **3-5 exemplos** (mais que isso raramente ajuda)
> - **Misture as classes** em tarefas de classificação (evite viés)
> - Inclua **casos extremos** (edge cases)
> - Exemplos devem ser **diversos** mas **consistentes** no formato
> - **Evite exemplos ruins** — o modelo copiará os erros

---

### 3. Prompt de Sistema

Define o **comportamento global** do modelo. Ideal para instruções que se aplicam a toda a conversa.

**Estrutura:**
```
[Identidade/Papel]
[Regras de comportamento]
[Formato de saída]
[Restrições]
```

**Exemplo:**

```
Você é um assistente especializado em análise de contratos jurídicos.

REGRAS:
- Identifique cláusulas de risco
- Destaque termos ambíguos
- Sugira melhorias de redação
- Use linguagem técnica mas acessível

FORMATO DE SAÍDA:
Para cada ponto identificado:
1. **Cláusula**: [citação]
2. **Risco**: [baixo/médio/alto]
3. **Explicação**: [análise]
4. **Sugestão**: [recomendação]

RESTRICOES:
- Não dê conselhos legais definitivos
- Sempre sugira consultar um advogado
```

**Benefícios:**
- Consistência em conversas longas
- Define "regras do jogo" uma vez
- Útil para chatbots e agentes

---

### 4. Prompt de Papel (Role)

Atribui uma **identidade/especialidade** ao modelo.

**Técnicas eficazes:**

| Papel | Quando Usar |
|-------|-------------|
| "Você é um expert em [área]" | Tarefas técnicas |
| "Aja como um [profissão]" | Tom específico |
| "Imagine que você é [pessoa]" | Perspectiva diferente |
| "Você tem 20 anos de experiência em [área]" | Autoridade |

**Exemplos:**

```
# Técnico
Você é um engenheiro de software sênior com 15 anos de experiência em Python e arquitetura de sistemas distribuídos. Revise o código abaixo focando em performance e escalabilidade.

# Criativo
Aja como um copywriter de propaganda premiada. Crie 5 headlines impactantes para um aplicativo de meditação.

# Educacional
Você é um professor de física do ensino médio. Explique relatividade para um estudante de 16 anos usando analogias do dia a dia.

# Crítico
Imagine que você é um investidor conservador analisando este pitch de startup. Identifique 5 riscos principais.
```

**Estilos de tom:**
- Direto
- Formal
- Informal
- Humorístico
- Inspiracional
- Persuasivo
- Descritivo
- Confrontacional
- Influente

---

### 5. Prompt Contextual

Fornece **informações específicas** relevantes para a tarefa atual.

**Tipos de contexto:**

| Tipo | Exemplo |
|------|---------|
| **Público-alvo** | "Este texto é para CEOs de startups" |
| **Restrições** | "Máximo 280 caracteres" |
| **Preferências** | "Prefira bullet points a parágrafos" |
| **Antecedentes** | "O usuário já tentou X e Y" |
| **Tom desejado** | "Tom profissional mas amigável" |

**Exemplo:**

```
CONTEXTO:
- Público: Gerentes de projeto iniciantes
- Objetivo: Explicar metodologias ágeis
- Restrição: Máximo 300 palavras
- Tom: Educativo e encorajador
- Formato: Comparação em tabela

TAREFA:
Compare Scrum e Kanban para iniciantes.
```

---

### 6. Step-back (Recuo)

Faz uma **pergunta geral primeiro**, depois usa a resposta para a tarefa específica.

**Processo:**
1. Pergunta geral/abstrata → ativa conhecimento amplo
2. Resposta como contexto → guia raciocínio específico

**Exemplo - Criando campanha de marketing:**

**Passo 1 (Recuo):**
```
Quais são os 5 princípios fundamentais de uma campanha de marketing digital bem-sucedida para produtos SaaS B2B?
```

**Resposta:** (1) Proposta de valor clara, (2) Persona definida, (3) Funil estruturado, (4) Prova social, (5) CTA persuasivo

**Passo 2 (Específico):**
```
Considerando esses 5 princípios:
[lista a resposta acima]

Crie uma campanha de marketing para um software de gestão de estoque para pequenos varejistas.
```

**Benefícios:**
- Ativa conhecimento mais amplo
- Reduz viés de detalhes específicos
- Melhora qualidade do raciocínio

---

### 7. Cadeia de Pensamento (CoT)

Faz o modelo **explicitar o raciocínio** passo a passo.

**Técnicas de ativação:**

| Técnica | Exemplo |
|---------|---------|
| Frase mágica | "Vamos pensar passo a passo." |
| Instrução direta | "Explique seu raciocínio antes de responder." |
| Few-shot com CoT | Exemplos que mostram raciocínio |

**Exemplo - Problema Lógico:**

❌ **Sem CoT:**
```
Um tanque tem 500L de água. Uma torneira enche 30L/h, outra esvazia 10L/h. Quanto tempo para encher?
```
Saída: `25 horas` (errado)

✅ **Com CoT:**
```
Um tanque tem 500L de água. Uma torneira enche 30L/h, outra esvazia 10L/h. Quanto tempo para encher?

Vamos pensar passo a passo.
```

Saída:
```
1. Volume necessário: 500L - 500L = 0L (já está cheio? Vou assumir que está vazio)
   Volume para encher: 500L

2. Taxa líquida de enchimento:
   Entra: 30L/h
   Sai: 10L/h
   Líquido: 30 - 10 = 20L/h

3. Tempo = Volume / Taxa
   Tempo = 500L / 20L/h = 25 horas

Resposta: 25 horas
```

> 📝 **Nota:** Neste caso a resposta está correta, mas sem CoT o modelo poderia ter pulado etapas.

**Quando usar CoT:**
- ✅ Matemática e lógica
- ✅ Problemas multi-passo
- ✅ Análise complexa
- ✅ Debugging de código
- ✅ Tomada de decisão

**Melhores Práticas CoT:**
- Combine com few-shot para tarefas complexas
- Use temperatura baixa (0-0.3)
- Peça explicitamente "pense alto"
- Monitore custo de tokens

---

### 8. Auto-consistência

Gera **múltiplas respostas** e escolhe a mais frequente (votação).

**Processo:**
1. Execute o mesmo prompt N vezes (temperatura alta)
2. Extraia a resposta de cada execução
3. Conte a frequência de cada resposta
4. Retorne a mais comum

**Exemplo - Classificação Ambígua:**

```
Email: "Olá, notei que seu site tem uma vulnerabilidade XSS interessante. 
Não se preocupe, não vou explorar. Só achei curioso. Abraços, Hackerman."

Classifique como: IMPORTANTE ou NÃO IMPORTANTE.
```

**Execução 1:** IMPORTANTE (risco de segurança)  
**Execução 2:** NÃO IMPORTANTE (tom amigável, sem ameaça)  
**Execução 3:** IMPORTANTE (vulnerabilidade real)  
**Execução 4:** IMPORTANTE (deve ser verificado)  
**Execução 5:** NÃO IMPORTANTE (parece teste amigável)

**Resultado por votação:** IMPORTANTE (3/5)

> ⚠️ **Trade-off:** Alto custo (N× tokens) mas maior confiança na resposta.

---

### 9. Árvore de Pensamentos (ToT)

Explora **múltiplos caminhos de raciocínio** em paralelo, ramificando como uma árvore.

**Diferença para CoT:**
- **CoT:** Uma cadeia linear de pensamentos
- **ToT:** Múltiplas cadeias ramificadas, podendo voltar e tentar outro caminho

**Estrutura:**
```
              [Problema]
                 |
        ┌────────┼────────┐
      [Opção A] [Opção B] [Opção C]
          |         |         |
      [A.1]     [B.1]     [C.1]
      [A.2]     [B.2]     [C.2]
          ↓         ↓         ↓
      [Eval A]  [Eval B]  [Eval C]
          └────────┼────────┘
                   ↓
            [Melhor Solução]
```

**Quando usar:**
- Problemas de otimização
- Jogos e puzzles
- Planejamento complexo
- Decisões com múltiplas alternativas

---

### 10. ReAct (Raciocinar e Agir)

Combina **raciocínio** com **uso de ferramentas** externas.

**Ciclo ReAct:**
1. **Thought** (Pensamento): O que preciso fazer?
2. **Action** (Ação): Qual ferramenta usar?
3. **Observation** (Observação): O que aconteceu?
4. Repete até completar

**Exemplo:**

```
Pergunta: Quantos filhos os membros do Metallica têm no total?

Thought: Preciso descobrir quem são os membros da banda e quantos filhos cada um tem.

Action: Search[Membros do Metallica]
Observation: James Hetfield, Lars Ulrich, Kirk Hammett, Robert Trujillo

Thought: Agora preciso descobrir quantos filhos cada um tem.

Action: Search[Quantos filhos James Hetfield tem]
Observation: Três filhos: Cali, Castor e Marcella

Action: Search[Quantos filhos Lars Ulrich tem]
Observation: Três filhos

Action: Search[Quantos filhos Kirk Hammett tem]
Observation: Dois filhos: Angel e Vincenzo

Action: Search[Quantos filhos Robert Trujillo tem]
Observation: Dois filhos

Thought: Agora posso somar: 3 + 3 + 2 + 2 = 10

Answer: Os membros do Metallica têm 10 filhos no total.
```

**Ferramentas comuns em ReAct:**
- Busca web
- Calculadora
- Executor de código
- APIs externas
- Banco de dados

---

## Prompting para Código

### Escrever Código

```
Escreva uma função Python que [descrição clara].

Requisitos:
- [Requisito 1]
- [Requisito 2]
- [Requisito 3]

Inclua:
- Docstring
- Type hints
- Tratamento de erros
- Exemplos de uso
```

### Explicar Código

```
Explique o código abaixo para um desenvolvedor júnior:

[código]

Cubra:
1. O que o código faz (visão geral)
2. Como funciona (passo a passo)
3. Conceitos importantes utilizados
4. Possíveis melhorias
```

### Traduzir Código

```
Traduza este código de [linguagem A] para [linguagem B]:

[código original]

Mantenha:
- A mesma lógica
- Boas práticas da linguagem destino
- Comentários relevantes
```

### Debugar Código

```
O código abaixo está apresentando o seguinte erro:

[erro/stack trace]

Código:
[código com bug]

Por favor:
1. Identifique a causa do erro
2. Explique por que acontece
3. Forneça o código corrigido
4. Sugira como evitar erros similares
```

### Revisar Código

```
Revise o código abaixo como um engenheiro sênior:

[código]

Avalie:
- Legibilidade
- Performance
- Segurança
- Manutenibilidade
- Padrões e boas práticas

Para cada ponto, dê nota (1-10) e sugestão de melhoria.
```

---

## Engenharia Automática de Prompts (APE)

Usa o próprio LLM para **gerar e otimizar prompts**.

**Processo:**

1. **Geração:** LLM cria N variantes do prompt
2. **Avaliação:** Testa cada variante com métricas (BLEU, ROUGE, accuracy)
3. **Seleção:** Escolhe a melhor variante
4. **Refinamento:** Itera sobre a melhor

**Exemplo:**

```
Tarefa: Criar prompts para um chatbot de e-commerce que ajuda clientes a encontrar produtos.

Prompt de entrada: "Quero uma camisa azul"

Gere 10 variantes de como clientes podem formular esse pedido:
```

**Saída:**
1. "Estou procurando uma camisa na cor azul"
2. "Vocês têm camisas azuis?"
3. "Me mostra as opções de camisa azul"
4. "Quero ver camisas masculinas azuis"
...

**Uso:** Treinar modelos, gerar datasets sintéticos, testar robustez.

---

## Melhores Práticas

### 1. ✅ Forneça Exemplos

**Recomendação:** 3-5 exemplos para few-shot

**Por que funciona:** Modelos aprendem por padrão. Exemplos mostram exatamente o que você espera.

---

### 2. ✅ Design com Simplicidade

**Antes:**
> Estou visitando Nova York agora com meus dois filhos de 3 anos e gostaria de saber sobre ótimos locais para visitar durante nossas férias de verão, considerando que as crianças ficam cansadas facilmente.

**Depois:**
> Sugira 5 lugares em Nova York para visitar com crianças de 3 anos. Prefira locais com ar-condicionado e tempo de visita curto (máx. 2h).

**Princípio:** Se está confuso para você, está confuso para o modelo.

---

### 3. ✅ Seja Específico sobre a Saída

| ❌ Vago | ✅ Específico |
|---------|---------------|
| "Resuma o texto" | "Resuma em 3 bullet points de no máximo 20 palavras cada" |
| "Classifique" | "Classifique como A, B ou C. Retorne apenas a letra." |
| "Explique" | "Explique em 2 parágrafos para um público leigo" |

---

### 4. ✅ Use Instruções Positivas

| ❌ Negativo | ✅ Positivo |
|-------------|-------------|
| "Não use jargões" | "Use linguagem simples e acessível" |
| "Não seja longo" | "Seja conciso (máx. 100 palavras)" |
| "Não invente" | "Responda apenas com informações do texto fornecido" |

---

### 5. ✅ Use Delimitadores

Separe partes do prompt claramente:

```
Analise o texto abaixo:

---TEXTO---
[texto aqui]
---FIM DO TEXTO---

Identifique: tema principal, tom e público-alvo.
```

**Delimitadores comuns:**
- `---` (traços)
- `"""` (aspas triplas)
- ``` ``` ``` (backticks)
- `###` (hashtags)
- Tags XML: `<texto>...</texto>`

---

### 6. ✅ Use Variáveis

Torne prompts reutilizáveis:

```python
prompt_template = """
Você é um {papel}.

Tarefa: {tarefa}
Contexto: {contexto}
Formato de saída: {formato}

Resposta:
"""
```

---

### 7. ✅ Divida Tarefas Complexas

**Em vez de um prompt gigante:**

```
Analise este contrato, identifique riscos, sugira melhorias, 
calcule multas potenciais, compare com a legislação atual...
```

**Divida em etapas:**

```
Prompt 1: Extraia as cláusulas principais
Prompt 2: Analise cada cláusula quanto a riscos
Prompt 3: Sugira melhorias para cláusulas de risco
Prompt 4: Resuma os pontos críticos
```

---

### 8. ✅ Peça para o Modelo Verificar

Adicione auto-verificação:

```
[Instrução principal]

Antes de responder, verifique:
1. A resposta está no formato solicitado?
2. Todas as partes da pergunta foram respondidas?
3. Há contradições na resposta?

Se houver problemas, corrija antes de finalizar.
```

---

### 9. ✅ Itere e Documente

**Template de documentação:**

| Versão | Data | Prompt | Config | Resultado | Observações |
|--------|------|--------|--------|-----------|-------------|
| 1.0 | 24/02 | [texto] | temp=0.5 | 70% accuracy | Muitos falsos positivos |
| 1.1 | 24/02 | [texto] | temp=0.3 | 85% accuracy | Adicionei 2 exemplos |
| 1.2 | 25/02 | [texto] | temp=0.2 | 92% accuracy | Few-shot + CoT |

---

### 10. ✅ Teste com Casos Extremos

**Edge cases para testar:**
- Entrada vazia
- Entrada muito longa
- Caracteres especiais
- Idiomas mistos
- Contradições no texto
- Informações ambíguas

---

### 11. ✅ Controle Alucinações

**Técnicas:**

```
# Apenas fatos do texto
"Responda apenas com informações explicitamente presentes no texto."

# Citar fonte
"Para cada afirmação, cite a frase exata do texto que a embasa."

# Admitir ignorância
"Se a informação não estiver no texto, responda 'INFORMAÇÃO NÃO DISPONÍVEL'."
```

---

### 12. ✅ Use Few-shot com Classes Balanceadas

**❌ Desbalanceado:**
```
Positivo: "Ótimo produto!"
Positivo: "Adorei!"
Positivo: "Recomendo!"
Positivo: "Excelente!"
Negativo: "Horrível."
```

**✅ Balanceado:**
```
Positivo: "Ótimo produto!"
Negativo: "Horrível."
Positivo: "Adorei!"
Negativo: "Não recomendo."
Positivo: "Excelente!"
```

---

### 13. ✅ Adapte-se ao Modelo

Cada modelo tem características diferentes:

| Modelo | Características | Dicas |
|--------|-----------------|-------|
| **GPT-4** | Raciocínio forte, verbose | Peça concisão |
| **Claude** | Segue instruções bem, menos verbose | Ótimo para instruções longas |
| **Gemini** | Multimodal, bom em código | Aproveite imagens |
| **LLaMA** | Open source, mais limitado | Prompts mais simples |

---

### 14. ✅ Teste Diferentes Formatos de Saída

| Formato | Quando Usar |
|---------|-------------|
| **JSON** | Integração com sistemas, APIs |
| **Markdown** | Documentação, relatórios |
| **CSV** | Dados tabulares |
| **XML** | Sistemas legados |
| **YAML** | Configurações |
| **Lista** | Leitura rápida |

---

### 15. ✅ Use Chain-of-Thought com Moderação

**Quando usar:**
- Problemas lógicos/matemáticos
- Análise multi-passo
- Debugging

**Quando NÃO usar:**
- Classificação simples
- Respostas de uma palavra
- Quando custo de tokens importa

---

## Anti-Padrões ⚠️ (O Que Evitar)

### ❌ Prompts Vagos

```
"Fale sobre marketing"
```

**Problema:** Sem direção, sem escopo, sem formato.  
**Correção:** "Explique 5 estratégias de marketing digital para pequenas empresas em 200 palavras."

---

### ❌ Instruções Conflitantes

```
"Seja breve mas cubra todos os detalhes importantes do documento de 50 páginas"
```

**Problema:** Impossível satisfazer ambas as restrições.  
**Correção:** "Resuma os 3 pontos mais importantes em 100 palavras."

---

### ❌ Ambiguidade

```
"O prêmio foi de 1000 reais. Quanto João recebeu?"
```

**Problema:** Não diz quem é João ou como o prêmio foi dividido.  
**Correção:** "O prêmio de 1000 reais foi dividido igualmente entre João e Maria. Quanto João recebeu?"

---

### ❌ Sobrecarga de Instruções

```
"Seja formal mas amigável, use termos técnicos mas explique para leigos, 
seja conciso mas detalhado, use humor mas seja profissional..."
```

**Problema:** Muitas restrições conflitantes.  
**Correção:** Escolha 2-3 características principais.

---

### ❌ Assumir Conhecimento

```
"Use a metodologia XYZ para analisar isso."
```

**Problema:** O modelo pode não conhecer ou ter definição diferente.  
**Correção:** "Use a metodologia XYZ (descrita abaixo)..." ou explique a metodologia.

---

### ❌ Exemplos Inconsistentes

```
EXEMPLO 1: Saída = "Positivo"
EXEMPLO 2: A resposta é: Negativo
EXEMPLO 3: POSITIVO
```

**Problema:** Formatos diferentes confundem o modelo.  
**Correção:** Mantenha formato consistente em todos os exemplos.

---

## Checklist de Revisão de Prompt

Antes de usar um prompt em produção, verifique:

### Clareza
- [ ] A tarefa está claramente definida?
- [ ] Não há ambiguidades?
- [ ] O formato de saída está especificado?

### Contexto
- [ ] Há contexto suficiente?
- [ ] O contexto é relevante (sem ruído)?
- [ ] Há exemplos (se necessário)?

### Restrições
- [ ] Há limite de tamanho?
- [ ] O formato está definido?
- [ ] Há restrições de tom/estilo?

### Testes
- [ ] Testei com entradas típicas?
- [ ] Testei com edge cases?
- [ ] Testei múltiplas vezes (consistência)?

### Técnico
- [ ] A temperatura está apropriada?
- [ ] O limite de tokens está adequado?
- [ ] O modelo escolhido é adequado para a tarefa?

---

## Templates Prontos para Usar

### 📝 Resumo de Texto

```
Resuma o texto abaixo em {n} bullet points.

REGRAS:
- Cada bullet: máximo {x} palavras
- Foque em informações factuais
- Mantenha linguagem neutra
- Não adicione informações externas

TEXTO:
{texto}

RESUMO:
```

---

### 🏷️ Classificação

```
Classifique o seguinte texto em uma das categorias: {categorias}

EXEMPLOS:
"{exemplo_1}" → {classe_1}
"{exemplo_2}" → {classe_2}

TEXTO:
"{texto}"

CATEGORIA:
```

---

### 🔍 Extração de Dados

```
Extraia as seguintes informações do texto:
- {campo_1}
- {campo_2}
- {campo_3}

Retorne em JSON:
{
  "{campo_1}": "...",
  "{campo_2}": "...",
  "{campo_3}": "..."
}

TEXTO:
{texto}

JSON:
```

---

### 💻 Geração de Código

```
Escreva uma função em {linguagem} que {descricao}.

REQUISITOS:
- {requisito_1}
- {requisito_2}
- Incluir docstring
- Incluir type hints
- Tratar erros

EXEMPLO DE USO:
{exemplo}

CÓDIGO:
```

---

### 🎭 Análise com Papel

```
Você é um {papel} com {anos} anos de experiência em {area}.

Analise o seguinte {tipo_conteudo}:

{conteudo}

Sua análise deve cobrir:
1. {aspecto_1}
2. {aspecto_2}
3. {aspecto_3}

Forneça críticas construtivas e sugestões práticas.

ANÁLISE:
```

---

### 🔄 Tradução com Contexto

```
Traduza o texto de {idioma_origem} para {idioma_destino}.

CONTEXTO:
- Público: {publico}
- Tom: {tom}
- Propósito: {proposito}

TEXTO ORIGINAL:
{texto}

TRADUÇÃO:
```

---

## Troubleshooting Comum

### Problema: Respostas muito longas

**Soluções:**
- Adicione "Seja conciso" ou "Máximo X palavras"
- Reduza max_tokens
- Peça bullet points em vez de parágrafos

---

### Problema: Respostas muito curtas

**Soluções:**
- Peça "Responda em detalhes"
- Aumente max_tokens
- Use "Explique seu raciocínio"

---

### Problema: Formato inconsistente

**Soluções:**
- Adicione exemplos few-shot
- Use delimitadores no formato esperado
- Seja mais específico sobre a estrutura

---

### Problema: Alucinações

**Soluções:**
- "Responda apenas com informações do texto"
- "Se não souber, diga 'Não sei'"
- Reduza temperatura
- Peça citações/fontes

---

### Problema: Loop de repetição

**Soluções:**
- Ajuste temperatura (nem muito baixa nem muito alta)
- Reduza top-K
- Limite max_tokens
- Reformule o prompt

---

### Problema: Ignora instruções

**Soluções:**
- Coloque instruções no início
- Use prompt de sistema
- Seja mais explícito
- Use delimitadores para separar instruções de conteúdo

---

## Referência Rápida

### Técnicas por Tipo de Tarefa

| Tarefa | Técnicas Recomendadas |
|--------|----------------------|
| Classificação | Zero-shot, Few-shot, Sistema |
| Extração | Few-shot, JSON output |
| Resumo | Sistema, Contexto |
| Raciocínio | CoT, Step-back |
| Criatividade | Papel, Temperatura alta |
| Código | Sistema, CoT, Few-shot |
| Análise | Papel, CoT, Step-back |
| Conversação | Sistema, Papel, Contexto |

---

### Configurações por Tipo de Tarefa

| Tarefa | Temperatura | Top-P | Top-K |
|--------|-------------|-------|-------|
| Fatos/Código | 0 | 0.9 | 20 |
| Classificação | 0.1 | 0.9 | 20 |
| Resumo | 0.2 | 0.95 | 30 |
| Conversação | 0.5 | 0.95 | 40 |
| Criatividade | 0.8 | 0.99 | 50 |

---

### Frases Mágicas

| Objetivo | Frase |
|----------|-------|
| Ativar CoT | "Vamos pensar passo a passo." |
| Evitar alucinação | "Se não estiver no texto, responda 'Não disponível'." |
| Garantir formato | "Retorne APENAS o JSON, sem texto adicional." |
| Melhor raciocínio | "Pense cuidadosamente antes de responder." |
| Auto-verificação | "Verifique sua resposta antes de finalizar." |

---

## Notas Finais

- **Engenharia de prompt é iterativa** — experimente, meça, melhore
- **Conheça seu modelo** — cada um tem características diferentes
- **Documente tudo** — versões, resultados, aprendizados
- **Teste extensivamente** — casos normais e edge cases
- **Valide sempre** — especialmente para código e fatos críticos

---

*Documento baseado no whitepaper "Prompt Engineering" de Lee Boonstra, Google, Fevereiro de 2025*  
*Versão expandida e aprimorada com práticas adicionais*
