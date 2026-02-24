# Engenharia de Prompt

**Autor:** Lee Boonstra  
**Fevereiro de 2025**

---

## Introdução

Ao pensar em uma entrada e saída de um modelo de linguagem grande, um prompt de texto (às vezes acompanhado de outras modalidades, como prompts de imagem) é a entrada que o modelo usa para prever uma saída específica. Você não precisa ser um cientista de dados ou um engenheiro de aprendizado de máquina – qualquer pessoa pode escrever um prompt. No entanto, criar o prompt mais eficaz pode ser complicado. Muitos aspectos do seu prompt afetam sua eficácia: o modelo que você usa, os dados de treinamento do modelo, as configurações do modelo, sua escolha de palavras, estilo e tom, estrutura e contexto, tudo importa. Portanto, a engenharia de prompt é um processo iterativo. Prompts inadequados podem levar a respostas ambíguas e imprecisas, e podem prejudicar a capacidade do modelo de fornecer saídas significativas.

Quando você conversa com o chatbot Gemini, basicamente você escreve prompts. Porém, este whitepaper foca em escrever prompts para o modelo Gemini dentro do Vertex AI ou usando a API, pois ao fazer o prompting diretamente do modelo, você terá acesso às configurações como temperatura etc.

Este whitepaper discute a engenharia de prompt em detalhes. Vamos examinar as várias técnicas de prompting para ajudá-lo a começar e compartilhar dicas e melhores práticas para se tornar um especialista em prompting. Também discutiremos alguns dos desafios que você pode enfrentar ao criar prompts.

---

## Engenharia de Prompt

Lembre-se de como um LLM funciona: é um mecanismo de previsão. O modelo recebe texto sequencial como entrada e então prevê qual deve ser o próximo token, com base nos dados em que foi treinado. O LLM é operacionalizado para fazer isso repetidamente, adicionando o token previsto anteriormente ao final do texto sequencial para prever o token seguinte. A previsão do próximo token é baseada na relação entre o que está nos tokens anteriores e o que o LLM viu durante seu treinamento.

Quando você escreve um prompt, você tenta configurar o LLM para prever a sequência correta de tokens. A engenharia de prompt é o processo de projetar prompts de alta qualidade que guiam os LLMs a produzir saídas precisas. Esse processo envolve experimentação para encontrar o melhor prompt, otimizar o comprimento do prompt e avaliar o estilo e a estrutura de escrita de um prompt em relação à tarefa. No contexto do processamento de linguagem natural e LLMs, um prompt é uma entrada fornecida ao modelo para gerar uma resposta ou previsão.

Esses prompts podem ser usados para alcançar vários tipos de tarefas de compreensão e geração, como resumo de texto, extração de informações, perguntas e respostas, classificação de texto, tradução de linguagem ou código, geração de código e documentação ou raciocínio de código.

Ao fazer engenharia de prompt, você começará escolhendo um modelo. Os prompts podem precisar ser otimizados para o seu modelo específico, independentemente de você usar os modelos de linguagem Gemini no Vertex AI, GPT, Claude ou um modelo de código aberto como Gemma ou LLaMA.

Além do prompt, você também precisará ajustar as várias configurações de um LLM.

---

## Configuração de Saída de LLM

Depois de escolher seu modelo, você precisará definir a configuração do modelo. A maioria dos LLMs vem com várias opções de configuração que controlam a saída do LLM. A engenharia de prompt eficaz requer a definição otimizada dessas configurações para sua tarefa.

### Comprimento da Saída

Uma configuração importante é o número de tokens a serem gerados em uma resposta. Gerar mais tokens requer mais computação do LLM, levando a maior consumo de energia, tempos de resposta potencialmente mais lentos e custos mais altos.

**Atenção:** Reduzir o comprimento de saída do LLM não faz o LLM se tornar mais sucinto estilística ou textualmente na saída que cria — apenas faz o LLM parar de prever mais tokens quando o limite é atingido. Se suas necessidades exigirem um comprimento de saída curto, você também possivelmente precisará fazer a engenharia do seu prompt para acomodar isso.

A restrição de comprimento de saída é especialmente importante para algumas técnicas de prompting de LLM, como o ReAct, em que o LLM continuará emitindo tokens inúteis após a resposta que você deseja.

> **Esteja ciente:** gerar mais tokens requer mais computação do LLM, levando a maior consumo de energia e tempos de resposta potencialmente mais lentos, o que resulta em custos mais altos.

### Controles de Amostragem

Os LLMs não preveem formalmente um único token. Em vez disso, os LLMs preveem probabilidades para qual pode ser o próximo token, com cada token no vocabulário do LLM recebendo uma probabilidade. Essas probabilidades de token são então amostradas para determinar qual será o próximo token produzido. Temperatura, top-K e top-P são as configurações mais comuns que determinam como as probabilidades de token previstas são processadas para escolher um único token de saída.

### Temperatura

A temperatura controla o grau de aleatoriedade na seleção de tokens. Temperaturas mais baixas são boas para prompts que esperam uma resposta mais determinística, enquanto temperaturas mais altas podem levar a resultados mais diversos ou inesperados. Uma temperatura de 0 (decodificação gananciosa) é determinística: o token de maior probabilidade é sempre selecionado (embora note que se dois tokens tiverem a mesma probabilidade máxima prevista, dependendo de como o empate é resolvido, você pode não obter sempre a mesma saída com temperatura 0).

Temperaturas próximas ao máximo tendem a criar saídas mais aleatórias. E à medida que a temperatura aumenta, todos os tokens se tornam igualmente prováveis de ser o próximo token previsto.

O controle de temperatura do Gemini pode ser entendido de forma semelhante à função softmax usada em aprendizado de máquina. Uma configuração de temperatura baixa espelha uma temperatura softmax baixa (T), enfatizando uma única temperatura preferida com alta certeza. Uma configuração de temperatura Gemini mais alta é como uma temperatura softmax alta, tornando uma faixa mais ampla de temperaturas em torno da configuração selecionada mais aceitável. Essa maior incerteza acomoda cenários em que uma temperatura rígida e precisa pode não ser essencial, como ao experimentar saídas criativas.

### Top-K e Top-P

Top-K e top-P (também conhecido como amostragem nuclear) são duas configurações de amostragem usadas em LLMs para restringir o próximo token previsto a vir de tokens com as maiores probabilidades previstas. Como a temperatura, essas configurações de amostragem controlam a aleatoriedade e diversidade do texto gerado.

- **Amostragem Top-K:** Seleciona os K tokens mais prováveis da distribuição prevista do modelo. Quanto maior o top-K, mais criativa e variada é a saída do modelo; quanto menor o top-K, mais restritiva e factual é a saída do modelo. Um top-K de 1 é equivalente à decodificação gananciosa.

- **Amostragem Top-P:** Seleciona os principais tokens cuja probabilidade cumulativa não excede um certo valor (P). Os valores de P variam de 0 (decodificação gananciosa) a 1 (todos os tokens no vocabulário do LLM).

A melhor maneira de escolher entre top-K e top-P é experimentar ambos os métodos (ou ambos juntos) e ver qual produz os resultados que você está procurando.

### Combinando Tudo

Escolher entre top-K, top-P, temperatura e o número de tokens a serem gerados depende da aplicação específica e do resultado desejado, e as configurações impactam umas às outras. Também é importante garantir que você entenda como o modelo escolhido combina as diferentes configurações de amostragem.

Se temperatura, top-K e top-P estiverem todos disponíveis (como no Vertex Studio), os tokens que atendem aos critérios de top-K e top-P são candidatos para o próximo token previsto, e então a temperatura é aplicada para amostrar dos tokens que passaram pelos critérios de top-K e top-P. Se apenas top-K ou top-P estiver disponível, o comportamento é o mesmo, mas apenas uma das configurações é usada.

Se a temperatura não estiver disponível, qualquer token que atenda aos critérios de top-K e/ou top-P é então selecionado aleatoriamente para produzir um único próximo token previsto.

Em configurações extremas de um valor de configuração de amostragem, essa configuração cancela outras ou se torna irrelevante:

- Se você definir a temperatura para 0, top-K e top-P se tornam irrelevantes — o token mais provável se torna o próximo token previsto.
- Se você definir top-K para 1, temperatura e top-P se tornam irrelevantes. Apenas um token passa pelo critério top-K.
- Se você definir top-P para 0 (ou um valor muito pequeno), a maioria das implementações considerará apenas o token mais provável.

#### Pontos de Partida Recomendados

| Objetivo | Temperatura | Top-P | Top-K |
|----------|-------------|-------|-------|
| Resultados coerentes, algum nível criativo | 0.2 | 0.95 | 30 |
| Resultados especialmente criativos | 0.9 | 0.99 | 40 |
| Resultados menos criativos | 0.1 | 0.9 | 20 |
| Tarefa com única resposta correta (ex: matemática) | 0 | - | - |

> **NOTA:** Com mais liberdade (temperatura, top-K, top-P e tokens de saída mais altos), o LLM pode gerar texto menos relevante.

> **AVISO:** O "bug do loop de repetição" é um problema comum em LLMs onde o modelo fica preso em um ciclo, gerando repetidamente a mesma palavra ou frase. Isso pode ocorrer com configurações de temperatura baixas e altas, embora por razões diferentes. Resolver isso frequentemente requer ajuste cuidadoso dos valores.

---

## Técnicas de Prompting

Os LLMs são ajustados para seguir instruções e são treinados em grandes quantidades de dados para que possam entender um prompt e gerar uma resposta. Mas os LLMs não são perfeitos; quanto mais claro o texto do seu prompt, melhor é para o LLM prever o próximo texto provável. Além disso, técnicas específicas que aproveitam como os LLMs são treinados e como funcionam ajudarão você a obter os resultados relevantes dos LLMs.

### Prompting Geral / Zero-shot

Um prompt zero-shot é o tipo mais simples de prompt. Ele fornece apenas uma descrição de uma tarefa e algum texto para o LLM começar. Essa entrada pode ser qualquer coisa: uma pergunta, o início de uma história ou instruções. O nome zero-shot significa "sem exemplos".

**Exemplo - Classificação de avaliações de filmes:**

| Nome | 1_1_movie_classification |
|------|--------------------------|
| **Objetivo** | Classificar avaliações de filmes como positivas ou negativas |
| **Prompt** | Classifique a avaliação do filme como "POSITIVO" ou "NEGATIVO". Não retorne nenhum outro texto. Avaliação: "Esse filme é perturbador, mas no bom sentido, uma obra-prima do horror." |
| **Saída** | POSITIVO |

A temperatura do modelo deve ser definida para um número baixo, já que não é necessária criatividade.

### One-shot e Few-shot

Ao criar prompts para modelos de IA, é útil fornecer exemplos. Esses exemplos podem ajudar o modelo a entender o que você está pedindo. Exemplos são especialmente úteis quando você deseja direcionar o modelo para uma certa estrutura ou padrão de saída.

- **One-shot:** Fornece um único exemplo para o modelo imitar
- **Few-shot:** Fornece múltiplos exemplos mostrando um padrão a seguir

Como regra geral, você deve usar pelo menos **três a cinco exemplos** para prompting few-shot. No entanto, pode ser necessário usar mais exemplos para tarefas mais complexas, ou pode ser necessário usar menos devido à limitação de comprimento de entrada do seu modelo.

**Exemplo - Análise de pedidos de pizza para JSON:**

| Objetivo | Analisar pedidos de pizza para JSON |
|----------|-------------------------------------|
| **Prompt** | Analise o pedido de pizza de um cliente em JSON válido:

EXEMPLO:
Quero uma pizza pequena com queijo, molho de tomate e pepperoni.
```json
{
  "tamanho": "pequena",
  "tipo": "normal",
  "ingredientes": [["queijo", "molho de tomate", "pepperoni"]]
}
```

EXEMPLO:
Posso pedir uma pizza grande com molho de tomate, manjericão e mozzarella?
```json
{
  "tamanho": "grande",
  "tipo": "normal",
  "ingredientes": [["molho de tomate", "manjericão", "mozzarella"]]
}
```

Agora, eu gostaria de uma pizza grande, com a primeira metade de queijo e mozzarella. E a outra de molho de tomate, presunto e abacaxi.

Resposta JSON: |
| **Saída** | ```json
{
  "tamanho": "grande",
  "tipo": "metade-metade",
  "ingredientes": [
    ["queijo", "mozzarella"],
    ["molho de tomate", "presunto", "abacaxi"]
  ]
}
``` |

> **Dica:** Ao escolher exemplos, use exemplos relevantes, diversos, de alta qualidade e bem escritos. Um pequeno erro pode confundir o modelo. Inclua casos extremos para tornar a saída robusta.

---

## Prompts de Sistema, Contextuais e de Papel

Essas técnicas focam em aspectos diferentes:

- **Prompting de sistema:** Define o contexto geral e propósito do modelo ("quadro geral")
- **Prompting contextual:** Fornece detalhes específicos relevantes para a tarefa atual
- **Prompting de papel:** Atribui um personagem ou identidade específica ao modelo

### Prompting de Sistema

Útil para gerar saída que atenda a requisitos específicos, como formatos de saída ou linguagens de programação específicas.

**Exemplo - Classificação com formato JSON:**

| Objetivo | Classificar avaliações de filmes, retornar JSON |
|----------|------------------------------------------------|
| **Prompt** | Classifique a avaliação do filme como POSITIVO, NEUTRO ou NEGATIVO. Retorne a resposta em JSON com a estrutura: {"movie_reviews": [{"sentiment": "...", "name": "..."}]}

Avaliação: "Esse filme é perturbador, mas no bom sentido, uma obra-prima do horror." Nome do filme: "Her" |
| **Saída** | ```json
{
  "movie_reviews": [
    {
      "sentiment": "NEGATIVE",
      "name": "Her"
    }
  ]
}
``` |

**Benefícios do JSON:**
- Força o modelo a criar estrutura
- Limita alucinações
- Facilita integração com aplicações

### Prompting de Papel

Atribui um papel específico ao modelo para gerar saída mais relevante.

**Exemplo:**

| Objetivo | Agir como guia de viagens e fornecer 3 sugestões |
|----------|--------------------------------------------------|
| **Prompt** | Quero que você aja como um guia de viagens. Escreverei para você sobre minha localização e você sugerirá 3 lugares para visitar perto de mim em um estilo humorístico.

Minha sugestão: "Estou em Manhattan." |
| **Saída** | 1. Contemple o Estado de Espírito do Império: Suba às alturas vertiginosas do Empire State Building...
2. Seja Artsy-Fartsy no MoMA...
3. Vá às Compras na Quinta Avenida... |

**Estilos eficazes:**
- Confrontacional
- Descritivo
- Direto
- Formal
- Humorístico
- Influente
- Informal
- Inspiracional
- Persuasivo

### Prompting Contextual

Fornece contexto específico para a tarefa atual, ajudando o modelo a entender nuances.

**Exemplo:**

| Objetivo | Sugerir artigos para um blog sobre jogos retrô |
|----------|------------------------------------------------|
| **Prompt** | Contexto: Estou escrevendo um blog para entusiastas de jogos de arcade retrô que amam a nostalgia dos anos 80. O público gosta de artigos detalhados sobre a história dos jogos e evolução do design.

Sugira 3 ideias de artigos |
| **Saída** | 1. **A Evolução do Design de Gabinetes de Arcade**
2. **Volta ao Passado: Jogos de Arcade Icônicos dos Anos 80**
3. **A Ascensão e o Revival Retrô da Arte em Pixel** |

---

## Prompting de Recuo (Step-back)

Técnica para melhorar o desempenho solicitando que o LLM primeiro considere uma questão geral relacionada à tarefa específica, e então alimente a resposta em um prompt subsequente. Esse "recuo" permite que o LLM ative conhecimento de contexto relevante e processos de raciocínio antes de tentar resolver o problema específico.

**Processo:**
1. Fazer uma pergunta geral/abstrata sobre o tema
2. Usar a resposta como contexto para o prompt específico

**Exemplo - Criando enredo de jogo:**

**Passo 1 - Prompt de recuo:**

| Prompt | Com base em jogos de ação de tiro em primeira pessoa populares, quais são 5 cenários-chave fictícios que contribuem para um enredo de nível desafiador e envolvente? |
|--------|----------------------------------------------------------------------------------------------------------------------------------|
| **Saída** | 1. Base Militar Abandonada
2. Cidade Cyberpunk
3. Nave Alienígena
4. Cidade Infestada de Zumbis
5. Instalação de Pesquisa Subaquática |

**Passo 2 - Prompt com contexto:**

| Prompt | Contexto: [lista dos 5 cenários acima]

Pegue um dos temas e escreva um enredo de um parágrafo para um novo nível de um jogo de tiro em primeira pessoa. |
|--------|--------------------------------------------------------------------------------------------------------|

---

## Cadeia de Pensamento (CoT)

Técnica para melhorar as capacidades de raciocínio dos LLMs gerando etapas de raciocínio intermediárias. Isso ajuda o LLM a gerar respostas mais precisas.

**Vantagens:**
- Baixo esforço, muito eficaz
- Funciona com LLMs prontos para uso (sem ajuste fino)
- Interpretabilidade: você pode ver as etapas de raciocínio
- Robustez entre diferentes versões de LLM

**Desvantagens:**
- Mais tokens de saída = mais custo e tempo

**Exemplo - Problema matemático:**

| Prompt (sem CoT) | Quando eu tinha 3 anos, meu parceiro tinha 3 vezes a minha idade. Agora tenho 20 anos. Qual é a idade do meu parceiro? |
|------------------|------------------------------------------------------------------------------------------------------------------------|
| **Saída** | 63 anos ❌ (errado) |

| Prompt (com CoT) | Quando eu tinha 3 anos, meu parceiro tinha 3 vezes a minha idade. Agora tenho 20 anos. Qual é a idade do meu parceiro? **Vamos pensar passo a passo.** |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| **Saída** | 1. Quando eu tinha 3 anos, meu parceiro tinha 3 × 3 = 9 anos.
2. A diferença de idade é 9 - 3 = 6 anos.
3. Agora tenho 20 anos, então meu parceiro tem 20 + 6 = 26 anos.

**Resposta: 26 anos** ✅ |

**Casos de uso ideais para CoT:**
- Geração de código (dividir solicitação em etapas)
- Criação de dados sintéticos
- Qualquer tarefa que possa ser resolvida "conversando"

---

## Auto-consistência

Combina amostragem e votação majoritária para gerar caminhos de raciocínio diversos e selecionar a resposta mais consistente. Melhora a precisão e coerência das respostas.

**Etapas:**
1. Gerar caminhos de raciocínio diversos (mesmo prompt várias vezes com temperatura alta)
2. Extrair a resposta de cada resposta gerada
3. Escolher a resposta mais comum (votação majoritária)

> **Nota:** Dá uma pseudo-probabilidade de uma resposta estar correta, mas tem custos elevados.

---

## Árvore de Pensamentos (ToT)

Generaliza o conceito de CoT permitindo que os LLMs explorem múltiplos caminhos de raciocínio diferentes simultaneamente, em vez de apenas seguir uma única cadeia linear.

**Características:**
- Mantém uma árvore de pensamentos
- Cada pensamento é um passo intermediário coerente
- O modelo pode explorar diferentes caminhos ramificando-se de diferentes nós
- Particularmente adequado para tarefas complexas que requerem exploração

---

## ReAct (Raciocinar e Agir)

Paradigma para permitir que LLMs resolvam tarefas complexas usando raciocínio em linguagem natural combinado com ferramentas externas (busca, interpretador de código etc.).

**Como funciona:**
1. LLM raciocina sobre o problema
2. Gera um plano de ação
3. Realiza as ações e observa os resultados
4. Usa as observações para atualizar raciocínio
5. Gera novo plano de ação
6. Repete até chegar à solução

**Exemplo prático - Descobrir filhos dos membros do Metallica:**

```text
> Iniciando nova cadeia AgentExecutor...

O Metallica tem 4 membros.

Ação: Buscar
Entrada: Quantos filhos James Hetfield tem?
Observação: três filhos

Pensamento: 1/4 membros da banda têm 3 filhos

Ação: Buscar
Entrada: Quantos filhos Lars Ulrich tem?
Observação: 3

[... continua para cada membro ...]

Resposta Final: 10
```

---

## Engenharia Automática de Prompts (APE)

Método para automatizar a criação de prompts usando o próprio LLM.

**Processo:**
1. Fazer o prompt de um modelo para gerar variantes de prompts
2. Avaliar todos os candidatos (BLEU, ROUGE, etc.)
3. Selecionar o candidato com melhor pontuação
4. Ajustar e avaliar novamente se necessário

**Exemplo:**

| Prompt | Temos uma loja online de camisetas de merchandise de banda, e para treinar um chatbot precisamos de várias maneiras de pedir: "Uma camiseta do Metallica tamanho P". Gere 10 variantes. |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Saída** | 1. Gostaria de comprar uma camiseta do Metallica no tamanho pequeno.
2. Posso pedir uma camiseta do Metallica de tamanho pequeno?
3. Gostaria de comprar uma camiseta do Metallica, tamanho P.
[... etc ...] |

---

## Prompting para Código

### Prompts para Escrever Código

O Gemini pode ajudar a escrever código em qualquer linguagem de programação.

**Exemplo - Script Bash para renomear arquivos:**

| Prompt | Escreva um script bash que pergunte pelo nome de uma pasta e renomeie todos os arquivos nela adicionando "draft_" ao início do nome. |
|--------|------------------------------------------------------------------------------------------------------------------------------------|
| **Saída** | ```bash
#!/bin/bash
echo "Digite o nome da pasta: "
read folder_name

if [ ! -d "$folder_name" ]; then
  echo "A pasta não existe."
  exit 1
fi

files=( "$folder_name"/* )
for file in "${files[@]}"; do
  new_file_name="draft_$(basename "$file")"
  mv "$file" "$new_file_name"
done

echo "Arquivos renomeados com sucesso."
``` |

### Prompts para Explicar Código

Útil para entender código de outras pessoas.

### Prompts para Traduzir Código

Traduzir código de uma linguagem para outra (ex: Bash → Python).

### Prompts para Depurar e Revisar Código

O LLM pode identificar bugs e sugerir melhorias.

---

## Melhores Práticas

### 1. Forneça Exemplos

A melhor prática mais importante é fornecer exemplos (one-shot / few-shot) dentro de um prompt. É como dar ao modelo um ponto de referência para mirar.

### 2. Design com Simplicidade

Prompts devem ser concisos, claros e fáceis de entender. Se já está confuso para você, provavelmente também estará confuso para o modelo.

**Antes:**
> Estou visitando Nova York agora, e gostaria de ouvir mais sobre ótimos locais. Estou com dois filhos de 3 anos. Onde devemos ir durante nossas férias?

**Depois:**
> Aja como um guia turístico. Sugira 3 lugares em Nova York para visitar com crianças de 3 anos.

### 3. Seja Específico sobre a Saída

Defina claramente o formato esperado (JSON, lista, parágrafo, etc.).

### 4. Use Instruções em Vez de Restrições

Prefira dizer o que fazer em vez do que não fazer.

### 5. Controle o Comprimento Máximo de Tokens

Importante para custos e para evitar saídas excessivamente longas.

### 6. Use Variáveis em Prompts

Facilita reutilização e testes.

### 7. Experimente com Formatos de Entrada

Teste diferentes estilos de escrita e estruturas.

### 8. Para Few-shot, Misture as Classes

Em tarefas de classificação, balanceie os exemplos entre as classes.

### 9. Adapte-se às Atualizações do Modelo

Modelos mudam; prompts podem precisar de ajustes.

### 10. Experimente com Formatos de Saída

Teste diferentes formatos (JSON, XML, markdown, etc.).

### 11. Reparação de JSON

Use instruções claras para garantir JSON válido.

### 12. Trabalhe com Schemas

Defina schemas para estruturas complexas.

### 13. Experimente com Outros Engenheiros

Colaboração ajuda a encontrar melhores soluções.

### 14. Melhores Práticas de CoT

- Use para tarefas que requerem raciocínio
- Combine com few-shot para melhores resultados
- Monitore os custos de tokens

### 15. Documente as Várias Tentativas

Mantenha registro de:
- Objetivo do prompt
- Texto do prompt
- Configurações do modelo
- Resultados
- Observações

---

## Resumo

A engenharia de prompt é uma habilidade essencial para trabalhar com LLMs. As principais técnicas incluem:

| Técnica | Quando Usar |
|---------|-------------|
| **Zero-shot** | Tarefas simples, bem definidas |
| **Few-shot** | Quando precisa de exemplos de formato/estilo |
| **Prompt de Sistema** | Definir comportamento global |
| **Prompt de Papel** | Personalizar tom e expertise |
| **Prompt Contextual** | Fornecer informações específicas da tarefa |
| **Step-back** | Problemas complexos que beneficiam de abstração |
| **Cadeia de Pensamento** | Raciocínio, matemática, lógica |
| **Auto-consistência** | Melhorar precisão com votação |
| **Árvore de Pensamentos** | Exploração de múltiplos caminhos |
| **ReAct** | Tarefas que precisam de ferramentas externas |

---

## Notas Finais

- A engenharia de prompt é iterativa — experimente e refine
- Conheça seu modelo e suas configurações
- Documente seus experimentos
- Teste com diferentes temperaturas e configurações de amostragem
- Valide sempre os resultados, especialmente para código

---

*Documento baseado no whitepaper "Prompt Engineering" de Lee Boonstra, Google, Fevereiro de 2025*
