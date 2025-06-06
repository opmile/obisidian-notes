[[java]]
**Reflection** em Java é um recurso da linguagem que permite **inspecionar e manipular objetos, classes, métodos e campos em tempo de execução**, mesmo que você não conheça a estrutura desses elementos em tempo de compilação.

### 🤓 Em termos simples:

Com Reflection, você pode acessar coisas "privadas", criar objetos, chamar métodos, e modificar atributos **sem saber exatamente o que está por trás** — desde que tenha o nome certo e permissões adequadas.

---

### 📦 O que dá pra fazer com Reflection?

- Descobrir informações de uma classe (nome, métodos, atributos, construtores).
    
- Instanciar objetos mesmo sem usar `new`.
    
- Acessar métodos e atributos privados.
    
- Chamar métodos dinamicamente.
    
- Criar ferramentas como **ORMs**, **frameworks de injeção de dependência**, **testes automatizados**, etc.
    

---

### 🧠 Exemplo prático

```java
import java.lang.reflect.Method;

public class Teste {
    private void mensagem() {
        System.out.println("Olá, Reflection!");
    }

    public static void main(String[] args) throws Exception {
        Teste t = new Teste();

        // Pegando a classe
        Class<?> classe = t.getClass();

        // Acessando o método privado
        Method metodo = classe.getDeclaredMethod("mensagem");

        // Tornando ele acessível
        metodo.setAccessible(true);

        // Executando o método
        metodo.invoke(t);
    }
}
```

#### 🧨 Saída:

```
Olá, Reflection!
```

---

### ⚠️ Cuidados

- **Performance**: Reflection é mais lento, pois ignora otimizações feitas pelo compilador.
    
- **Segurança**: Pode quebrar encapsulamento (acessar `private`), o que pode gerar falhas ou vulnerabilidades.
    
- **Manutenibilidade**: Código com Reflection pode ser difícil de entender e depurar.
    

---

### 🧰 Onde se usa Reflection no mundo real?

- **JUnit/TestNG**: Frameworks de testes usam Reflection pra descobrir e rodar testes.
    
- **Spring Framework**: Faz injeção de dependência e gerenciamento de beans com Reflection.
    
- **Hibernate**: Mapeia objetos para bancos de dados (ORM).
    
- **APIs de serialização**: Como Gson ou Jackson para JSON.
    

---

Se quiser, posso te mostrar como usar Reflection para criar instâncias de objetos, acessar atributos privados ou clonar objetos. Quer seguir por esse caminho?