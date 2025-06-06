[[java]]

Boa pergunta, Milena! Quando eu digo que **streams são imutáveis**, estou dizendo o seguinte:

> ⚠️ **Eles não modificam os dados da coleção original.**

---

### 📦 Imutabilidade na prática

Digamos que você tenha uma lista de números:

```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);
```

Agora você usa um stream para **dobrar** esses números:

```java
numeros.stream()
    .map(n -> n * 2)
    .forEach(System.out::println); // Vai imprimir 2 4 6 8 10
```

👉 Mas se você imprimir a lista original depois:

```java
System.out.println(numeros); // Vai mostrar [1, 2, 3, 4, 5]
```

💥 O `stream()` **cria um fluxo de dados separado**, **trabalha sobre ele**, e **não altera a lista original**.

---

### 🧠 Por que isso é bom?

1. ✅ **Evita efeitos colaterais:** você sabe que sua lista original continua intacta.
    
2. ✅ **Facilita o paralelismo:** o Java pode otimizar e paralelizar operações com mais segurança.
    
3. ✅ **Mais previsível:** ao evitar que funções alterem o estado dos dados, o código fica mais fácil de entender e testar.
    

---

### 🛠 E se eu quiser modificar?

Aí você precisa **criar uma nova lista**, coletando o resultado:

```java
List<Integer> dobrados = numeros.stream()
    .map(n -> n * 2)
    .collect(Collectors.toList());
```

Agora `dobrados` vai ter `[2, 4, 6, 8, 10]`, mas `numeros` continua `[1, 2, 3, 4, 5]`.

---

### 🧪 Contraexemplo (mutable):

Se você fizesse isso com um `for`, poderia modificar a lista diretamente:

```java
for (int i = 0; i < numeros.size(); i++) {
    numeros.set(i, numeros.get(i) * 2); // Modifica a lista original!
}
```

---

### ✨ Resumo: Streams são imutáveis porque:

- **Não modificam a fonte (a lista original).**
    
- Só transformam os dados dentro do fluxo.
    
- Se você quiser manter os resultados, precisa **armazená-los em uma nova estrutura**.
    

Quer que eu mostre isso rodando com prints pra deixar mais claro?