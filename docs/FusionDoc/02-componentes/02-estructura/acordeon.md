---
title: Acordeón
description: Cómo organizar información desplegable usando el componente Accordion.
icon: 'lucide:layout-list'
order: 3
---

# Acordeón

El componente `Accordion` permite agrupar contenido que el usuario puede expandir o contraer, ideal para FAQs o detalles técnicos opcionales.

## Ejemplo

Puedes usar etiquetas `<Accordion>` y `<AccordionItem>`. Por defecto, solo permite abrir un elemento a la vez. Si quieres permitir que el usuario abra varios elementos simultáneamente, usa la propiedad `allowMultiple`.

<Accordion allowMultiple>
  <AccordionItem title="¿Qué es FusionDoc?">
    FusionDoc es un generador de documentación ultrarrápido construido con Next.js y MDX.
  </AccordionItem>
  <AccordionItem title="Instalación">
    Puedes instalarlo vía npm: `npm install fusiondoc`.
  </AccordionItem>
</Accordion>

## Uso en MDX

```mdx
<Accordion>
  <AccordionItem title="Mi Título">
    Este es el contenido desplegable.
  </AccordionItem>
</Accordion>
```

## Propiedades del objeto

### `<Accordion>`
| Prop | Tipo | Descripción |
| :--- | :--- | :--- |
| `allowMultiple` | `boolean` | Determina si se pueden abrir varios items al mismo tiempo. |



<CodeExplainer 
  title="Explicación de sum()" 
  code={`function sum(a, b) {
  return a + b;
}`}
  steps={[
    { line: 1, text: "Firma de la función con dos parámetros." },
    { line: 2, text: "Retorno aritmético simple." }
  ]}
/>


<Terminal title="bash">
  npm run dev
</Terminal>

### `<AccordionItem>`
| Prop | Tipo | Descripción |
| :--- | :--- | :--- |
| `title` | `string` | **Requerido**. El título que se despliega. |
