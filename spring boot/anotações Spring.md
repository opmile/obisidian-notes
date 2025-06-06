[[java]]
Excelente, Milena. Agora você foi direto no núcleo atômico do Spring. Vamos desenrolar esse **rolê das anotações, componentes e containers**, porque é ESSENCIAL entender isso pra dominar Spring com segurança.

---

## 🌱 Primeiro: Qual é a do Spring?

Spring é um **framework de Inversão de Controle (IoC)** e **Injeção de Dependência (DI)**.  
Ou seja: ele **toma conta da criação e ligação dos objetos** por você.

Pra isso funcionar, ele precisa de três coisas:

1. **Componentes** (os objetos que você quer que ele gerencie)
    
2. **Anotações** (pra dizer quem é quem)
    
3. **Container** (a "caixa mágica" onde o Spring guarda e organiza tudo)
    

---

## 🏷️ ANOTAÇÕES: o que são e por que importam?

Anotações (aquelas com `@`) são a forma que o Spring usa pra **entender a intenção do seu código**.  
Tipo um **mapa de instruções** pra ele saber:

- “Esse aqui é um serviço!”
    
- “Esse precisa ser instanciado automaticamente!”
    
- “Esse método aqui produz um bean!”
    

---

### 🎯 As principais anotações iniciais:

|Anotação|O que faz|
|---|---|
|`@Component`|Diz: "Essa classe é um bean do Spring, crie e gerencie pra mim"|
|`@Service`|Igual ao `@Component`, mas semanticamente diz: "Essa classe é de lógica de negócio"|
|`@Repository`|Outro `@Component`, mas usado pra classes que acessam o banco|
|`@Controller` / `@RestController`|Classes que lidam com requisições web (MVC ou API REST)|
|`@Autowired`|Injeta automaticamente outro bean|
|`@Bean`|Diz: “Esse método devolve um objeto que você deve registrar no container”|
|`@Configuration`|Marca uma classe que contém métodos com `@Bean`|
|`@SpringBootApplication`|Junta tudo: `@Configuration`, `@ComponentScan`, e `@EnableAutoConfiguration`|

---

### Exemplo rápido:

```java
@Service
public class UsuarioService {
    public void cadastrar() {
        System.out.println("Usuário cadastrado!");
    }
}
```

```java
@Component
public class StartupRunner implements CommandLineRunner {

    private final UsuarioService usuarioService;

    public StartupRunner(UsuarioService usuarioService) {
        this.usuarioService = usuarioService;
    }

    @Override
    public void run(String... args) {
        usuarioService.cadastrar();
    }
}
```

➡️ Aqui, você **não instanciou nada com `new`**. O Spring fez isso e injetou.

---

## 📦 O que é o "container"?

Pensa assim:

> O **container** do Spring é tipo uma mochila invisível onde ele guarda todos os objetos (beans) que você anotou.

- Ele **cria, gerencia, injeta, destrói** esses beans quando necessário.
    
- Ele é iniciado quando você roda o `SpringApplication.run()`.
    

---

## 💡 Por que tudo isso?

Imagine que você precisa usar várias classes conectadas entre si.  
**Sem o Spring**, você faria isso assim:

```java
UsuarioService service = new UsuarioService();
```

Mas isso acopla demais seu código e te impede de:

- Testar fácil
    
- Reutilizar lógica
    
- Trocar implementações
    

**Com Spring**, você faz assim:

```java
@Autowired
UsuarioService service;
```

E o Spring injeta automaticamente a implementação correta, já configurada.

---

## ⚙️ A tal da _Inversão de Controle_

Esse é o coração do Spring. Antes:

```java
ClasseA chama ClasseB → você controla tudo
```

Com Spring:

```java
Spring monta tudo pra você → e entrega quando você precisa
```

Essa inversão é o que permite o Spring fazer mágica com:

- Testes
    
- Escalabilidade
    
- Substituição de implementações
    
- Reuso de código
    

---

## ✅ Resumão no estilo bullet:

- O Spring gerencia **beans** (objetos anotados).
    
- Ele usa anotações (`@Service`, `@Component`, etc) pra saber o que criar.
    
- Ele guarda tudo no **container** (a mochila mágica).
    
- Ele **injeta** os objetos onde forem necessários.
    
- Você economiza tempo, reduz acoplamento e escreve código limpo.
    

---

Se quiser, posso te montar um mini projetinho 100% em linha de comando só com `@Component`, `@Service`, `@Autowired` e nada de web, pra treinar esse lance de container e injeção. Que tal?