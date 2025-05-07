# Guía Completa de **Funciones en Python**

> *"Las funciones son como recetas de cocina: tienes ingredientes (parámetros), pasos a seguir (código) y un resultado final (valor de retorno)."*

## ¿Qué es una función?

Imagina que una función es como una **máquina expendedora**:

```mermaid
flowchart LR
  A[Insertas monedas \n(parámetros)] --> B[Máquina \n(función)]
  B --> C[Procesa tu pedido \n(código)]
  C --> D[Entrega producto \n(valor de retorno)]
```

**Ejemplo de siempre ;)**
```python
def preparar_cafe(tipo, azucar):
    """Prepara una taza de café según preferencias."""
    return f"Taza de {tipo} con {azucar} cucharadas de azúcar"

mi_cafe = preparar_cafe("expreso", 1)
print(mi_cafe)  # "Taza de expreso con 1 cucharada de azúcar"

```

## Tabla de Contenidos

1. [Introducción](#1-introducción)
2. [¿Por qué usar funciones?](#2-por-qué-usar-funciones)
3. [Sintaxis básica](#3-sintaxis-básica)
4. [Parámetros y argumentos](#4-parámetros-y-argumentos)

   * [Posicionales](#41-posicionales)
   * [Nombrados (keywords)](#42-nombrados-keywords)
   * [Valores por defecto](#43-valores-por-defecto)
   * [Parámetros variables \*args y \*\*kwargs](#44-parámetros-variables-args-y-kwargs)
5. [Valores de retorno](#5-valores-de-retorno)
6. [Ámbito (scope) de las variables](#6-Ámbito-scope-de-las-variables)
7. [Documentación de funciones (docstrings)](#7-documentación-de-funciones-docstrings)
8. [Buenas prácticas](#8-buenas-prácticas)
9. [Funciones anónimas (`lambda`)](#9-funciones-anónimas-lambda)
10. [Funciones de orden superior](#10-funciones-de-orden-superior)
11. [Decoradores básicos](#11-decoradores-básicos)
12. [Anotaciones de tipo](#12-anotaciones-de-tipo)
13. [Manejo de errores en funciones](#13-manejo-de-errores-en-funciones)


---

## 1. Introducción

Una función en programación es similar a una función matemática: toma entradas (parámetros), realiza un procesamiento, y produce una salida (valor de retorno).

**Características principales**:
- **Modularidad**: Permite dividir programas complejos en partes más pequeñas
- **Encapsulamiento**: Oculta los detalles de implementación
- **Abstracción**: Solo necesitas saber qué hace, no cómo lo hace

**Ejemplo conceptual**:
```python
def cajero_automatico(tarjeta, monto, clave):
    # Verificar saldo
    # Validar clave
    # Entregar dinero
    return "Transacción completada"
```

Una **función** es un bloque reutilizable de código que realiza una tarea específica, recibe entradas opcionales (parámetros) y devuelve un resultado (opcional). Las funciones te permiten **organizar**, **reutilizar** y **probar** tu código de forma más eficiente.

## Conceptos Clave (Versión Simplificada)

1. **Partes de una función**:
   - `def`: Palabra clave para definir
   - Nombre: Como llamarás a tu función
   - Parámetros: Datos que recibe (opcionales)
   - Cuerpo: Instrucciones que ejecuta
   - `return`: Lo que devuelve (opcional)

2. **¿Por qué son útiles?**
   - Evita repetir código
   - Organiza tu programa
   - Facilita encontrar errores
   - Permite reutilizar código

3. **Tu primera función**:
```python
def decir_hola():
    print("¡Hola mundo!")

# Llamando a la función
decir_hola()
```

---

## 2. ¿Por qué usar funciones?
**Beneficios clave**:
1. **Reducción de errores**: Al centralizar la lógica en un solo lugar
2. **Eficiencia**: Puedes llamar la función muchas veces sin repetir código
3. **Colaboración**: Diferentes programadores pueden trabajar en funciones separadas

**Analogía**:
> Las funciones son como los electrodomésticos en tu cocina: no necesitas saber cómo funciona internamente el microondas para calentar tu comida, solo necesitas saber usarlo.

* **Reutilización**: Escribes una vez, usas mil veces.
* **Legibilidad**: Fragmenta problemas grandes en piezas pequeñas y manejables.
* **Mantenibilidad**: Cambios localizados en una sola parte del código.
* **Pruebas**: Facilita las pruebas unitarias.

---

## 3. Sintaxis básica

**Anatomía de una función**:
1. `def`: Palabra clave que inicia la definición
2. `nombre_funcion`: Debe ser descriptivo y usar snake_case
3. `()`: Contienen los parámetros (pueden estar vacíos)
4. `:`: Indica el inicio del cuerpo de la función
5. Cuerpo: Sangrado con 4 espacios, contiene la lógica
6. `return` (opcional): Devuelve un valor al llamador

**Ejemplo completo**:
```python
def calcular_iva(precio, tasa=0.19):
    """Calcula el IVA de un producto.

    Args:
        precio (float): Valor base del producto
        tasa (float, optional): Porcentaje de IVA. Default 19%.

    Returns:
        float: Valor del IVA calculado
    """
    iva = precio * tasa
    return round(iva, 2)
```

```python
# Definición
def saludar(nombre):
    """Imprime un saludo personalizado."""
    print(f"¡Hola, {nombre}!")

# Llamada	saludar("Sebastián")
```

---

## 4. Parámetros y argumentos 
### 4.1 Posicionales

El orden importa.

```python
def resta(a, b):
    return a - b

resta(5, 2)  # Resultado: 3
```

Los argumentos se asignan en el orden declarado:
```mermaid
graph LR
  A[Llamada: func(1, 2)] --> B[Parámetro 1: a=1]
  A --> C[Parámetro 2: b=2]
```

### 4.2 Nombrados (keywords)

Especificas el nombre del parámetro para mayor claridad.

```python
resta(b=2, a=5)  # Resultado: 3
```

Mejora la legibilidad y permite cambiar el orden:
```python
# Mejor legibilidad aunque más verboso
resultado = resta(b=2, a=5)
```

### 4.3 Valores por defecto

```python
def potencia(base, exp=2):
    return base ** exp

potencia(3)      # 9 (cuadrado por defecto)
potencia(3, 3)   # 27
```

Se usan cuando no se provee el argumento:
```python
def conectar(servidor, puerto=5432, timeout=30):
    # puerto y timeout son opcionales
```

### 4.4 Parámetros variables \*args y \*\*kwargs

```python
def promedio(*numeros):
    return sum(numeros) / len(numeros)

promedio(1, 2, 3, 4)  # 2.5


def mostrar_info(**datos):
    for clave, valor in datos.items():
        print(f"{clave}: {valor}")

mostrar_info(nombre="Ana", edad=30)
```

**Casos de uso comunes**:
- Cuando el número de argumentos es desconocido
- Para crear wrappers de funciones
- Para pasar configuraciones flexibles

---

## 5. Valores de retorno

```python
def dividir(a, b):
    if b == 0:
        return None  # Evita división por cero
    return a / b
```

Puedes retornar múltiples valores con **tuplas**:

```python
def operaciones(a, b):
    return a + b, a - b, a * b, a / b

suma, resta, mult, div = operaciones(10, 2)
```

**Buenas prácticas**:
- Una función debería tener un solo tipo de retorno consistente
- Evitar retornar diferentes tipos en diferentes casos
- Documentar siempre el valor de retorno

**Patrón útil**: Retornar diccionarios para múltiples valores
```python
def analizar_texto(texto):
    return {
        'longitud': len(texto),
        'palabras': len(texto.split()),
        'mayusculas': sum(1 for c in texto if c.isupper())
    }
```

---

## 6. Ámbito (scope) de las variables

* **Local**: Solo existe dentro de la función.
* **Global**: Definida fuera de todas las funciones.

```python
x = "global"

def ejemplo():
    x = "local"
    print(x)  # local

print(x)  # global
```

> 💡 **Tip**: Evita modificar variables globales dentro de funciones; crea efectos secundarios difíciles de rastrear.

---

## 6. Ámbito de variables (Scope) - Profundización

**Jerarquía de alcances** (LEGB Rule):
1. **L**ocal: Dentro de la función
2. **E**nclosing: Funciones anidadas
3. **G**lobal: Módulo actual
4. **B**uilt-in: Python incorporado

**Ejemplo avanzado**:
```python
def exterior():
    mensaje = "exterior"
    
    def interior():
        nonlocal mensaje  # Accede al scope enclosing
        mensaje = "interior"
    
    interior()
    return mensaje

print(exterior())  # "interior"
```

---

## 7. Documentación de funciones (docstrings)

```python
def area_rectangulo(base: float, altura: float) -> float:
    """Calcula el área de un rectángulo.

    Args:
        base (float): Base del rectángulo.
        altura (float): Altura del rectángulo.

    Returns:
        float: Área calculada.
    """
    return base * altura
```

---

## 7. Documentación de funciones - Estándares

**Tipos de docstrings**:
1. **Una línea**: Breve descripción
   ```python
   def suma(a, b): """Suma dos números."""
   ```
2. **Multilínea (PEP 257)**:
   - Descripción
   - Args
   - Returns
   - Raises
   - Ejemplos

**Ejemplo completo**:
```python
def filtrar_pares(numeros):
    """Filtra números pares de una lista.
    
    Ejemplo:
        >>> filtrar_pares([1, 2, 3, 4])
        [2, 4]
    
    Args:
        numeros: Lista de números enteros
        
    Returns:
        Lista con solo los números pares
        
    Raises:
        TypeError: Si entrada no es lista
    """
    return [n for n in numeros if n % 2 == 0]
```

---

## 8. Buenas prácticas

| Práctica                       | Descripción                                          |
| ------------------------------ | ---------------------------------------------------- |
| **Nombre descriptivo**         | Usa verbos y sustantivos claros: `calcular_total()`. |
| **Un único propósito**         | Cada función debe hacer **una** cosa.                |
| **Docstrings**                 | Documenta qué hace, sus parámetros y retorno.        |
| **Evitar efectos colaterales** | No alteres variables globales inesperadamente.       |
| **Pequeñas y cohesivas**       | Si una función es muy larga, ¡divídela!              |
| **Tipado opcional**            | Añade anotaciones de tipo para mayor claridad.       |

---

## 8. Buenas prácticas - Principios SOLID para Funciones

### Single Responsibility Principle (SRP)
```python
# Mal
def procesar_usuario(usuario):
    # Valida, procesa, guarda y envía email
    ...

# Bien
def validar_usuario(usuario): ...
def guardar_usuario(usuario): ...
def enviar_email_bienvenida(usuario): ...
```

### Open/Closed Principle (OCP)
```python
def procesar_pago(metodo_pago):
    if isinstance(metodo_pago, Tarjeta):
        return procesar_tarjeta(metodo_pago)
    elif isinstance(metodo_pago, PayPal):
        return procesar_paypal(metodo_pago)
    # Difícil de extender

# Alternativa usando abstracción
def procesar_pago(metodo_pago):
    return metodo_pago.procesar()
```

### Liskov Substitution Principle (LSP)
```python
def calcular_area(figura):
    # Debe funcionar igual con cualquier subtipo
    return figura.area()
```

### Interface Segregation Principle (ISP)
```python
# En lugar de:
def operaciones_complejas(objeto):
    objeto.operacion_a()
    objeto.operacion_b()
    objeto.operacion_c()

# Mejor:
def operacion_especifica(objeto):
    objeto.operacion_a()
```

### Dependency Inversion Principle (DIP)
```python
# Acoplamiento directo (evitar)
def generar_reporte():
    db = MySQLConnection()
    ...

# Con dependencia inyectada
def generar_reporte(conexion_db):
    ...
```

**Checklist SOLID**:
- [ ] Cada función hace una sola cosa (SRP)
- [ ] Fácil de extender sin modificar (OCP)
- [ ] Comportamiento predecible en subtipos (LSP)
- [ ] No fuerza dependencias innecesarias (ISP)
- [ ] Depende de abstracciones, no implementaciones (DIP)

---

## 8. Buenas prácticas - Checklist

**✅ Lista de verificación**:
- [ ] Nombre sigue convención snake_case
- [ ] Hace una sola cosa (principio SRP)
- [ ] Menos de 20 líneas (ideal)
- [ ] No modifica variables globales
- [ ] Tiene docstring
- [ ] Parámetros con tipos opcionales
- [ ] Maneja errores adecuadamente

**Ejemplo refactorizado**:
```python
# Antes
def proc(datos):
    # Muchas cosas mezcladas
    ...

# Después
def validar_datos(datos): ...
def guardar_datos(datos): ...
def enviar_email_bienvenida(datos): ...
```

---

## 9. Funciones anónimas (`lambda`)

```python
cuadrado = lambda x: x ** 2
print(cuadrado(5))  # 25
```

Útiles para operaciones rápidas, aunque menos legibles que una función normal.

---

## 9. Funciones Lambda - Casos Reales

**Usos apropiados**:
1. **Ordenamiento personalizado**:
```python
usuarios = [{'nombre': 'Ana', 'edad': 30}, {'nombre': 'Luis', 'edad': 25}]
usuarios_ordenados = sorted(usuarios, key=lambda u: u['edad'])
```

2. **Pandas apply()**:
```python
import pandas as pd
df['doble'] = df['columna'].apply(lambda x: x * 2)
```

3. **Filtros rápidos**:
```python
mayores = filter(lambda edad: edad >= 18, edades)
```

---

## 10. Funciones de orden superior

Funciones que reciben otras funciones como argumentos o las devuelven.

```python
numeros = [1, 2, 3, 4]
cuadrados = list(map(lambda x: x**2, numeros))
pares = list(filter(lambda x: x % 2 == 0, numeros))
from functools import reduce
suma_total = reduce(lambda a, b: a + b, numeros)
```

---

## 10. Funciones de orden superior - Patrones

**Patrones comunes**:
1. **Decoradores**: Añaden comportamiento a funciones
2. **Map-Reduce**: Procesamiento de datos
3. **Callbacks**: Funciones que reciben otras funciones

**Ejemplo avanzado**:
```python
def retry(max_intentos):
    """Decorador para reintentar operaciones fallidas."""
    def decorador(func):
        def wrapper(*args, **kwargs):
            intentos = 0
            while intentos < max_intentos:
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    print(f"Intento {intentos} fallido: {e}")
                    intentos += 1
            raise Exception("Máximo de intentos alcanzado")
        return wrapper
    return decorador

@retry(3)
def conexion_api():
    # Lógica de conexión
    ...
```

---

## 11. Decoradores básicos

```python
def logger(func):
    def wrapper(*args, **kwargs):
        print(f"Llamando a {func.__name__}...")
        resultado = func(*args, **kwargs)
        print(f"{func.__name__} finalizó.")
        return resultado
    return wrapper

@logger
def saluda(nombre):
    print(f"Hola {nombre}")

saluda("Violeta")
```

---

## 11. Decoradores

**Concepto clave**:
Los decoradores son funciones que modifican el comportamiento de otras funciones, manteniendo su interfaz original.

**Patrones comunes**:
1. **Logging**: Registrar llamadas a funciones
2. **Caching**: Memorizar resultados costosos
3. **Validación**: Chequear parámetros
4. **Retry**: Reintentar operaciones fallidas

**Ejemplo avanzado (caching)**:
```python
from functools import lru_cache

@lru_cache(maxsize=100)
def fib(n):
    """Calcula Fibonacci con memoización"""
    return n if n < 2 else fib(n-1) + fib(n-2)
```

---

## 12. Anotaciones de tipo

```python
def concatenar(a: str, b: str) -> str:
    return a + b
```

Las anotaciones no son obligatorias pero mejoran la comprensión y el soporte de herramientas como *type checkers*.

---

## 12. Anotaciones de Tipo - Mejores Prácticas

**Ventajas**:
- Mejor documentación
- Soporte IDE (autocompletado)
- Detección temprana de errores

**Ejemplo completo**:
```python
from typing import Union, List, Dict

def procesar_items(
    items: List[Union[str, int]], 
    config: Dict[str, float]
) -> List[float]:
    """Procesa lista heterogénea según configuración."""
    return [float(item) * config.get('factor', 1.0) for item in items]
```

**Herramientas**:
- `mypy`: Type checker estático
- `typing`: Módulo estándar para tipos complejos

---

## 13. Manejo de errores en funciones

```python
def dividir_seguro(a: float, b: float) -> float:
    try:
        return a / b
    except ZeroDivisionError as e:
        print("Error: no se puede dividir por cero")
        raise e
```

---

## 13. Manejo de Errores - Estrategias

**Jerarquía recomendada**:
1. Manejar errores específicos
2. Proporcionar contexto útil
3. Preservar el stack trace original
4. Implementar backoff para errores transitorios

**Ejemplo robusto**:
```python
def descargar_url(url: str, intentos: int = 3) -> str:
    """Descarga contenido con reintentos automáticos."""
    import requests
    from time import sleep
    
    for i in range(intentos):
        try:
            respuesta = requests.get(url, timeout=5)
            respuesta.raise_for_status()
            return respuesta.text
        except requests.RequestException as e:
            if i == intentos - 1:
                raise RuntimeError(f"Fallo al descargar {url}") from e
            sleep(2 ** i)  # Backoff exponencial
```

---
