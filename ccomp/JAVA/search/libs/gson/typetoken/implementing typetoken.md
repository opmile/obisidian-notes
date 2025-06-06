[[java]]
Beleza! Vamos abrir essa “caixa-preta” e entender exatamente como essa mágica acontece. 🤯

---

## 🧠 O Conceito: Type Erasure e Classes Anônimas

### 🔹 Type Erasure (apagamento de tipo)

No Java, os **tipos genéricos são apagados** em tempo de compilação. Ou seja:

```java
List<String> lista = new ArrayList<>();
List<Integer> outraLista = new ArrayList<>();
```

Ambas são só `List` em tempo de execução. O Java não sabe mais que era `List<String>` ou `List<Integer>`.

---

## 🔎 O Truque da `TypeToken`

A `TypeToken` (como a da Gson) funciona porque **ela consegue capturar o tipo genérico passado na definição da classe anônima** — porque o Java ainda guarda isso na superclasse via reflexão.

---

### 👇 Exemplo real:

```java
Type type = new TypeToken<List<String>>() {}.getType();
```

Isso cria uma **classe anônima** que estende `TypeToken<List<String>>`.

Vamos ver como ela pode capturar o tipo real:

---

### 📂 Como a `TypeToken` funciona por dentro

```java
public class TypeToken<T> {
    private final Type type;

    protected TypeToken() {
        // Aqui ele acessa a superclasse direta (com o tipo ainda presente!)
        Type superclass = getClass().getGenericSuperclass();

        if (superclass instanceof ParameterizedType) {
            // Aqui ele extrai o tipo real: List<String>
            this.type = ((ParameterizedType) superclass).getActualTypeArguments()[0];
        } else {
            throw new RuntimeException("Missing type parameter.");
        }
    }

    public Type getType() {
        return this.type;
    }
}
```

---

### 🛠️ O que acontece no `getClass().getGenericSuperclass()`?

Vamos ilustrar:

```java
TypeToken<List<String>> token = new TypeToken<List<String>>() {};
```

Esse código cria algo parecido com:

```java
class Anonima extends TypeToken<List<String>> {}
```

A chamada `getClass().getGenericSuperclass()` feita dentro do construtor de `TypeToken` retorna:

```java
TypeToken<java.util.List<java.lang.String>>
```

Isso **ainda guarda o tipo `List<String>`**, mesmo com type erasure, porque está armazenado na **superclasse genérica da classe anônima**.

---

### 🧪 Teste simples (sem Gson):

```java
TypeToken<List<String>> token = new TypeToken<List<String>>() {};
System.out.println(token.getType());
```

Saída:

```
java.util.List<java.lang.String>
```

---

## 🧩 TL;DR: O Segredo

|Etapa|O que acontece|
|---|---|
|`new TypeToken<List<String>>() {}`|Cria uma classe anônima que estende `TypeToken<List<String>>`|
|`getClass().getGenericSuperclass()`|Acessa `TypeToken<List<String>>` com os tipos ainda presentes|
|`getActualTypeArguments()`|Extrai o tipo real `List<String>`|
|Resultado|Você tem o tipo genérico **preservado** em tempo de execução!|

---

Se quiser, posso te mostrar como criar uma `TypeToken` personalizada, ou até como fazer isso com múltiplos tipos genéricos (`Map<String, List<Integer>>`, por exemplo). Quer que a gente monte uma versão simplificada dessa classe?