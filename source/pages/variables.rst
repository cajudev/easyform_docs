===================
3. Usando Variáveis
===================

Modificaremos nosso template criado anteriormente, tornando dinâmico o texto que será atribuído a tag label 
bem como o tipo do input. 

A sintaxe para a criação de variáveis é:
Dois pontos, seguido do nome da variável, seguido opcionalmente por um operador especial.

.. code:: php

   <?php

   $inputTemplate = new \Cajudev\UI\Template('input', [
      'label' => [
         'text' => '::label'
      ],
      'input' => [
         'attributes' => [
            'class' => 'form-control',
            'type'  => '::type'
         ],
      ]
   ]);

   $easyForm = new \Cajudev\EasyForm();
   $easyForm->templates->add($inputTemplate);

   //Agora na criação dos componentes, devemos informar os valores das variáveis

   $easyForm->create('input', [
      '::label' => 'Nome de Usuário',
      '::type'  => 'text',
   ]);

   $easyForm->create('input', [
      '::label' => 'Senha',
      '::type'  => 'password',
   ]);

   $easyForm->create('input', [
      '::label' => 'Repita a Senha',
      '::type'  => 'password',
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. raw:: html

   <div class="container mb-4">
      <div class="title-container">
        <h1 class="title">Guia do Usuário Easy Form</h1>
      </div>
      <form>
         <label>Nome de Usuário</label>
         <input class="form-control" type="text"/>
         <label>Senha</label>
         <input class="form-control" type="password"/>
         <label>Repita a Senha</label>
         <input class="form-control" type="password"/>
      </form>
   </div>

O código HTML até então está sendo gerado assim:

.. code:: html

   <form>
      <label>Nome de Usuário</label>
      <input class="form-control" type="text">
      <label>Senha</label>
      <input class="form-control" type="password">
      <label>Repita a Senha</label>
      <input class="form-control" type="password">
   </form>

Geralmente labels e inputs são relacionado pelos atributos for e id, adicionaremos essa relação
através de uma única variável a mais que colocaremos em nosso template.

.. code:: php

   <?php

   $inputTemplate = new \Cajudev\UI\Template('input', [
      'label' => [
         'attributes' => [
            'for' => '::id' // variável nova aqui
         ],
         'text' => '::label'
      ],
      'input' => [
         'attributes' => [
            'id'    => '::id', // mesma variável aqui
            'class' => 'form-control',
            'type'  => '::type'
         ],
      ]
   ]);

   $easyForm = new \Cajudev\EasyForm();
   $easyForm->templates->add($inputTemplate);

   $easyForm->create('input', [
      '::id'    => 'username',
      '::label' => 'Nome de Usuário',
      '::type'  => 'text',
   ]);

   $easyForm->create('input', [
      '::id'    => 'password',
      '::label' => 'Senha',
      '::type'  => 'password',
   ]);

   $easyForm->create('input', [
      '::id'    => 'repeat-password',
      '::label' => 'Repita a Senha',
      '::type'  => 'password',
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. code:: html

   <form>
      <label for="username">Nome de Usuário</label>
      <input id="username" class="form-control" type="text"/>
      <label for="password">Senha</label>
      <input id="password" class="form-control" type="password"/>
      <label for="repeat-password">Senha</label>
      <input id="repeat-password" class="form-control" type="password"/>
   </form>

Agora adicionaremos outras duas tags em nosso template, um fieldset para agrupar os elementos
e um small para incluir uma explicação mais detalhada em cada um.

Para informar a hierarquia entre o fieldset e os demais, utilizamos a chave ``children``.

.. code:: php

   $inputTemplate = new \Cajudev\UI\Template('input', [
      'fieldset' => [ // novo elemento adicionado
         'attributes' => [
            'class' => 'form-group'
         ],
         'children' => [ // indica que os próximos elementos estarão dentro do elemento fieldset
            'label' => [
               'attributes' => [
                  'for' => '::id'
               ],
               'text' => '::label'
            ],
            'input' => [
               'attributes' => [
                  'id'    => '::id',
                  'class' => 'form-control',
                  'type'  => '::type'
               ],
            ],
            'small' => [ // novo elemento adicionado
               'text' => '::small'
            ]
         ]
      ],
   ]);

   $easyForm = new \Cajudev\EasyForm();
   $easyForm->templates->add($inputTemplate);

   $easyForm->create('input', [
      '::id'    => 'username',
      '::label' => 'Nome de Usuário',
      '::type'  => 'text',
      '::small' => 'Informe um nome de usuário sem caracteres especiais'
   ]);

   $easyForm->create('input', [
      '::id'    => 'password',
      '::label' => 'Senha',
      '::type'  => 'password',
      '::small' => 'Informe uma senha de 8 caracteres, incluindo letras e números'
   ]);

   $easyForm->create('input', [
      '::id'    => 'password',
      '::label' => 'Repita a Senha',
      '::type'  => 'password',
      '::small' => 'Confirme a senha informada anteriormente'
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. raw:: html

   <form>
      <fieldset class="form-group">
         <label for="username">Nome de Usuário</label>
         <input id="username" class="form-control" type="text"/>
         <small>Informe um nome de usuário sem caracteres especiais</small>
      </fieldset>
      <fieldset class="form-group">
         <label for="password">Senha</label>
         <input id="password" class="form-control" type="password"/>
         <small>Informe uma senha de 8 caracteres, incluindo letras e números</small>
      </fieldset>
      <fieldset class="form-group">
         <label for="password">Repita a Senha</label>
         <input id="password" class="form-control" type="password"/>
         <small>Confirme a senha informada anteriormente</small>
      </fieldset>
   </form>