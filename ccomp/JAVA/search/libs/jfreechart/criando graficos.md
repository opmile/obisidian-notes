JFreeChart é uma biblioteca Java muito poderosa e gratuita para criação de gráficos 2D como pizza, barra, linha, dispersão e muitos outros. Se você está começando agora, vou te mostrar **como usá-la de forma prática** com um passo a passo simples.

---

### 🔧 1. **Adicionar a biblioteca ao seu projeto**

Você pode usar o JFreeChart com Maven, Gradle, ou adicionando o `.jar` manualmente.

#### ✅ Se estiver usando Maven:

Adicione isso no `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.jfree</groupId>
        <artifactId>jfreechart</artifactId>
        <version>1.5.3</version>
    </dependency>
</dependencies>
```

#### ✅ Sem Maven:

Baixe os `.jar` no site oficial:  
👉 [https://sourceforge.net/projects/jfreechart/](https://sourceforge.net/projects/jfreechart/)

Inclua os arquivos no seu projeto (normalmente `jfreechart-x.x.x.jar` + `jcommon-x.x.x.jar`).

---

### 📊 2. **Exemplo de gráfico de barras**

```java
import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartFrame;
import org.jfree.chart.JFreeChart;
import org.jfree.data.category.DefaultCategoryDataset;

public class ExemploGraficoBarras {
    public static void main(String[] args) {
        // Criando os dados
        DefaultCategoryDataset dataset = new DefaultCategoryDataset();
        dataset.addValue(10, "Alunos", "Java");
        dataset.addValue(8, "Alunos", "Python");
        dataset.addValue(6, "Alunos", "JavaScript");

        // Criando o gráfico
        JFreeChart chart = ChartFactory.createBarChart(
                "Popularidade das Linguagens", // título
                "Linguagens",                  // eixo X
                "Quantidade de Alunos",        // eixo Y
                dataset                        // dados
        );

        // Mostrando o gráfico em uma janela
        ChartFrame frame = new ChartFrame("Gráfico de Barras", chart);
        frame.pack();
        frame.setVisible(true);
    }
}
```

---

### 🧁 Outros tipos de gráficos

- **Pizza**: `ChartFactory.createPieChart(...)`
    
- **Linha**: `ChartFactory.createLineChart(...)`
    
- **Dispersão**: `ChartFactory.createScatterPlot(...)`
    
- **Área**: `ChartFactory.createAreaChart(...)`
    

Cada um desses usa um tipo diferente de `Dataset`, como `DefaultPieDataset`, `XYSeriesCollection`, etc.

---

### 🔍 Dicas extras

- Você pode salvar o gráfico como imagem com `ChartUtils.saveChartAsPNG(...)`.
    
- Dá pra customizar cores, fontes, legendas e mais com a API do `JFreeChart`.
    
- Ideal para dashboards Java Swing, aplicações desktop, ou geração de relatórios.
    

---

Se quiser, posso te mostrar **como fazer um gráfico de pizza**, **gravar o gráfico como imagem** ou até **inserir em uma aplicação Swing com botões**, é só pedir!JFreeChart é uma biblioteca Java muito poderosa e gratuita para criação de gráficos 2D como pizza, barra, linha, dispersão e muitos outros. Se você está começando agora, vou te mostrar **como usá-la de forma prática** com um passo a passo simples.

---

### 🔧 1. **Adicionar a biblioteca ao seu projeto**

Você pode usar o JFreeChart com Maven, Gradle, ou adicionando o `.jar` manualmente.

#### ✅ Se estiver usando Maven:

Adicione isso no `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.jfree</groupId>
        <artifactId>jfreechart</artifactId>
        <version>1.5.3</version>
    </dependency>
</dependencies>
```

#### ✅ Sem Maven:

Baixe os `.jar` no site oficial:  
👉 [https://sourceforge.net/projects/jfreechart/](https://sourceforge.net/projects/jfreechart/)

Inclua os arquivos no seu projeto (normalmente `jfreechart-x.x.x.jar` + `jcommon-x.x.x.jar`).

---

### 📊 2. **Exemplo de gráfico de barras**

```java
import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartFrame;
import org.jfree.chart.JFreeChart;
import org.jfree.data.category.DefaultCategoryDataset;

public class ExemploGraficoBarras {
    public static void main(String[] args) {
        // Criando os dados
        DefaultCategoryDataset dataset = new DefaultCategoryDataset();
        dataset.addValue(10, "Alunos", "Java");
        dataset.addValue(8, "Alunos", "Python");
        dataset.addValue(6, "Alunos", "JavaScript");

        // Criando o gráfico
        JFreeChart chart = ChartFactory.createBarChart(
                "Popularidade das Linguagens", // título
                "Linguagens",                  // eixo X
                "Quantidade de Alunos",        // eixo Y
                dataset                        // dados
        );

        // Mostrando o gráfico em uma janela
        ChartFrame frame = new ChartFrame("Gráfico de Barras", chart);
        frame.pack();
        frame.setVisible(true);
    }
}
```

---

### 🧁 Outros tipos de gráficos

- **Pizza**: `ChartFactory.createPieChart(...)`
    
- **Linha**: `ChartFactory.createLineChart(...)`
    
- **Dispersão**: `ChartFactory.createScatterPlot(...)`
    
- **Área**: `ChartFactory.createAreaChart(...)`
    

Cada um desses usa um tipo diferente de `Dataset`, como `DefaultPieDataset`, `XYSeriesCollection`, etc.

---

### 🔍 Dicas extras

- Você pode salvar o gráfico como imagem com `ChartUtils.saveChartAsPNG(...)`.
    
- Dá pra customizar cores, fontes, legendas e mais com a API do `JFreeChart`.
    
- Ideal para dashboards Java Swing, aplicações desktop, ou geração de relatórios.
    

---

Se quiser, posso te mostrar **como fazer um gráfico de pizza**, **gravar o gráfico como imagem** ou até **inserir em uma aplicação Swing com botões**, é só pedir!