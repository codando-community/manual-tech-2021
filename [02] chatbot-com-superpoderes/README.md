# [01] Watson Assistant - Hands on

## Instanciando o serviço

1. Crie uma conta em [cloud.ibm.com](http://cloud.ibm.com)
2. Clique em **Catálogo** e pesquise por "Watson Assistant", ou clique em **Serviços** no menu esquerdo, clique na opção de IA/Aprendizado de máquina e procure pelo serviço do Watson Assistant.

![imagens/Untitled.png](imagens/Untitled.png)

Ao clicar no serviço você terá a opção de configurar algumas coisas, como por exemplo a região onde seu serviço será criado, o plano que irá utilizar e o nome com o qual seu serviço será salvo. Não é necessário modificar nada, pois por padrão ele já seleciona o plano lite, que é o que iremos utilizar durante o nosso lab.

3. Após criar o serviço você será redirecionado para a tela principal com todas as informações sobre sua instância. Clique em **Launch Watson Assistant** para que possa começar a editar seu assistente.

---

## Criando seu primeiro assistente

Dentro de uma única instância, é possível criar diversos assistentes, e assim que você inicia o seu serviço pela primeira vez verá que já existe um primeiro assistente lá, mas nós não iremos utilizá-lo.

Clique em **Create assistant** para desenvolver o seu próprio chatbot. Dê a ele um nome e escreva uma descrição dizendo qual o objetivo do assistente que está criando.

![imagens/Untitled%201.png](imagens/Untitled%201.png)

Nesse hands on será desenvolvido um chatbot para a landing page do Codando, e seu objetivo é responder perguntas comumente feitas pelos integrantes da comunidade, como por exemplo como se tornar um staff, quando acontecem nossos eventos e quais nossas redes sociais.

Para isso, será necessário criar uma skill, que é o lugar onde será definido tudo o que o assistente é capaz de responder, e o fluxo da conversa. 

Pense no seu assistente como um funcionário da sua empresa, que desenvolve uma tarefa específica, e para isso é necessário o treinamento de uma habilidade. No caso do Watson Assistant acontece da mesma forma, ao criar uma nova skill estará definindo qual função ele irá desempenhar, e quanto mais exercitada, mais precisa ficarão as respostas.

![imagens/Untitled%202.png](imagens/Untitled%202.png)

Ao clicar na opção **Add dialog skill** aparecerão algumas opções:

- **Add existing skill:** Permite que utilize uma skill já existente no seu serviço;
- **Create skill:** Desenvolver uma habilidade do zero, que é a opção que iremos usar;
- **Import skill:** Permite importar uma skill de um arquivo JSON.

Mais informações sobre criação de skill na documentação: [clique aqui](https://cloud.ibm.com/docs/assistant?topic=assistant-skill-dialog-add#skill-dialog-add-to-assistant)

![imagens/Untitled%203.png](imagens/Untitled%203.png)

Selecione a opção Create skill e preencha as informações solicitadas.

**Observação:** É de extrema importância que selecione a opção Português no select de Language. Essa opção não pode ser modificada depois, e caso não faça isso, seu modelo não será treinado corretamente.

Ao entrar na skill que acabou de criar irá se deparar com um ambiente vazio, onde irá de fato criar os principais aspectos do seu assistente, sendo eles a intenção, entidade e por fim o diálogo.

---

## Intenção

Quando dizemos algo, principalmente em uma situação como essa, sempre existe um objetivo. O usuário sempre espera um retorno daquilo que ele disse. Como por exemplo na sentença abaixo:

> "Vocês estão no LinkedIn?"

Aqui o objetivo é claro, ele deseja saber se estamos produzindo conteúdo para o LinkedIn. Mas ele poderia perguntar por outras informações, como por exemplo como acessar nosso servidor ou como se tornar um membro da nossa equipe.

A intenção tem a função de mapear o objetivo que o usuário pretende alcançar na mensagem, e isso serve para que, com base nessa informação, o assistente saiba o que deve responder.

Uma única intenção é formada por uma série de frases que possuem o mesmo sentido, pois existem diferentes formas de se dizer uma mesma coisa. No exemplo acima foi dito "Vocês estão no LinkedIn?", porém poderia ter sido "por um acaso vocês produzem conteúdo para o LinkedIn também?". No final, ambas as frases possuem o mesmo objetivo.

Isso poderia ser um problema, considerando que não é possível presumir todas as variedades de como se dizer algo, entretanto o Watson Assistant utiliza uma tecnologia chamada NLP (Natural Language Processing) que tem como objetivo "traduzir" linguagem natural, ou seja, a forma como nos expressamos, para linguagem de máquina.

Além disso, utilizando um motor de IA, ao receber uma série de exemplo ele irá não só compreender o que está sendo dito, como também será capaz de classificar outras frases que não estão nos exemplos mencionados, mas que tenham o mesmo contexto.

Para criar uma intenção basta clicar no botão azul escrito **Create intent** (ou "Criar intenção" dependendo da linguagem do seu navegador).

Para nomear sua intenção é uma boa prática que não seja utilizado acentos, caracteres especiais e nem espaço, pois esse nome é uma variável que será utilizada outras vezes.

Adicione uma descrição e comece a digitar seus exemplos.

**Observação:** É obrigatório que sejam criados no mínimo 5 exemplos únicos, porém quanto mais, melhor.

![imagens/Untitled%204.png](imagens/Untitled%204.png)

No exemplo acima foi criada a intenção **#codando_onde_estamos**, o símbolo # é o que representa que essa variável se refere a uma intenção. Nela foram usados os seguintes exemplos:

1. Em quais plataformas vocês estão?
2. Não sei mexer no discord, vocês tem outra plataforma?
3. onde eu posso encontrar vocês?
4. onde vocês estão presentes?
5. quais as redes do Codando?

Repare que as 5 sentenças expressam a mesma vontade, porém ditas de forma completamente diferente.

Além disso, para o cenários que estamos usando, que é o site do Codando, também foram criadas as seguintes intenções:

- #codando_como_ser_organizador
- #discord_reservar_sala_de_estudos
- #eventos_quando_acontecem

Mais informações sobre intenções na documentação: [clique aqui](https://cloud.ibm.com/docs/assistant?topic=assistant-intents&locale=pt-BR)

---

## Entidade

Ainda com base no exemplo anterior, quando o usuário pergunta sobre nossas redes, ainda assim existem uma série de questões. No exemplo citado ele pergunta sobre o LinkedIn, mas ele também poderia ter perguntado sobre o YouTube ou até mesmo sobre o Instagram.

A diferença na rede citada interfere diretamente no link que vamos colocar na resposta, então para uma mesma intenção podem existir diferentes tipos de resposta, e é para isso que serve a entidade.

Com o objetivo de tirar qualquer tipo de ambiguidade do que está sendo dito, a entidade classifica palavras-chave encontradas na frase, possibilitando que a resposta seja ainda mais completa.

Para criar uma entidade basta clicar no botão azul escrito **Create entity** (ou em português "Criar entidade"). Assim como na intenção, o nome de uma entidade também é uma variável representada pelo símbolo **@**, Então os mesmos cuidados devem ser tomados.

![imagens/Untitled%205.png](imagens/Untitled%205.png)

No exemplo acima está sendo criada uma entidade para **@discord**, e nesse momento existem algumas opções:

**Fuzzy matching:** Essa funcionalidade permite que o assistente entenda a palavra mesmo que exista algum erro de digitação. Por exemplo, caso o valor da minha entidade fosse "email" e o usuário escrevesse "meail" ou "emal" o assistente irá reconhecer da mesma forma. Por conta disso é recomendado que esteja sempre acionada.

**Value:** Diferente da intenção, aqui não será passado um exemplo, e sim a palavra chave exata que deseja identificar no meio da mensagem do usuário. Existem duas funções para ajudar a tornar essa identificação ainda mais apurada:

- **Synonyms:** Caso deseje que outras palavras que possuam o mesmo sentido do valor digitado seja identificado da mesma forma.
- **Patterns:** Caso deseje identificar um padrão na mensagem. Por exemplo, todo email possui "@" e ".", então posso digitar uma expressão regular que identifique esse padrão.

Além da entidade de **@discord** também foi criada uma para **@rede**, onde é listado todas as redes sociais em que estamos presentes.

Ainda em entidades também existem as **System entities** (Entidades de sistema), que são entidades já existentes dentro do próprio Watson Assistant, e para utilizá-las basta ativar. Para o nosso caso vamos ativar a **@sys-date** que irá identificar qualquer tipo de data, e a **@sys-number** responsável por identificar numerais.

Mais informações sobre entidades na documentação: [clique aqui](https://cloud.ibm.com/docs/assistant?topic=assistant-entities)

---

## Diálogo

Nesse momento é onde, com base nas intenções e entidades definidas anteriormente, irá começar a desenvolver as respostas que serão dadas ao usuário.

O diálogo possui uma estrutura de árvore, e isso significa que ele sempre será percorrido de cima pra baixo, e só irá executar o nó que corresponde ao parâmetro que foi passado. Ou seja, se o assistente identificar que a mensagem do usuário é referente a intenção de **#codando_onde_estamos**, o nó que tem essa variável como parâmetro é a que será executada.

### Nó

Um nó é o local onde será criada a resposta para cada situação, é onde será definido a intenção ou entidade que deve ser respondido, e para isso conta com diversas opções de resposta para que a conversa seja o mais fluída possível.

![imagens/Untitled%206.png](imagens/Untitled%206.png)

Por padrão, um diálogo começa com dois nós. O de **Bem-vindo**, que é onde será escrita a primeira mensagem que será exibida para o usuário, é onde o assistente irá se apresentar e dizer sobre quais assuntos ele saberá responder. E o segundo que é o nó de **Em outros casos**, que é onde ficará a mensagem que será exibida sempre que o seu bot não souber responder sobre algo, essa mensagem deve ser muito bem construída para que o usuário não fique frustrado por não receber a resposta desejada. Todo o restante do diálogo deverá ser criado entre esses dois nós.

### Configuração

Para criar um nó basta clicar no botão azul escrito **Add node**, e ele já irá adicionar um novo nó logo abaixo do primeiro. Quando clicar em cima dele irá aparecer no lado direito da tela a área de edição.

![imagens/Untitled%207.png](imagens/Untitled%207.png)

Logo no topo a primeira coisa que deve fazer é nomear o seu nó, e isso é importante para que consiga encontrar mais facilmente onde está cada coisa quando a sua estrutura começar a crescer. Em seguida tem a opção de **If assistant recognizes** (se o assistente reconhecer) que é onde irá colocar a condição, ou seja, a intenção ou a entidade que irá acionar aquele nó.

Também é permitida a validação de mais de um parâmetro utilizando operadores lógicos como **and** e **or**, ou adicionando mais parâmetros clicando no botão de + do lado do campo já existente. Nesse ponto é possível validar não só outras intenções ou entidades, mas também o nível de confiança que o assistente tem que, a mensagem dita pelo usuário, realmente corresponde a aquele parâmetro, e para isso é utilizado o seguinte código:

```bash
intents.get(0).confidence < 0.8
```

Além disso, lá em baixo tem a opção **Then assistant should** (Depois o assistente deve) que define o que o nó deve fazer após exibir a mensagem. E aqui existem duas possibilidades.

- **Wait for reply:** Espera que o usuário envie mais alguma mensagem para acionar algum outro nó;
- **Jump to:** Após exibir a resposta desse nó irá acionar logo em seguida algum outro nó que deseja exibir.

### Opções de resposta

Existem alguns tipos diferentes de resposta, e isso permite que tenha mais flexibilidade para decidir qual a melhor forma de responder sobre um determinado assunto. E além disso apertando o botão **Add response type** (Adicione um tipo de resposta), é possível trabalhar com mais de um tipo para que, caso desejado, faça uma resposta ainda mais completa. Os tipos disponíveis são:

**Text:** Possibilita que responda com um texto simples para o usuário. É possível escrever mais de uma resposta em um único nó, e existem algumas opções para controlar como deseja que isso seja exibido:

- **random:** Uma das mensagens será exibida para o usuário de forma randômica a cada vez que ele ativar o mesmo nó;
- **multiline:** Todas as mensagens serão exibidas sequencialmente toda vez que o nó for ativado;
- **sequential:** Assim como no modo random, apenas uma mensagem será exibida a cada vez que o nó for ativado, porém serão exibidas se acordo com a sequência em que foram escritas.

**Image:** Permite que responda com uma imagem que esteja disponível na internet, além de possibilitar que escreva um título e uma descrição para ela.

![imagens/Untitled%208.png](imagens/Untitled%208.png)

**Pause:** Permite que determine uma pausa antes de responder a mensagem, além disso também te dá a opção de habilitar ou não o indicador de digitação, para simular que a resposta que virá em seguida ainda está sendo escrita.

![imagens/Untitled%209.png](imagens/Untitled%209.png)

**Option:** Permite que algumas opções sejam exibidas para que o usuário clique, e para isso duas coisas são necessárias:

- **List label:** Texto que será exibido para o usuário clicar;
- **Value:** A mensagem que será interpretada pelo assistente para executar algum outro nó.

![imagens/Untitled%2010.png](imagens/Untitled%2010.png)

---

## Escrito por:

![imagens/Mask_Group_(2).png](imagens/Mask_Group_(2).png)

### [Alexia Gabrielly](https://www.linkedin.com/in/alexia-gabrielly/)

IT Service Specialist