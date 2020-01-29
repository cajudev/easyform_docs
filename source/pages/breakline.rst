8. Quebras de Linha
===================

8.1 Método BreakLine
--------------------

Esse método permite quebrar uma linha em um layout flex.

Acompanhe o exemplo:

.. code:: php

   $inputTemplate = new \Cajudev\UI\Template('input', [
      'fieldset' => [
         'attributes' => [
            'class' => 'form-group col-::col'
         ],
         'children' => [
            'label' => [
               'text' => '::label'
            ],
            'input' => [
               'attributes' => [
               'class' => 'form-control',
               'type'  => '::type'
               ],
            ],
         ]
      ]
   ]);

   $easyForm = new \Cajudev\EasyForm([
      'class' => 'd-flex flex-wrap'
   ]);

   $easyForm->templates->add($inputTemplate);

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

.. raw:: html

   <form class="d-flex flex-wrap">
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
   </form>

Se adicionarmos mais um input aqui, ele consequentemente ficará na segunda fileira. Mas caso você queira colocá-lo
na linha de baixo, basta fazer uma chamada ao método breakLine e continuar criando os elementos.

.. code:: php

   // código anterior omitido

   $easyForm->breakLine();

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

Resultado:

.. raw:: html

   <form class="d-flex flex-wrap">
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <div style="flex: 0 0 100%; max-width: 100%; margin: 10px 0"></div>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
   </form>

Você também pode passar por parâmetro o valor do espaçamento desejado:

.. code:: php

   // código anterior omitido

   $easyForm->breakLine();

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

   $easyForm->breakLine(60);

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

Resultado:

.. raw:: html

   <form class="d-flex flex-wrap">
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <div style="flex: 0 0 100%; max-width: 100%; margin: 10px 0"></div>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <div style="flex: 0 0 100%; max-width: 100%; margin: 60px 0"></div>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
   </form>

8.2 Método DrawLine
-------------------

O método drawLine também permite inserir uma quebra de linha, porém adicionando também uma borda.

Usaremos o mesmo exemplo anterior:

.. code:: php

   // código anterior omitido

   $easyForm->drawLine();

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

Resultado:

.. raw:: html

   <form class="d-flex flex-wrap">
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <div style="flex: 0 0 100%; max-width: 100%; margin: 10px 0">
         <hr width="100%" style="border-color: #DADADA; float: none;"/>
      </div>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
   </form>

As opções que podem ser passadas por parâmetro são: Espaçamento, Largura da Linha, Cor e Posição.
Sendo que a posição pode ser left ou right. Caso não seja informada ficará ao centro.

.. code:: php

   $line = [30, 70, '#fe9999', 'left'];

   $easyForm->drawLine(...$line);

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

   $easyForm->drawLine(...$line);

   $easyForm->create('input', [
      '::col'   => '4',
      '::type'  => 'text',
      '::label' => 'Alguma coisa'
   ]);

Resultado:

.. raw:: html

   <form class="d-flex flex-wrap">
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <div style="flex: 0 0 100%; max-width: 100%; margin: 30px 0">
         <hr width="70%" style="border-color: #fe9999; float: left;"/>
      </div>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
      <div style="flex: 0 0 100%; max-width: 100%; margin: 30px 0">
         <hr width="70%" style="border-color: #fe9999; float: left;"/>
      </div>
      <fieldset class="form-group col-4">
         <label>Alguma coisa</label>
         <input class="form-control" type="text"/>
      </fieldset>
   </form>