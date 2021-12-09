# Como reduzir em 60% o tempo de carregamento das aplicações com React

- https://www.infoq.com/br/profile/Adonias-Santos/)

### Pontos Principais

- Usar o React por si só não resultará em uma aplicação de alto desempenho. Se não tomar cuidado, pode aumentar o tamanho dela facilmente. É uma boa prática realizar auditorias periodicamente;
- O Chrome DevTools oferece uma poderosa medição de desempenho para aplicações JavaScript. Aprenda a ler e entender os perfis de desempenho;
- A divisão do código é fácil de ser configurada com o Webpack 4 e deve, definitivamente, ser usada para otimizar a aplicação;
- Identifique onde longas listas de conteúdo são renderizadas e otimize-as com o react-window;
- Entenda como o React funciona internamente. Isso ajudará a identificar renderizações desnecessárias e corrigi-las. Use a opção "Highlight Updates" no React DevTools para ajudá-lo nesta etapa;
- Existem vários outros métodos para melhorar o desempenho das aplicações React, como o prefetching, o service workers, o bundle analysis, entre outros que reduzem o tamanho dos pacotes.

Desde sua introdução, há 6 anos, o React mudou a maneira como criamos aplicações web. Várias bibliotecas de interface do usuário, como [Vue.js](https://vuejs.org/) e [Preact.js](https://preactjs.com/), foram desenvolvidas após o React. Bibliotecas existentes, como [Angular](https://angular.io/), [Dojo](https://dojo.io/) e [Ember](https://emberjs.com/), atualizaram-se para otimizar a maneira como os updates do DOM são tratadas, cada uma criando sua própria maneira de otimizar o desempenho da renderização. Muitas bibliotecas e módulos npm foram criados em torno do React para facilitar o desenvolvimento. Hoje existem dezenas de milhares de pacotes referentes ao React no repositório do NPM. E estão sendo lançados novos, todos os dias.

Somos recém convertidos do React no [Rocketium](https://rocketium.com/). Passamos por vários ciclos de mudanças de tecnologia, pois a empresa mudou de uma criadora de jogos em 2015 para uma empresa de criação de apresentações de slides em 2016 e posteriormente para uma rica plataforma de vídeos na segunda metade de 2016. A experiência com o React foi amor à primeira vista, e obtivemos rápidas vitórias na engenharia. No entanto, logo atingimos um limite de desempenho, pois passamos a utilizar o React em mais produtos. Por fim, tivemos que equilibrar o desenvolvimento de novos recursos e a criação da maneira já conhecida com o React. Como qualquer ferramenta, o React não é mágico e deve ser usado com cuidado para obter os melhores resultados.

Abaixo estão algumas das coisas que aprendemos que devem ajudar aqueles que estão considerando mudar para o React e aqueles que estão vendo as aplicações React rodando com certa dificuldade. Vamos nos aprofundar!

## Nossa jornada com o React

### **A vida antes do React**

A primeira versão do aplicativo web foi criada em 2015 com o Vanilla JavaScript, patchwork de utilitários e bibliotecas de UI. Éramos uma equipe pequena e manipular o DOM ou gerenciar o estado em funções individuais, foi suficiente para concluir o trabalho.

Dois anos depois, queríamos adicionar uma camada de colaboração e *workflow* (pense no Google Docs + Trello para vídeo). A equipe de desenvolvimento também cresceu, precisávamos de uma maneira melhor de adicionar recursos, garantir a testabilidade e evitar a imprevisibilidade de uma grande base de código mal estruturada. Parecia a hora certa de entrar, cuidadosamente, no ecossistema React.

### **Mudando para o React**

O React foi uma escolha fácil, pois vinha com um fluxo previsível de atualizações para *UI*. O React não define bem o gerenciamento do estado da aplicação ou como lidar com o roteamento, por isso decidimos usar o [Redux](https://redux.js.org/) para o gerenciamento do estado e o [React Router](https://github.com/ReactTraining/react-router) para o roteamento do lado do cliente.

Criar um aplicativo com o React é tranquilo, pois fornece uma ótima maneira de estruturar a interface do usuário em componentes, facilitando a visualização de como a interface do usuário funciona, inclusive fornece uma maneira mais fácil de reutilizar os componentes. Não tivemos boas experiências com o Redux no começo, mas nos salvou de muitas dores de cabeça no longo prazo.

### **Atingindo o limite da performance**

O React lida com as atualizações da interface do usuário com eficiência, mas isso não o torna a aplicação web mais rápida. Precisávamos saber como funcionava, como o controle fluía dentro dos componentes e como atualizava o DOM. À medida que o aplicativo avançava, percebemos algumas desvantagens na configuração. Embora soubéssemos como o React funcionava e como o Redux gerenciava o estado, a aplicação tinha aumentado de tamanho. Começamos a notar falhas no carregamento. Estava na hora de reduzir a ignorância técnica e fazer melhorias de desempenho!

Abaixo estão algumas coisas que fizemos e o que esperamos fazer no futuro para melhorar o desempenho da aplicação.

## Otimização de performance do React

### **Medindo a performance com o Chrome DevTools.**

O primeiro passo da otimização é a medição. Somente após identificar os gargalos, podemos eliminá-los. O Chrome DevTools oferece poderosas medições de desempenho para aplicações React.

[![img](https://res.infoq.com/articles/reduce-react-load-time/en/resources/1reduce-react-load-time-1-s-1559641832538.png)](https://res.infoq.com/articles/reduce-react-load-time/en/resources/reduce-react-load-time-1-1559641863144.png)

**O Chrome Devtools mostra quais componentes são renderizados**

[![img](https://res.infoq.com/articles/reduce-react-load-time/en/resources/1reduce-react-load-time-2-s-1559641831864.png)](https://res.infoq.com/articles/reduce-react-load-time/en/resources/reduce-react-load-time-2-1559641832257.png)

**Linhas vermelhas mostram picos no FPS**

### **Atualização para webpack 4**

Por um ano, usamos o Webpack 3 sem preocupação. Funcionou muito bem e não tivemos nenhuma queixa. O Webpack 4 não influencia diretamente no desempenho, mas atualizamos para facilitar a [divisão de código](https://webpack.js.org/guides/code-splitting/). Infelizmente, o Webpack 4 mudou muitas APIs, tornando a transição um pouco mais desafiadora do que havíamos esperado. No entanto, essa mudança nos permitiu adicionar alguns detalhes ao *workflow* de desenvolvimento, como passar do `CommonChunksPlugin descontinuado` para o `SplitChunksPlugin` além de configurar a divisão de código.

### **Divisão de código**

A configuração inicial não incluiu a divisão de código por padrão. Isso não era necessário quando o aplicativo era relativamente pequeno, com poucos componentes e lógica comercial simples. Com ritmo feroz de desenvolvimento de produtos com flags de recursos e testes A/B, muito mais componentes foram adicionados e o fluxo lógico ficou complicado. Colocar tudo isso em um único pacote estava travando o desempenho da aplicação.

Por que isso é um problema? Um pacote com muito mais código do que o necessário, será sempre maior do que deveria. O navegador analisará todo o código, independentemente de qual seção será carregada. Carregar um código extra significa downloads mais lentos e mais trabalho para o navegador, levando a tempos de resposta longos. Isso é muito mais perceptível em conexões lentas e hardware com baixo desempenho.

Para resolver esses problemas, configuramos a divisão de código baseada em rota usando o pacote npm [react-loadable](https://github.com/jamiebuilds/react-loadable). Em seguida, passamos para o `React.lazy` e o `Suspense` apesar de não suportar a renderização do servidor no momento. Trocamos porque agora havia uma maneira integrada de lidar com importações dinâmicas.

Configurar a divisão de código com `SplitChunksPlugin` foi fácil. Foram necessárias algumas iterações para corrigir o número de blocos. O tamanho de pacote inicial para toda a aplicação era de 7 MB. Após a divisão do código, os pacotes configuráveis iniciais tinham um tamanho combinado de 230kb, uma enorme redução de 97% no tamanho dos pacotes da aplicação!

### **Otimização de \*Long list\***

Existem alguns locais nas aplicações em que utilizamos *Long lists*, lista de fontes, faixas de música, imagens e clipes, modelos, gráficos em movimento, entre outros. Algumas dessas listas fazem chamadas HTTP em segundo plano e adicionam novos itens quando finalizadas, por exemplo, um scroll infinito. A maioria das listas na aplicação não fez isso e renderizou um grande número de itens.

A renderização desses itens estava sobrecarregando o navegador e vimos muitas falhas no carregamento. Para corrigir isso, usamos o módulo npm [react-window](https://github.com/bvaughn/react-window), que fornece um componente de ordem superior que controla a renderização de listas longas. Não processa itens que não são imediatamente visíveis. Suporta carregamento lento, propriedades personalizadas e manipuladores de eventos. Isso nos deu renderização de lista a 60fps.

### **Reduzindo renderizações desnecessárias**

As atualizações de estado geralmente acontecem em aplicações grandes e complexas. Algumas são assíncronas, como chamadas HTTP em segundo plano, e outras ocorrem após a aplicação da lógica de negócios. É bastante comum ver componentes renderizando várias vezes antes de qualquer interação do usuário. Cabe aos desenvolvedores detectar essas renderizações desnecessárias e evitá-las quando não forem necessárias.

Renderizações desnecessárias são renderizações de componentes que não precisam deste processo. É um problema em especial se as renderizações acontecerem nos componentes pai. Isso ocorre porque o React renderiza novamente todos os componentes em uma árvore quando o pai é renderizado. Isso causa processamento desnecessário.

[![img](https://res.infoq.com/articles/reduce-react-load-time/en/resources/1reduce-react-load-time-3-s-1559642986957.png)](https://res.infoq.com/articles/reduce-react-load-time/en/resources/reduce-react-load-time-3-1559642987372.png)

**Encontrando componentes que fazem renderizações desnecessárias**

A extensão [React developer tool](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) possui a opção "Highlight Updates" que usamos para encontrar os componentes que renderizam sem necessidade. Depois de identificar os componentes, corrigimos de duas maneiras diferentes.

1. Usando `shouldComponentUpdate` para informar ao React que o resultado do componente não é afetado pela alteração de estado para controlar quando um componente deve ser renderizado novamente;
2. Reorganizando a estrutura dos componentes e como as mudanças de estado acontecem. Esse é um processo mais envolvido e demoramos mais para identificar os componentes que são renderizados desnecessariamente.

## Próximos passos

Temos vários objetivos para melhorar ainda mais o desempenho das aplicações num futuro próximo.

### **Utilizar React.PureComponent**

O `React.PureComponent` é semelhante ao `React.Component`. A principal diferença é que o PureComponent implementa o `shouldComponentUpdate` com uma comparação superficial. Diz-se que isso melhora o desempenho, mas vem com algumas consequências indesejadas.

### Análise de compilação

Visualizar compilações é uma ótima maneira de entender o que ocorre nos pacotes. O analisador de pacotes [Webpack](https://github.com/webpack-contrib/webpack-bundle-analyzer) mostra a separação de todos os pacotes gerados para a aplicação em uma página da web interativa. O Webpack também permite definir orçamentos de desempenho para que possamos saber quando ativos e pacotes configuráveis excedem os limites de arquivo. Também podemos identificar e remover códigos duplicados nos pacotes com o plugin [third party Webpack](https://github.com/formidablelabs/inspectpack/).

### **Tree shaking melhorado**

O *Tree shaking* é o processo de remoção do código não utilizado ou inoperante dos pacotes configuráveis. Isso é importante principalmente ao utilizar as bibliotecas de utilitários como o *Lodash*, onde não precisamos de todos os recursos da biblioteca importada.

### ***Service Workers\* e o \*PWA\***

Os web apps progressivos são confiáveis, rápidos e envolventes. São carregados rapidamente, mesmo com internet discada, e possuem alto desempenho. Foram criados usando as mais recentes tecnologias web e oferecem experiências semelhantes a aplicativos.

### ***Prefetching\***

O *Prefetching* é uma maneira de informar ao navegador sobre os recursos que provavelmente serão solicitados e buscá-los antes que sejam necessários. Isso é feito assim que os recursos necessários para a página atual são carregados e quando o navegador está ocioso. Para aplicativos renderizados no servidor, a API Push HTTP/2 possui suporte no Node.js.

## Tornando aplicações React rápidas novamente

Após seguir as etapas deste artigo, conseguimos melhorar o desempenho geral das aplicações em mais de 60%, reduzindo o tamanho do pacote inicial de 7 MB para 230 KB, o tempo de carregamento total de 47 segundos para 19 segundos (4G lento) e o tempo de interação de 23 segundos a 15 segundos (4G lento), melhorando bastante a experiência do usuário para as aplicações.

![img](https://res.infoq.com/articles/reduce-react-load-time/en/resources/1reduce-react-load-time-4-1559642987637.jpg)

**Melhorias gerais pós otimizações**

O ecossistema React é vasto e poderoso. Podemos aproveitar as inúmeras ferramentas disponíveis para criar aplicações grandes e complexas. Acima, estão apenas algumas técnicas que podem tornar as aplicações rápidas e mais suaves. Definitivamente, o esforço adicional vale os benefícios de obter uma base de código de maior desempenho e mais sustentável.