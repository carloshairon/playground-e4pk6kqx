 
 # Enumerations - Intro
 
 Um Enumeration define um tipo para um grupo de valores associados, permitindo trabalhar com eles de uma maneira type-safe (tipos seguros) dentro do seu código. Assim, você cria uma faixa de valores que podem ser usado e evita falta de padronização em seu código.
 
 Enumerations são tipos de primeira classe, ou seja:
 * Podem ser retorno de funções
 * Podem ser passadas com paramêtros em funções
 * Podem ser construídas em tempo de execução
 
 Além de adotar funcionalidades tradicionalmente suportadas apenas por classes, tais quais:
 * Inits
 * Funções de instância e estáticas
 * Podem ser extendidas
 * Assinar protocolos
 * Possuír variavéis computadas
 
 
# Enumerations - Intro - Prática 01

==> Começamos a declaração de dois enums abaixo, mas não colocamos todos os itens. Você pode gerar uma nova versão com todos os itens de cada conjunto ?  



```swift runnable
enum Cardinal { // pontos cardeais 
    case south
    case north
}

enum Planet {
    case mercury, venus, earth, mars // planetas do sistema solar 
}

```

# Enumerations - Intro - Prática 02

Cada enumeration define um novo tipo, e como outros tipos em Swift seus nomes devem começar com uma letra maiúscula.
 
Vamos agora atribuir a uma constante *direction* um *Cardinal*. Lembre-se de trazer sua declaração para aqui também. 

==>Você poderia fazer outras declarações de costante e variáevis para os planetas? 


```swift runnable
enum Cardinal { // pontos cardeais 
    case south
    case north
}

let direction = Cardinal.south

```

# Enumerations - Switch e Enums

Enums podem ser usados com Switches de maneira muito simples.
 
Um switch deve ser exaustivo quando utilizado enums, quando não for apropriado um caso para cada enum, você pode utilizar o *default*
 
Vamos criar um switch que imprima uma String de acordo com o *Cardinal* dado. 

==> Você pode completar o enum com os demais porntos cardeias e fazer com o o switch possa prever todos os casos sem o defeault?


```swift runnable

enum Cardinal { // pontos cardeais 
    case south
    case north
}

let direction = Cardinal.south

switch direction {
case .north:
    print("go to the north son")
default:
    print("go wherever you want")
}

```

# Enumerations - Switch e Enums + Variáveis Computadas

Podemos também como comentado, atribuir variavéis computadas aos nossos Enums. Ainda não falamos de extension (extensões), por hora encare como o próprio nome sugere uma foma de adicionar "atributos e métodos" a um enum. 

```swift runnable

enum Cardinal {  
    case south
    case north
}

extension Cardinal {
    var phrase: String {
        switch self {
        case .north:
            return "go to the north son"
        default:
            return "go wherever you want"
        }
    }
}


print(Cardinal.north.phrase) // veja que agora o enum possui um atributo do tipo String e que devolve um valor a depente do caso da enumeração referenciado. 
```

# Enumerations - Switch e Enums + Variáveis Computadas - Prática

Use o seu enum de planetas e crie um atributo Double para devolver os  diâmetros equatoriais de cada planeta dos sistema solar (https://planetario.ufsc.br/o-sistema-solar/). Em seguida exiba o diâmetro de 3 planetas

```swift runnable

enum Planet {
    case mercury, venus, earth, mars // planetas do sistema solar 
}
```


 # Iterando entre cases de Enumeration
 
 Para alguns enums, é interessante que tenhamos uma coleção com todos os possiveis casos, para isso, tudo que você precisa fazer é assinar o protocolo `CaseIterable`.
 Ainda não falamos de protocolos, mas são semelhantes as interfaces do JAVA e especificam um tipo de "herança". Assim a característica dos cases (itens do enum) serem percorridas por um for, por exemplo, torna-se possível. 


 ==> Vamos declarar um Enum que assine o protocolo e iterar sob seus casos. Você pode fazer um for e interar sobre os seus planetas ? lebre-se que o seu enum de plantas deve impementar o protocolo CaseIterable

```swift runnable

enum Animals : CaseIterable    {
    case Dog, Cat, Mouse, Horse, Cow
}

for animal in Animals.allCases {
    print(animal)
}
```

# Enumeration - Associated Values (Valores Associados)

No **Swift** Enumerations podem associar valores de qualquer tipo a seus cases.
Isso permite:
 * Armazenar informações adicionais ao case
 * Informações variadas a cada uso dentro do código
 * Associar tipos diferentes para cada case
 
==> Vejamos no exemplo que foram declarados 3 tipos de dispositivos da Apple. Vocês poderiam declarar mais 2? 
 
 
```swift runnable

enum Device {
  case iPad  (String, Float, Float) // nome, polegadas, preço em $
  case iPhone (String, Float, Float) // nome, polegadas, preço em $
  case appleTV (String, Int, Float) // nome, memória, preço em $
}

var deviceCarlos : Device = .iPad ("iPad Pro", 12.9, 1099.00)
var deviceJose   : Device = .iPhone ("iPhone 13 Pro Max", 6.7,1099.00)
var deviceMaria  : Device = .appleTV ("Apple TV HD",32,149.00)

print(deviceCarlos, deviceJose, deviceMaria)

//*** IMPORTANTE *** veja como fazer acesso a cada um dos valores do enum de forma separada. Faça um exemplo disse também e comente por que é necessário o uso do IF aqui (lembre-se dos opcionais)

if case let .iPad(nome, tela, preco) = deviceCarlos {
  print ("Nome do Dispositivo: \(nome)")
  print ("Tela em Polegadas: \(tela)")
  print ("Preço: \(preco)")
}

```

Por que foi necessário usar "if" no seguinte código: 

//if case let .iPad(nome, tela, preco) = deviceCarlos {
//  print ("Nome do Dispositivo: \(nome)")
//  print ("Tela em Polegadas: \(tela)")
//  print ("Preço: \(preco)")
//}

==> Faça também um exemplo disso também e comente porque é necessário o uso do "if" aqui (lembre-se dos opcionais)

==> faça também um exemplo agora com "if..else" em que o else é executado. 

```swift runnable
//Faça seu exemplo aqui

```


# Enumerations - Raw Values
 
 Raw Values (valores crus, primários) são valores valores padrões para os cases de um enumeration. Raw Values são sempre do mesmo tipo

```swift runnable

enum ASCIIControlCharacter: Character { //veja que é necessário definir o tipo do cases
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}

var ch = ASCIIControlCharacter.tab
print ("Texto com o TAB=\(ch.rawValue) aqui no meio")

ch = .lineFeed
print ("Pula Linha = \(ch.rawValue) Linha") // utilize o atributo rawValue para fazer acesso ao valor
```


# Enumerations - Atribuição implícita

Você pode atribuir um valor de .rawValue como no exemplo anterior e o swift tentará colocar um valor para o próximo case (elemento) se você não deixar explícito. Veja qual será o valor de venus. 

==> Teste nenhum valor para mercury, o que acontece com venus ? E se o valor de mercury fosse 20 qual seria o valor de mars? Mostre o código para esses exemplos. 

```swift runnable

enum Planets: Int {
    case mercury = 10 , venus, earth, mars
}
print(Planets.venus.rawValue)
```

==>Veja agora que nenhum valor foi atribuído. Você pode exlicar o que ocorre na seguinte linha: print(CompassPoint.south.rawValue.uppercased()) ? Você pode criar outro exemplo ? 

==>Você poderia interar em todos os elementos do enum com um for e imprimir o número de caracteres de cada um da strings associadas ao case? Pesquise o atributo de tamanho de string na documentação do swift.  

```swift runnable

enum CompassPoint: String {
    case north 
    case south
    case west
    case east
}
print(CompassPoint.south.rawValue.uppercased())

```
