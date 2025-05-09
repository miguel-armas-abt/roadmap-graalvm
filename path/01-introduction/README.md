# GRAALVM

[← Regresar a notas](../../README.md) <br>

---

GraalVM es una máquina virtual políglota de alto rendimiento y certificada como un JDK.

## GraalVM como plataforma políglota
Así como la JVM es una plataforma políglota, GraalVM expande su compatibilidad con diferentes 
lenguajes de programación.

- **Lenguajes de la JVM** (como Scala, Kotlin, Rubby, etc) que se compilan en bytecode.
- **Lenguajes que utilicen AST** (como JavaScript, NodeJS, Python, etc) pueden ser interpretados por una implementación de `Truffle`.
- **Lenguajes nativos** (como C, C++, Rust, etc) pueden ser interpretados por `LLVM`.

![GraalVM](resources/polyglot.png)

## Imagen nativa

> #### 🔎 Diccionario
> 1. `Compilación ahead-of-time (AOT)`: Técnica en la que se compila un lenguaje de programación a un código de máquina nativo antes de la ejecución del programa, dando como resultado un archivo binario.
> 2. `Static linking`: Técnica que consiste en añadirle a un ejecutable nativo todas sus dependencias y empaquetarlo en un nuevo ejecutable. Por ejemplo, en Windows los ejecutables dependen de bibliotecas dll instaladas en el SO. Cuando las bibliotecas están separadas del ejecutable hablamos de un `dinamic linking`, mientras que cuando están dentro del mismo ejecutable se trata de un static linking.

GraalVM es una tecnología de `compilación AOT` que permite crear un ejecutable mediante `static linking`, el cual incluye 
clases, bibliotecas y los módulos necesarios del JDK para abordar el thread scheduling y el garbage collection mediante la `SubstrateVM`.

![GraalVM](resources/native-image.png)

---

## Importancia

### Cloud native
Las principales ventajas de la GraalVM surgen apartir del uso de las imágenes nativas en un ecosistema cloud native, ya
que en este tipo de entornos elásticos es importante la <u>rapidez en que se aprovisionan y eliminan copias de la aplicación</u>.  

Se ha comprobado que la GraalVM en aplicaciones con imágenes nativas <u>el tiempo de arranque mejora hasta cincuenta veces</u>. 
Así mismo <u>el uso de la memoria reduce hasta cinco veces</u>, ya que bajo este enfoque se quita la compilación JIT en tiempo de ejecución.

Algunos de los frameworks modernos permiten una integración con GraalVM. Por ejemplo Helidon, Quarkus, Micronaut y Spring.

### Desarrollo local
El compilador JIT de GraalVM ha demostrado un gran desempeño como reemplazo del compilador JIT de la JVM. 

Es común utilizar compilación JIT durante el desarrollo local, ya que permite optimizaciones en tiempo de ejecución:

```shell
java -jar my-application.jar
```

También es posible usar compilación AOT localmente para probar el comportamiento de la aplicación en su forma nativa:

```shell
native-image -jar my-application.jar
./my-application
```