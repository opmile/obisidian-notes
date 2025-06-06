[[java]]

Claro, Milena! Vamos descomplicar **expressões lambda** e **streams**, que são dois recursos modernos, muito usados em **Java** para deixar o código mais limpo, conciso e expressivo — principalmente quando você começa a trabalhar com coleções (listas, conjuntos, etc.).

---

## 🧠 1. **Expressões Lambda** — O que são?

Lambda é uma **função anônima**, ou seja, **sem nome**. Ela serve para representar **blocos de código que podem ser passados como parâmetros** ou atribuídos a variáveis.

> É uma forma curta de escrever uma implementação de uma interface funcional.

### 📌 O que é uma _interface funcional_?

É uma interface com **apenas um método abstrato**. Exemplos:

- `Runnable` (tem o método `run()`)
    
- `Comparator<T>` (tem o método `compare(T o1, T o2)`)
    
- `Consumer<T>` (tem o método `accept(T t)`)
    
- `Function<T, R>` (tem o método `apply(T t)`)
    

---

### 🧪 Sintaxe básica da Lambda:

```java
(parâmetros) -> { corpo da função }
```

### 🔍 Exemplo prático:

```java
// Sem lambda
List<String> nomes = Arrays.asList("Ana", "Beatriz", "Carlos");
Collections.sort(nomes, new Comparator<String>() {
    public int compare(String s1, String s2) {
        return s1.compareTo(s2);
    }
});
```

Com lambda, muito mais limpo:

```java
List<String> nomes = Arrays.asList("Ana", "Beatriz", "Carlos");
Collections.sort(nomes, (s1, s2) -> s1.compareTo(s2));
```

Ou ainda mais enxuto (já que `compareTo` é um método direto da String):

```java
Collections.sort(nomes, String::compareTo);
```

---

## 🌊 2. **Streams** — O que são?

`Stream` é uma **forma funcional** de **processar coleções de dados** em etapas (pipeline), usando operações como `filter`, `map`, `reduce`, `sorted`, entre outras.

Pensa como um **fluxo de dados**, onde cada passo transforma ou filtra os dados.

---

### 🔁 Exemplo clássico (sem stream):

```java
List<String> nomes = Arrays.asList("Ana", "Beatriz", "Carlos");
List<String> nomesFiltrados = new ArrayList<>();

for (String nome : nomes) {
    if (nome.startsWith("B")) {
        nomesFiltrados.add(nome.toUpperCase());
    }
}
```

### ✅ Com Stream + Lambda:

```java
List<String> nomes = Arrays.asList("Ana", "Beatriz", "Carlos");

List<String> resultado = nomes.stream()
    .filter(n -> n.startsWith("B"))        // Filtra nomes que começam com B
    .map(String::toUpperCase)              // Converte para maiúsculo
    .collect(Collectors.toList());         // Junta tudo em uma nova lista
```

---

## 🛠️ Principais Operações de Stream

|Método|Descrição breve|Tipo|
|---|---|---|
|`filter()`|Filtra elementos com base em uma condição|intermediária|
|`map()`|Transforma os elementos|intermediária|
|`forEach()`|Executa uma ação para cada elemento|terminal|
|`collect()`|Junta os dados num formato (lista, set etc)|terminal|
|`sorted()`|Ordena os elementos|intermediária|
|`count()`|Conta os elementos|terminal|
|`distinct()`|Remove duplicados|intermediária|

---

### 💥 Exemplo completo com tudo:

```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);

List<Integer> paresAoQuadrado = numeros.stream()
    .filter(n -> n % 2 == 0)         // pega só os pares
    .map(n -> n * n)                 // eleva ao quadrado
    .collect(Collectors.toList());  // transforma em lista
```

Resultado: `[4, 16, 36]`

---

## 🔄 Diferença entre `map` e `filter`:

|`filter()`|`map()`|
|---|---|
|**Remove** elementos com base em uma regra|**Transforma** cada elemento|
|Retorna menos ou igual elementos|Retorna mesma quantidade de elementos|

---

## 🧩 Streams são **imutáveis**

Ou seja, a lista original **não é alterada**:

```java
List<String> nomes = Arrays.asList("Ana", "Beatriz", "Carlos");

nomes.stream()
    .map(String::toUpperCase)
    .forEach(System.out::println); // só imprime, não muda a lista

System.out.println(nomes); // Lista original permanece a mesma
```

---

## ⚠️ Dicas finais

- Streams **não são coleções**: são uma forma de **percorrer e processar** coleções.
    
- Usar `parallelStream()` ativa o processamento paralelo (mas use com cuidado).
    
- Streams podem ser usados uma única vez.
    
- As operações **intermediárias** (como `map`, `filter`) são preguiçosas — só são executadas quando uma operação **terminal** (como `collect`, `forEach`, `count`) é chamada.
    

---

Se quiser, posso te passar uma **lista de exercícios** com gabarito sobre lambda e stream, ou montar um mini-projetinho com esses conceitos. Quer?