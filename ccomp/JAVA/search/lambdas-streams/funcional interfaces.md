[[java]]
Excelente pergunta, Milena! Saber as **interfaces funcionais mais usadas** é essencial pra dominar **lambda expressions**, `streams`, e toda a vibe funcional no Java moderno.

Vamos explorar as **principais interfaces funcionais** do pacote `java.util.function` que você mais vai ver **na prática**, com explicações e exemplos diretos ao ponto.

---

## 🧠 O que é uma interface funcional?

Uma **interface funcional** é aquela que tem **apenas um método abstrato**. Isso permite que ela seja usada em **lambdas** e **referências de métodos**.

> Todas do pacote `java.util.function` foram feitas pra esse propósito.

---

## 🧩 As 6 mais comuns (+ bônus)

---

### 1. **Consumer**

- **Faz algo com um valor, mas não retorna nada**
    
- Método: `void accept(T t)`
    

```java
Consumer<String> imprime = System.out::println;
imprime.accept("Oi, Milena!");
```

---

### 2. **Function<T, R>**

- **Transforma um valor** de tipo `T` em outro valor de tipo `R`
    
- Método: `R apply(T t)`
    

```java
Function<String, Integer> tamanho = s -> s.length();
System.out.println(tamanho.apply("banana")); // 6
```

---

### 3. **Predicate**

- **Testa uma condição lógica** e retorna `true` ou `false`
    
- Método: `boolean test(T t)`
    

```java
Predicate<String> comecaComM = s -> s.startsWith("M");
System.out.println(comecaComM.test("Milena")); // true
```

Usado direto em `.filter()` nos streams!

---

### 4. **Supplier**

- **Fornece um valor**, sem precisar de entrada
    
- Método: `T get()`
    

```java
Supplier<Double> aleatorio = () -> Math.random();
System.out.println(aleatorio.get()); // número aleatório entre 0 e 1
```

---

### 5. **UnaryOperator**

- É uma **Function<T, T>** (mesmo tipo de entrada e saída)
    
- Método: `T apply(T t)`
    

```java
UnaryOperator<String> paraMaiusculo = s -> s.toUpperCase();
System.out.println(paraMaiusculo.apply("java")); // JAVA
```

Usado em `.map()` quando não muda o tipo da stream.

---

### 6. **BinaryOperator**

- Recebe **dois argumentos do mesmo tipo** e retorna um do mesmo tipo
    
- Método: `T apply(T t1, T t2)`
    

```java
BinaryOperator<Integer> soma = (a, b) -> a + b;
System.out.println(soma.apply(3, 4)); // 7
```

Ideal para `.reduce()` no Stream API!

---

## 🧃 BÔNUS: Versões especializadas para tipos primitivos

Evita **autoboxing** (ganha performance):

- `IntConsumer`, `IntPredicate`, `IntFunction`, `IntSupplier`
    
- `DoubleFunction`, `LongFunction`, etc.
    

Exemplo:

```java
IntPredicate par = n -> n % 2 == 0;
System.out.println(par.test(4)); // true
```

---

## 📌 Tabela resumo rápida

|Interface|O que faz|Método|Exemplo|
|---|---|---|---|
|`Consumer<T>`|Executa uma ação com T|`accept(T t)`|`System.out::println`|
|`Function<T, R>`|Transforma T em R|`apply(T t)`|`s -> s.length()`|
|`Predicate<T>`|Retorna `true/false`|`test(T t)`|`s -> s.isEmpty()`|
|`Supplier<T>`|Gera valor sem entrada|`get()`|`() -> Math.random()`|
|`UnaryOperator<T>`|Transforma T em T|`apply(T t)`|`s -> s.toUpperCase()`|
|`BinaryOperator<T>`|Combina dois T em um|`apply(T t1, T t2)`|`(a, b) -> a + b`|

---

Se quiser, posso te montar uma lista de **exercícios temáticos**, tipo:  
➡ "Qual interface usar aqui?"  
➡ "Reescreva com lambda"  
➡ "Transforme lambda em referência de método"  
➡ "Use essas interfaces em streams com `map`, `filter`, `reduce`"

Só pedir!