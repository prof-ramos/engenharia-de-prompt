# 04.10 - ReAct (Raciocinar e Agir)

[← Árvore de Pensamentos](09-tot.md) | [Voltar ao Sumário →](../00-sumario.md)

---

Combina **raciocínio** com **uso de ferramentas** externas.

## Ciclo ReAct

```
1. Thought (Pensamento): O que preciso fazer?
2. Action (Ação): Qual ferramenta usar?
3. Observation (Observação): O que aconteceu?
4. Repete até completar
```

## Exemplo - Pesquisa sobre Metallica

**Pergunta:** Quantos filhos os membros do Metallica têm no total?

```
Thought: Preciso descobrir quem são os membros da banda.

Action: Search[Membros do Metallica]
Observation: James Hetfield, Lars Ulrich, Kirk Hammett, Robert Trujillo

Thought: Agora preciso descobrir quantos filhos cada um tem.

Action: Search[Quantos filhos James Hetfield tem]
Observation: Três filhos: Cali, Castor e Marcella

Thought: 1/4 membros. Vou buscar o próximo.

Action: Search[Quantos filhos Lars Ulrich tem]
Observation: Três filhos

Thought: 2/4 membros. Continuando.

Action: Search[Quantos filhos Kirk Hammett tem]
Observation: Dois filhos: Angel e Vincenzo

Thought: 3/4 membros. Último.

Action: Search[Quantos filhos Robert Trujillo tem]
Observation: Dois filhos

Thought: Agora posso somar: 3 + 3 + 2 + 2 = 10

Final Answer: Os membros do Metallica têm 10 filhos no total.
```

## Ferramentas Comuns

| Ferramenta | Uso |
|------------|-----|
| Search | Buscar informações na web |
| Calculator | Cálculos matemáticos |
| Code | Executar código |
| Database | Consultar banco de dados |
| API | Chamar APIs externas |

## Estrutura do Prompt

```
Você tem acesso às seguintes ferramentas:
- Search[query]: Busca na web
- Calculator[expression]: Calcula expressão

Use o formato:
Thought: [seu raciocínio]
Action: [ferramenta][entrada]
Observation: [resultado da ferramenta]
... (repita quantas vezes necessário)
Thought: [raciocínio final]
Final Answer: [resposta]

Pergunta: [pergunta do usuário]
```

## Benefícios

| ✅ Vantagem | Descrição |
|------------|-----------|
| **Informações atualizadas** | Busca dados em tempo real |
| **Cálculos precisos** | Usa ferramentas dedicadas |
| **Rastreabilidade** | Cada passo é documentado |
| **Flexibilidade** | Adiciona novas ferramentas |

## Quando Usar

| ✅ Ideal para | ❌ Evitar quando |
|--------------|------------------|
| Informações que mudam | Conhecimento estático |
| Cálculos complexos | Resposta simples |
| Integração com APIs | Não há ferramentas disponíveis |
| Agentes autônomos | Controle fino necessário |

## Implementação com LangChain

```python
from langchain.agents import create_react_agent
from langchain.tools import Tool

tools = [
    Tool(
        name="Search",
        func=search.run,
        description="útil para buscar informações na web"
    )
]

agent = create_react_agent(llm, tools, prompt)
agent.invoke({"input": "Quantos filhos os membros do Metallica têm?"})
```

## Dicas

1. **Limite o número de passos** para evitar loops infinitos
2. **Defina ferramentas claramente** com descrições precisas
3. **Trate erros** das ferramentas graciosamente
4. **Monitore custos** — cada ação consome tokens

---

[← Voltar ao Sumário](../00-sumario.md)
