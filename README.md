
  

# Projeto Engenharia de Software NODE

  

Exemplo de projeto utilizando Node.js.

  

Este exemplo é um aplicativo web que pode ser executado localmente assim como realizar o deploy em hosts de homologação/produção.

  

* Este projeto utiliza o framework web [Express](https://expressjs.com/)

* Está configurado com o banco de dados Mongo DB com o utilitário [Mongoose](https://mongoosejs.com/) para modelagem dos objetos

* Para a definição das views e templates é utilizado a engine [EJS](https://ejs.co)

* Também está implmentado alguns testes unitários e de comportamento com as diretivas _assert_ do NODE e com o utilitário [MOCHA](https://mochajs.org/). Também está sendo utilizado o [Chai](https://www.chaijs.com) (BDD/TDD)

  

## Arquitetura da aplicação

* Esta aplicação utiliza uma arquitetura MVC (Model, View e Control)

  

* O **Model** é responsável pela estrutura de dados da aplicação, e neste caso utiliza o Schema do mogoose para modelagem dos dados. Os arquivos de Models fica no diretório `/models/`. Todos arquivos dentro do diretório /models são carregados automaticamente pelo autoload *consign*

* O **Controller** é responsável pela regra de negócio, assim como instanciar os models e gerenciar os dados para renderizar as views. O model fica no diretório `/controllers/`. Todos arquivos dentro do diretório /controllers são carregados automaticamente pelo autoload *consign*

* As **Views** tem a responsabilidade de renderizar e mostrar as informações oriundas do model e é controlada pelo controller. O diretório de localização das views é `/views/`

  

* Todas as rotas, ou seja as urls que serão utilizadas para acessar cada função no sistema são definidas no diretório `/routes/`. Todos arquivos dentro do diretório /routes são carregados automaticamente pelo autoload *consign*

* O diretório `/middleware/` é destinado para funções que irão "interceptar" alguma ação, como por exemplo os erros são interceptados pelo arquivo `/middleware/error.js` que é utilizado para renderizar uma página "amigável" caso ocorra um erro 500 ou página não encontrada (404).

* Os testes são executados todos arquivos *.js que estão localizados no diretório `/tests/`

  
  

## Banco de dados

É utilizado um banco de dados MongoDB. Você poderá utilizar para rodar localmente, uma instância do banco de dados também local [Instalar MongoDB](https://docs.mongodb.com/manual/administration/install-community/).

Para uma instância em rede, tem um Database as a Service (DBaaS) MongoDB que possui um plano gratuito. 
[mLab](https://mlab.com/)

As configurações do banco de dados devem ser criadas em um arquivo chamado `.env`. O projeto tem um exemplo das requeridas configurações
```sh
$ cp .env.example .env
```
Editar o arquivo `.env` com as suas configurações 
  

## Executando Localmente

  

Deve ter instalado o [Node.js](http://nodejs.org/)

  

```sh

$ git clone https://github.com/engenhariadesoftwareuepg/projetonode.git

$ cd projetonode

$ npm install

$ cp .env.example .env

$ nano .env # ou outro editor para configurar as variáveis ambiente

$ npm start

```

  

A aplicação deverá estar executando no endereço [localhost:5000](http://localhost:5000/).

  

  

## Deploying no Heroku (método 1)

  

Deve ter instalado o [Heroku CLI](https://cli.heroku.com/)

  

```

$ heroku create

$ git push heroku master

$ heroku open

```

  

  

### Documentação do Heroku

  

Para maiores informações segue os artigos da documentação sobre Node.js no Heroku:

  

-  [Iniciando com Node.js no Heroku](https://devcenter.heroku.com/articles/getting-started-with-nodejs)

  

-  [Suporte Heroku Node.js ](https://devcenter.heroku.com/articles/nodejs-support)

  

-  [Node.js no Heroku](https://devcenter.heroku.com/categories/nodejs)

  

-  [Melhores práticas para o desenvolvimento Node.js](https://devcenter.heroku.com/articles/node-best-practices)

  

-  [Usando WebSockets no Heroku com Node.js](https://devcenter.heroku.com/articles/node-websockets)

  

## Realizando o deploy através do Travis-CI (método 2 - recomendado)

  

Este processo é configurado pelo arquivo chamado `.travis.yml`

  

- Utilizar a sua conta no Heroku

- Fazer o login [https://id.heroku.com/login](https://id.heroku.com/login)

- Criar um novo APP com o nome que desejar (o nome deve ser único no Heroku).

- Editar o arquivo `.travis.yml` e adicionar o nome que você escolheu para a sua app:

`app: \<nome da sua app\>`

- Acessar o seu App no heroku, e na aba "Settings" e em "Config vars" configurar todas as variáveis ambientes disponíveis no .env.example para o seu ambiente de produção (com exceção da PORT, pois o heroku já possui uma variável ambiente da porta onde o servidor será instanciado)

- Acessar o seu perfil e verificar a sua API KEY (ela será utilizada posteriormente no Travis-CI)

- Criar uma conta no [Travis-CI](https://travis-ci.org/). Utilizar a mesma conta do github "Sign in with GitHub"

- Buscar o repositório do seu projeto e habilitar a integração

- Clicar em "settings" do projeto e em "Environment Variables"

- Adicionar uma variável ambiente com o name: "HEROKU_API_KEY" (sem aspas)

- O value copiar do seu perfil no heroku.

- Adicionar as demais variáveis ambiente do arquivo .env dentro do travis-ci para a execução dos testes

  

Neste momento o Travis-CI já deverá estar monitorando a sua branch master.

Cada vez que um push é realizado será iniciado um processo no travis, onde instanciará um ambiente transitório (temporário) para instalar a aplicação, realizar os testes automatizados e se tudo estiver corretor, automaticamente realiza o deploy na plataforma do Heroku.