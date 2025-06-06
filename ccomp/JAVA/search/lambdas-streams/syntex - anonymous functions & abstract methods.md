[[java]]

Excelente pergunta, Milena! Essa aqui é a base de tudo quando falamos de lambdas e programação funcional em Java moderno. Vamos por partes, direto ao ponto:

---

## ✅ Função anônima vs. método abstrato

### 📌 O que é um **método abstrato**?

- É um **método sem corpo**, definido numa **interface ou classe abstrata**.
    
- Ele **precisa ser implementado** por quem usar a interface/classe.
    

Exemplo:

```java
@FunctionalInterface
interface MinhaFuncao {
    void executar(); // método abstrato
}
```

---

### 📌 O que é uma **função anônima** (lambda)?

- É uma forma **compacta e sem nome** de implementar o método **de uma interface funcional**.
    
- Ela é **ligada automaticamente ao único método abstrato** dessa interface.
    

Exemplo:

```java
MinhaFuncao f = () -> System.out.println("Executando!");
f.executar(); // Executa a função anônima
```

➡ Aqui, a lambda `() -> System.out.println("Executando!")` **é uma função anônima que implementa o método `executar()` da interface**.

---

## 💡 RELAÇÃO DIRETA

> Uma **função anônima (lambda)** em Java **implementa** o **único método abstrato** de uma **interface funcional**.

O Java **usa o método abstrato como contrato** e associa a função anônima automaticamente.

---

### 📌 Exemplo mais técnico com `Consumer<T>`

```java
Consumer<String> consumidor = s -> System.out.println(s.toUpperCase());
```

Aqui:

- `Consumer<T>` é uma **interface funcional**
    
- O método abstrato dela é: `void accept(T t)`
    
- A função anônima `s -> System.out.println(s.toUpperCase())` implementa esse método
    

Então internamente é como se você tivesse escrito:

```java
Consumer<String> consumidor = new Consumer<>() {
    @Override
    public void accept(String s) {
        System.out.println(s.toUpperCase());
    }
};
```

Mesma lógica, menos código.

---

## 🎯 Por que isso é importante?

1. Toda **lambda** em Java **é uma implementação de um método abstrato** de uma **interface funcional**.
    
2. Por isso **não dá pra usar lambdas** com interfaces ou classes com **mais de um método abstrato**.
    
3. A lambda **"encaixa" perfeitamente** no método, se os tipos e a quantidade de argumentos baterem.
    

---

## 🧠 Resumo rápido

|Conceito|Explicação|
|---|---|
|Método abstrato|Método sem corpo que precisa ser implementado|
|Interface funcional|Interface com exatamente 1 método abstrato|
|Função anônima|Lambda que implementa esse único método abstrato|
|Relação|O corpo da função anônima **vira a implementação** do método abstrato da interface funcional|

---

Se quiser, posso te passar exercícios onde você **cria suas próprias interfaces funcionais** e depois escreve lambdas que se encaixam nelas. Isso ajuda MUITO a internalizar essa relação. É só pedir!