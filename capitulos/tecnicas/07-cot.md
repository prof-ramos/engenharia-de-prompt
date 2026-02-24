# 04.07 - Cadeia de Pensamento (CoT)

[← Step-back](06-step-back.md) | [Próximo: Auto-consistência →](08-auto-consistencia.md)

---

Faz o modelo **explicitar o raciocínio** passo a passo.

## A Frase Mágica

```
"Vamos pensar passo a passo."
```

## Por Que Funciona

- Modelos não "pensam" internamente
- Ao explicitar etapas, o raciocínio se torna mais confiável
- Reduz erros em problemas multi-passo

## Exemplo - Problema Matemático

### ❌ Sem CoT

```
Quando eu tinha 3 anos, meu parceiro tinha 3 vezes a minha idade. 
Agora tenho 20 anos. Qual é a idade do meu parceiro?
```

**Saída:** `63 anos` ❌ (errado!)

### ✅ Com CoT

```
Quando eu tinha 3 anos, meu parceiro tinha 3 vezes a minha idade. 
Agora tenho 20 anos. Qual é a idade do meu parceiro?

Vamos pensar passo a passo.
```

**Saída:**
```
1. Quando eu tinha 3 anos, meu parceiro tinha 3 × 3 = 9 anos.
2. A diferença de idade é 9 - 3 = 6 anos.
3. Agora tenho 20 anos, então meu parceiro tem 20 + 6 = 26 anos.

Resposta: 26 anos ✅
```

## Técnicas de Ativação

| Técnica | Exemplo |
|---------|---------|
| Frase mágica | "Vamos pensar passo a passo." |
| Instrução direta | "Explique seu raciocínio antes de responder." |
| Few-shot com CoT | Exemplos que mostram raciocínio |

## CoT com Few-shot

```
P: Quando meu irmão tinha 2 anos, eu tinha o dobro da sua idade. 
Agora tenho 40 anos. Quantos anos tem meu irmão?

R: Quando meu irmão tinha 2 anos, eu tinha 2 × 2 = 4 anos. 
Diferença de idade: 2 anos. Agora tenho 40, então ele tem 38. 
Resposta: 38

P: Quando eu tinha 3 anos, meu parceiro tinha 3 vezes a minha idade. 
Agora tenho 20 anos. Qual é a idade do meu parceiro?

R:
```

## Vantagens e Desvantagens

| ✅ Vantagens | ❌ Desvantagens |
|-------------|-----------------|
| Baixo esforço | Mais tokens = mais custo |
| Muito eficaz | Respostas mais longas |
| Funciona sem fine-tuning | Pode ser verboso |
| Interpretabilidade | Nem sempre necessário |
| Robustez entre modelos | |

## Quando Usar

| ✅ Ideal para | ❌ Evitar quando |
|--------------|------------------|
| Matemática e lógica | Classificação simples |
| Problemas multi-passo | Respostas de uma palavra |
| Análise complexa | Custo de tokens é crítico |
| Debugging de código | Tarefa não requer raciocínio |
| Tomada de decisão | |

## Melhores Práticas

### 1. Combine com Temperatura Baixa
```
Temperatura: 0 - 0.3 para CoT
```

### 2. Peça Verificação
```
[Problema]

Vamos pensar passo a passo.

Antes de dar a resposta final, verifique cada etapa.
```

### 3. Estruture a Saída
```
Responda no formato:
1. [Passo 1]
2. [Passo 2]
3. [Conclusão]

Resposta final: [valor]
```

## Variações

### Zero-shot CoT
```
[Problema]
Vamos pensar passo a passo.
```

### Few-shot CoT
```
[Exemplos com raciocínio]
[Problema]
```

### Auto-verificação
```
[Problema]
Pense passo a passo, depois verifique sua resposta.
```

---

[Próximo: Auto-consistência →](08-auto-consistencia.md)
