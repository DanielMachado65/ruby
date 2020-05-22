# Ruby

> "linguagem dinâmica, open source com foco na simplicidade e na produtividade" - Ruby [Lang](https://www.ruby-lang.org/pt/)

até o final da `apostila` você vai conseguir entender esse pedaço de código:

```ruby
class Api::PedidoControllers << Api::ApiController
    include Mongoid::Document

    def iniciatlize(attrs)
        attrs(attrs)
    end

    def attrs
        @variavel =
end
```

### Tópicos do Aprendizado

1. Linguagem Básica
   1. __Variáveis__
   2. __Controle__
   3. __Funções__
   4. __Classe__
   
2. Linguagem Avançada
   1. __Thread__
   2. __Socket__

## 1. Linguagem Básica

#### 1.1 Variáveis 

No ruby a linguagem é dinamica, então você vai poder declarar básicamente qualquer coisa, que ela consegue assumir. (_Locais de Memória_)

O `Ruby` pode conter:
 1. ### Variáveis Globais
    Variáveis globais com `$`. 
    * tem valor nulo
    * produzem avisos com a opção `-w`
    
    ```ruby
    $global_variable = 10
    ```

 2. ### Variáveis de Instância
    Variáveis instância com `@`. 
    * tem valor __nll__
    * produzem avisos com a opção `-w`
    
    ```ruby
    @instance_variable = 10
    ```

 3. ### Variáveis de Classe
    Variáveis classe com `@@`. 
    * devem ser inicializadas para poderem ser usadas. 
    * produzem errors quando não são inicializadas 
    
    ```ruby
    class Classe
        @@class_variable = 10

        def initialize(id, name, addr)
            @cust_id = id
            @name = name
            @addr = addr
        end
         
         def total_no_of_classes()
            @@class_variable += 1
            p "Total numbers of classes: #{@@class_variable}"
        end
    end

    ## para usar
    cust1 = Customer.new("1", "Daniel", "Curitiba")
    cust2 = Customer.new("2", "Rafael", "Curitiba")

    cust1.total_no_of_classes()
    cust2.total_no_of_classes()

    # TODO: produzirá
    # Total numbers of classes: 1
    # Total numbers of classes: 2
    ```  
 4. ### Variáveis Locais de Ruby
    Variáveis locais com `_` ou `letras minúscula`. 
    * varia de classe, módulo, def ou chave de abertura. 
    * produzem errors quando não são inicializadas 

 5. ### Constantes em Ruby
    Variáveis constantes com `LETRAS MAIÚSCULAS`. 
    * Fora de uma classe ou módulo podem ser acessadas globalmente.
    * não podem ser inicializadas dentro de métodos
    * referência não inicializada produz um erro 
  
 6. ### Pseudo Variáveis em Ruby
    Pseudo variáveis são palavras reservadas que representam variáveis locais. 
    * São palavras:
      * `self` - objeto receptor do método atual
      * `true`
      * `false`
      * `nil` - indefinido
      * `__FILE__` - nome do arquivo atual
      * `__LINE__` - número de linha atual no arquivo de origem
  
 7. ### Basic Literais em Ruby
    São as variáveis padrão. 
    1. Números Inteiros - __Fixnum__ e inteiros 
       1. __Bignum__ - números grandes
       2. `0` - octal
       3. `0x` - hexadecimal
       4. `0b` - binário
       5. representação de caractér: `?(_caracter_) - ?a
    2. Números Flutantes - __Float__ 
   
    3.  Strings - sequência de 8 bits e são objetos de classe __String__. 
    
    4. Array - série de reférência de objetos separados por vírgula entre os colchotes
    
    5. Hash  - chave e valor entre chaves, com virgula ou da representação: `=>`
    
    6. Ranges(*intervalo*) - conjunto de valores com início ou fim. Os intervalos podem ser construídos usando `s..e` ou `Range.new`
 
 8. ### Hashes
      Aceitam um conjunto `chave-valor`;
      ```ruby
      config = Hash.new
      config['porta'] = 80
      config['ssh'] = false
      config['server'] = "Caelum.com.br"
      ```
 9.  ### Array 


### Attr_acessor:

um atalho para crião de métodos de leitura e escrita para as classes, exemplo:

```ruby
class Pessoa
end 

pessoa = Pessoa.new
pessoa.nome
# NoMethodError: undifened method 'nome'

class Pessoa
   attr_accessor :nome
end

pessoa = Pessoa.new
pessoa.nome
# nil

```

### Métodos(Função)

Como ruby, é uma linguagem OO completamente, você ouvira mais o nome método do que função normalmente. Enfim sua declaração é:

```ruby
def exemplo(param)
   # code
end
```

Para trabalhar com classes é mais ou menos alguma coisa parecida com: 

```ruby
class Exemplo
   def exemplo.faz(alguma_coisa)
      p 'Foi passado para essse método' + alguma_coisa
   end
end
```


lembrando que não precisa escrever o `return` normalmente declarado em outras linguagens, exemplo: 

```ruby
# ruído de código
def method(params)
   return params*params
end

# pode ser definido como
def method(params)
   params*params
end
```

há possibilidade de chamar o método atrás do método `send`, exemplo: 

```ruby
pessoa.send(:nome_metodo, variáveis)
```


### Classes

Como foi já tratado ao longo do arquivo é assim que define uma classe:

```ruby
class NomeClasse < ExtendeAlgumaClasse
   
   # constructo 
   def iniciatlize(params)
      @params = params
   end

   # método normal da classe
   def method(params)
   end

   # método estático
   def self.method(params)
   end

   # método privado
   private
   def method(params)
   end
end
```

Algumas convenções: 

```ruby
class Pessoa
   def nome #acessor
      @nome
   end

   def nome=(novo_nome)
      @nome  = novo_nome
   end
end
```

* ### Syntax Sugar
   O que seria uma simples **atribuição** passa para ser uma chamada de método
   
   ```ruby
   # antigamente
   pessoa.nome=("Novo nome")

   # novo
   pessoa.nome = "Novo nome"
   ```
* ### `&` - passando código, como parâmetro
   
   O que acontece é que passamos um pedaço de código, que queremos executar:

   ```ruby
   ## código que vamos passar
   banco.status do | saldo_parcial |
      p saldo_parcial
   end
   ```

   como vai ser executada: 

   ```ruby
   class Banco
      def status(&block)
         saldo = 0
         for conta in @contas
            saldo += contas
            
            if block_given?
               block.call(saldo)
            end
         end
         saldo
      end
   end
   ```

   podemos usar ainda o uso de `chaves`:

   ```ruby
   banco.status { | saldo_parcial | puts saldo_parcial }
   ```

   podemos chamar atrás do **yield**

   ```ruby
   if block_given?
      yield(saldo)
   end
   ```

   para entedimento melhor: 

   ```ruby
   funcionario = ["Gui", "Tope"]
   nomes_maisculas = funcionarios.cria_uma_array do | nome |
      nome.upcase
   end

   class Array
      def cria_uma_array
         array = []
         self.each do |elemento|
            array << yield(elemento)
         end
      end  
   end
   ```