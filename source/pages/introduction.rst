=============
1. Introdução
=============

O primeiro passo para entender a motivação e o funcionamento dessa biblioteca é pensar que
geralmente, elementos de formulário possuem estruturas padronizadas.

.. note::

   Para todos os exemplos que serão mostrados, o uso do framework **bootstrap** estará presente,
   porém a biblioteca não possui nenhum tipo de vinculo ou limitação em relação a isso.

Nesse primeiro exemplo, vamos tomar como principio que uma tag input, geralmente vem precedida
de uma tag label.

Em HTML sua estrutura seria algo como:

.. code:: html

   <label for="username">Nome de Usuário</label>
   <input id="username" type="text" class="form-control">

Colocaremos isso dentro de uma estrutura básica HTML e veremos sua renderização na tela

.. code:: html

   <!DOCTYPE html>
   <html lang="pt-br">
   <head>
      <title>Easy Form</title>
      <meta charset="utf-8" />
      <link
         rel="stylesheet"
         href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
         integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
         crossorigin="anonymous"
      />
      <link rel="stylesheet" href="style.css" />
   </head>
   <body>
      <div class="container mt-5">
         <div class="title-container">
            <h1 class="title">Guia do Usuário Easy Form</h1>
         </div>
         <form>
            <label for="username">Nome de Usuário</label>
            <input id="username" type="text" class="form-control" />
         </form>
      </div>
   </body>
   </html>

Resultado:

.. raw:: html

   <div class="container mb-4">
      <div class="title-container">
         <h1 class="title">Guia do Usuário Easy Form</h1>
      </div>
      <form>
         <label for="username">Nome de Usuário</label>
         <input id="username" type="text" class="form-control" />
      </form>
   </div>

O css usado pode ser observado a seguir

.. code:: css

   .title-container {
      background: rgba(0, 0, 0, 0.2);
      border-radius: 1rem;
      margin-bottom: 2rem;
   }

   .title {
      font-size: 22px;
      text-align: center;
      padding: 2rem 0;
   }


Agora removeremos o formulário do HTML deixando uma tag como referência para ser substituída pelo back end.
Esse trabalho geralmente é feito usando um template engine, no nosso caso utilizaremos o twig_, mas fique a 
vontade para escolher outro.

.. code:: html

   <div class="container mt-5">
      <div class="title-container">
         <h1 class="title">Guia do Usuário Easy Form</h1>
      </div>
      {{ formulario | raw }}
   </div>

Para instalar o twig basta usar o comando ``composer require "twig/twig:^2.0"``

O arquivo php fica assim:

.. code:: php

   <?php

   require_once 'vendor/autoload.php';

   // inicializa as variáveis do twig
   $loader = new \Twig\Loader\FilesystemLoader('./');
   $twig = new \Twig\Environment($loader, ['cache' => './']);

   // carrega o arquivo html que você criou
   $template = $twig->load('index.html');

   echo $template->render(['formulario' => 'Olá Mundo']);

Ao executar esse arquivo, você deverá obter o seguinte resultado

.. raw:: html

   <div class="container mb-4">
      <div class="title-container">
         <h1 class="title">Guia do Usuário Easy Form</h1>
      </div>
      Olá Mundo
   </div>

Se tudo ocorreu bem, você pode prosseguir para a próxima etapa.

.. _twig: https://twig.symfony.com/

