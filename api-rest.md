### API RESTful

#### API: (Application Programming Interface)
- Interface de comunicação entre sistemas.
- Toda comunicação dessa interface é via web.

#### REST: (Representation State Transfer)
- Um estilo de arquitetura de software que define um conjunto de restrições e boas regras para o desenvolvimento dessas APIs.

#### Endpoint
- A URL que serve para fazer a requisição.
- **Base URL**
  - Ínicio da URL da requisição.
  - Ex. **https://api.programadores.com**
- **Resource ou Path**
  - Recurso é tipo de informação que você está buscando.
  - Ex. **https://api.programadores.com/php**
- **Query String**
  - A query string são os parâmetros daquela requisição.
  - Ex. **https://api.programadores.com/php?pais=brasil&contratacao=clt**
  - Parâmetros da URL, usa-se p (?) e adicionar novos parâmetros usa-se (&)

#### Métodos
- O método informa o tipo de acão daquela requisição.
- **GET**
  - Buscar dados.
- **POST**
  - Enviar dados.
- **PUT**
  - Atualizar todos dados.
- **PATCH**
  - Atualizar dados parciais.
- **DELETE**
  - Deletar dados.

#### Headers
- Permite que você envie dados informações adicionais na requisiçõa.
- Ex. Autenticação, formatação de objetos...
- Ex. **"Authorization: token123242343534".**

#### Body
- O body é o corpo da mensagem que você quer enviar na requisição.
 - Utiliza-se nos métodos (POST, PUT, PATCH).

#### HTTP Status Code:
- O Status code serve para facilitar o entendimento das respostas da APIs.
- Mais utilizados.
- **200 (OK), 201 (created), 204 (no content), 404 (not found), 400 (bad request) e 500 (internal server error)**.
- **Prefixo 20x**: Sucesso.
- **Prefixo 30x**: Redirecionamento.
- **Prefixo 40x**: Erro do cliente.
- **Prefixo 50x**: Erro do servidor.

#### Autenticação
- Principais métodos de autenticações.
- **Basic authentication**
  - Baseado em usuário e senha codificados em Base64 e utilizado no header da requisição.
- **Secret token**
  - Token de acesso que pode ser limitado a escopo, e que é enviado na requisição pelo Header ou pela Query String.

#### Autenticação vs Autorização
- **Autenticação:** Quem é você? A autenticação confirma que os usuários são quem dizem ser, validando suas identidades.
- **Autorização:** O que você pode fazer? Já a autorização concede a esses usuários autenticados permissão para acessar recursos.

#### Principais métodos de autenticação
 
#### Basic Authentication
- Basic authentication é um esquema de autenticação bem simples especificado no protocolo HTTP.
- O cliente envia uma requisição com o header (Authorization) que contém a palavra Basic e o nome de usuário e senha, separados por dois pontos (:) no formato de base64.
- Ex. **Authorization: Basic dGhpYWdvOnRoaWFnb0AxMjM=**

#### API Keys
- API Keys é um método de autenticação que teoricamente veio para resolver alguns problemas do modelo de Basic Authentication.
- A ideia do método de API Keys é simples, o servidor gera uma chave de acesso única para o client, e para utilizar a API, o client envia essa chave única em toda requisição.
- Normalmente essa key é utilizada no header.
- Ex. **Api-key: thi123456**

#### OAuth
- O OAuth está na sua versão 2.0, e não é apenas um método de autenticação, e sim um protocolo completo com diversas especificações de segurança.
- Ele é extremamente útil para o processo de autenticação e autorização, e por isso, atualmente é o método mais recomendado para o cenário de APIs.
- **Resource Owner:** entidade dona do recurso, ou seja, que é capaz de controlar o acesso a um recurso. Normalmente é o próprio usuário.
- **Resource Server:** servidor que possui os recursos, e por sua vez, recebe as requisições.
- **Authorization Server:** servidor que gera tokens de acesso para permitir que o client acesse os recursos autorizados pelo resource owner.
- **Client:** aplicação que acessa os recursos do resource server.
- **OpenID Connect:** Extensão da funcionalidade de autenticação do OAuth. Como o OAuth foi projetado para autorização, o OpenID Connect acaba sendo um ótimo complemento na segurança de APIs, conseguindo ajudar no sentido de provar que o usuário é realmente quem ele diz que é.
- **JWT:** Formato de token seguro que utiliza JSON como base.

### SAML
- Temos também o SAML, ou Security Assertion Markup Language. Que é um padrão aberto que permite que provedores de identidade (IDP) passem credenciais de autorização para provedores de serviços (SP).

#### Boas práticas de segurança
- Mantenha simples a sua implementação.
- Sempre utilize HTTPS.
- Não exponha dados sensíveis na URL.
- Considere a utilização de OAuth.
- Utilize o Rate Limit.
  - Com a implementação, você sempre retorna os seguintes headers na resposta de uma requisição:
  - **X-Rate-Limit-Limit** — Número de requisições permitidas durante um período específico (dia, hora, etc)
  - **X-Rate-Limit-Remaining** —Número de requisições restantes do período corrente
  - **X-Rate-Limit-Reset** — Segundos restantes do período corrente
- Timestamp na requisição.
- Valide o parâmetros da requisição.
- Utilize uma ferramenta de API Gateway

#### Versionando APIs RESTful

#### Versionamento pela URL
- Quando versionamos pela URL temos três maneiras de fazer isso: subdomínio, path ou query string.
- **subdomínio**: Ex. https://**api-v1**.api.programadores.com/php
- **path**: Ex. Ex. https://api.programadores.com/**v1**/php
- **query string**: Ex. https://api.programadores.com/php?**version=1.0**

#### Versionamento pelo Header
- O versionamento via header pode ser via HTTP content-type, ou seja, utilizando o header "Accept" na requisição, como por exemplo:
- Ex. **Accept: application/vnd.gastronomia.v2+json**

#### Paginação, Ordenação e Filtros em APIs RESTful

#### Paginação
- **Cursor:** A paginação baseada em cursor funciona por uma chave única e sequencial que indica a partir de que registro os dados serão retornados.
- Ex. https://api.programadores.com/php?**since_id=156&max_id=200**
- **Page e PageSize:** É utilizada através dos parâmetros de número da página a ser navegada e o seu respectivo tamanho (em número de registros).
- Ex. https://api.programadores.com/php?**page=3&page_size=10**
- **Offset e Limit:** É utilizada a partir de um deslocamento de registros.
- Ex. https://api.programadores.com/php?**offset=10&limit=30**

#### Filtros e Ordenação
- É utilizado através de query string para dar mais inteligência a sua API.
- Exemplo de filtro. https://api.programadores.com/php?**pais=brasil&contratacao=clt**
- Exemplo de ordenação. https://api.programadores.com/php?**sort=pais:asc,estado**

#### Políticas em APIs RESTful

#### Rate limiting
- Rate-limiting é a configuração do limite de requisições aceitas pela API em uma determinada janela de tempo, e que 
pode ser em segundos, horas, dias, etc. Por exemplo: 100 requisições a cada 1 hora.

#### Throttling 
- Throttling por sua vez é a configuração da fila de requisições excedidas para processamento em uma janela de tempo 
posterior, ou seja, é o tempo de delay do processamento da requisição após o client exceder os parâmetros de rate limit. Por exemplo: 2 retentativas com delay de 1 minuto.

#### API Quota
- Isso normalmente é utilizado quando o consumo da API é cobrado do client.

#### API Burst (Plus)
- Sua configuração de rate-limit é de 10 requisições por minuto, porém um client envia 20 requisições de uma vez, 
porém sua API está com capacidade ociosa no servidor, então você processa todas as requisições em alta performance e retorna ao client

#### Cache, compressão e muito mais sobre performance em APIs RESTful
- O que é cache?
  - Cache é uma estrutura computacional de armazenamento focada em manter cópias de dados que são acessados com frequência.
- Com o cache, você tem os seguintes benefícios na sua API:
  - Redução da latência de rede.
  - Redução de carga de processamento dos servidores.
  - Otimização de tempo de resposta ao client.
- **Shared cache**: Armazena respostas de servidores para reutilização entre diversos usuários.
- **Private cache**: Armazena respostas de servidores para utilização de um usuário único.

#### Cache no client
- O protocolo HTTP tem suas especificações (RFC) para utilização de políticas de cache.
- Todas elas são especificadas no header de uma requisição.

#### Controle de cache
- O header cache-control é recomendado para declaração de mecanismos de cache. As principais diretivas disponíveis são:
- **No caching**: Com a diretiva "no-store", você estará especificando para que nem na requisição do client, e nem na resposta do server seja utilizado cache.
- Ex. **Cache-Control: no-store**

- **Cache but revalidate**: Com a diretiva "no-cache", o browser irá enviar uma requisição ao servidor para validação desses dados.
- Ex. **Cache-Control: no-cache**

- **Private and public caches**: A diretiva "public" permite que os dados de resposta do servidor sejam armazenados
  em um cache compartilhado. Enquanto a diretiva "private" permite que os dados de resposta do servidor sejam armazenados no browser para utilização de apenas um usuário.

- **Expiration**: A diretiva "max-age" é utilizada para setar o máximo de tempo (segundos) em que os dados ficarão disponíveis em cache.
- Ex. **Cache-Control: max-age=30**

- **Validation**: A diretiva "must-revalidate" obriga que o browser sempre revalide os dados com o servidor antes de utilizar o cache.
- Ex. **Cache-Control: must-revalidate**

#### Entity Tags
- Ele é utilizado como resposta do server para especificar uma versão dos dados que estão sendo retornados.

#### Cache no Server

#### Load Balancing
- Em cenários que sua API tem uma quantidade de requisições alta para apenas um servidor, então você utiliza essa
técnica para distribuir a capacidade de processamento das requisições e tráfego de rede, com isso você torna sua API mais escalável e segura, pois se um servidor falhar, você terá outros funcionando.

#### Proxy Reverso
- Um proxy reverso é basicamente uma interface pública da sua API, ou seja, ele funciona como um intermediador de todas as requisições externas.

#### Gateway
- Na prática além de ser a interface de acesso a sua API para a internet, o gateway normalmente traz funcionalidades 
interessantes como: roteamento, monitoramento, autenticação e autorização, transformação de dados, segurança avançada por políticas, etc.

#### CDN
- CDN é um conceito muito difundido no mundo Web, e quer dizer Content Delivery Network — Rede de Distribuição de Conteúdo.

#### Compressão de dados
- O padrão REST permite diversos formatos de dados como XML, JSON, HTML, etc.
- Em todos eles, é possível comprimir a mensagem, fazendo com que o servidor trafegue menos dados, e gerando uma melhoria de performance na API.

- Accept-Encoding: **Accept-Encoding: gzip,compress**

####  Como chegar ao nível supremo de APIs RESTful
- Vamos utilizar um framework chamado "Richardson Maturity Model"
- Níveis:
- 0: The swarm of POX.
- 1: Resources.
- 2: Http Verbs.
- 3: Hypermedia Controls.
- 4: Developer Experience.

Anotações retirada do blog:
- https://thiagolima.blog.br/