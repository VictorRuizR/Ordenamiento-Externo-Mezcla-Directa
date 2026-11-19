# Mezcla Directa en Java

Implementación en Java del algoritmo de ordenamiento externo Mezcla Directa (*Straight Merge*), realizada para la Unidad 5 de la materia de Estructura de Datos. El programa intercala dos archivos auxiliares que ya traen bloques ordenados y los une de forma ordenada en un archivo de salida, aplicando la lógica de archivos temporales y bloques de tamaño `L`.

## ¿Qué hace Mezcla Directa?

Mezcla Directa es un algoritmo de ordenamiento externo: se usa cuando los datos no caben completos en memoria y hay que trabajarlos por partes desde archivos en disco.

El proceso es el siguiente:

1. Los datos se reparten en archivos auxiliares (`f1.txt` y `f2.txt`), en bloques ordenados de tamaño `L`.
2. Se comparan frente a frente los primeros elementos de cada bloque.
3. El menor de los dos se escribe en el archivo de salida (`f3.txt`) y se avanza en ese archivo.
4. Cuando un bloque se acaba, se vacía lo que sobra del otro bloque.
5. El resultado es un archivo con los elementos de los dos bloques mezclados y ordenados.

En este proyecto, el método principal es `intercalarBloques(String archivoF1, String archivoF2, String archivoSalida, int L)`, en la clase `MezclaDirectaPractica`.

## ¿Cómo funciona `intercalarBloques`?

1. Abre los tres archivos con un `try-with-resources`: dos lectores (`BufferedReader`) para `f1.txt` y `f2.txt`, y un escritor (`PrintWriter`) para `f3.txt`. Los archivos se cierran solos al terminar.
2. Lee el primer número de cada archivo, que es el frente de cada bloque.
3. Lleva dos contadores, `elementosEscritos1` y `elementosEscritos2`, para saber cuántos números se han sacado del bloque actual de tamaño `L`.
4. Mientras ninguno de los dos archivos se haya quedado vacío, compara los dos frentes:
   - **Caso 1:** todavía quedan elementos por comparar en ambos bloques. Se convierten las líneas a enteros con `Integer.parseInt` y se escribe el menor en la salida.
   - **Caso 2:** el bloque de `f2.txt` ya se acabó (llegó a `L`), así que se vacía lo que sobró de `f1.txt`.
   - **Caso 3:** el bloque de `f1.txt` ya se acabó primero, así que se vacía lo que sobró de `f2.txt`.
5. Al terminar, imprime en consola `Bloque intercalado con exito!`.
6. Si `f1.txt` o `f2.txt` no existen antes de correr el programa, se atrapa la `IOException` y se imprime `Error en E/S de archivos:` con el mensaje del error.

## Las partes completadas

El código base traía tres partes para completar en `intercalarBloques`, y son las que se completaron:

**1: condición para saber si el número de F1 es menor o igual al de F2**

```java
if (val1 <= val2) {
```

**2: si el menor fue el de F2, hacer lo mismo pero con F2**

```java
escritor.println(val2);
linea2 = lector2.readLine();
elementosEscritos2++;
```

**3: vaciar el elemento restante de F2**

```java
escritor.println(linea2);
linea2 = lector2.readLine();
elementosEscritos2++;
```

Además, se agregaron dos ajustes marcados en el código, porque sin ellos el programa perdía datos: cuando los dos bloques de tamaño `L` ya se terminaron, los contadores se reinician para empezar el siguiente par de bloques, y al final se vacía lo que quedó en el otro archivo cuando uno de los dos se acaba. Sin ese vaciado final, el `45` se perdería y `f3.txt` quedaría solo con el `12`.

## Ejemplo

Los archivos de entrada son los del ejemplo del maestro, con un número por renglón:

- `f1.txt`: `45`
- `f2.txt`: `12`
- Tamaño de bloque: `L = 1`

El programa compara `45` con `12`, escribe primero el `12` y después el `45` que quedó, así que el archivo de salida es:

- `f3.txt`:
  ```text
  12
  45
  ```

## Estructura del proyecto

```text
├── MezclaDirectaPractica.java
├── f1.txt
├── f2.txt
└── README.md
```

- `MezclaDirectaPractica.java`: contiene el método `intercalarBloques(String archivoF1, String archivoF2, String archivoSalida, int L)` y el método `main`, que llama a `intercalarBloques("f1.txt", "f2.txt", "f3.txt", 1)`.
- `f1.txt`: archivo auxiliar con el número `45`.
- `f2.txt`: archivo auxiliar con el número `12`.
- `f3.txt`: archivo de salida generado por el programa, con `12` y `45` ya ordenados.
- `README.md`: este archivo.

## Requisitos

- Java Development Kit (JDK) instalado.
- IntelliJ IDEA u otro editor, o bien una terminal para compilar desde la línea de comandos.

## Cómo clonar, configurar y ejecutar

### 1. Clonar el repositorio

```bash
git clone <url-del-repositorio>
cd <nombre-del-repositorio>
```

### 2. Configurar los archivos de entrada

Antes de darle Run, crea o verifica que en la carpeta raíz del proyecto existan `f1.txt` y `f2.txt`, con un número por renglón. En este repositorio ya vienen incluidos:

- `f1.txt` con `45`
- `f2.txt` con `12`

Si no existen esos archivos antes de correr el programa, el programa lanzará la excepción de lectura de archivos y mostrará `Error en E/S de archivos:` en consola.

### 3. Ejecutar desde IntelliJ IDEA

1. Abre el proyecto en IntelliJ IDEA.
2. Localiza la clase `MezclaDirectaPractica`.
3. Ejecútala con el botón de ejecución junto a su método `main` o con **Run**.

### 4. Ejecutar desde la terminal

Desde la carpeta que contiene `MezclaDirectaPractica.java`, `f1.txt` y `f2.txt`:

```bash
javac MezclaDirectaPractica.java
java MezclaDirectaPractica
```

## Salida en consola

Al ejecutar el programa, la salida en consola es exactamente:

```text
Bloque intercalado con exito!
```

El programa termina con código de salida 0 y genera el archivo `f3.txt` con el siguiente contenido:

```text
12
45
```

## Autor

- **Autor:** Victor Ruiz Ruiz
- **Número de control:** C257O04133
- **Docente:** Víctor Hugo Vásquez Herrera
- **Materia:** Estructura de Datos (AED-1026) — Unidad 5
- **Instituto:** Instituto Tecnológico Superior de Xalapa
- **Carrera:** Ingeniería en Sistemas Computacionales
