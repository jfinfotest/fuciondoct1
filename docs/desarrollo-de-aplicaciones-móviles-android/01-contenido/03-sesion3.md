---
title: "Sesión 3: Orientación a Objetos Moderna (POO)"
description: "Elimina el código repetitivo con Data Classes, Companion Objects y Singleton Patterns."
icon: mdi:numeric-3-box-outline
order: 3
---

# Sesión 3: Orientación a Objetos Moderna (POO)

Kotlin redefine la Programación Orientada a Objetos para hacerla más concisa y menos propensa a errores. En esta sesión, aprenderemos a modelar datos y comportamientos de forma eficiente.

## 1. El Fin del "Boilerplate": Data Classes

En Java, una clase para guardar datos requería getters, setters, `equals`, `hashCode` y `toString`. En Kotlin, solo necesitas una línea.

<CodeExplainer>
  ```kotlin
  data class Usuario(val id: Int, val nombre: String, val email: String)

  val user1 = Usuario(1, "Ana", "ana@mail.com")
  val user2 = user1.copy(id = 2) // Crea una copia con un valor cambiado

  println(user1) // Usuario(id=1, nombre=Ana, email=ana@mail.com)
  ```
  <CodeExplainerStep lines="1">
    **data class:** El compilador genera automáticamente métodos para comparar, copiar e imprimir el objeto de forma legible.
  </CodeExplainerStep>
  <CodeExplainerStep lines="4">
    **Método copy():** Fundamental para mantener la inmutabilidad. Crea un nuevo objeto basado en uno existente modificando solo lo necesario.
  </CodeExplainerStep>
</CodeExplainer>

## 2. Jerarquía y Contratos

Kotlin usa un sistema de herencia cerrado por defecto. Para que una clase sea heredable, debe marcarse como `open`.

<X6Diagram height={300} data="{
  nodes: [
    { id: 'base', label: 'abstract class Empleado', x: 300, y: 50, color: '#94a3b8', width: 200 },
    { id: 'dev', label: 'Developer', x: 150, y: 180, color: '#6366f1', width: 140 },
    { id: 'manager', label: 'Manager', x: 450, y: 180, color: '#8b5cf6', width: 140 }
  ],
  edges: [
    { source: 'dev', target: 'base', label: 'Herencia', animated: true },
    { source: 'manager', target: 'base', label: 'Herencia', animated: true }
  ]
}" />

<CodeExplainer>
  ```kotlin
  abstract class Empleado(val nombre: String) {
      abstract fun calcularSalario(): Double
  }

  class Developer(nombre: String, val lenguaje: String) : Empleado(nombre) {
      override fun calcularSalario() = 3000.0
  }
  ```
  <CodeExplainerStep lines="1-3">
    **Clases Abstractas:** Definen el contrato. No se pueden instanciar.
  </CodeExplainerStep>
  <CodeExplainerStep lines="5-7">
    **Implementación:** Usamos el símbolo `:` para heredar y `override` para implementar los métodos obligatorios.
  </CodeExplainerStep>
</CodeExplainer>

## 3. Objetos Especiales: Companion y Singleton

¿Necesitas miembros estáticos o una única instancia de una clase? Kotlin tiene palabras clave específicas para esto.

*   **`object`**: Crea un Singleton instantáneo.
*   **`companion object`**: Equivalente a los miembros `static` de Java, pero vinculado a una instancia de clase.

<Alert variant="warning" title="Dato Importante">
  En Kotlin no existe la palabra clave `static`. Todo lo que necesite ser global o compartido debe ir dentro de un `object` o un `companion object`.
</Alert>

---

## 🛠️ Práctica: Modelado de Roles
Diseña un sistema donde existan `Usuarios` (Data Class) y un `AdministradorDeSesion` (Singleton Object) que guarde al usuario que ha iniciado sesión actualmente.

1.  Crea la Data Class `Usuario`.
2.  Crea un `object AuthManager` con una variable `usuarioActual`.
3.  Simula un login cambiando el `usuarioActual` y verifica que los datos se mantengan consistentes en toda la app.
