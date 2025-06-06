[[java]]
Ótimo! Vamos meter a mão no código e ver na **prática** onde o **Jackson reina** e o **Gson tropeça**.

---

## 🧪 Cenário 1: Lista Genérica (`List<Pessoa>`)

### 🔧 Modelo:

```java
public class Pessoa {
    private String nome;
    private int idade;

    // Construtores, Getters e Setters
}
```

Agora vamos supor que você tem um JSON assim:

```json
[
  { "nome": "Milena", "idade": 18 },
  { "nome": "João", "idade": 20 }
]
```

---

### ✅ Com **Jackson**:

```java
ObjectMapper mapper = new ObjectMapper();
List<Pessoa> pessoas = mapper.readValue(json, new TypeReference<List<Pessoa>>() {});
```

✅ Funciona liso! O `TypeReference` informa o tipo genérico completo — e o Jackson respeita.

---

### ❌ Com **Gson**:

```java
Gson gson = new Gson();
List<Pessoa> pessoas = gson.fromJson(json, new TypeToken<List<Pessoa>>() {}.getType());
```

🟡 Isso _parece_ funcionar, **mas dá problema** quando os objetos têm herança, tipos mais complexos, ou anotações específicas (como `@SerializedName`, etc). Gson tem problemas em refletir tipos genéricos com precisão, especialmente em estruturas mais complexas.

---

## 🧪 Cenário 2: Datas

Vamos adicionar uma data à sua `Pessoa`:

```java
private LocalDate nascimento;
```

Agora seu JSON virou:

```json
{ "nome": "Milena", "idade": 18, "nascimento": "2006-05-10" }
```

---

### ✅ Com **Jackson**:

```java
ObjectMapper mapper = new ObjectMapper();
mapper.registerModule(new JavaTimeModule());
mapper.disable(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS);

Pessoa pessoa = mapper.readValue(json, Pessoa.class);
```

✅ Suave! O Jackson, com `JavaTimeModule`, entende `LocalDate`, `ZonedDateTime`, etc., certinho.

---

### ❌ Com **Gson**:

```java
Gson gson = new Gson();
Pessoa pessoa = gson.fromJson(json, Pessoa.class);
```

💥 **Vai explodir** com erro de conversão, porque Gson **não entende `LocalDate` ou `LocalDateTime`** por padrão.

➡️ Você teria que escrever um **TypeAdapter** manual:

```java
Gson gson = new GsonBuilder()
    .registerTypeAdapter(LocalDate.class, new LocalDateAdapter())
    .create();
```

👎 Mais código, mais manutenção.

---

## 🔥 Moral da história

|Cenário|Jackson|Gson|
|---|---|---|
|Listas genéricas|✅|⚠️ pode falhar|
|Datas Java 8+|✅ com módulo|❌ exige TypeAdapter|
|Integração com Spring|✅ perfeito|❌ manual e chato|
|Anotações poderosas|✅ muitas opções|⚠️ limitado|

---

### Quer um mini-projeto Java pra rodar esses testes em tempo real?

Posso montar um `main` com todos esses exemplos e te passar o código pra colar e testar no seu projeto de linha de comando com Spring. Só dizer!

Boa, Milena. Bora provar isso com **exemplos reais e código na prática**, mostrando como o Gson tropeça em cenários com **herança** e **genéricos complexos**, enquanto o Jackson lida de boa.

---

## 💣 1. **HERANÇA** — O calcanhar de Aquiles do Gson

### 🧱 Classes:

```java
public class Animal {
    public String nome;
}

public class Cachorro extends Animal {
    public boolean late;
}
```

### 🧪 Lista de `Animal` com elementos `Cachorro`:

```java
List<Animal> animais = new ArrayList<>();
Cachorro dog = new Cachorro();
dog.nome = "Toby";
dog.late = true;
animais.add(dog);
```

---

### ❌ **GSON falha feio aqui:**

```java
Gson gson = new Gson();
String json = gson.toJson(animais);
System.out.println(json);

List<Animal> animaisDesserializados = gson.fromJson(json, new TypeToken<List<Animal>>() {}.getType());
```

### 🧨 Problema:

- O JSON até é gerado, mas **ao desserializar**, o Gson **perde completamente a informação do tipo concreto (`Cachorro`)**.
    
- O resultado é uma lista de `Animal` com **`late = false` (valor padrão)**, porque ele não sabe que era `Cachorro`.
    

---

### ✅ Com **Jackson**, isso funciona com uma linha:

```java
@JsonTypeInfo(use = JsonTypeInfo.Id.CLASS)
public class Animal {
    public String nome;
}

public class Cachorro extends Animal {
    public boolean late;
}
```

```java
ObjectMapper mapper = new ObjectMapper();
mapper.enableDefaultTyping(); // ou use anotações como acima

String json = mapper.writeValueAsString(animais);
List<Animal> animaisDesserializados = mapper.readValue(json, new TypeReference<List<Animal>>() {});
```

✅ O Jackson mantém a informação do tipo `Cachorro`, e tudo funciona como esperado.

---

## 💣 2. **GENÉRICOS COMPLEXOS** — Gson tropeça de novo

### 🧱 Classe genérica com aninhamento:

```java
public class Wrapper<T> {
    public T dado;
}

public class Pessoa {
    public String nome;
}
```

### JSON:

```json
{ "dado": { "nome": "Milena" } }
```

---

### ❌ Com Gson:

```java
String json = "{\"dado\":{\"nome\":\"Milena\"}}";

Wrapper<Pessoa> resultado = new Gson()
    .fromJson(json, new TypeToken<Wrapper<Pessoa>>(){}.getType());

System.out.println(resultado.dado.nome); // Esperado: "Milena"
```

💥 _Às vezes funciona_, mas com tipos mais complexos (listas aninhadas, mapas com objetos, enums...) **começa a dar pau**. O Gson **não lida bem com reflexão de tipos genéricos aninhados**, pois o Java perde parte das informações de tipo em tempo de execução.

---

### ✅ Com Jackson:

```java
ObjectMapper mapper = new ObjectMapper();
Wrapper<Pessoa> resultado = mapper.readValue(json, new TypeReference<Wrapper<Pessoa>>() {});
System.out.println(resultado.dado.nome); // "Milena"
```

✔️ Funciona perfeitamente. O Jackson interpreta o tipo genérico corretamente, mesmo com aninhamentos.

---

## 💣 3. **@SerializedName do Gson não se aplica no Jackson**

```java
public class Produto {
    @SerializedName("nome_do_produto") // <-- só funciona com Gson!
    public String nome;
}
```

Gson lê isso, mas se você tentar misturar isso com Jackson, **ele ignora completamente** essa anotação.

Jackson usa:

```java
public class Produto {
    @JsonProperty("nome_do_produto")
    public String nome;
}
```

---

## ✅ Conclusão

|Cenário|Gson|Jackson|
|---|---|---|
|Herança|❌ perde tipo concreto|✅ preserva tipo com `@JsonTypeInfo`|
|Genéricos complexos|❌ problemas de reflexão|✅ `TypeReference` resolve|
|Anotações|❌ só entende `@SerializedName`|✅ `@JsonProperty`, `@JsonIgnore`, etc|
|Compatível com Spring Boot|❌ não é padrão|✅ integração total|

---

Se quiser, posso montar um mini-projeto Maven só com esses testes pra você colar e rodar na IDE rapidinho. Quer que eu gere esse `main()` com todos os testes acima pra você testar sozinha?