# 04.04 - Prompt de Papel (Role)

[← Prompt de Sistema](03-prompt-sistema.md) | [Próximo: Prompt Contextual →](05-prompt-contextual.md)

---

Atribui uma **identidade/especialidade** ao modelo.

## Por Que Funciona

Modelos são treinados em textos de diferentes fontes. Ao definir um papel, você ativa conhecimentos específicos associados àquela identidade.

## Técnicas de Ativação

| Técnica | Exemplo |
|---------|---------|
| Expert em área | "Você é um expert em marketing digital" |
| Profissão | "Aja como um engenheiro de software sênior" |
| Pessoa específica | "Imagine que você é Steve Jobs" |
| Experiência | "Você tem 20 anos de experiência em finanças" |

## Exemplos Práticos

### Técnico
```
Você é um engenheiro de software sênior com 15 anos de experiência 
em Python e arquitetura de sistemas distribuídos. 

Revise o código abaixo focando em performance e escalabilidade.
```

### Criativo
```
Aja como um copywriter de propaganda premiada, vencedor de Cannes Lions.

Crie 5 headlines impactantes para um aplicativo de meditação.
```

### Educacional
```
Você é um professor de física do ensino médio com talento para explicações.

Explique relatividade para um estudante de 16 anos usando analogias do dia a dia.
```

### Crítico
```
Imagine que você é um investidor conservador, focado em valor e segurança.

Analise este pitch de startup e identifique 5 riscos principais.
```

### Especialista
```
Você é um médico cardiologista com 25 anos de prática clínica.

Explique os efeitos do café no coração para um paciente leigo.
```

## Estilos de Tom

| Estilo | Quando Usar |
|--------|-------------|
| **Direto** | Instruções, tutoriais |
| **Formal** | Documentos, relatórios |
| **Informal** | Blogs, redes sociais |
| **Humorístico** | Engajamento, marketing |
| **Inspiracional** | Motivação, discursos |
| **Persuasivo** | Vendas, argumentação |
| **Descritivo** | Documentação, manuais |
| **Confrontacional** | Debates, análises críticas |

## Exemplo com Tom

```
Você é um guia de viagens. Escreva em estilo humorístico e inspiracional.

Minha localização: "Estou em Manhattan."

Sugira 3 lugares para visitar.
```

**Saída:**
> 1. Contemple o Estado de Espírito do Império: Suba às alturas vertiginosas do Empire State Building e banhe-se na gloria do horizonte de Manhattan...
> 2. Seja Artsy-Fartsy no MoMA: Libere seu aficionado de arte interior...
> 3. Vá às Compras na Quinta Avenida: Prepare-se para o choque de etiqueta...

## Combinação com Outras Técnicas

```
[PAPEL]
Você é um consultor de carreira especializado em tech.

[CONTEXTO]
O usuário tem 5 anos de experiência em desenvolvimento web.

[TAREFA]
Sugira 3 caminhos de carreira possíveis.

[FORMATO]
Para cada caminho:
- Título do cargo
- Skills necessárias
- Tempo estimado para transição
- Salário médio
```

---

[Próximo: Prompt Contextual →](05-prompt-contextual.md)
