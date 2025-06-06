[[java]]
Boa, Milena! Agora que você deixou o Gson no passado (com razão), **bora aprender a usar o Jackson direito**, principalmente com **Spring Boot**, onde ele já é o **serializador padrão**. Te guio agora pelos **principais conceitos, anotações e práticas com exemplos**, como se você estivesse começando com Jackson **hoje**.

---

## 🔥 Primeira coisa: Jackson já vem no Spring Boot

Ou seja: **você não precisa importar nada**, a não ser que vá trabalhar com datas Java 8+ (`LocalDate`, `ZonedDateTime`, etc), onde pode usar:

```xml
<!-- Se precisar, adicione no pom.xml -->
<dependency>
    <groupId>com.fasterxml.jackson.datatype</groupId>
    <artifactId>jackson-datatype-jsr310</artifactId>
</dependency>
```

E registre no `ObjectMapper`:

```java
@Bean
public ObjectMapper objectMapper() {
    ObjectMapper mapper = new ObjectMapper();
    mapper.registerModule(new JavaTimeModule());
    mapper.disable(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS);
    return mapper;
}
```

---

## ✅ Estrutura base

```java
@RestController
public class UsuarioController {

    @GetMapping("/usuario")
    public Usuario getUsuario() {
        return new Usuario("Milena", 18);
    }
}
```

```java
public class Usuario {
    private String nome;
    private int idade;

    // Getters e setters obrigatórios!
}
```

Quando você acessar `/usuario`, o Spring Boot vai usar **Jackson** para converter o objeto em JSON automaticamente.

---

## 🎯 Anotações MAIS IMPORTANTES

### 📌 `@JsonProperty`

Renomeia o campo no JSON sem mudar o nome da variável:

```java
public class Usuario {
    @JsonProperty("nome_completo")
    private String nome;
}
```

JSON de saída:

```json
{ "nome_completo": "Milena" }
```

---

### 📌 `@JsonIgnore`

Ignora o campo na serialização/desserialização:

```java
@JsonIgnore
private String senha;
```

---

### 📌 `@JsonInclude`

Controla o que aparece no JSON:

```java
@JsonInclude(JsonInclude.Include.NON_NULL)
private String apelido;
```

➡️ Esse campo **só será incluído** se **não for `null`**.

---

### 📌 `@JsonFormat`

Formata datas ou números:

```java
@JsonFormat(pattern = "dd/MM/yyyy")
private LocalDate nascimento;
```

---

### 📌 `@JsonCreator` + `@JsonProperty`

Construtores imutáveis? Use isso para desserializar:

```java
public class Usuario {
    private final String nome;
    private final int idade;

    @JsonCreator
    public Usuario(@JsonProperty("nome") String nome,
                   @JsonProperty("idade") int idade) {
        this.nome = nome;
        this.idade = idade;
    }
}
```

---

### 📌 `@JsonAlias`

Aceita múltiplos nomes para um mesmo campo **na entrada**:

```java
@JsonAlias({ "nomeCompleto", "nome_usuario" })
private String nome;
```

---

### 📌 `@JsonAnyGetter` e `@JsonAnySetter`

Útil quando você tem **chaves dinâmicas**:

```java
private Map<String, Object> propriedadesExtras = new HashMap<>();

@JsonAnySetter
public void addExtra(String chave, Object valor) {
    propriedadesExtras.put(chave, valor);
}
```

---

### 📌 `@JsonTypeInfo` (💡 para herança)

```java
@JsonTypeInfo(use = JsonTypeInfo.Id.CLASS, include = JsonTypeInfo.As.PROPERTY, property = "@type")
public class Animal { ... }
```

Assim o JSON terá algo como:

```json
{ "@type": "com.exemplo.Cachorro", "nome": "Toby" }
```

---

## 🤯 Dica bônus: Mix-ins (caso você não possa modificar a classe original)

```java
public abstract class UsuarioMixin {
    @JsonProperty("nome_completo")
    abstract String getNome();
}
```

```java
mapper.addMixIn(Usuario.class, UsuarioMixin.class);
```

---

## 🧪 Quer testar tudo isso?

No seu projeto Spring Boot, crie endpoints REST simples que retornem objetos anotados com essas anotações, tipo:

```java
@GetMapping("/exemplo")
public Pessoa getPessoa() {
    return new Pessoa("Milena", null, LocalDate.now());
}
```

E varie os cenários com:

- Campos nulos
    
- Datas
    
- Herança
    
- Mapas dinâmicos
    

---

## 🔚 Conclusão prática

|O que você quer|Anotação Jackson|
|---|---|
|Renomear campo|`@JsonProperty`|
|Ignorar campo|`@JsonIgnore`|
|Mostrar só se não for nulo|`@JsonInclude`|
|Formatar datas|`@JsonFormat`|
|Lidar com construtores|`@JsonCreator` + `@JsonProperty`|
|Herança funcional|`@JsonTypeInfo`|
|Receber vários nomes no input|`@JsonAlias`|
|Serializar mapas com chave dinâmica|`@JsonAnyGetter` / `@JsonAnySetter`|

---

Se quiser, eu posso montar um repositório mínimo no estilo “**Jackson para quem vinha do Gson**”, com cada exemplo desses como um endpoint REST. Quer isso?