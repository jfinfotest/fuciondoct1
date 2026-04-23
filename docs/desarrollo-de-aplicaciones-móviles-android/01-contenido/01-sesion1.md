---
title: "Sesión 1: El Salto a Kotlin (Sintaxis y Seguridad)"
description: "Domina los fundamentos de Kotlin: desde la declaración de variables inmutables hasta la erradicación de NullPointerException."
icon: mdi:numeric-1-box-outline
order: 1
---

# Sesión 1: El Salto a Kotlin

Kotlin no es solo un lenguaje "menos verboso" que Java; es un lenguaje diseñado para la **seguridad** y la **productividad**. En esta sesión, sentaremos las bases sólidas que necesitas para el desarrollo Android moderno.

<Steps>
  <Step title="Configuración del Entorno">
    Antes de escribir código, asegúrate de tener instalado **IntelliJ IDEA** o **Android Studio**. Kotlin se ejecuta sobre la JVM, por lo que la interoperabilidad es total.
    <Terminal 
      title="Verificar Instalación"
      shell="bash"
      staticText="Comprobando versión de Kotlin..."
      commands="kotlinc -version"
    />
  </Step>

  <Step title="Variables: val vs var">
    En Kotlin, la inmutabilidad es la norma, no la excepción. Usamos `val` para valores constantes y `var` para variables que pueden cambiar.
    
    <CodeExplainer>
      ```kotlin
      val nombre = "Kotlin" // Read-only (Inmutable)
      var version = 1.9
      
      // nombre = "Java" // ❌ Error de compilación
      version = 2.0      // ✅ Permitido
      ```
      <CodeExplainerStep lines="1">
        **val (Value):** Se asigna una sola vez. Es equivalente a `final` en Java. Favorece la programación funcional.
      </CodeExplainerStep>
      <CodeExplainerStep lines="2">
        **var (Variable):** Puede ser reasignada. Úsala con precaución.
      </CodeExplainerStep>
    </CodeExplainer>
  </Step>

  <Step title="El Sistema de Tipos y Null Safety">
    El "error del billón de dólares" (NullPointerException) se resuelve en Kotlin dividiendo los tipos en **No-Nulos** y **Nulos**.
    
    <CodeExplainer>
      ```kotlin
      var mensaje: String = "Hola"
      // mensaje = null // ❌ Error: El tipo es String, no String?

      var mensajeNulo: String? = "Soy opcional"
      mensajeNulo = null // ✅ Permitido

      // Acceso seguro
      val longitud = mensajeNulo?.length ?: 0
      ```
      <CodeExplainerStep lines="4-5">
        **Tipos Anulables (?):** Al añadir `?` al final del tipo, le indicamos al compilador que la variable puede contener `null`.
      </CodeExplainerStep>
      <CodeExplainerStep lines="8">
        **Operador Elvis (?:):** Si la expresión de la izquierda es nula, devuelve el valor de la derecha (en este caso, `0`).
      </CodeExplainerStep>
    </CodeExplainer>
  </Step>

  <Step title="Control de Flujo Moderno">
    En Kotlin, `if` y `when` son **expresiones**, lo que significa que devuelven un valor.
    
    <CodeExplainer>
      ```kotlin
      val puntuacion = 85
      val resultado = when (puntuacion) {
          in 90..100 -> "Excelente"
          in 70..89 -> "Aprobado"
          else -> "Reprobado"
      }
      println(resultado) // Imprime: Aprobado
      ```
      <CodeExplainerStep lines="2-6">
        **Expresión when:** Es el sustituto superpotente del `switch`. Soporta rangos (`in`), tipos y expresiones complejas.
      </CodeExplainerStep>
    </CodeExplainer>
  </Step>
</Steps>

---

## 🛠️ Práctica de la Sesión
**Reto: Validador de Usuarios**
Escribe un pequeño programa que reciba un nombre de usuario (que puede ser nulo) y una edad. Si el nombre es nulo, debe usar "Invitado". Si la edad es mayor a 18, debe imprimir "Acceso Concedido".

> [!TIP]
> Intenta usar el operador `?.` y `?:` para que tu código ocupe menos de 5 líneas.

---

> [!IMPORTANT]
> La seguridad ante nulos no es solo una ayuda; es una restricción que te obliga a pensar en los casos de error desde el diseño, haciendo tu app Android mucho más estable.
