[[java]]

Ótima pergunta, Milena! Essa dúvida é comum, mas super importante pra entender bem o que está rolando por trás dos bastidores com lambdas e streams. Bora quebrar tudo com clareza. 👇

---

## 💡 O que é a interface `Consumer<T>`?

A `Consumer<T>` é uma **interface funcional** do pacote `java.util.function`, e ela representa **uma operação que aceita um único argumento e não retorna resultado**.

👉 Em outras palavras:

- **Ela consome um valor** (do tipo `T`)
    
- **Faz algo com ele** (tipo imprimir, gravar, enviar etc.)
    
- **Mas não retorna nada** (`void`)
    

---

## 📦 Estrutura da interface

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```

Ou seja, qualquer função que **receba um argumento do tipo `T` e retorne void** pode ser representada por um `Consumer<T>`.

---

## ✅ Exemplo básico

```java
Consumer<String> printer = s -> System.out.println(s);
printer.accept("Olá, mundo!");
```

Aqui:

- Criamos um `Consumer<String>` chamado `printer`
    
- Ele **consome uma string** (`s`) e faz `System.out.println(s)`
    
- Quando usamos `printer.accept("Olá, mundo!")`, ele imprime a string
    

---

## ✅ Usando **referência de método**

Agora que sabemos que `System.out::println` é um método que **recebe uma String e imprime**, podemos usar isso direto como `Consumer<String>`:

```java
Consumer<String> printer = System.out::println;
printer.accept("Oi, Milena!");
```

O `System.out::println` bate perfeitamente com o método `accept(T)` da interface `Consumer<String>` — pois ele **aceita uma `String` e retorna void**.

---

## 🌀 Onde o `Consumer<T>` é muito usado?

1. **No `forEach()` de streams**:
    

```java
List<String> nomes = List.of("Ana", "Bia", "Caio");

nomes.forEach(System.out::println); // Isso é um Consumer<String>
```

2. **Em APIs funcionais**, onde você quer executar algo com cada item de uma lista.
    
3. **Com métodos utilitários que querem aplicar uma ação a um elemento.**
    

---

## 🎯 Outros exemplos de `Consumer<T>`

```java
Consumer<Integer> duplicador = n -> System.out.println(n * 2);
duplicador.accept(10); // imprime 20

Consumer<String> exclamador = texto -> System.out.println(texto + "!");
exclamador.accept("Java"); // imprime "Java!"
```

---

## 📌 Consumer com lista e `forEach`

```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4);

numeros.forEach(n -> System.out.println(n * 3)); // Consumer<Integer>
```

Ou com referência de método:

```java
numeros.forEach(System.out::println); // também é um Consumer<Integer>
```

---

## 🧠 Resumo final

|Conceito|O que é|
|---|---|
|`Consumer<T>`|Interface funcional que **recebe um valor** e **executa uma ação**, sem retornar nada.|
|Método principal|`void accept(T t)`|
|Exemplo comum|`forEach(System.out::println)`|
|Ideal para|Imprimir, salvar, notificar, aplicar lógica de forma declarativa.|

---

Se quiser, posso montar um mini "joguinho" onde você combina tipos com interfaces funcionais como `Function`, `Predicate`, `Consumer`, `Supplier` etc. Topa?