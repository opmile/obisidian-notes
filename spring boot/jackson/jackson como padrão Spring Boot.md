[[java]]

Perfeito, Milena. Essa dúvida é muito comum pra quem começa com Java e precisa transformar objetos em JSON (e vice-versa). Vamos direto ao ponto: **Gson** vs. **Jackson**.

---

## 🤔 Antes de tudo: o que são Gson e Jackson?

Ambos são **bibliotecas de serialização e desserialização de objetos Java em JSON**:

- 🔁 _Serializar_ = transformar um objeto Java em JSON
    
- 🔁 _Desserializar_ = transformar um JSON em objeto Java
    

---

## ⚔️ Por que o Spring usa **Jackson** como padrão (e não Gson)?

### 🟢 **Jackson é o padrão no Spring Boot por alguns motivos MUITO fortes:**

|🔥 Vantagem de Jackson|✅ Explicação|
|---|---|
|**Integração total com Spring Boot**|O Spring Boot já vem com Jackson embutido. Ele é usado em REST Controllers, testes, etc, sem precisar configurar|
|**Mais rápido**|Jackson tem performance superior em benchmarks de serialização|
|**Suporte melhor a tipos complexos**|Lida melhor com listas genéricas, enums, datas, annotations etc|
|**Customização poderosa**|Jackson tem MUITAS opções via annotations (`@JsonProperty`, `@JsonIgnore`, `@JsonInclude`)|
|**Streaming API**|Tem suporte para manipulação de JSON em nível de stream (útil pra arquivos grandes)|
|**Mais maduro e completo**|É o mais usado em sistemas empresariais Java|

---

### 🔴 E o Gson?

Gson foi criado pelo Google e é **muito simples de usar**, mais "plug-and-play", mas...

|❌ Limitações do Gson|😬 Impacto|
|---|---|
|Pouca integração com Spring|Você tem que configurar tudo manualmente|
|Suporte limitado a tipos genéricos|Sofre com `List<MyClasse>` ou `Map<String, Object>`|
|Lida mal com data/hora|Precisa de custom serializers pra `LocalDate`, `ZonedDateTime`, etc|
|Performance inferior|Serialização mais lenta comparada ao Jackson|
|Menos opções de customização|Poucas anotações, menos controle sobre o JSON final|

---

## 🧪 Exemplo simples com Jackson

Imagine essa classe:

```java
public class Pessoa {
    private String nome;
    private int idade;

    // getters e setters
}
```

Serializando com Jackson:

```java
ObjectMapper mapper = new ObjectMapper();
Pessoa p = new Pessoa("Milena", 18);
String json = mapper.writeValueAsString(p);
```

Desserializando:

```java
Pessoa p2 = mapper.readValue(json, Pessoa.class);
```

✅ Fácil, rápido e já funciona com Spring REST sem esforço.

---

## 📦 No Spring Boot:

Se você tem um endpoint tipo:

```java
@RestController
public class PessoaController {

    @PostMapping("/pessoas")
    public Pessoa criarPessoa(@RequestBody Pessoa pessoa) {
        return pessoa;
    }
}
```

👉 O Spring já usa **Jackson por baixo dos panos** para:

- Desserializar o JSON do corpo da requisição em um objeto `Pessoa`
    
- Serializar o objeto `Pessoa` da resposta em JSON de volta
    

---

## 🔧 E se eu quisesse usar Gson?

Dá? Dá. Mas você teria que:

- Adicionar a dependência Gson no `pom.xml`
    
- Criar um `@Bean` de `GsonHttpMessageConverter`
    
- Desabilitar o `MappingJackson2HttpMessageConverter`
    

👉 Ou seja: muito mais trabalho pra algo que o Spring já faz **melhor** com Jackson.

---

## 🎯 Conclusão simples e direta:

> Use **Jackson** com Spring Boot. Ele é o padrão, mais rápido, mais poderoso e muito bem integrado.

Gson ainda é válido em projetos pequenos ou fora do ecossistema Spring (tipo Android), mas **pra aplicações backend com Java e Spring**, **Jackson é o rei.**

---

Se quiser, posso te mostrar um exemplo onde **Jackson brilha e o Gson tropeça**, como em listas genéricas ou serialização de datas. Quer ver isso na prática?