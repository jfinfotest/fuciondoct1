---
title: "Sesión 2: Funciones y Estructuras de Datos"
description: "Aprende a organizar lógica con funciones avanzadas y a manejar datos con colecciones inmutables."
icon: mdi:numeric-2-box-outline
order: 2
---

# Sesión 2: Funciones y Estructuras de Datos

En esta sesión pasaremos de scripts lineales a una arquitectura de código reutilizable. Kotlin nos ofrece herramientas para que nuestras funciones sean más legibles y nuestras colecciones más seguras.

## 1. Funciones Modernas

Kotlin permite simplificar las funciones hasta el punto de parecer lenguaje natural.

<CodeExplainer>
  ```kotlin
  // Función de una sola línea
  fun saludar(nombre: String) = "Hola, $nombre"

  // Parámetros por defecto y nombrados
  fun configurarPerfil(
      usuario: String, 
      esAdmin: Boolean = false,
      tema: String = "Oscuro"
  ) {
      println("Configurando a $usuario (Admin: $esAdmin) en modo $tema")
  }

  // Llamada usando parámetros nombrados
  configurarPerfil("Juan", tema = "Claro")
  ```
  <CodeExplainerStep lines="2">
    **Single-Expression Functions:** Si una función solo devuelve un valor, podemos omitir las llaves `{}` y el `return`.
  </CodeExplainerStep>
  <CodeExplainerStep lines="5-9">
    **Parámetros por Defecto:** Evitan la sobrecarga de métodos (Overloading) común en Java.
  </CodeExplainerStep>
  <CodeExplainerStep lines="14">
    **Named Arguments:** Puedes saltarte parámetros con valores por defecto o simplemente mejorar la legibilidad especificando el nombre.
  </CodeExplainerStep>
</CodeExplainer>

## 2. Colecciones: Mutables vs Inmutables

A diferencia de otros lenguajes, Kotlin distingue estrictamente entre colecciones que puedes leer y colecciones que puedes modificar.

| Característica | Inmutable (Read-only) | Mutable (Read-Write) |
| :--- | :--- | :--- |
| **Declaración** | `listOf()`, `mapOf()`, `setOf()` | `mutableListOf()`, `mutableMapOf()` |
| **Operaciones** | Solo lectura, `filter`, `map` | `add()`, `remove()`, `clear()` |
| **Seguridad** | Hilos seguros por naturaleza | Requiere sincronización manual |

<Alert variant="info">
  **Regla de Oro:** Empieza siempre con colecciones inmutables. Solo cámbialas a mutables si el requerimiento de negocio lo exige explícitamente.
</Alert>

## 3. Extension Functions: "Magia" en el Código

¿Alguna vez quisiste añadir un método a la clase `String` o `Int`? En Kotlin puedes hacerlo sin herencia.

<CodeExplainer>
  ```kotlin
  // Extendemos la clase String
  fun String.quitarEspacios(): String {
      return this.replace(" ", "")
  }

  val texto = "Hola Mundo Kotlin"
  println(texto.quitarEspacios()) // Imprime: HolaMundoKotlin
  ```
  <CodeExplainerStep lines="2-4">
    **Extension Function:** El receptor `String` nos permite acceder al contenido mediante `this`. Ahora cualquier String en nuestro proyecto tiene este método.
  </CodeExplainerStep>
</CodeExplainer>

---

## 🛠️ Práctica: Sistema de Inventario
Crea una lista inmutable de productos. Implementa una función que reciba esa lista y retorne solo los productos que tengan un precio mayor a $50, utilizando funciones de extensión si es posible.

<Steps>
  <Step title="Modelar el Dato">
    Define una estructura básica para tus productos (nombre y precio).
  </Step>
  <Step title="Crear la Colección">
    Usa `listOf` para inicializar tu inventario base.
  </Step>
  <Step title="Filtrar">
    Aplica la lógica de filtrado y muestra los resultados en consola.
  </Step>
</Steps>
