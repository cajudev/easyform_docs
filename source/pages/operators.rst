=======================
6. Operadores Especiais
=======================

Nessa seção veremos como utilizar os operadores especiais que podem ser usados para dar
um significado diferente à uma variável.

6.1 Operador Opcional (?)
-------------------------

Quando uma variável é criada mas não recebe seu valor na criação do componente, entende-se que
foi uma falha do programador, e por consequência todo o atributo do qual essa variável faz parte
é removido da estrutura.

Primeiro, vamos analisar um exempo válido:

.. code:: php

   $buttonTemplate = new \Cajudev\UI\Template('button', [
      'button' => [
         'attributes' => [
            'class' => 'btn btn-::style btn-::size',
         ],
         'text' => '::text'
      ],
   ]);

   $easyForm = new \Cajudev\EasyForm();

   $easyForm->templates->add($buttonTemplate);

   $easyForm->create('button', [
      '::style' => 'primary',
      '::size'  => 'lg',
      '::text'  => 'Enviar',
   ]);

Resultado:

.. raw:: html

   <form>
      <button class="btn btn-primary btn-lg mb-3">Enviar</button>
   </form>

Mas o que acontece se eu não informar um valor para a variável ::size?

.. code:: php

   $easyForm->create('button', [
      '::style' => 'primary',
      '::text'  => 'Enviar',
   ]);

Resultado:

.. raw:: html

   <form>
      <button>Enviar</button>
   </form>

Todo o atributo ``class`` da qual aquela variável faz parte foi removido. Esse comportamento serve para indicar
ao programador que ele esqueceu de inicializar alguma variável, pois a mesma poderia passar desapercebida
e ter coisas como ::size aparecendo no código fonte da página.

Quando surge a necessidade de ter variáveis opcionais, ou seja, que nem sempre deverão ser informadas,
você pode utilizar o operador ``?``, que ao invés de remover todo o atributo removerá apenas essa variavel,
caso a mesma não seja informada.

.. code:: php

   $buttonTemplate = new \Cajudev\UI\Template('button', [
      'button' => [
         'attributes' => [
            'class' => 'btn btn-::style btn-::size?', //operador aqui
         ],
         'text' => '::text'
      ],
   ]);

   $easyForm = new \Cajudev\EasyForm();

   $easyForm->templates->add($buttonTemplate);

   $easyForm->create('button', [
      '::style' => 'primary', //size não foi inicializada
      '::text'  => 'Enviar',
   ]);

Resultado:

.. raw:: html

   <form>
      <button class="btn btn-primary mb-3">Enviar</button>
   </form>

6.2 Operador Condicional (!)
----------------------------

O operador condicional serve para relacionar a existência de um atributo com a existência de uma variável.

No exemplo a seguir, criamos uma condição onde o elemento ``span``, somente será exibido,
caso a variável ``::required`` tenha sido informada.

.. code:: php

   $inputTemplate = new \Cajudev\UI\Template('input', [
      'label' => [
         'text' => '::label',
         'children' => [
            'span' => [
               'display' => '::required!', // operador aqui
               'text' => '*'
            ]
         ]
      ], 
      'input' => [
         'attributes' => [
            'type'  => '::type',
            'class' => 'form-control',
            '::required'
         ],
      ]
   ]);

   $easyForm = new \Cajudev\EasyForm();

   $easyForm->templates->add($inputTemplate);

   $easyForm->create('input', [
      '::type'  => 'text',
      '::label' => 'Nome de Usuário'
   ]);

Resultado:

.. raw:: html

   <form class="mb-3">
      <label>Nome de Usuário</label>
      <input type="text" class="form-control"/>
   </form>

Agora inicializando a variável:

.. code:: php

   $easyForm->create('input', [
      '::type'  => 'text',
      '::label' => 'Nome de Usuário',
      '::required' => 'required'
   ]);

Resultado:

.. raw:: html

   <form class="mb-3">
      <label>Nome de Usuário<span>*</span></label>
      <input type="text" class="form-control" required/>
   </form>