=======================
4. Estilização Dinâmica
=======================

Agora que temos uma melhor estrutura, adicionaremos variáveis responsáveis pela estilização
dos nossos elementos

.. code:: php

   $inputTemplate = new \Cajudev\UI\Template('input', [
      'fieldset' => [
         'attributes' => [
            'class' => 'form-group col-::col' // nova variável
         ],
         'children' => [
            'label' => [
               'attributes' => [
                  'for'   => '::id',
                  'class' => 'color-::color' // nova variável
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
            'small' => [
               'text' => '::small',
               'attributes' => [
                  'class' => 'color-light-::color'  // nova variável
               ]
            ]
         ]
      ],
   ]);

Também colocaremos algumas informações básicas na criação do objeto

.. code:: php

   $easyForm = new \Cajudev\EasyForm([
      'id'     => 'form',
      'action' => '#',
      'class'  => 'd-flex flex-wrap',
   ]);

   $easyForm->templates->add($inputTemplate);

Adicionamos também no css algumas classes

.. code:: css

   .color-blue {
      color: #0d4cac;
   }
   .color-light-blue {
      color: #00c3ff;
   }
   .color-purple {
      color: #770d69;
   }
   .color-light-purple {
      color: #c515a8;
   }

Finalmente atribuímos valores às novas variáveis

.. code:: php

   $easyForm->create('input', [
      '::col'   => '12',
      '::id'    => 'username',
      '::label' => 'Nome de Usuário',
      '::type'  => 'text',
      '::small' => 'Informe um nome de usuário sem caracteres especiais',
      '::color' => 'blue'
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::id'    => 'password',
      '::label' => 'Senha',
      '::type'  => 'password',
      '::small' => 'Informe uma senha de 8 caracteres, incluindo letras e números',
      '::color' => 'blue'
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::id'    => 'password',
      '::label' => 'Repita a Senha',
      '::type'  => 'password',
      '::small' => 'Confirme a senha informada anteriormente',
      '::color' => 'blue'
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. raw:: html

   <form id="form" action="#" class="d-flex flex-wrap">
      <fieldset class="form-group col-12">
         <label for="username" class="color-blue">Nome de Usuário</label>
         <input id="username" class="form-control" type="text"/>
         <small class="color-light-blue">Informe um nome de usuário sem caracteres especiais</small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label for="password" class="color-blue">Senha</label>
         <input id="password" class="form-control" type="password"/>
         <small class="color-light-blue">Informe uma senha de 8 caracteres, incluindo letras e números</small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label for="password" class="color-blue">Repita a Senha</label>
         <input id="password" class="form-control" type="password"/>
         <small class="color-light-blue">Confirme a senha informada anteriormente</small>
      </fieldset>
   </form>

Caso queira depois alterar o estilo, basta trocar a variável ::color e tudo será atualizado.

.. code:: php

   $easyForm->create('input', [
      '::col'   => '12',
      '::id'    => 'username',
      '::label' => 'Nome de Usuário',
      '::type'  => 'text',
      '::small' => 'Informe um nome de usuário sem caracteres especiais',
      '::color' => 'blue'
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::id'    => 'password',
      '::label' => 'Senha',
      '::type'  => 'password',
      '::small' => 'Informe uma senha de 8 caracteres, incluindo letras e números',
      '::color' => 'purple' // alterado aqui
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::id'    => 'password',
      '::label' => 'Repita a Senha',
      '::type'  => 'password',
      '::small' => 'Confirme a senha informada anteriormente',
      '::color' => 'purple'  // alterado aqui
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado

.. raw:: html

   <form id="form" action="#" class="d-flex flex-wrap">
      <fieldset class="form-group col-12">
         <label for="username" class="color-blue">Nome de Usuário</label>
         <input id="username" class="form-control" type="text"/>
         <small class="color-light-blue">Informe um nome de usuário sem caracteres especiais</small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label for="password" class="color-purple">Senha</label>
         <input id="password" class="form-control" type="password"/>
         <small class="color-light-purple">Informe uma senha de 8 caracteres, incluindo letras e números</small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label for="password" class="color-purple">Repita a Senha</label>
         <input id="password" class="form-control" type="password"/>
         <small class="color-light-purple">Confirme a senha informada anteriormente</small>
      </fieldset>
   </form>