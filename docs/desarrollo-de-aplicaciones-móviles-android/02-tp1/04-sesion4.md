---
title: "Sesión 4: Programación Funcional y Scope Functions"
description: "Escribe código elegante y declarativo. Introducción a la asincronía con Corrutinas."
icon: mdi:numeric-4-box-outline
order: 4
---

# Sesión 4: Programación Funcional y Scope Functions

Esta sesión es donde Kotlin realmente brilla. Aprenderemos a transformar datos de forma declarativa y a manejar procesos asíncronos sin bloquear la interfaz de usuario de Android.

## 1. El Poder de las Lambdas

Las lambdas nos permiten pasar bloques de código como si fueran variables.

<CodeExplainer>
  ```kotlin
  val numeros = listOf(1, 2, 3, 4, 5, 6)

  // Programación Declarativa
  val paresDuplicados = numeros
      .filter { it % 2 == 0 } // Filtra pares
      .map { it * 2 }         // Duplica cada uno

  println(paresDuplicados) // [4, 8, 12]
  ```
  <CodeExplainerStep lines="5">
    **Operador filter:** Crea una nueva lista solo con los elementos que cumplen la condición. `it` es el nombre por defecto del elemento actual.
  </CodeExplainerStep>
  <CodeExplainerStep lines="6">
    **Operador map:** Transforma cada elemento de la lista según la función proporcionada.
  </CodeExplainerStep>
</CodeExplainer>

## 2. Scope Functions: Limpiando el Código

Kotlin ofrece 5 funciones especiales para ejecutar un bloque de código dentro del contexto de un objeto: `let`, `run`, `with`, `apply` y `also`.

| Función | Referencia al Objeto | Valor de Retorno | Caso de Uso Común |
| :--- | :--- | :--- | :--- |
| **`let`** | `it` | Resultado de lambda | Operaciones con nulos (`?.let`) |
| **`apply`** | `this` | El mismo objeto | Configuración de objetos (Builder) |
| **`run`** | `this` | Resultado de lambda | Inicialización y computación |
| **`also`** | `it` | El mismo objeto | Acciones adicionales (logging) |

<CodeExplainer>
  ```kotlin
  val intent = Intent().apply {
      action = "ACTION_VIEW"
      data = Uri.parse("https://kotlinlang.org")
  }
  
  intent.also { println("Iniciando navegación a ${it.data}") }
  ```
  <CodeExplainerStep lines="1-4">
    **apply:** Muy usado en Android para configurar vistas o intents sin repetir el nombre de la variable.
  </CodeExplainerStep>
  <CodeExplainerStep lines="6">
    **also:** Ideal para efectos secundarios que no deben alterar el objeto principal.
  </CodeExplainerStep>
</CodeExplainer>

## 3. Introducción a Corrutinas

En Android, nunca debemos realizar operaciones pesadas (red, base de datos) en el hilo principal (Main Thread). Las corrutinas permiten escribir código asíncrono que se lee como si fuera síncrono.

<X6Diagram height={350} data="{
  nodes: [
    { id: 'ui', label: 'Main Thread (UI)', x: 100, y: 100, color: '#22c55e' },
    { id: 'io', label: 'IO Thread (Background)', x: 400, y: 200, color: '#3b82f6' },
    { id: 'task', label: 'Descarga API', x: 400, y: 100, color: '#f59e0b' }
  ],
  edges: [
    { source: 'ui', target: 'task', label: 'Suspend', animated: true },
    { source: 'task', target: 'io', label: 'Resume', animated: true }
  ]
}" />

> [!CAUTION]
> Una **Suspend Function** es una función que puede pausar la ejecución de la corrutina sin bloquear el hilo. Se marcan con la palabra clave `suspend`.

---

## 🏆 Proyecto Final: Procesador de Usuarios
Integra todo lo aprendido en una aplicación de consola final:

<Steps>
  <Step title="Preparar Datos">
    Crea una lista de objetos `Usuario` (data class) con campos como `nombre`, `puntos` y `activo`.
  </Step>
  <Step title="Procesamiento Funcional">
    Filtra los usuarios activos, multiplica sus puntos por un factor de bono y ordena el resultado de mayor a menor.
  </Step>
  <Step title="Visualización Limpia">
    Usa `apply` o `also` para mostrar un log de cada transformación realizada.
  </Step>
  <Step title="Simulación Asíncrona">
    Envuelve el proceso en una función `suspend` y simula una carga de red de 2 segundos.
  </Step>
</Steps>

<Alert variant="success">
  ¡Felicidades! Has completado los fundamentos de Kotlin para Android. Estás listo para empezar a construir interfaces con Jetpack Compose.
</Alert>
