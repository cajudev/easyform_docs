=====================
7. Lista de Elementos
=====================

As opções abaixo são elementos válidos na criação de templates.

- button
- datalist
- div
- fieldset
- i
- input
- label
- legend
- optgroup
- option
- output
- select
- small
- textarea

Veja mais um exemplo de template usando alguns dos elementos da Lista

.. code:: php

   $iconInputTemplate = new \Cajudev\UI\Template('icon-input', [
      'div' => [
         'attributes' => [
            'class' => 'input-container'
         ],
         'children' => [
            'div' => [
               'attributes' => [
                  'class' => 'icon-container'
               ],
               'children' => [
                  'i' => [
                     'attributes' => [
                        'class' => 'icon icon-::icon'
                     ],
                  ]
               ]
            ],
            'input' => [
               'attributes' => [
                  'class' => 'input',
                  'id' => '::id',
                  'type' => '::type',
                  'placeholder' => '::placeholder'
               ],
            ],
         ],
      ],
   ]);

   $easyForm = new \Cajudev\EasyForm([
      'class' => 'd-flex flex-wrap'
   ]);

   $easyForm->templates->add($iconInputTemplate);

   $easyForm->create('icon-input', [
      '::id'    => 'email',
      '::type'  => 'email',
      '::icon'  => 'email',
      '::placeholder' => 'Email',
   ]);

Resultado:

.. raw:: html

      <form class="d-flex flex-wrap mb-3">
         <div class="input-container">
            <div class="icon-container">
               <i class="icon icon-email"></i>
            </div>
            <input class="input" id="email" type="email" placeholder="Email"/>
         </div>
      </form>

Para esse exemplo o seguinte css foi aplicado

.. code:: css

   .input-container {
      box-shadow: 2px 2px 2px 0px #e3e4ff;
   }

   .icon-container {
      width: 35px;
      text-align: center;
      background: linear-gradient(#ff471a, #ec3b0f);
      margin-right: -1px;
      float: left;
      height: 100%;
   }

   .icon-email:before {
      content: '\f0e0';
   }

   .icon {
      font-size: 20px;
      color: white;
      vertical-align: sub;
   }

   .input {
      padding-left: 10px;
      padding-top: 3px;
      border: solid 1px #71a6ff;
   }