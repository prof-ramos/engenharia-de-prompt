# 04.08 - Auto-consistência

[← Cadeia de Pensamento](07-cot.md) | [Próximo: Árvore de Pensamentos →](09-tot.md)

---

Gera **múltiplas respostas** e escolhe a mais frequente (votação).

## Processo

```
1. Execute o mesmo prompt N vezes (temperatura alta)
2. Extraia a resposta de cada execução
3. Conte a frequência de cada resposta
4. Retorne a mais comum
```

## Por Que Funciona

- Diferentes caminhos de raciocínio podem levar a respostas diferentes
- A resposta correta tende a aparecer mais frequentemente
- Reduz impacto de raciocínios falhos ocasionais

## Exemplo - Classificação Ambígua

```
Email: "Olá, notei que seu site tem uma vulnerabilidade XSS interessante. 
Não se preocupe, não vou explorar. Só achei curioso. Abraços, Hackerman."

Classifique como: IMPORTANTE ou NÃO IMPORTANTE.
Vamos pensar passo a passo.
```

**Execução 1:** IMPORTANTE (risco de segurança)  
**Execução 2:** NÃO IMPORTANTE (tom amigável)  
**Execução 3:** IMPORTANTE (vulnerabilidade real)  
**Execução 4:** IMPORTANTE (deve ser verificado)  
**Execução 5:** NÃO IMPORTANTE (parece teste)

**Resultado por votação:** IMPORTANTE (3/5) ✅

## Configuração

| Parâmetro | Valor Recomendado |
|-----------|-------------------|
| Temperatura | 0.7 - 1.0 (alta) |
| N execuções | 3 - 10 |
| Método de seleção | Votação majoritária |

## Trade-offs

| ✅ Vantagens | ❌ Desvantagens |
|-------------|-----------------|
| Maior precisão | Custo N× maior |
| Pseudo-probabilidade | Mais tempo |
| Robustez | Complexidade de implementação |
| Bom para ambiguidades | |

## Quando Usar

| ✅ Ideal para | ❌ Evitar quando |
|--------------|------------------|
| Classificações ambíguas | Custo é crítico |
| Decisões críticas | Tarefa é simples |
| Alta precisão necessária | Latência importa |
| Casos com subjetividade | |

## Implementação

```python
def auto_consistency(prompt, n=5):
    responses = []
    for _ in range(n):
        response = llm.generate(prompt, temperature=0.8)
        answer = extract_answer(response)
        responses.append(answer)
    
    # Votação majoritária
    from collections import Counter
    most_common = Counter(responses).most_common(1)[0][0]
    return most_common
```

## Variação: Ponderada por Confiança

```
1. Execute N vezes
2. Extraia resposta E confiança de cada uma
3. Some confianças por resposta
4. Retorne a com maior soma
```

---

[Próximo: Árvore de Pensamentos →](09-tot.md)
