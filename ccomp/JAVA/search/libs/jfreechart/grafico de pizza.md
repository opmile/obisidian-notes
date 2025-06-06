Claro, Milena! Vamos direto ao ponto: usar a biblioteca **JFreeChart** para criar um **gráfico de pizza (pie chart)** e **salvar como imagem** para um relatório.

---

### 📦 Passo 1 – Adicionar a biblioteca JFreeChart ao seu projeto

Se estiver usando **Maven**, adicione ao `pom.xml`:

```xml
<dependency>
    <groupId>org.jfree</groupId>
    <artifactId>jfreechart</artifactId>
    <version>1.5.3</version> <!-- ou a mais recente -->
</dependency>
```

Se não usa Maven, baixe o `.jar` do [site oficial](https://sourceforge.net/projects/jfreechart/) e adicione ao seu classpath.

---

### 🧱 Passo 2 – Criar o gráfico de pizza com JFreeChart

Aqui vai um exemplo **completo**:

```java
import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartUtils;
import org.jfree.chart.JFreeChart;
import org.jfree.data.general.DefaultPieDataset;

import java.io.File;
import java.io.IOException;

public class GraficoPizza {

    public static void main(String[] args) {
        // 1. Criar dataset
        DefaultPieDataset dataset = new DefaultPieDataset();
        dataset.setValue("Java", 40);
        dataset.setValue("Python", 30);
        dataset.setValue("JavaScript", 20);
        dataset.setValue("Outros", 10);

        // 2. Criar o gráfico
        JFreeChart graficoPizza = ChartFactory.createPieChart(
                "Linguagens favoritas", // título
                dataset,                // dados
                true,                   // legenda
                true,                   // tooltips
                false                   // URLs
        );

        // 3. Salvar o gráfico como imagem PNG
        try {
            ChartUtils.saveChartAsPNG(new File("grafico_pizza.png"), graficoPizza, 800, 600);
            System.out.println("Gráfico salvo como 'grafico_pizza.png'");
        } catch (IOException e) {
            System.err.println("Erro ao salvar gráfico: " + e.getMessage());
        }
    }
}
```

---

### 🧠 Dicas extras:

- Se for usar em **relatórios automatizados**, o gráfico gerado pode ser incluído em PDF com libs como iText ou JasperReports.
    
- Pode mudar o formato para `.jpg` usando `saveChartAsJPEG`.
    
- Dá pra customizar cores, fontes, ângulos do rótulo, etc. Se quiser personalizações, posso te mostrar também.
    

---

Quer que eu adicione integração com JasperReports ou exportação direta pra PDF também?