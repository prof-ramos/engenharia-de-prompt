# 04.06 - Step-back (Recuo)

[← Prompt Contextual](05-prompt-contextual.md) | [Próximo: Cadeia de Pensamento →](07-cot.md)

---

Faz uma **pergunta geral primeiro**, depois usa a resposta para a tarefa específica.

## Por Que Funciona

O "recuo" permite que o LLM:
- Ative conhecimento mais amplo
- Considere princípios gerais antes de detalhes
- Reduza viés de informações específicas

## Processo

```
1. Pergunta geral/abstrata → ativa conhecimento amplo
2. Resposta como contexto → guia raciocínio específico
3. Tarefa específica → usa conhecimento ativado
```

## Exemplo - Campanha de Marketing

### Passo 1 (Recuo)
```
Quais são os 5 princípios fundamentais de uma campanha 
de marketing digital bem-sucedida para produtos SaaS B2B?
```

**Resposta:**
1. Proposta de valor clara
2. Persona definida
3. Funil estruturado
4. Prova social
5. CTA persuasivo

### Passo 2 (Específico)
```
Considerando esses 5 princípios:
1. Proposta de valor clara
2. Persona definida
3. Funil estruturado
4. Prova social
5. CTA persuasivo

Crie uma campanha de marketing para um software de 
gestão de estoque para pequenos varejistas.
```

## Exemplo - Enredo de Jogo

### Passo 1 (Recuo)
```
Com base em jogos de tiro em primeira pessoa populares, 
quais são 5 cenários que contribuem para um enredo envolvente?
```

**Resposta:**
1. Base Militar Abandonada
2. Cidade Cyberpunk
3. Nave Alienígena
4. Cidade Infestada de Zumbis
5. Instalação Subaquática

### Passo 2 (Específico)
```
Contexto: [cenários acima]

Escolha um tema e escreva um enredo detalhado para 
um nível de jogo de tiro em primeira pessoa.
```

## Quando Usar

| ✅ Ideal para | ❌ Evitar quando |
|--------------|------------------|
| Problemas complexos | Tarefas simples |
| Necessidade de abstração | Resposta direta |
| Criatividade | Classificação simples |
| Planejamento | Extração de dados |

## Benefícios

- 🎯 **Maior qualidade** - conhecimento mais amplo ativado
- 🔄 **Menos viés** - foca em princípios, não detalhes
- 💡 **Mais criatividade** - explora antes de focar

## Implementação Prática

### Em uma única chamada:
```
Antes de responder, considere: 
[pergunta geral sobre o tema]

Agora, responda: [pergunta específica]
```

### Em duas chamadas:
```
Chamada 1: Pergunta geral → resposta A
Chamada 2: "Considerando [resposta A], [pergunta específica]"
```

---

[Próximo: Cadeia de Pensamento →](07-cot.md)
