[[1 css]]
[[1 tailwind css]]

No **Tailwind CSS**, os valores como `my-40` ou `p-12` são **baseados em uma escala numérica** que utiliza a unidade **`rem`** como base.

### 🧠 Explicação rápida:

- `1rem` = tamanho da fonte raiz do HTML, geralmente `16px`.
    
- Os números em Tailwind correspondem a **fatores multiplicados por 0.25rem** (ou 4px por unidade).
    

### 📏 Tabela prática:

|Classe Tailwind|Valor em rem|Valor em px (supondo 1rem = 16px)|
|---|---|---|
|`p-1`|0.25rem|4px|
|`p-2`|0.5rem|8px|
|`p-12`|3rem|48px|
|`my-40`|10rem|160px|

> ✅ Então, **`p-12` equivale a `padding: 3rem` (ou 48px)** e **`my-40` equivale a `margin-top` e `margin-bottom: 10rem` (ou 160px)**.

Se quiser usar valores customizados em `px`, você pode usar:

```html
<div class="p-[30px] my-[100px]">...</div>
```

Mas o recomendado no Tailwind é seguir a escala para manter consistência no design.