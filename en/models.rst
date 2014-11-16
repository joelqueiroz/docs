Models
######

Modelos são as classes que formam a camada de negócios em sua aplicação. 
Eles devem ser responsáveis pela gestão de quase tudo a respeito de seus dados, 
a sua validade, e suas interações, bem como a evolução 
do fluxo de trabalho de informações em seu domínio.

Normalmente, as classes do modelo representam dados e são usados em aplicações 
CakePHP para acesso a dados. Eles geralmente representam uma tabela de banco de dados, 
mas pode ser usado para acessar qualquer coisa que manipula dados, 
como arquivos, serviços web externos ou eventos iCal.

Um modelo pode ser associado com outros modelos. 
Por exemplo, uma receita pode ser associado com um Autor, bem como um ingrediente.

Esta seção irá explicar quais as características do modelo podem ser automatizadas, 
como substituir essas características, e quais os métodos e propriedades de um modelo pode ter. 
Irá explicar as diferentes formas de construir associações para seus dados. 
Irá descrever como encontrar, salvar e excluir dados. Por fim, vai olhar para Datasources.

Entendendo Models
====================

Um model representa o seu modelo de dados. Na programação orientada a objetos,
um modelo de dados é um objeto que representa uma coisa, como um carro, um
pessoa, ou uma casa. Um blog, por exemplo, pode ter muitos posts do blog
e cada post pode ter muitos comentários. O Blog, Post, e
Comentário são exemplos de modelos, cada um associado com um outro.

Aqui está um exemplo simples de uma definição de modelo no CakePHP ::

    App::uses('AppModel', 'Model');
    class Ingredient extends AppModel {
        public $name = 'Ingredient';
    }

Com apenas esta simples declaração, o modelo é dotado Ingrediente
com todas as funcionalidades que você precisa para criar consultas e
salvar e excluir dados. Estes métodos vêm a partir do CakePHP
Classe Model pela magia da herança. O modelo Ingrediente
estende o modelo de aplicação, AppModel, que por sua vez se estende CakePHP de
classe Modelo interno. É esta classe Model núcleo que confere o
funcionalidade para o seu modelo Ingrediente. `` App :: usos ('appmodel', 'modelo') ``
garante que o modelo é carregado quando for necessário.

A classe intermediária, AppModel, está vazio. Se você não tem
criou seu próprio, ele é retirado da pasta núcleo do CakePHP. primordial
a AppModel permite que você defina a funcionalidade que deve ser feito
disponível para todos os modelos dentro da sua aplicação. Para fazer isso, você precisa
para criar seu próprio `` AppModel.php`` arquivo que reside na pasta Model,
assim como todos os outros modelos na sua aplicação. Criando um projeto usando
: doc: `Asse <console-e-shells / code-geração com-bake>` será automaticamente
gerar este arquivo para você.

Veja também: doc: `Comportamentos <modelos / comportamentos>` para mais informações sobre
como aplicar lógica similar para vários modelos.

De volta ao nosso modelo Ingrediente. A fim de trabalhar com ele, criar o arquivo PHP no
`/` `` diretório / app / Model. Por convenção, ele deve ter o mesmo nome que a classe,
que para este exemplo será `` Ingredient.php``.

.. Nota ::

     CakePHP criará dinamicamente um objeto de modelo para você se não puder
     encontrar um arquivo correspondente em / app / Model. Isto também significa que se
     seu arquivo de modelo não é o nome correcto (por exemplo, se for chamado
     ingredient.php ou Ingredients.php em vez de Ingredient.php),
     CakePHP usará uma instância do AppModel vez
     do que o seu arquivo de modelo (que CakePHP assume está ausente). se
     você está tentando usar um método que você definiu no seu modelo, ou um
     comportamento anexado ao seu modelo, e você está recebendo erros de SQL que
     são o nome do método que você está chamando, é um sinal claro de que
     CakePHP não pode encontrar o seu modelo e você precisa verificar o arquivo
     nomes, o cache de aplicativos, ou ambos.

.. Nota ::

     Alguns nomes de classe não são utilizáveis para nomes de modelos. Por exemplo,
     "Arquivo" não pode ser utilizado, uma vez que "File" é uma classe que já existe no
     Núcleo do CakePHP.


Quando o modelo é definido, ele pode ser acessado de dentro do seu
: doc: `Controlador <controladores>`. CakePHP automaticamente
tornar o modelo disponível para acesso quando seu nome corresponde ao do
o controlador. Por exemplo, um controlador de chamada
IngredientesController irá inicializar automaticamente o Ingrediente
modelo e anexá-lo ao controlador em `` $ this-> Ingredient`` ::

    class IngredientsController extends AppController {
        public function index() {
            //grab all ingredients and pass it to the view:
            $ingredients = $this->Ingredient->find('all');
            $this->set('ingredients', $ingredients);
        }
    }

Modelos associados estão disponíveis por meio do modelo principal. no
seguinte exemplo, Receita tem uma associação com o Ingrediente
modelo ::

    class Recipe extends AppModel {

        public function steakRecipes() {
            $ingredient = $this->Ingredient->findByName('Steak');
            return $this->findAllByMainIngredient($ingredient['Ingredient']['id']);
        }
    }

Isso mostra como usar modelos que já estão ligados. Para entender como as associações são
definida, dê uma olhada no: doc: `seção Associações <modelos / associações ligando-modelos-juntos>`


Mais sobre models
==============

.. toctree::
    :maxdepth: 1

    models/associations-linking-models-together
    models/retrieving-your-data
    models/saving-your-data
    models/deleting-data
    models/data-validation
    models/callback-methods
    models/behaviors
    models/datasources
    models/model-attributes
    models/additional-methods-and-properties
    models/virtual-fields
    models/transactions


.. meta::
    :title lang=en: Models
    :keywords lang=en: information workflow,csv file,object oriented programming,model class,model classes,model definition,internal model,core model,simple declaration,application model,php class,database table,data model,data access,external web,inheritance,different ways,validity,functionality,queries
