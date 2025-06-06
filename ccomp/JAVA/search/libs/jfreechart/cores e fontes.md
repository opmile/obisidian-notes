
Perfeito, Milena! Vamos deixar esse gráfico de pizza **bonito** e depois integrá-lo em **relatórios automatizados com JasperReports**. Te explico em **duas partes**:

---

## 🖌️ PARTE 1 – **Customizando o Gráfico (cores, fontes, etc.)**

### Exemplo completo com:

- Fonte personalizada
    
- Cores definidas manualmente
    
- Rótulos visíveis e ajustados
    

```java
import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartUtils;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.plot.PiePlot;
import org.jfree.data.general.DefaultPieDataset;

import java.awt.*;
import java.io.File;
import java.io.IOException;

public class GraficoPizzaCustomizado {

    public static void main(String[] args) {
        // Dataset
        DefaultPieDataset dataset = new DefaultPieDataset();
        dataset.setValue("Java", 40);
        dataset.setValue("Python", 30);
        dataset.setValue("JavaScript", 20);
        dataset.setValue("Outros", 10);

        // Cria o gráfico
        JFreeChart chart = ChartFactory.createPieChart(
                "Linguagens favoritas",
                dataset,
                true,
                true,
                false
        );

        // Customização
        PiePlot plot = (PiePlot) chart.getPlot();

        // Fonte do título
        chart.getTitle().setFont(new Font("SansSerif", Font.BOLD, 18));

        // Cores personalizadas
        plot.setSectionPaint("Java", new Color(102, 178, 255));
        plot.setSectionPaint("Python", new Color(255, 204, 102));
        plot.setSectionPaint("JavaScript", new Color(255, 153, 153));
        plot.setSectionPaint("Outros", new Color(204, 204, 204));

        // Fonte dos rótulos
        plot.setLabelFont(new Font("SansSerif", Font.PLAIN, 14));
        plot.setSimpleLabels(true);
        plot.setLabelGap(0.02);

        // Fundo transparente
        chart.setBackgroundPaint(Color.WHITE);
        plot.setBackgroundPaint(Color.WHITE);

        // Salvar como imagem
        try {
            ChartUtils.saveChartAsPNG(new File("grafico_pizza_custom.png"), chart, 800, 600);
            System.out.println("Gráfico customizado salvo!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

> 🔧 Dica: Pode substituir `"SansSerif"` por `"Arial"`, `"Tahoma"`, etc. conforme sua preferência.

---

## 📄 PARTE 2 – **Integrando com JasperReports**

### 🧩 Visão geral do processo:

1. Criar o gráfico (já fizemos).
    
2. Incluir o gráfico como **imagem** em um relatório `.jrxml`.
    
3. Gerar o relatório com JasperReports.
    

---

### 📦 Dependências Maven necessárias:

```xml
<!-- JasperReports -->
<dependency>
    <groupId>net.sf.jasperreports</groupId>
    <artifactId>jasperreports</artifactId>
    <version>6.21.0</version> <!-- ou versão atual -->
</dependency>
```

---

### 🧪 Código Java para gerar o relatório

Assumindo que você tem um modelo `.jrxml` com um campo de imagem:

```java
import net.sf.jasperreports.engine.*;
import net.sf.jasperreports.engine.data.JRBeanCollectionDataSource;

import java.io.File;
import java.util.*;

public class RelatorioComGrafico {

    public static void main(String[] args) throws Exception {
        // 1. Caminho do relatório (modelo criado no JasperSoft Studio)
        String jrxmlPath = "src/main/resources/relatorio_com_grafico.jrxml";

        // 2. Compilar o modelo JRXML
        JasperReport report = JasperCompileManager.compileReport(jrxmlPath);

        // 3. Parametros do relatório
        Map<String, Object> params = new HashMap<>();
        params.put("titulo", "Relatório com Gráfico de Pizza");
        params.put("graficoPath", "grafico_pizza_custom.png"); // caminho da imagem gerada

        // 4. Fonte de dados (pode ser vazia se tudo é por parâmetros)
        JRDataSource dataSource = new JREmptyDataSource();

        // 5. Gerar o relatório
        JasperPrint print = JasperFillManager.fillReport(report, params, dataSource);

        // 6. Exportar para PDF
        JasperExportManager.exportReportToPdfFile(print, "relatorio_final.pdf");
        System.out.println("Relatório gerado como PDF!");
    }
}
```

---

### 🧱 Como criar o `.jrxml` com a imagem:

1. Crie um relatório no **JasperSoft Studio**.
    
2. Adicione uma **Image** no designer.
    
3. Vá na aba "Properties" e:
    
    - Marque "Expression" como `new java.io.File($P{graficoPath}).getAbsolutePath()`
        
    - Marque a opção "Scale Image" como `Retain Shape` ou `Clip` conforme o layout.
        
4. Adicione um parâmetro do tipo `String` chamado `graficoPath`.
    

---

## ⚡ Quer mais praticidade?

Posso te mandar:

- Um exemplo `.jrxml` pronto
    
- A geração do gráfico **dinamicamente no relatório**, sem salvar imagem (usando `JRRenderable`)
    
- Exportação para **HTML ou DOCX**
    

Só me dizer o que você prefere!