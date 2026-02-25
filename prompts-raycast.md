# Biblioteca de Prompts - Raycast

**Fonte:** [github.com/raycast/ray-so](https://github.com/raycast/ray-so/tree/main/app/(navigation)/prompts)

Esta biblioteca contém prompts prontos para uso, extraídos do projeto Raycast. Organizados por categoria com tradução e adaptação para português.

---

## Como Usar

As variáveis especiais nos prompts:
- `{selection}` - Texto selecionado pelo usuário
- `{argument name=valor}` - Argumento customizável
- `{browser-tab}` - Conteúdo da aba do navegador

---

## Código

### Processamento de Linguagem Natural
```
Atue como um software de processamento de linguagem natural. Analise o texto fornecido e retorne apenas um objeto JSON analisável e minificado.

Aqui está a estrutura do objeto JSON:
{
  "chave1": /* Algumas instruções */,
  "chave2": /* Algumas instruções */,
}

Aqui estão as regras que você deve seguir:
- Você DEVE retornar um objeto JSON válido e analisável.
- Mais regras…

Aqui estão alguns exemplos para ajudar:
- Exemplo 1…
- Exemplo 2…

Texto: {selection}

Dados JSON:
```

### Converter CSS para Tailwind
```
Converta o seguinte código em classes CSS do Tailwind e me dê o resultado em um bloco de código. Certifique-se de remover quaisquer prefixos de navegador. Dê-me apenas o que posso colocar nas propriedades `class` dos meus elementos HTML.

Código: {selection}

Classes CSS Tailwind:
```

### Terminal Linux
```
Atue como um terminal Linux. Execute o seguinte código e responda com o que o terminal deve mostrar. Responda apenas com a saída do terminal dentro de um único bloco de código, e nada mais. Não escreva explicações.

Código: {selection}

Terminal:
```

### Interpretador de Código
```
Atue como um interpretador de {argument name=linguagem}. Execute o código {argument name=linguagem} e responda com a saída. Não forneça explicações.

Código: {selection}

Saída:
```

### Comandos Git
```
Traduza o texto para comandos Git. Responda apenas com um único bloco de código, e nada mais. Não escreva explicações.

Texto: {selection}

Comandos Git:
```

### Gerador de Regex
```
Gere uma expressão regular que corresponda aos padrões específicos no texto. Retorne a expressão regular em um formato que possa ser facilmente copiado e colado em um editor de texto ou linguagem de programação habilitada para regex. Em seguida, dê explicações claras e compreensíveis sobre o que a regex está fazendo e como ela é construída.

Texto: {selection}

Regex:
```

### Converter HTML para Markdown
```
Converta o código HTML para Markdown.

Código HTML: {selection}

Markdown:
```

### Adicionar Statements de Debug
```
Atue como um engenheiro de software depurando seu código. Adicione statements de debug ao código. Adicione quantos forem necessários para facilitar a depuração.

Código: {selection}

Código com debug:
```

### Escrever Testes
```
Como desenvolvedor de software, estou trabalhando em um projeto usando Jest, TypeScript e React Testing Library. Gostaria que você me ajudasse a gerar testes unitários para o código fornecido. Analise o código e forneça um único teste unitário com as importações necessárias, sem explicações ou comentários adicionais, a menos que absolutamente necessário. Evite repetir importações e mocks já mencionados.

Se eu disser 'próximo', por favor me dê outro teste para o mesmo código. Caso eu envie novo código, descarte o código anterior e comece a gerar testes para o novo. Priorize testar a lógica do código em diferentes cenários como primeira prioridade.

Se eu fornecer instruções específicas ou pedir para testar uma parte ou cenário específico, siga essas instruções e gere o teste unitário de acordo. Se eu enviar um erro do Jest, corrija o problema e retorne apenas as linhas que precisam ser alteradas em um formato legível. Formate a saída como um bloco de código único.

Código: {selection}

Saída:
```

### Escrever Docstring
```
Escreva uma docstring para a função. Certifique-se de que a documentação seja detalhada.

Função: {selection}

Docstring:
```

### Converter para Crontab
```
Atue como um administrador de servidor Unix experiente. Dado um agendamento de cronjob em linguagem natural, responda com o formato crontab correto para este agendamento exato. Verifique seus resultados, certifique-se de que é uma sintaxe crontab válida, e responda apenas com o formato crontab.

Exemplo de Agendamento: às 5:30 da manhã toda terça-feira de maio
Crontab Esperado: 30 5 * 5 2

Agendamento: {argument name="agendamento"}

Crontab:
```

### Feedback Honesto de Código
```
Seja brutalmente honesto, não seja um puxa-saco. Se eu estiver errado, aponte de forma direta.
Preciso de feedback honesto sobre meu código. Revise o seguinte código e forneça feedback brutalmente honesto.
Aponte quaisquer problemas, práticas ruins, ineficiências ou áreas para melhoria. Não amenize nada - quero a verdade sobre o que está errado e como corrigir.

Código: {selection}

Revisão:
```

### Refatorar para Legibilidade
```
Refatore o seguinte código para melhorar a legibilidade e manutenibilidade. Foque em nomes de variáveis claros, decomposição adequada de funções e remoção de code smells. Explique as mudanças que você fez e por quê.

Código: {selection}

Código refatorado:
```

### Otimizar Performance
```
Analise o seguinte código para gargalos de performance e sugira otimizações. Considere complexidade de tempo, complexidade de espaço e performance de runtime. Forneça a versão otimizada com explicações.

Código: {selection}

Código otimizado:
```

### Gerar Interface de Props de Componente
```
Gere uma interface TypeScript para as props do componente baseado no código do componente. Inclua comentários JSDoc para cada prop explicando seu propósito. Torne a interface estrita e type-safe.

Código do componente: {selection}

Interface das props:
```

---

## Navegador

### Inspecionar Website
```
Descreva a stack tecnológica usada com base no seguinte documento HTML:

{browser-tab format="html"}

Considere todos os elementos de uma stack tecnológica, de frameworks a APIs, passando por ferramentas (analytics, monitoramento, etc.). Inclua quais fontes são usadas. Não faça suposições sobre o que é usado se não houver evidência.
```

### Resumir Vídeo do YouTube
```
Crie um resumo de um vídeo do YouTube usando sua transcrição. Você usará o seguinte modelo:

## Resumo
{Múltiplas frases resumindo o vídeo do YouTube}

## Notas
{Bullet points que resumem os pontos-chave ou momentos importantes da transcrição do vídeo com explicações}

## Citações
{Extraia as melhores frases da transcrição em uma lista}

Transcrição: {browser-tab}
```

### Deepwiki
```
Substitua "github.com" da URL {browser-tab} por "deepwiki.com". Produza apenas a nova URL, sem explicações ou instruções.
```

---

## Comunicação

### Traduzir para Idioma
```
Traduza o texto para {argument name=idioma}.

Texto: {selection}

Tradução:
```

### Recusar Email
```
Escreva um email educado e amigável para recusar o seguinte email. O email deve ser escrito de forma que possa ser enviado ao destinatário.

Email: {selection}

Email recusado:
```

### Fazer Pergunta
```
Reescreva o seguinte texto como uma mensagem concisa e amigável, formulada como uma pergunta. Deve ser escrita de forma que possa ser enviada em um aplicativo de chat como o Slack.

Texto: {selection}

Pergunta:
```

### Mensagem BLUF (Bottom Line Up Front)
```
Reescreva o seguinte texto como uma mensagem BLUF formatada em Markdown. O formato da mensagem deve ser composto de duas partes:

- A primeira parte deve ser escrita em negrito e transmitir as informações principais da mensagem. Pode ser uma declaração ou uma pergunta. Não perca nenhum detalhe importante nesta parte.
- A segunda parte deve ser colocada em uma nova linha. Deve dar mais detalhes e fornecer algum contexto sobre a mensagem.

Certifique-se de que a mensagem permaneça concisa e clara para que os leitores não percam tempo extra lendo.

Texto: {selection}

Texto reescrito:
```

### Resumir Emails Longos
```
Ajude-me a resumir os pontos-chave do texto do email em no máximo 5 bullet points, cada um preferencialmente com uma frase, e no máximo duas frases. Além disso, identifique quaisquer itens de ação solicitados de mim.

Pontos-chave:
<bullet 1>
<bullet 2>
...

Solicitado de você:
<item de ação 1>
<item de ação 2>

Se não houver itens de ação, a seção "Solicitado de você" ficará vazia.

Email: {selection}

Saída:
```

### Debater um Tópico
```
Tome uma posição sobre o tópico e {argument default=a favor} dele. Construa um argumento convincente e forneça evidências para apoiar sua posição.

Tópico: {selection}

Argumento:
```

### Criar Evento de Calendário
```
Crie um evento de calendário no formato ICS com base nas informações. Inclua o horário de início, horário de término, local, todos os participantes e um resumo. Se nenhum horário de término for fornecido, assuma que o evento terá uma hora de duração. Adicione um lembrete 1 hora antes do evento começar e 1 dia antes do evento começar. Não inclua a propriedade PRODID. Produza apenas o bloco de código. Não adicione comentários.

Informações: {selection}

ICS:
```

### Quebrar Texto em Parágrafos
```
Pegue o texto abaixo e escreva uma versão limpa inserindo quebras de parágrafo naturalmente apropriadas. É importante que o texto não mude, apenas o espaçamento em branco.

Texto corrido:
{selection}

Versão formatada:
```

### Resumir e Simpatizar
```
Por favor, resuma e omita o seguinte. Depois expresse sua empatia.

Texto: {selection}

Simpatia:
```

### Preencher a Lacuna
```
Use as seguintes instruções para reescrever o texto

Dê-me 5 palavras que preencham com mais precisão o espaço em branco em uma frase.

O espaço em branco é representado por alguns underscores, como ___, ou ______.

Então, por exemplo: "Estou super ___ para anunciar meu novo produto".

1. Estou super feliz em anunciar meu novo produto
2. Estou super animado em anunciar meu novo produto
3. Estou super empolgado em anunciar meu novo produto
4. Estou super orgulhoso em anunciar meu novo produto
5. Estou super nervoso em anunciar meu novo produto

Agora faça o mesmo para esta sentença:

Texto: {selection}

Texto reescrito:
```

---

## Imagem

### Criar Roteiro do YouTube
```
Crie um roteiro de YouTube convincente e cativante baseado no texto. Certifique-se de incluir B-Rolls no roteiro. Faça o roteiro tão longo quanto necessário para fazer um vídeo de {argument name=minutos default=10} minutos.

Texto: {selection}

Roteiro:
```

### Gerador de Prompts Midjourney
```
Com base no texto, gere um "prompt imagine" que contenha no máximo 1.500 palavras que será usado como entrada para um programa de IA de texto para imagem chamado MidJourney baseado nos seguintes parâmetros: /imagine prompt: [1], [2], [3], [4], [5], [6]

Neste prompt, [1] deve ser substituído por um assunto aleatório e [2] deve ser uma descrição curta e concisa sobre esse assunto. Seja específico e detalhado em suas descrições, usando adjetivos e advérbios descritivos, um amplo vocabulário e linguagem sensorial. Forneça contexto e informações de fundo sobre o assunto e considere a perspectiva e o ponto de vista da imagem.

[3] deve ser uma descrição curta e concisa sobre o ambiente da cena.
[4] deve ser uma descrição curta e concisa sobre o humor da cena.
[5] deve ser uma descrição curta e concisa sobre a atmosfera da cena.
[6] deve ser uma descrição curta e concisa do efeito de iluminação.

Texto: {selection}

Prompt Midjourney:
```

### Gerar Ícones
```
Gere URIs de dados base64 de ícones SVG 100x100 representando o texto. Não forneça nenhum comentário além da lista de URIs de dados como imagens markdown. Para cada ícone, explique como ele se relaciona com o texto.

Texto: {selection}

Ícones:
```

### Gerar Cores para Design System
```
Gere uma paleta de cores completa para um design system baseada na cor da marca. Inclua cores primária, secundária, de destaque, neutras, de sucesso, aviso, erro e informação. Para cada cor, forneça tons de 50 a 900. Produza como CSS custom properties e config do Tailwind.

Cor da marca (hex): {selection}

Paleta de cores:
```

### Gerar Breakpoints Responsivos
```
Analise o design e sugira breakpoints responsivos ideais. Forneça media queries CSS e explique o raciocínio para cada breakpoint com base no conteúdo e tamanhos comuns de dispositivos.

Descrição do design: {selection}

Breakpoints:
```

---

## Escrita

### Escrever uma História
```
Escreva uma história baseada no texto. Torne a história envolvente. A história não deve ter mais de {argument name=numero default=500} palavras.

Texto: {selection}

História:
```

### Escrever um Blog Post
```
Escreva um post de blog sobre o tópico. Não use mais de {argument name=numero default=1000} palavras.

Tópico: {selection}

Post do blog:
```

### Thread do Twitter
```
Converta o texto em uma lista de tweets (= thread do Twitter). O primeiro tweet deve ser claro e envolvente. Cada tweet deve fluir suavemente para o próximo, construindo antecipação e momento. O último tweet deve ser impactante para que o usuário possa refletir sobre toda a thread. Certifique-se de que cada tweet não exceda 280 caracteres. Não adicione uma única hashtag a nenhum dos tweets.

Texto: {selection}

Tweets:
```

### Compressor Semântico
```
Você é um especialista em semântica e escrita que ajuda a tornar a escrita mais concisa e impactante. Sua tarefa é analisar frases e sugerir substituições poderosas para frases verbosas enquanto preserva o significado e tom originais.

Quando dada uma frase, analise-a e sugira 3-5 alternativas concisas.

Para cada análise, use este formato:
<analysis>
Frase Alvo: [identifique a frase verbosa]
Tipo de Frase: [adverbial/preposicional/adjetival/etc.]
Sugestões de Substituição:
1. [substituição] - [breve explicação da eficácia]
2. [substituição] - [breve explicação]
3. [substituição] - [breve explicação]
Substituição Recomendada: [sua melhor escolha]
Frase Revisada: [frase completa com a substituição recomendada]
</analysis>

Frase: {selection}

Análise:
```

---

## Música

### Escrever uma Música
```
Escreva uma música baseada no texto fornecido. A música deve ter uma melodia clara, letras que contem uma história e um refrão memorável. O humor da música deve ser {argument name=humor}.

Texto: {selection}

Música:
```

### Criador de Playlist
```
Atue como um recomendador de músicas. Com base na música fornecida, crie uma playlist de 10 músicas similares. Forneça um nome e descrição para a playlist. Não escolha músicas com o mesmo nome ou artista. Não inclua a música original na playlist.

Música: {selection}

Playlist:
```

---

## Ideias

### Escrever 10 Alternativas
```
Dê-me 10 versões alternativas do texto. Certifique-se de que as alternativas sejam todas distintas umas das outras.

Texto: {selection}

Alternativas:
```

### Ideias de Projetos
```
Faça um brainstorm de 5 ideias de projetos baseadas no texto. Certifique-se de que as ideias sejam distintas umas das outras.

Texto: {selection}

Ideias:
```

### Criar Analogias
```
Desenvolva {argument name=numero default=3} analogias ou metáforas criativas que ajudem a explicar a ideia principal do texto.

Texto: {selection}

Analogias:
```

---

## Diversão

### Atuar Como Personagem
```
Reescreva o texto como se você fosse {argument name=personagem default=yoda}. Use o tom, maneira e vocabulário de {argument name=personagem default=yoda}. Você deve conhecer todo o conhecimento de {argument name=personagem default=yoda}.

Texto: {selection}

Texto reescrito:
```

### DrunkGPT
```
Reescreva o texto como se você estivesse bêbado.

Texto: {selection}

Texto reescrito:
```

---

## Miscelânea

### TL;DR
```
Extraia todos os fatos do texto e resuma em todos os aspectos relevantes em até sete bullet points e um resumo de uma linha. Escolha um emoji correspondente para cada bullet point.

Texto: {selection}

Resumo:
```

### Title Case
```
Converta {selection} para title case.
```

### Sugestão de Emoji
```
Sugira emojis que se relacionem com o texto. Sugira cerca de 10 emojis e ordene-os por relevância. Não adicione duplicatas. Responda apenas com emojis.

Texto: {selection}

Emojis:
```

### Encontrar Sinônimos
```
Encontre sinônimos para a palavra {selection} e formate a saída como uma lista. As palavras devem existir. Não escreva explicações. Não inclua a palavra original na lista. A lista não deve ter duplicatas.
```

### Criar Receita
```
Dê-me uma receita baseada nos ingredientes. A receita deve ser fácil de seguir.

Ingredientes: {selection}

Receita:
```

### Criar Itens de Ação
```
Gere uma lista markdown de itens de ação para completar com base no texto, usando um identificador único para cada item como títulos em negrito. Se houver erros no texto, crie itens de ação para corrigi-los. Em uma sublista de cada item, forneça uma descrição, prioridade, nível estimado de dificuldade e uma duração razoável para a tarefa.

Texto: {selection}

Itens de ação:
```

### Extrair Endereços de Email
```
Extraia todos os endereços de email no texto e liste-os usando markdown. Inclua qualquer coisa que possa ser um endereço de email. Se possível, forneça o nome da pessoa ou empresa ao qual o endereço de email pertence.

Texto: {selection}

Endereços de email:
```

### Extrair Números de Telefone
```
Identifique todos os números de telefone no texto e liste-os usando markdown. Inclua qualquer coisa que possa ser um número de telefone. Se possível, forneça o nome da pessoa ou empresa ao qual o número de telefone pertence.

Texto: {selection}

Números de telefone:
```

### Extrair Links
```
Extraia links no texto. Não forneça nenhum comentário além da lista de links Markdown.

Texto: {selection}

Links:
```

### Prós e Contras
```
Liste prós e contras para o texto baseado nos tópicos mencionados. Formate a resposta como uma lista markdown de prós e contras. Não forneça nenhum outro comentário.

Texto: {selection}

Prós e Contras:
```

### Explique Como Se Eu Fosse...
```
Explique o texto como se eu fosse um {argument name=identidade default="criança de 5 anos"}

Texto: {selection}

Explicação:
```

### Análise de Texto
```
Analise o texto e forneça insights sobre seu tom, estilo e potencial público.

Texto: {selection}

Análise:
```

### Resumir Avaliações de Produtos
```
Leia cuidadosamente as avaliações do produto abaixo. Traduza para português e crie um resumo de todas as avaliações em português e liste-as como Prós e Contras no formato de bullet points. Lembre-se de que cada bullet point deve ser uma frase ou no máximo duas frases curtas. Os mais frequentemente mencionados devem vir primeiro em cada lista e cada bullet point deve ter uma porcentagem mostrando quanta evidência as avaliações trouxeram para esse pró ou contra.

No final, escreva um parágrafo sobre o que devo prestar atenção antes de comprar este produto.

Modelo:

## Resumo das avaliações

**✅ Prós:**
- Pró 1 - porcentagem de confiança%
- Pró 2 - porcentagem de confiança%

**❌ Contras:**
- Con 1 - porcentagem de confiança%
- Con 2 - porcentagem de confiança%

**💡 Você deve prestar atenção a:**
- Dica 1
- Dica 2

Avaliações: {selection}

Resumo:
```

---

## Prompts Raycast (Edição de Texto)

### Melhorar Escrita
```
Atue como corretor ortográfico, redator de conteúdo e melhorador/editor de texto. Responda a cada mensagem apenas com o texto reescrito.

Siga estritamente estas regras:
- Corrija erros de ortografia, gramática e pontuação no texto fornecido
- Melhore a clareza e concisão sem alterar o significado original
- Divida frases longas em frases mais curtas e legíveis
- Elimine repetições desnecessárias enquanto preserva pontos importantes
- Priorize voz ativa sobre voz passiva para um tom mais envolvente
- Opte por vocabulário mais simples e acessível quando possível
- SEMPRE mantenha o significado e intenção original do texto
- SEMPRE mantenha o idioma original
- SEMPRE mantenha o tom de voz e estilo existente
- NUNCA cerque o texto melhorado com aspas ou formatação adicional
- Se o texto já está bem escrito e não requer melhoria, não altere o texto fornecido

Texto: {selection}

Texto melhorado:
```

### Corrigir Ortografia e Gramática
```
Atue como corretor ortográfico e melhorador.

Siga estritamente estas regras:
- Corrija ortografia, gramática e pontuação
- Mantenha o idioma original
- NUNCA cerque o texto reescrito com aspas
- Mantenha URLs no formato original
- Não altere emojis

Texto: {selection}

Texto corrigido:
```

### Explicar em Termos Simples
```
Atue como um dicionário e enciclopédia, fornecendo explicações claras e concisas para palavras ou conceitos fornecidos.

Siga estritamente estas regras:
- Explique o texto em linguagem simples e concisa
  - Para uma única palavra, forneça uma definição breve e fácil de entender
  - Para um conceito ou frase, dê uma explicação concisa que divida as ideias principais em termos simples
- Use exemplos ou analogias para esclarecer tópicos complexos quando necessário
- Responda apenas com a explicação ou definição

Texto: {selection}

Explicação:
```

### Fazer Mais Longo
```
Atue como um redator de conteúdo profissional encarregado de expandir o texto de um cliente enquanto mantém sua essência e estilo.

Siga estritamente estas regras:
- SEMPRE preserve o tom, voz e idioma original do texto
- Identifique e expanda as informações mais críticas e pontos-chave
- Evite repetição
- Mantenha-se factualmente próximo ao texto fornecido
- Mantenha URLs em seu formato original
- Responda apenas com o texto expandido

Texto: {selection}

Texto expandido:
```

### Fazer Mais Curto
```
Atue como um redator de conteúdo profissional encarregado de encurtar o texto de um cliente enquanto mantém sua essência e estilo.

Siga estritamente estas regras:
- SEMPRE preserve o tom, voz e idioma original do texto
- Identifique e retenha as informações mais críticas e pontos-chave
- Elimine redundâncias e frases repetitivas
- Mantenha URLs em seu formato original
- Certifique-se de que o texto encurtado flua suavemente e mantenha coerência
- Tente reduzir a contagem de palavras o máximo possível sem comprometer o significado e estilo principais
- Responda apenas com o texto encurtado

Texto: {selection}

Texto encurtado:
```

### Mudar Tom para Profissional
```
Atue como um redator e editor de conteúdo profissional.

Siga estritamente estas regras:
- Tom de voz profissional
- Linguagem formal
- Fatos precisos
- Ortografia, gramática e pontuação corretas
- Fraseado conciso
- Significado inalterado
- Comprimento mantido
- Mantenha URLs no formato original
- Mantenha o idioma original

Texto: {selection}

Texto reescrito:
```

### Mudar Tom para Amigável
```
Atue como um redator e editor de conteúdo.

Siga estritamente estas regras:
- Tom de voz amigável e otimista
- Ortografia, gramática e pontuação corretas
- Significado inalterado
- Comprimento mantido
- Mantenha URLs no formato original
- Mantenha o idioma original

Texto: {selection}

Texto reescrito:
```

### Mudar Tom para Confiante
```
Atue como um redator e editor de conteúdo.

Siga estritamente estas regras:
- Use tom de voz confiante, formal e amigável
- Evite hedging, seja definitivo quando possível
- Pule desculpas
- Foque nos argumentos principais
- Ortografia, gramática e pontuação corretas
- Mantenha significado inalterado
- Mantenha comprimento retido
- Mantenha URLs no formato original
- Mantenha o idioma original

Texto: {selection}

Texto reescrito:
```

### Mudar Tom para Casual
```
Atue como um redator e editor de conteúdo.

Siga estritamente estas regras:
- Use tom de voz casual e amigável
- Use voz ativa
- Mantenha frases curtas
- Ok usar gírias e contrações
- Mantenha a pessoa gramatical
- Ortografia, gramática e pontuação corretas
- Mantenha significado inalterado
- Mantenha comprimento retido
- Mantenha URLs no formato original
- Mantenha o idioma original

Texto: {selection}

Texto reescrito:
```

### Reformular como Tweet
```
Você é um especialista no campo e tem a oportunidade perfeita de compartilhar suas ideias e insights com um público enorme! Reescreva o texto como um tweet que seja:
- Casual e animado
- Criativo e cativante
- Focado nos principais aprendizados que desafiam o status quo
- Envolvente e impactante
- IMPORTANTE: menos de 25 palavras
- IMPORTANTE: não inclua hashtag, hashtags e palavras começando com #
- Mantenha o idioma original

Texto: {selection}

Tweet:
```

### Explicar Código Passo a Passo
```
Atue como um engenheiro de software com profundo conhecimento de qualquer linguagem de programação e sua documentação. Explique como o código funciona passo a passo em uma lista. Seja conciso com um tom de voz casual e escreva como documentação para outros.

Código: {selection}

Explicação:
```

### Encontrar Bugs no Código
```
Atue como um engenheiro de software com profundo conhecimento de qualquer linguagem de programação. Revise o código para corrigir bugs lógicos no código. Considere apenas o contexto fornecido, responda de forma concisa e adicione um bloco de código com as mudanças propostas. Se não conseguir encontrar bugs com confiança, responda com "Nada encontrado - LGTM 👍".

Código: {selection}

Revisão:
```

### Resumir Website
```
Resuma o site fornecido com o seguinte formato:

## <título do site conciso e fácil de ler>

<resumo de uma a duas frases com as informações mais importantes>

### Principais Aprendizados

- <EXATAMENTE três bullet points com os principais aprendizados, mantenha os bullet points o mais curtos possível>

Regras a seguir precisamente:
- SEMPRE capture o tom, perspectiva e POV do autor
- NUNCA invente informações adicionais

Informações do site: {browser-tab}
```

---

## Créditos

Prompts extraídos do repositório [ray-so](https://github.com/raycast/ray-so) da Raycast.

Autores contribuidores incluem:
- Alireza Sheikholmolouki
- Philipp Daun
- Tommy Nguyen
- Tanweer Ahmed
- Stephen Kaplan
- Nathan Cheng
- Samuel Kraft
- E outros

---

*Extraído e traduzido em Fevereiro de 2026*
