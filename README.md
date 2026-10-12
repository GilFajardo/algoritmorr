# AlgoritmoRR

Simulador de planificación **Round Robin (RR)** con interfaz gráfica en Java Swing.

El proyecto modela la ejecución de procesos por turnos usando un **quantum fijo** y muestra:

- Una tabla de procesos en cola/listos.
- Su estado durante la ejecución (`Listo`, `Procesando`, `Espera`, `Terminado`).
- Una tabla final con resumen de finalización.
- Un gráfico básico de bloques pintados por proceso.

## Análisis del proyecto

### Tipo de proyecto
- Aplicación de escritorio Java (Swing), creada con NetBeans.
- Sistema de build: **Ant** (archivo [build.xml](C:/Users/gilit/Downloads/AlgoritmoRR/build.xml)).
- Clase principal: [AlgoritmoRR.java](C:/Users/gilit/Downloads/AlgoritmoRR/src/algoritmorr/AlgoritmoRR.java).
- Ventana principal y lógica de simulación: [Simulador.java](C:/Users/gilit/Downloads/AlgoritmoRR/src/algoritmorr/Simulador.java).

### Configuración relevante
- Java source/target: **17** (ver [project.properties](C:/Users/gilit/Downloads/AlgoritmoRR/nbproject/project.properties)).
- Main class: `algoritmorr.AlgoritmoRR`.
- Dependencia de layout de NetBeans: `AbsoluteLayout` (presente en [dist/lib/AbsoluteLayout.jar](C:/Users/gilit/Downloads/AlgoritmoRR/dist/lib/AbsoluteLayout.jar)).

### Cómo funciona la simulación (según implementación actual)
1. Se selecciona un quantum con botones (`Q 1`, `Q 2`, `Q 5`).
2. Se agregan procesos con botones predefinidos (`Fornite`, `Steam`, `Visual Studio`, `Google`, `Word`, `Excel`).
3. Cada proceso se crea con ráfaga aleatoria entre 1 y 9.
4. Al iniciar, un hilo recorre la tabla aplicando Round Robin y descuenta ráfaga residual.
5. Se actualizan estado/tablas y se pinta un bloque por unidad de tiempo.

## Requisitos

- JDK 17 o superior.
- (Opcional) NetBeans para abrir/editar visualmente el formulario.
- (Opcional) Ant para compilar desde terminal.

## Ejecución rápida

### Opción 1: ejecutar el JAR ya generado
Desde la carpeta [dist](C:/Users/gilit/Downloads/AlgoritmoRR/dist):

```bash
java -jar AlgoritmoRR.jar
```

### Opción 2: compilar y ejecutar con Ant
Desde la raíz del proyecto:

```bash
ant clean
ant run
```

### Opción 3: ejecutar desde NetBeans
1. Abrir la carpeta del proyecto.
2. Verificar JDK 17.
3. Ejecutar el proyecto (`Run`).

## Uso del simulador

1. **Seleccionar quantum** (solo una vez por corrida, ver notas).
2. **Agregar procesos** usando los botones de aplicaciones.
3. Pulsar **Iniciar**.
4. Revisar:
   - Tabla de entrada (proceso y estado).
   - Tabla final (tiempo acumulado al terminar).
   - Panel gráfico de ejecución.

## Estructura

```text
AlgoritmoRR/
├─ src/algoritmorr/
│  ├─ AlgoritmoRR.java
│  ├─ Simulador.java
│  ├─ Simulador.form
│  └─ wallpaper.jpg
├─ nbproject/
├─ build.xml
├─ manifest.mf
└─ dist/
   ├─ AlgoritmoRR.jar
   └─ lib/AbsoluteLayout.jar
```

## Limitaciones observadas en la versión actual

- El quantum se fija solo si su valor inicial es 0; luego no se puede cambiar en ejecución.
- Cada botón de proceso se deshabilita tras un clic (cantidad limitada de procesos predefinidos).
- El hilo de simulación usa un ciclo continuo interno sin condición explícita de salida, por lo que puede seguir iterando incluso cuando ya no hay trabajo pendiente.
- El pintado gráfico se hace con `getGraphics()` directamente sobre el panel, lo que puede perderse ante repintados de la ventana.

## Mejoras recomendadas

- Definir una condición de término clara para detener el hilo al finalizar todos los procesos.
- Modelar procesos en una cola explícita RR en lugar de mutar filas directamente.
- Migrar el gráfico a `paintComponent(...)` con un modelo de datos de timeline.
- Permitir agregar procesos dinámicamente y cambiar/validar quantum de forma controlada.
- Agregar pruebas unitarias para la lógica de planificación separada de la UI.

