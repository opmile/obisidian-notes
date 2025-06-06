[[why share mvn libs]]

Ótima pergunta! Bora direto ao ponto: compartilhar uma biblioteca interna no Maven é **como criar um projeto Java comum**, empacotar ele como `.jar`, **instalar no repositório local (ou remoto)**, e depois **importar nos outros projetos** como dependência. Isso é super comum em ambientes corporativos.

---

## ✅ Exemplo prático: criando e usando uma biblioteca interna

### 🎯 Cenário:

Você quer criar uma biblioteca com funções utilitárias chamada `utils`, e usá-la em outros projetos da sua empresa (todos com `groupId` igual a `com.opmile3`).

---

### 1. 📦 Criar o projeto da biblioteca

```bash
mvn archetype:generate \
  -DgroupId=com.opmile3 \
  -DartifactId=utils \
  -Dversion=1.0.0 \
  -DinteractiveMode=false
```

Esse projeto terá:

```xml
<!-- utils/pom.xml -->
<project>
  <groupId>com.opmile3</groupId>
  <artifactId>utils</artifactId>
  <version>1.0.0</version>
</project>
```

---

### 2. 🛠️ Adicionar classes utilitárias

```java
// src/main/java/com/opmile3/utils/StringUtils.java
package com.opmile3.utils;

public class StringUtils {
    public static String capitalize(String input) {
        return input == null || input.isEmpty()
            ? input
            : input.substring(0, 1).toUpperCase() + input.substring(1);
    }
}
```

---

### 3. 📥 Instalar a lib no repositório local

```bash
cd utils
mvn install
```

Isso vai empacotar o JAR e jogar ele no seu repositório local `~/.m2/repository/com/opmile3/utils`.

---

### 4. 📎 Usar a lib em outro projeto

No seu outro projeto Maven (`api-client`, por exemplo), adicione isso no `pom.xml`:

```xml
<dependency>
    <groupId>com.opmile3</groupId>
    <artifactId>utils</artifactId>
    <version>1.0.0</version>
</dependency>
```

Agora você pode fazer:

```java
import com.opmile3.utils.StringUtils;

String nome = StringUtils.capitalize("milena"); // "Milena"
```

---

### 5. (Opcional) 📡 Repositório remoto

Se você estiver em equipe, pode publicar sua lib em um **repositório remoto privado**, como:

- **Nexus**
    
- **Artifactory**
    
- **GitHub Packages**
    
- **JitPack (grátis)**
    

Assim todo mundo da equipe pode importar e manter as versões sincronizadas.

---

## ✅ Vantagens disso

- Evita duplicação de código.
    
- Permite versionamento independente.
    
- Facilita manutenção centralizada.
    
- Reforça o conceito de **arquitetura modular**.
    

Se quiser, posso te mostrar como publicar no GitHub Packages ou criar um repositório Maven privado local rapidinho.

