---
title: "Sesión 1: El Salto a Kotlin (Sintaxis y Seguridad)"
description: "Guía detallada sobre la interoperabilidad JVM, inmutabilidad, Null Safety y estructuras de control modernas en Kotlin."
icon: mdi:numeric-1-box-outline
order: 1
---

# Sesión 1: El Salto a Kotlin

Kotlin no es solo un lenguaje "menos verboso" que Java; es un lenguaje diseñado para la **seguridad** y la **productividad**. En esta sesión, profundizaremos en los pilares que hacen de Kotlin el lenguaje preferido para Android.

---

## 1. Introducción: Interoperabilidad y Configuración

### Interoperabilidad con la JVM
Kotlin está diseñado para ser **100% interoperable** con Java. Esto significa que puedes tener archivos Java y Kotlin coexistiendo en el mismo proyecto, y llamar a funciones de uno desde el otro sin problemas. 

*   **JVM (Java Virtual Machine):** Kotlin se compila a Bytecode de Java, lo que permite que se ejecute en cualquier lugar donde Java lo haga.
*   **Ecosistema:** Puedes usar todas las librerías de Java existentes (como Retrofit, Glide, Room) de forma nativa en Kotlin.

### Configuración de IntelliJ / Android Studio
Para comenzar, solo necesitas instalar el IDE oficial. Kotlin viene integrado por defecto.

<Steps>
  <Step title="Instalación del IDE">
    Descarga e instala **Android Studio** (recomendado para apps) o **IntelliJ IDEA** (para scripts y backend).
  </Step>
  <Step title="Creación del Proyecto">
    Al crear un nuevo proyecto, asegúrate de seleccionar **Kotlin** como el lenguaje principal.
  </Step>
</Steps>

<CodeTabs>
  <CodeTab title="Kotlin" icon="vscode-icons:file-type-kotlin">
    ```kotlin
    fun main() {
        println("Hola desde Kotlin!")
    }
    ```
  </CodeTab>
  <CodeTab title="Java" icon="vscode-icons:file-type-java">
    ```java
    public class Main {
        public static void main(String[] args) {
            System.out.println("Hola desde Java!");
        }
    }
    ```
  </CodeTab>
</CodeTabs>

---

## 2. Variables: val vs var e Inmutabilidad

En Kotlin, la declaración de variables se centra en la intención del programador sobre la mutabilidad de los datos.

### La Importancia de la Inmutabilidad
En el desarrollo de aplicaciones Android, la inmutabilidad ayuda a prevenir errores comunes en hilos (threads) y hace que el estado de la aplicación sea predecible.

*   **`val` (Value):** Referencia inmutable. Una vez asignado el valor, no puede cambiar. Es equivalente a `final` en Java. **Úsalo por defecto.**
*   **`var` (Variable):** Referencia mutable. Puede ser reasignada en cualquier momento.

<CodeTabs>
  <CodeTab title="Asignaciones" icon="mdi:code-tags">
    ```kotlin
    val nombre = "Kotlin" 
    // nombre = "Java" // [!code error] // ❌ Error: Val cannot be reassigned

    var version = 1.9
    version = 2.0 // ✅ Correcto: Var puede cambiar
    ```
  </CodeTab>
  <CodeTab title="¿Por qué val?" icon="mdi:help-circle">
    ```kotlin
    // Al usar val, garantizas que este objeto no cambiará 
    // accidentalmente durante la ejecución de una función compleja.
    val configuracionBase = APIConfig("https://api.com")
    ```
  </CodeTab>
</CodeTabs>

---

## 3. Null Safety: El Fin del Billón de Dólares

El error más común en Java es el `NullPointerException`. Kotlin soluciona esto integrando la nulidad directamente en el sistema de tipos.

### Tipos Nulos (?)
Por defecto, ninguna variable en Kotlin puede ser nula. Para permitirlo, debes marcar el tipo con un signo de interrogación.

<CodeTabs>
  <CodeTab title="Definición de Tipos" icon="vscode-icons:file-type-kotlin">
    ```kotlin
    var obligatorio: String = "No puedo ser nulo"
    // obligatorio = null // ❌ Error de compilación

    var opcional: String? = "Puedo ser nulo"
    opcional = null // ✅ Correcto
    ```
  </CodeTab>
  <CodeTab title="Safe Calls & Elvis" icon="mdi:flash">
    ```kotlin
    val longitud: Int = opcional?.length ?: 0
    
    // Explicación:
    // 1. opcional?.length -> Si 'opcional' es nulo, devuelve nulo. Si no, su longitud.
    // 2. ?: 0 -> Si el resultado de la izquierda es nulo, usa '0'.
    ```
  </CodeTab>
</CodeTabs>

> [!CAUTION]
> Evita usar el operador `!!` (Not-null assertion). Este operador fuerza al compilador a tratar una variable como no nula, pero si realmente es nula, lanzará una excepción inmediatamente.

---

## 4. Control de Flujo Moderno

### if como Expresión
A diferencia de Java, en Kotlin `if` es una expresión, lo que significa que puede devolver un valor directamente.

### El Poder de `when`
Es el sustituto de `switch`, pero mucho más flexible. Puede evaluar rangos, tipos y múltiples condiciones sin necesidad de `break`.

<CodeTabs>
  <CodeTab title="If como Expresión" icon="mdi:code-braces">
    ```kotlin
    val edad = 20
    val mensaje = if (edad >= 18) "Adulto" else "Menor"
    // No necesitas una variable temporal ni múltiples returns.
    ```
  </CodeTab>
  <CodeTab title="Estructura when" icon="mdi:function-variant">
    ```kotlin
    val nota = 85
    when (nota) {
        in 90..100 -> println("Sobresaliente")
        in 70..89 -> println("Aprobado")
        in 0..69 -> println("Reprobado")
        else -> println("Nota inválida")
    }
    ```
  </CodeTab>
  <CodeTab title="Rangos (1..10)" icon="mdi:numeric">
    ```kotlin
    // Iteración simple
    for (i in 1..5) {
        print(i) // 12345
    }

    // Verificación de pertenencia
    val x = 5
    if (x in 1..10) {
        println("Está en el rango")
    }
    ```
  </CodeTab>
</CodeTabs>

---

## 🛠️ Práctica de la Sesión
**Reto Final:** Crea un sistema de validación de perfil.
1. Declara una variable `val usuario: String?` que pueda ser nula.
2. Usa un bloque `when` para verificar una variable `puntos`. Si está entre `1..100` es "Principiante", si es mayor a `100` es "Pro".
3. Imprime un mensaje final usando interpolación de strings: `"Usuario: ${usuario ?: "Anónimo"} - Rango: $rango"`.

> [!TIP]
> La interpolación de strings se hace con el símbolo `$`. Si necesitas ejecutar lógica dentro del string, usa `${...}`.
