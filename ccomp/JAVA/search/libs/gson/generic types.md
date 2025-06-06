[[java]]
Tipos genéricos em Java são uma forma de **escrever código que funciona com diferentes tipos de dados**, mantendo **segurança de tipo** (type safety) e evitando **casts desnecessários**. Eles foram introduzidos no Java 5 com o objetivo de tornar as estruturas de dados mais reutilizáveis e robustas.

---

### 📦 Exemplo simples de tipo genérico

Sem genéricos (antes do Java 5):

```java
List lista = new ArrayList();
lista.add("texto");

String s = (String) lista.get(0);  // Precisa de cast manual
```

Com genéricos:

```java
List<String> lista = new ArrayList<>();
lista.add("texto");

String s = lista.get(0);  // Sem cast, mais seguro
```

---

### 🧠 Mas o que é um tipo genérico de verdade?

Quando você vê algo como `<T>`, esse `T` é um **parâmetro de tipo genérico** — como uma variável, mas que representa um tipo.

Exemplo de classe genérica:

```java
public class Caixa<T> {
    private T valor;

    public void guardar(T valor) {
        this.valor = valor;
    }

    public T abrir() {
        return valor;
    }
}
```

Usando a classe:

```java
Caixa<String> caixaDeTexto = new Caixa<>();
caixaDeTexto.guardar("Olá mundo!");
System.out.println(caixaDeTexto.abrir());  // Saída: Olá mundo!

Caixa<Integer> caixaDeNumero = new Caixa<>();
caixaDeNumero.guardar(42);
System.out.println(caixaDeNumero.abrir());  // Saída: 42
```

---

### ✅ Vantagens dos tipos genéricos

1. **Reutilização de código**: uma mesma classe funciona com qualquer tipo.
    
2. **Segurança de tipo**: erros de tipo são detectados em tempo de compilação.
    
3. **Elimina cast**: o compilador já sabe o tipo.
    

---

### 🔤 Nomes comuns usados como parâmetros de tipo

- `T` – Type (tipo qualquer)
    
- `E` – Element (usado em coleções)
    
- `K` – Key
    
- `V` – Value
    
- `N` – Number
    

Você pode usar qualquer nome, mas esses são os padrões de mercado.

---

### 🚀 Dica de ouro

Se você for estudar mais a fundo Java e trabalhar com frameworks como Spring, Hibernate ou qualquer API de coleções, vai lidar com **genéricos o tempo todo**. Então vale muito a pena dominar isso cedo!

Se quiser, posso te passar exercícios ou montar exemplos mais avançados com genéricos, tipo usando `Map<K, V>` ou métodos genéricos. Quer seguir nessa?