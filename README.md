
# SOBRE

Compilação de classe java.

___

Criamos o diretório de _output_.

```shell
mkdir class
```

Neste exemplo o diretório _class_ já existe. 
Quando for executar o exemplo o conteúdo do diretório _class_ pode ser apagado para a criação de novos arquivos _class_.
Mesmo que os arquivos existam, eles serão substituídos.




Executamos o comando _javac_ passando o caminho até a classe _(src/org/naka/somePackage/SomeClass.java)_ e o diretório de saída _(-d class)_

```shell 
javac -d class src/org/naka/somePackage/SomeClass.java
```

Podemos ver que foi criado o arquivo _class_ na mesma estrutura do arquivo _java_

```shell
class
└── org
    └── naka
        └── somePackage
            └── SomeClass.class
```
            
Para compilar a classe que depende de SomeClass precisamos passar o caminho do diretório onde ela se encontra

```shell
javac -d class -cp class/org/naka/somePackage/ src/org/naka/sample/Teste.java
import org.naka.somePackage.SomeClass;
                           ^
src/org/naka/sample/Teste.java:9: error: cannot find symbol
                new SomeClass(";)");
                    ^
  symbol:   class SomeClass
  location: class Teste
2 errors
```

Não funciona. No classpath estamos dizendo que o diretório a ser considerado deve ser apenas o _somePackage_, sendo que no import feito, o path é:

```java
import org.naka.somePackage.SomeClass;
```

Sendo assim, precisamos apenas definir o diretório _class_ no _classpath_ para podermos respeitar o _path_ informado na classe _Teste.java_.

Passando apenas o diretório _class_ no _classpath_ a navegação pode ser feita a partir do diretório  _class_ e não a partir de _somePackage_ como haviamos configurado antes.

```shell
javac -d class -cp class src/org/naka/sample/Teste.java
```

Resultado:

```shell
class
└── org
    └── naka
        ├── sample
        │   └── Teste.class
        └── somePackage
            └── SomeClass.class
```


Para executarmos a classe, também precisamos definir o _classpath_ para o java saber onde deve procurar as classes que são importadas.

```shell
java -cp class org.naka.sample.Teste
Hello World //saída da classe Teste.java
I'm some class! ;) //saída da classe SomeClass.java
```

Se não definirmos o _classpath_. teremos a seguinte saída:

```shell
java org.naka.sample.Teste 
Error: Could not find or load main class org.naka.sample.Teste
```

