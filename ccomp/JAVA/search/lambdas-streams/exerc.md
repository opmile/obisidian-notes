[[java]]

Perfeito, Milena! Bora reforçar tudo com uma **lista casca-grossa de exercícios sobre lambda expressions e streams**. Essa lista está organizada de forma progressiva e abrangente, cobrindo:

1. ✅ Sintaxe de lambda
    
2. 🔁 Uso de `filter`, `map`, `collect`, `forEach`, `sorted`, `distinct`, `reduce`, `anyMatch`, `allMatch`, etc.
    
3. 🧠 Exercícios combinados que exigem raciocínio e escrita fluente.
    

---

## 🧩 NÍVEL 1 — AQUECIMENTO (Lambdas básicas e stream simples)

1. Crie uma `List<Integer>` com os valores de 1 a 10 e:
    
    - Imprima todos com `forEach` usando lambda.
        
    - Filtre apenas os pares e imprima.
        
2. Com uma lista de nomes (`"Ana"`, `"Carlos"`, `"Pedro"`, `"João"`):
    
    - Use `map()` para colocar todos os nomes em maiúsculo.
        
    - Use `filter()` para pegar apenas os que têm mais de 4 letras.
        
    - Combine ambos: nomes com mais de 4 letras em maiúsculo.
        
3. Dada uma `List<String>` com nomes que se repetem:
    
    - Use `distinct()` para remover duplicatas.
        
    - Em seguida, ordene os nomes alfabeticamente.
        

---

## 🧠 NÍVEL 2 — TRANSFORMAÇÕES E FILTROS

4. Dada `List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);`:
    
    - Gere uma nova lista com os quadrados dos números ímpares.
        
    - Filtre os múltiplos de 3 e retorne uma lista com os cubos desses números.
        
5. Dada uma `List<String>` de palavras:
    
    - Converta todas para minúsculo e filtre as que **contêm a letra "a"**.
        
    - Depois, pegue a **primeira palavra**, em ordem alfabética, que atende ao filtro.
        
6. Crie um programa que:
    
    - Filtra uma lista de strings para manter apenas as que **começam com vogal**.
        
    - Transforma em letras maiúsculas.
        
    - Ordena em ordem decrescente.
        

---

## 🔧 NÍVEL 3 — REDUCE, ANYMATCH, E MATCHERS

7. Some todos os elementos de uma `List<Integer>` usando `reduce`.
    
8. Dada a mesma lista:
    
    - Verifique se **todos** os elementos são positivos.
        
    - Verifique se **algum** é múltiplo de 7.
        
9. Conte quantos elementos são **maiores que 50** numa `List<Integer>` aleatória.
    

---

## 🧰 NÍVEL 4 — COMBINAÇÕES COMPLEXAS

10. Crie uma classe `Pessoa` com `nome`, `idade` e `sexo`. Faça uma lista com pelo menos 6 pessoas variadas.
    
11. A partir dessa lista:
    

- Liste o nome das pessoas com mais de 18 anos.
    
- Liste apenas os nomes **em maiúsculo**, de pessoas do sexo feminino.
    
- Calcule a **média de idade** das pessoas do sexo masculino.
    
- Encontre a **pessoa mais velha**.
    
- Agrupe as pessoas por sexo (`Map<String, List<Pessoa>>`).
    

12. Crie um dicionário (`Map<String, List<Integer>>`) com nomes e listas de notas.
    

- Filtre os alunos com média acima de 7.
    
- Retorne só os nomes desses alunos.
    
- Transforme isso num novo `Map<String, Double>` com nome e média final.
    

---

## 💥 DESAFIOS AVANÇADOS

13. Dada uma lista de frases (`List<String>`):
    

- Conte **quantas palavras no total** há (use `flatMap` para dividir por espaço).
    
- Liste todas as **palavras únicas em ordem alfabética**.
    
- Conte quantas vezes a palavra `"java"` aparece (case-insensitive).
    

14. Crie um algoritmo que recebe uma lista de preços (como `BigDecimal`) e:
    

- Filtra os que estão entre 100 e 500.
    
- Aplica um desconto de 10% em cada.
    
- Soma o total final usando `reduce`.
    

15. A partir de uma lista de números aleatórios:
    

- Filtre apenas os primos.
    
- Some todos.
    
- Retorne uma string do tipo `"A soma dos primos foi: X"`.
    

---

## 🎓 EXTRA — MINI PROJETINHO

Crie um programa com uma classe `Produto` que tenha:

```java
String nome;
double preco;
String categoria;
```

E então:

- Crie uma lista com produtos variados.
    
- Filtre todos da categoria `"Eletrônicos"` com preço menor que 1000.
    
- Aplique 20% de desconto em todos.
    
- Agrupe os produtos restantes por categoria.
    
- Ordene por preço.
    
- Calcule o valor total da categoria `"Livros"`.
    

---

## 📚 EXERCÍCIO BÔNUS — EXPRESSÕES LAMBDA PURAS

Sem usar `stream`, pratique lambda isoladamente:

16. Crie uma `Comparator<Pessoa>` por idade, usando lambda.
    
17. Crie uma `Function<String, Integer>` que retorna o tamanho da string.
    
18. Crie uma `Predicate<Integer>` que verifica se um número é par.
    
19. Crie uma `BiFunction<String, Integer, String>` que recebe um nome e idade, e retorna `"Nome tem X anos"`.
    

---

Se quiser, posso montar um **repositório de exemplos com soluções passo a passo**, ou te mandar aos poucos os **gabaritos comentados**, pra você resolver um a um e ir consolidando.

Quer começar resolvendo alguns e eu te dou feedback?