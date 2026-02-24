# 04.09 - Árvore de Pensamentos (ToT)

[← Auto-consistência](08-auto-consistencia.md) | [Próximo: ReAct →](10-react.md)

---

Explora **múltiplos caminhos de raciocínio** em paralelo, ramificando como uma árvore.

## Diferença para CoT

| CoT | ToT |
|-----|-----|
| Uma cadeia linear | Múltiplas cadeias ramificadas |
| Segue um caminho | Explora vários caminhos |
| Não pode voltar | Pode retroceder e tentar outro |

## Visualização

```
                [Problema]
                    |
         ┌──────────┼──────────┐
       [Opção A]  [Opção B]  [Opção C]
           |          |          |
       [A.1]      [B.1]      [C.1]
       [A.2]      [B.2]      [C.2]
           ↓          ↓          ↓
       [Eval A]   [Eval B]   [Eval C]
           └──────────┼──────────┘
                      ↓
              [Melhor Solução]
```

## Como Funciona

```
1. Gere múltiplas opções iniciais
2. Expanda cada opção em sub-opções
3. Avalie cada caminho
4. Descarte caminhos ruins
5. Expanda os promissores
6. Repita até encontrar solução
```

## Exemplo - Jogo de Palavras

**Problema:** Formar a maior palavra possível com as letras: A, R, T, E, S, M, O

```
Passo 1: Gere opções iniciais
- Começar com "AR..."
- Começar com "TE..."
- Começar com "MO..."

Passo 2: Expanda cada opção
- AR → ART, ARE, ARM...
- TE → TER, TES, TEM...
- MO → MOR, MOS, MOA...

Passo 3: Avalie e expanda as melhores
- ART → ARTE, ARTES, ARTESÃO
- TER → TERMO, TERMOS
- MOS → MOSTRA, MOSTRAS

Passo 4: Encontre a melhor
- ARTE (4 letras)
- ARTES (5 letras)
- ARTESÃO (7 letras) ✅ VENCEDOR

Solução: ARTESÃO
```

## Quando Usar

| ✅ Ideal para | ❌ Evitar quando |
|--------------|------------------|
| Problemas de otimização | Tarefas simples |
| Jogos e puzzles | Resposta direta |
| Planejamento complexo | Custo é crítico |
| Decisões com múltiplas alternativas | |

## Implementação Conceitual

```
1. Thought Generation: Gere N pensamentos possíveis
2. State Evaluation: Avalie qualidade de cada estado
3. Search Strategy: BFS, DFS, ou best-first
4. Backtracking: Volte se caminho falhar
```

## Comparação

| Técnica | Complexidade | Custo | Precisão |
|---------|-------------|-------|----------|
| Zero-shot | Baixa | Baixo | Variável |
| CoT | Média | Médio | Alta |
| ToT | Alta | Alto | Muito alta |

---

[Próximo: ReAct →](10-react.md)
