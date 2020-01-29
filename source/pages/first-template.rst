====================
2. Primeiro Template
====================

Antes de podermos criar elementos de um formulário, é necessário primeiro criar
templates que serão como componentes pré configurados. O código fica assim.

.. code:: php

   <?php

   require_once 'vendor/autoload.php';

   $loader = new \Twig\Loader\FilesystemLoader('./');
   $twig = new \Twig\Environment($loader, ['cache' => './']);
   $template = $twig->load('index.html');

   // Aqui instanciamos um objeto Template, que recebe 2 argumentos.
   // O primeiro é o nome do template e o segundo é sua estrutura
   // Em nosso caso criamos a mesma estrutura que antes foi criada diretamente no HTML
    $inputTemplate = new \Cajudev\UI\Template('input', [
        'label' => [
            'text' => 'Nome de Usuário'
        ],
        'input' => [
            'attributes' => [
                'class' => 'form-control',
                'type'  => 'text'
            ],
        ]
    ]);

    //Em seguida instanciaremos um objeto EasyForm
    $easyForm = new \Cajudev\EasyForm();

    //E adicionamos o template criado anteriormente
    $easyForm->templates->add($inputTemplate);

    //Finalmente, podemos criar o componente input
    $easyForm->create('input');

    //E passamos o objeto para ser renderizado
    echo $template->render(['formulario' => $easyForm]);

Se tudo ocorreu bem, você deverá visualizar o mesmo resultado de quando havia criado em HTML

.. raw:: html

   <div class="container mb-4">
      <div class="title-container">
        <h1 class="title">Guia do Usuário Easy Form</h1>
      </div>
      <form><label>Nome de Usuário</label><input class="form-control"/></form>
    </div>

Agora podemos criar quandos componentes quisermos de maneira muito fácil

.. code:: php

   <?php

   // Ocultamos o restante do código para poupar espaço

   $easyForm->create('input');
   $easyForm->create('input');
   $easyForm->create('input');
   $easyForm->create('input');

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. raw:: html

   <div class="container mb-4">
      <div class="title-container">
         <h1 class="title">Guia do Usuário Easy Form</h1>
      </div>
      <form>
         <label>Nome de Usuário</label>
         <input class="form-control" />
         <label>Nome de Usuário</label>
         <input class="form-control" />
         <label>Nome de Usuário</label>
         <input class="form-control" />
         <label>Nome de Usuário</label>
         <input class="form-control" />
      </form>
   </div>

Obviamente não faz sentido ter diversos inputs para nome de usuário, veremos na próxima seção
como utilizar variáveis na criação de templates.