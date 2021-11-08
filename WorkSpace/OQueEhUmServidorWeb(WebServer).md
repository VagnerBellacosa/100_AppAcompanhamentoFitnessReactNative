# O que é um servidor web (web server)?

Neste artigo vamos revisar o que são web servers, como eles funcionam, e por que eles são importantes.

| Pré-requisitos: | Você deve saber [como a Internet funciona](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/How_does_the_Internet_work) e [entender a diferença entre uma página web, um site, um servidor web e um mecanismo de busca](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/Pages_sites_servers_and_search_engines). |
| :-------------- | ------------------------------------------------------------ |
| Objetivo:       | Você irá aprender o que é um servidor web e compreender de modo geral como ele funciona. |

## [Sumário](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/What_is_a_web_server#sumário)

"Servidor web (*web server*)" pode referir ao hardware ou ao software, ou ambos trabalhando juntos.

1. Referente ao hardware, um servidor web é um computador que armazena arquivos que compõem os sites (por exemplo, documentos HTML, imagens, folhas de estilo, e arquivos JavaScript) e os entrega para o dispositivo do usuário final. Está conectado a Internet e pode ser acessado através do seu nome de domínio (DNS), como por exemplo `mozilla.org`.
2. Referente ao software, um servidor web inclui diversos componentes que controlam como os usuários acessam os arquivos hospedados (armazenados para disponibilização), no mínimo um *servidor HTTP.* Um servidor HTTP é um software que compreende [URLs](https://developer.mozilla.org/pt-BR/docs/Glossary/URL) (endereços web) e [HTTP](https://developer.mozilla.org/pt-BR/docs/Glossary/HTTP) (o protocolo que seu navegador utiliza para visualizar páginas web.

Em um nível mais básico, o navegador fará uma requisição utilizando o protocolo HTTP sempre que necessitar de um um arquivo hospedado em um servidor web. Quando a requisição alcançar o servidor web correto (hardware), o *servidor HTTP* (software) enviará o documento requerido, também via HTTP.

![Basic representation of a client/server connection through HTTP](https://mdn.mozillademos.org/files/8659/web-server.svg)

Para publicar um website, é necessário ou um servidor web estático ou um dinâmico.

Um **servidor web estático** consiste em um computador (hardware) com um servidor HTTP (software). É chamado "estático" porque o servidor envia seus arquivos tal como foram criados e armazenados (hospedados) ao navegador.

Um **servidor web dinâmico** consiste em um servidor web estático com software adicional, mais comumente um servidor de aplicações (*application server)* e um banco de dados (*database).* É chamado "dinâmico" porque o servidor de aplicações atualiza os arquivos hospedados antes de enviá-los ao navegador através do servidor HTTP.

Por exemplo, para produzir as páginas finalizadas que você vê em seu navegador, o servidor de aplicações pode completar um modelo de página HTML (*HTML template*) com o conteúdo obtido de um banco de dados. Sites como o MDN ou a Wikipédia possuem vários milhares de páginas web, mas elas não são realmente documentos HTML, mas apenas alguns poucos *templates* HTML e uma gigantesca base de dados. Essa configuração agiliza e facilita o gerenciamento e a entrega do conteúdo.

## [Aprendizado ativo](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/What_is_a_web_server#aprendizado_ativo)

*Ainda não há aprendizado ativo disponível. [Por favor, considere contribuir](https://developer.mozilla.org/en-US/docs/MDN/Getting_started).*

## [Entrando a  fundo](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/What_is_a_web_server#entrando_a_fundo)

Para carregar uma página *web*, como já foi dito, seu *browser* envia uma requisição ao servidor *web*, que busca pelo arquivo requisitado no seu próprio espaço de armazenamento. Ao encontrar o arquivo, o servidor *web* realiza a leitura, faz os processamentos necessários e o envia ao *browser*. Vamos olhar mais detalhamente para essas etapas.

### [Servindo arquivos](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/What_is_a_web_server#servindo_arquivos)

Um servidor *web* precisa primeiro armazenar os arquivos dos *websites*, como todos os documentos HTML e seus *assets*, que incluem imagens, páginas de estilo CSS, arquivos JavaScript, fontes e vídeos.

Técnicamente, você pode servir todos esses arquivos em seu próprio computador. Mas, é muito mais conveniente armazená-los em um servidor web dedicado que

- está sempre "vivo" e rodando
- está sempre conectado à Internet
- tem o mesmo endereço IP sempre (nem todos [ISPs (en-US)](https://developer.mozilla.org/en-US/docs/Glossary/ISP) fornecem um endereço IP fixo para linhas domésticas)
- é mantido por um provedor de terceiros

Por todas essas razões, encontrar um bom provedor de servidores é a chave para criar seu próprio *website*.  Pesquise pelos vários serviços oferecidos e escolha aquele que melhor se alinha às suas necessidades e ao bolso (os serviçoes variam em uma faixa desde zero até milhares de dólares por mês). Você pode encontrar mais detalhes [nesse artigo](https://developer.mozilla.org/en-US/Learn/How_much_does_it_cost#Hosting).

Uma vez que você escolheu uma solução de servidores web, você só precisa [fazer o *upload* dos seus arquivos para o servidor *web*](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Upload_files_to_a_web_server).

### [Comunicando através do HTTP](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/What_is_a_web_server#comunicando_através_do_http)

Segundo, um servidor web fornece suporte para [HTTP](https://developer.mozilla.org/pt-BR/docs/Glossary/HTTP) (protocolo de transferência de hipertexto). Como o próprio nome indica, o HTTP especifica como transferir arquivos de hipertexto (ou seja, documentos vinculados da web) entre dois computadores.

Um *protocolo* é um conjunto de regras para comunicação entre dois computadores. HTTP é um protocolo textual sem estado.

- Textual

  Todos os comandos são de texto simples e legíveis por humanos.

- Sem estado

  Nem o servidor nem o cliente lembram de comunicações anteriores. Por exemplo, confiando apenas no HTTP, um servidor não consegue se lembrar de uma senha digitada ou da etapa em que você está em uma transação. Você precisa de um servidor de aplicativos para tarefas como essa. (Nós vamos cobrir esse tipo de tecnologia em mais artigos.)

O HTTP fornece regras claras sobre como um cliente e um servidor se comunicam. Abordaremos o próprio HTTP em um artigo técnico mais adiante. Por enquanto, apenas fique atento a estas coisas:

- Somente *clientes* podem fazer requisições HTTP, e somente para *servidores.* Servidores podem apenas *responder* a uma requisição HTTP dos *clientes*.
- Quando fizer a requisição de um arquivo via HTTP, os clientes devem fornecer a [URL](https://developer.mozilla.org/pt-BR/docs/Glossary/URL) do arquivo.
- O servidor web *deve responder* todas as requisições HTTP, mesmo que seja com uma mensagem de erro.

[![The MDN 404 page as an example of such error page](https://mdn.mozillademos.org/files/8661/mdn-404.jpg)](https://developer.mozilla.org/en-US/404)Em um servidor web, o servidor HTTP é responsável por processar e responder as requisições recebidas.

1. Ao receber uma requisição, um servidor HTTP primeiramente confirma se a URL requisitada corresponde ao arquivo existente.
2. Se confirmar, o servidor web envia o conteúdo do arquivo de volta ao navegador. Senão, o servidor de aplicações cria o arquivo necessário.
3. Se nenhum dos processos for possível, o servidor web retorna uma mensagem de erro ao navegador, mais conhecido como "404 Not Found". (Esse erro é tão comum que muitos desevolvedores web passam um bom tempo criando [páginas de erro do 404](http://www.404notfound.fr/).)

### [Conteúdo estático vs. dinâmico](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/What_is_a_web_server#conteúdo_estático_vs._dinâmico)

A grosso modo, um servidor pode fornecer tanto um conteúdo estático quanto dinâmico. "Estático" significa "da forma que está". Websites estáticos são os mais fáceis de configurar, então sugerimos que faça seu primeiro site estático.

"Dinâmico" significa que o servidor processa o conteúdo ou o gera a partir de um banco de dados. Essa solução fornece mais flexibilidade, mas a arquitetura fica mais difícil de lidar, fazendo com que seja dramaticamente mais complexo desenvolver o website.

Veja por exemplo a página na qual está lendo agora. No servidor web que a hospeda, há um servidor de aplicações que pega o conteúdo do artigo de um banco de dados, o formata, coloca dentro de um template HTML e lhe envia o resultado. Nesse caso, o servidor de aplicações é chamado de [Kuma](https://developer.mozilla.org/en-US/docs/MDN/Yari) e é desevolvido em [Python](https://www.python.org/) (usando o framework [Django](https://www.djangoproject.com/) ). A equipe da Mozilla desenvolveu o Kuma devido a necessidades específicas do MDN, mas há muitas aplicações similares em muitas outras tecnologias..

Existem tantos servidores de aplicações que é muito difícil sugerir algum em particular. Alguns servidores de aplicações atendem à categorias específicas de websites como blogs, wikis ou lojas virtuais. Outros, os chamados [CMSs](https://developer.mozilla.org/pt-BR/docs/Glossary/CMS) (sistemas de gerenciamento de conteúdo), são mais genéricos. Se estiver desenvolvendo um website dinâmico, reserve um tempo para escolher uma ferramenta que atenda às suas necessidades. A menos que queria aprender sobre o desenvolvimento de um servidor web (que é uma área interessante por si só!), não há necessidade de criar seu próprio servidor de aplicação. Estará apenas reinventando a roda.

## [Próximos passos](https://developer.mozilla.org/pt-BR/docs/Learn/Common_questions/What_is_a_web_server#próximos_passos)

Agora que está familiarizado com os servidores web, você pode:

- ler sobre [quanto custa desenvolver para a web](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/How_much_does_it_cost) (em inglês)
- aprender mais sobre os [vários softwares necessários para criar um site](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_software_do_I_need) (em inglês)
- partir para a prática de [como fazer o upload de arquivos em um servidor web](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Upload_files_to_a_web_server) (em inglês).