===============
5. Propriedades
===============

Nesta seção veremos as propriedades que podem ser informadas na criação dos componentes.

5.1 Display
-----------

Essa propriedade determina se o elemento será ou não adicionado no momento de sua criação.

.. code:: php

   $inputTemplate = new \Cajudev\UI\Template('input', [
      'label' => [
         'display' => '::display',
         'text' => 'Olá Mundo'
      ],
      'input' => [
         'attributes' => [
            'class' => 'form-control mb-5',
            'type' => 'text'
         ]
      ]
   ]);

   $easyForm = new \Cajudev\EasyForm();

   $easyForm->templates->add($inputTemplate);

   $easyForm->create('input', [
      '::display' => true
   ]);

   $easyForm->create('input', [
      '::display' => false
   ]);

   echo $template->render(['formulario' => $easyForm]); 

Resultado:

.. raw:: html

   <form>
      <label>Olá Mundo</label>
      <input class="form-control mb-5" type="text"/>
      <input class="form-control mb-5" type="text"/>
   </form>


5.2 Attributes
--------------

Essa propriedade recebe um array com todos os atributos html que
você deseja adicionar a esse elemento.

.. code:: php

   $inputTemplate = new \Cajudev\UI\Template('input', [
      'input' => [
         'attributes' => [
            'id'    => '::id',
            'class' => 'form-control mb-5',
            'type'  => '::type',
            'name'  => '::id',
            'value' => '::value',
            'readonly',
         ]
      ]
   ]);

   $easyForm = new \Cajudev\EasyForm();

   $easyForm->templates->add($inputTemplate);

   $easyForm->create('input', [
      '::id'    => 'username',
      '::type'  => 'text',
      '::value' => 'joao',
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. code:: html

   <form>
      <input id="username" class="form-control mb-5" type="text" name="username" value="joao" readonly/>
   </form>

.. raw:: html

   <form>
      <input id="username" class="form-control mb-5" type="text" name="username" value="joao" readonly/>
   </form>

5.3 Text
--------

Essa propriedade adiciona um nó de texto ao elemento

.. code:: php

   $labelTemplate = new \Cajudev\UI\Template('label', [
      'label' => [
         'text' => '::text'
      ]
   ]);

   $easyForm = new \Cajudev\EasyForm();

   $easyForm->templates->add($labelTemplate);

   $easyForm->create('label', [
      '::text'    => 'Olá Mundo',
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. code:: html

   <form>
      <label>Olá Mundo</label>
   </form>

.. raw:: html

   <form>
      <label>Olá Mundo</label>
   </form>

5.4 Options
-----------

Essa propriedade é exclusiva do elemento select, e recebe um array associativo, onde as chaves são os
atributos "value" e os valores são os nós de texto.

.. code:: php

   $selectTemplate = new \Cajudev\UI\Template('select', [
      'select' => [
         'attributes' => [
            'class' => 'custom-select mb-5'
         ],
         'options' => '::options'
      ]
   ]);

   $easyForm = new \Cajudev\EasyForm();

   $easyForm->templates->add($selectTemplate);

   $easyForm->create('select', [
      '::options'    => [
         'RS' => 'Rio de Janeiro',
         'SP' => 'São Paulo',
         'ES' => 'Espirito Santo'
      ],
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. code:: html

   <form>
      <select class="custom-select mb-5">
         <option value="RS">Rio de Janeiro</option>
         <option value="SP">São Paulo</option>
         <option value="ES">Espirito Santo</option>
      </select>
   </form>

.. raw:: html

   <form>
      <select class="custom-select mb-5">
         <option value="RS">Rio de Janeiro</option>
         <option value="SP">São Paulo</option>
         <option value="ES">Espirito Santo</option>
      </select>
   </form>

5.5 Children
------------

Essa propriedade permite definir a hierarquia dos elementos no template, permitindo
construir estruturas mais complexas, como a do exemplo abaixo.

.. code:: php

   $selectTemplate = new \Cajudev\UI\Template('select', [
      'fieldset' => [
         'attributes' => [
            'class' => 'form-group col-::col'
         ],
         'children' => [
            'label' => [
               'attributes' => [
                  'class' => 'color-::color text-weight-bold',
                  'for' => '::id'
               ],
               'text' => '::label',
               'children' => [
                  'span' => [
                     'display' => '::required!',
                     'attributes' => [
                        'class' => 'color-::color required'
                     ],
                     'text' => '*'
                  ]
               ]
            ], 
            'select' => [
               'attributes' => [
                  'class' => 'custom-select color-::color border-::color arrow-::color',
                  'id' => '::id', '::multiple', '::required'
               ],
               'options' => '::options'
            ],
            'small' => [
               'attributes' => [
                  'class' => 'color-light-::color float-right font-italic'
               ],
               'text' => '::small'
            ]
         ],
      ],
   ]);

   $easyForm = new \Cajudev\EasyForm();

   $easyForm->templates->add($selectTemplate);

   $states = [
      'RJ' => 'Rio de Janeiro',
      'SP' => 'São Paulo',
      'ES' => 'Espirito Santo',
      'PR' => 'Paraná',
      'SC' => 'Santa Catarina',
      'RS' => 'Rio Grande do Sul',
   ];
   
   $easyForm->create('select', [
      '::col'      => '4',
      '::label'    => 'Cidade',
      '::color'    => 'blue',
      '::small'    => 'Selecione sua cidade',
      '::required' => 'required',
      '::options'  => $states
   ]);

   echo $template->render(['formulario' => $easyForm]);

Resultado:

.. code:: html

   <form>
      <fieldset class="form-group col-4">
         <label class="color-blue text-weight-bold">Cidade
            <span class="color-blue required">*</span>
         </label>
         <select class="custom-select color-blue border-blue arrow-blue" required>
            <option value="RJ">Rio de Janeiro</option>
            <option value="SP">São Paulo</option>
            <option value="ES">Espirito Santo</option>
            <option value="PR">Paraná</option>
            <option value="SC">Santa Catarina</option>
            <option value="RS">Rio Grande do Sul</option>
         </select>
         <small class="color-light-blue float-right font-italic">Selecione sua cidade</small>
      </fieldset>
   </form>

.. raw:: html

   <form>
      <fieldset class="form-group col-4">
         <label class="color-blue text-weight-bold">Cidade
            <span class="color-blue required">*</span>
         </label>
         <select class="custom-select color-blue border-blue arrow-blue" required>
            <option value="RJ">Rio de Janeiro</option>
            <option value="SP">São Paulo</option>
            <option value="ES">Espirito Santo</option>
            <option value="PR">Paraná</option>
            <option value="SC">Santa Catarina</option>
            <option value="RS">Rio Grande do Sul</option>
         </select>
         <small class="color-light-blue float-right font-italic">Selecione sua cidade</small>
      </fieldset>
   </form>

O css adicionado foi o seguinte

.. code:: css

   .required {
      font-size: 30px;
      position: relative;
      top: 5px;
      font-weight: bold;
   }

Se você é o tipo de pessoa que prefere olhar as coisas de maneira mais desacoplada,
uma possibilidade seria desmembrar as partes da estrutura como no exemplo a seguir,
onde criamos o template por partes. O resultado é o mesmo.

.. code:: php

   $selectStructure['fieldset'] = [
      'attributes' => [
         'class' => 'form-group col-::col'
      ],
   ];

   $fieldset =& $selectStructure['fieldset']['children'];

   $fieldset['label'] = [
      'attributes' => [
         'class' => 'color-::color text-weight-bold',
         'for' => '::id'
      ],
      'text' => '::label',
   ];

   $label =& $fieldset['label']['children'];

   $label['span'] = [
      'display' => '::required!',
      'attributes' => ['class' => 'color-::color required'],
      'text' => '*'
   ];

   $fieldset['select'] = [
      'attributes' => [
         'class' => 'custom-select color-::color border-::color arrow-::color',
         'id' => '::id', '::multiple', '::required'
      ],
      'options' => '::options'
   ];

   $fieldset['small'] = [
      'attributes' => [
         'class' => 'color-light-::color float-right font-italic'
      ],
      'text' => '::small'
   ];

   $selectTemplate = new \Cajudev\UI\Template('select', $selectStructure);