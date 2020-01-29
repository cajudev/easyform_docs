9. Criando Seções
=================

Criar seções dentro de um formulário é muito simples. Basta um template e um pouco de css, como no exemplo abaixo:

.. code:: php

   $sectionTemplate = new \Cajudev\UI\Template('section', [
      'div' => [
         'attributes' => [
            'class' => 'col-12 section-container'
         ],
         'children' => [
            'span' => [
               'attributes' => [
                  'class' => 'section-title'
               ],
               'text' => '::text'
            ]
         ]
      ]
   ]);

.. code:: css

   .section-container {
      width: 100%;
      border-radius: 2px;
      margin-bottom: 20px;
      background: linear-gradient(to bottom, #ff471a 0%, #ec3b0f 100%);
   }

   .section-title {
      font-size: 25px;
      color: white;
      font-weight: bold;
   }

.. code:: php

   $easyForm = new \Cajudev\EasyForm([
      'class' => 'd-flex flex-wrap'
   ]);

   $easyForm->templates->add($sectionTemplate);

   $easyForm->create('section', ['::text' => 'Seção 1']);

Resultado:

.. raw:: html

   <form class="d-flex flex-wrap">
      <div class="col-12 section-container">
         <span class="section-title">Seção 1</span>
      </div>
   </form>

Agora é só criar alguns inputs, cujos templates já foram mostrados nas seções anteriores desta documentação.

.. code:: php

   $easyForm->create('section', ['::text' => 'Seção 1']);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

   $easyForm->create('section', ['::text' => 'Seção 2']);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

   $easyForm->create('section', ['::text' => 'Seção 3']);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

   $easyForm->create('input', [
      '::col'   => '6',
      '::label' => 'Alguma Coisa',
      '::type'  => 'text',
   ]);

Resultado:

.. raw:: html

   <form class="d-flex flex-wrap">
      <div class="col-12 section-container">
         <span class="section-title">Seção 1</span>
      </div>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
      <div class="col-12 section-container">
         <span class="section-title">Seção 2</span>
      </div>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
      <div class="col-12 section-container">
         <span class="section-title">Seção 3</span>
      </div>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
      <fieldset class="form-group col-6">
         <label>Alguma Coisa</label>
         <input class="form-control" type="text"/>
         <small></small>
      </fieldset>
   </form>