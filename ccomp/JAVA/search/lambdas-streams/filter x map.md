[[java]]

Perfeito, Milena. Vamos destrinchar as **diferenças entre `map()` e `filter()`** com calma e sem enrolação — os dois são métodos usados em **streams**, mas fazem **coisas completamente diferentes**.

---

## 🔍 Diferença conceitual

|Característica|`filter()`|`map()`|
|---|---|---|
|Objetivo|**Selecionar** elementos|**Transformar** elementos|
|Tipo de retorno|Stream com **menos ou igual** elementos|Stream com **mesmo número** de elementos|
|Entrada|Predicado (retorna `true` ou `false`)|Função que transforma um valor em outro|
|Quando usar|Quando quer **remover** com base numa condição|Quando quer **mudar os dados**, mantendo a estrutura|

---

## 📌 Exemplos práticos com uma lista de strings:

```java
List<String> nomes = Arrays.asList("Ana", "Bruno", "Beatriz", "Carlos");
```

---

### 🧪 Usando `filter()`: **filtra elementos com base numa condição**

```java
List<String> comB = nomes.stream()
    .filter(nome -> nome.startsWith("B"))
    .collect(Collectors.toList());
```

🧾 Resultado: `[Bruno, Beatriz]`

> O `filter()` **excluiu** os nomes que não começam com "B".

---

### 🧪 Usando `map()`: **transforma elementos**

```java
List<String> maiusculos = nomes.stream()
    .map(nome -> nome.toUpperCase())
    .collect(Collectors.toList());
```

🧾 Resultado: `[ANA, BRUNO, BEATRIZ, CARLOS]`

> O `map()` **manteve todos os elementos**, mas **transformou cada um** para letras maiúsculas.

---

## 🧠 Visual comparativo com emojis

Imagina uma lista:

```java
["🍎", "🍌", "🍇", "🍌"]
```

### `filter(fruta -> fruta.equals("🍌"))`

👉 Seleciona só o que você quer:

```
Entrada:    ["🍎", "🍌", "🍇", "🍌"]
Resultado:         ["🍌",      "🍌"]
```

---

### `map(fruta -> "🍹")`

👉 Transforma tudo numa vitamina:

```
Entrada:    ["🍎", "🍌", "🍇", "🍌"]
Resultado:  ["🍹", "🍹", "🍹", "🍹"]
```

---

## 🧪 Exemplo com `Integer`:

```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);
```

### `filter` → pega só pares:

```java
numeros.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList()); // [2, 4, 6]
```

### `map` → dobra todos:

```java
numeros.stream()
    .map(n -> n * 2)
    .collect(Collectors.toList()); // [2, 4, 6, 8, 10, 12]
```

---

## ✨ Pode combinar os dois!

Sim, e fica superpoderoso:

```java
List<Integer> dobradosPares = numeros.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * 2)
    .collect(Collectors.toList());
```

🧾 Resultado: `[4, 8, 12]`  
(pegou os pares `2, 4, 6` e dobrou)

---

## 🔚 Resumão de bolso:

|Método|Seleciona?|Transforma?|Altera quantidade de elementos?|
|---|---|---|---|
|`filter`|✅|❌|Sim (pode reduzir)|
|`map`|❌|✅|Não (mantém a quantidade)|

---

Se quiser, posso te passar uma lista de exercícios onde você **tem que escolher qual usar (`map` ou `filter`)** pra reforçar bem essa diferença! Quer?