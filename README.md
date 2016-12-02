Teste para Desenvolvedor PHP - Synus
====================================

Este teste tem por objetivo validar os conhecimentos dos desenvolvedores PHP interessados em trabalhar 
na área de desenvolvimento de sistemas da Synus.

Esse teste poderá ser executado pelo candidato de forma remota, não sendo necessário nenhuma intervenção presencial.

Se o candidato não tiver a estrutura necessária para realizar o teste (computador e internet), deve agendar um horário
para realizá-lo na sede da **Synus**.

Não existe limite de tempo para a execução do teste. Esperamos receber a resposta em até uma semana após a entrega.


Preparação do ambiente
----------------------

Esse projeto contém apenas um ambiente Vagrant configurado, para que você possa escrever o código 
do seu teste e nos enviar.

Este ambiente contém:

* **Sistema Operacional:** CentOS 6.1
* **Web server:** Nginx 1.10.2
* **Relational Database:** MariaDB 10.1.19
* **Schemaless Database:** MongoDB 3.2.11
* **PHP:** PHP 7.0.13
* **Ferramentas Adicionais:** Composer e xdebug

São pré-requisitos para rodar o ambiente, os seguintes sistemas (devem ser instalados na máquina local, 
em sua última versão):

* [Git](https://git-scm.com/downloads)
* [Oracle Virtual Box](https://www.virtualbox.org/wiki/Downloads) 
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [Ansible](http://docs.ansible.com/ansible/intro_installation.html) (Apenas para Linux ou Mac, para Windows não é 
necessário)

Uma vez instalados todos os requisitos, deve-se então criar um *branch* com o seu nome_sobrenome e 
clonar o repositório para sua máquina local.

****Atenção!!! Você deve criar um _branch_ com o seu nome antes de clonar o projeto!**** 

Dentro da raiz do projeto clonado, deve-se então rodar, via linha de comando, o seguinte comando:

    vagrant up
    
Esse comando pode levar um bom tempo para executar a primeira vez, dependendo da sua conexão com a internet, 
pois ele vai baixar o box do CentOS e instalar todo o ambiente.

A partir daí pode-se acessar o endereço http://192.168.33.99 para ter acesso ao projeto rodando.

O código estará dentro da pasta `src`, que se encontra na raiz do projeto. Essa pasta é o *document root* 
do *webserver*.

Informações do servidor MariaDB:

    Database: synus
    Senha de root: 123
    Usuário: user
    Senha: password

Se o seu código depender de alguma alteração de ambiente (como a instalação de um novo pacote de software), 
essa alteração deve ser realizada dentro do playbook do Ansible, para que seja reproduzida no momento da 
correção pela equipe da Synus.

Todo commit deve ser realizado no *branch* criado.

Ao concluir o seu trabalho, realize um *pull request* para o *branch* master. Nesse momento avaliaremos o seu 
código.


Execução do Teste
-----------------

Esse teste é aplicado para todos os níveis de desenvolvedores PHP (Junior, Pleno e Senior), antes de integrarem a 
equipe de desenvolvimento da Synus. Apenas algumas regras são alteradas dependendo do nível pretendido.

O teste consiste na criação de um microblog corporativo, extremamente simples, semelhante ao 
[Twitter](https://twitter.com/).

Todas as funcionalidades do sistema, devem ser apresentadas como aplicação web e como uma API rest, para
ser acessada por outras aplicações (como por exemplo aplicativos mobile).

Na aplicação web, os usuários são autenticados por nome de usuário e senha, na API deverão ser identificados
por um token, gerado e validado pela API.

Não é necessário se preocupar com limites de acesso na API (isso não se faz em produção, mas isso é um teste).

Toda a modelagem e arquitetura do sistema fica a critério do desenvolvedor, a única exigência, é usar 
PHP sobre um design MVC (ou similar).

Pode-se usar uma abordagem relacional, *schemaless*, ou ainda um *mix* de ambas para a persistência dos 
dados. Pede-se para utilizar MariaDB e/ou MongoDB para tal.
 
A análise e criação de *test-cases* deve ser baseada nas *user stories* descritas abaixo.


### User Stories

* Como um usuário anônimo, devo me registrar para me tornar um usuário registrado.
* Como um usuário anônimo, devo ser capaz de me logar no sistema.
* Como um usuário registrado, devo ser capaz de alterar minha senha.
* Como um usuário registrado, devo ser capaz de criar posts.
* Como um usuário registrado, devo ser capaz de editar os posts criados por mim.
* Como um usuário registrado, devo ser capaz de excluir os posts criados por mim.
* Como um usuário registrado, devo ser capaz de listar todos os posts de um determinado usuário (qualquer um).
* Como um usuário registrado, devo ser capaz de clicar em um link de usuário, e acessar a lista com seus 
posts.
* Como um usuário registrado, devo ser capaz de seguir outros usuários registrados.
* Como um usuário registrado, devo ser capaz de visualizar minha timeline (*homepage*), que mostra todos 
os meus posts e os posts dos usuários que eu sigo, ordenados por data de criação.
* Como um usuário registrado, devo ser capaz de listar todos os posts que contém uma determinada hashtag.
* Como um usuário registrado, devo ser capaz de clicar em um link de hashtag, e acessar a lista com todos 
os posts que contém essa hashtag. 
* Como um usuário registrado, devo ser capaz de desconectar do sistema, voltando a ser um usuário anônimo.


### Regras

* Posts devem conter um número limitado de caracteres e esse valor deve ser definido como um parâmetro 
global.
* Posts podem conter markups básicos:
    * **Negrito**: Qualquer sequencia de caracteres entre asteriscos (`\*texto em negrito\*`);
    * *Itálico*: Qualquer sequencia de caracteres entre percentagens (`%texto em itálico%`);
    * <u>Sublinhado</u>: Qualquer sequencia de caracteres entre underlines (`_texto sublinhado_`);
    * [Link](http://synux.com.br): Colchetes, com dois valores (texto e endereço), separados por dois
    pontos ( `[Texto do link:http://enderecodolink.com]`  );
    * Hashtags: Qualquer sequencia de letras e números (sem espaços) precedida por um sustenido (#textodahashtag);
    * Usuários: Um nome de usuário precedido por um arrouba (@nomedousuario);
* As hashtags devem ser *case insensitive* e ser formadas apenas por letras e números. 
* As hashtags devem ser exibidas como links.
* Os nomes de usuário devem ser exibidas como links.
* Usuários anônimos só podem acessar a página de registro e login.
* Usuários registrados podem acessar todas as páginas, menos a de registro e login.
* Em todas as páginas que listam posts, os mesmos devem ser listados em ordem de criação, do mais novo para
o mais antigo.


Avaliação
---------

Algumas regras devem ser seguidas para apresentação do código (todos os níveis):

* Só inicie o projeto se você se considera capaz de realizá-lo. Caso contrário, você não tem o nível
de conhecimento necessário para integrar o time da Synus. Continue evoluindo, sempre haverá novas vagas.
* Só solicite o *pull request* de finalização se o seu projeto cumpre os requisitos.
* O arquivo src/README.md, deve ser preenchido com as instruções de setup do seu projeto.
* Utilize instruções simples, preferencialmente um script único que faça todo o setup.
* Inclua o procedimento para acesso, tanto da aplicação web, quanto da API.
* Seu código deve rodar! Nós não vamos perder tempo corrigindo problemas de setup, então garanta
que seu ambiente está rodando antes de realizar o pull request.
* É importante que o projeto tenha dados para teste (por meio de um seeder), para que seja fácil não só subir, 
mas também testar seu projeto.  
* Se não conseguir subir o ambiente, nos avise, mas certifique-se que realmente é um problema no ambiente,
e não na sua máquina.
* A utilização de ferramentas como git/github, Vagrant e Ansible, faz parte da avaliação.
* A aplicação deve serguir o *pattern* MVC, ou alguma variação do mesmo.
* Nós faremos um code review, portanto comente seu código de forma que alguém que apenas conhece as regras
de negócio do sistema possa entender o que você está fazendo.
* Tente seguir as recomendações [PSR-1](http://www.php-fig.org/psr/psr-1/) e [PSR-2](http://www.php-fig.org/psr/psr-1/).
* Faça seus commits fazerem sentido (mensagens simples, que dizem o que o commit faz), isso será avaliado.


Nível **Junior**:

* Utilizar algum framework MVC para o projeto. Pode ser qualquer um a sua escolha (Zend, Laravel, Symphony, 
Yii, Phalcon, Code Igniter). O que queremos avaliar é a sua capacidade de entender e interagir com uma 
arquitetura MVC.
* Será avaliada a utilização do *composer* e do *git* também. 
* Cumpra os requisitos do projeto e você tem enormes chances de ser aprovado.


Nível **Pleno**:

* Utilizar um framework MVC, como no nível Júnior.
* Seguir os princípios SOLID, o mais a risca possível.
* Criar outras camadas auxiliares ao MVC, como services por exemplo (necessário para seguir os SOLID).
* Usar anotações *PHPdoc* com maestria, em todo o código.
* Criar testes unitários para o projeto, e incluir no *readme* as instruções para rodá-los.
* Gerar dados do ambiente com migrations e seeders.


Nível **Senior**:

* **Não utilizar framework MVC!** Claro que em um projeto real não tomaremos essa decisão, mas a idéia 
aqui, é testar sua capacidade de entender o real funcionamento de uma arquitetura MVC, e não apenas 
utilizá-la como uma caixa preta.
* Você pode, e é encorajado, a utilizar bibliotecas, mas não um framework para o projeto todo.
* Dominar o *composer* é essencial.
* Anotações PHPdoc impecáveis.
* Princípios SOLID respeitados.
* TDD - Crie primeiro os testes, depois o código.
* Documentação gerada automaticamente a partir das anotações


Dicas:

* Recrie seu ambiente do zero depois de concluir a codificação e verifique se tudo funciona antes de 
solicitar o *pull request*.
* Temos faixas salariais para cada nível, sendo que o ponto onde você se enquadrará nessas faixas depende 
do seu desempenho no teste. Não tenha medo de mostrar seu conhecimento. Nos impressione!



