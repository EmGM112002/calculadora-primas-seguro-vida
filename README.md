# Calculadora de Primas de Seguro de Vida

![Excel](https://img.shields.io/badge/Excel-217346?style=flat&logo=microsoft-excel&logoColor=white)
![VBA](https://img.shields.io/badge/VBA-867DB1?style=flat)
![Área](https://img.shields.io/badge/Área-Matemáticas%20Actuariales-1B3A6B?style=flat)
![Ramo](https://img.shields.io/badge/Ramo-Seguro%20de%20Vida-2E6DB4?style=flat)

Herramienta actuarial desarrollada en **Microsoft Excel y VBA** para automatizar el cálculo de primas de diferentes productos de seguro de vida individual.

La calculadora integra una tabla de mortalidad, parámetros actuariales, validaciones de entrada y automatización mediante macros para transformar un procedimiento matemático de tarificación en una herramienta interactiva y reproducible.

El desarrollo matemático y conceptual completo se encuentra en el documento teórico incluido en el repositorio.

---

## 1. Problema actuarial

La tarificación de un seguro de vida requiere combinar información biométrica y financiera para determinar una prima consistente con las obligaciones esperadas del contrato.

El problema consiste en automatizar el cálculo de primas para distintos productos de vida considerando variables como:

- edad del asegurado;
- suma asegurada;
- duración del contrato;
- tasa de interés;
- mortalidad;
- tipo de producto;
- y parámetros de recargo utilizados para obtener la prima bruta.

El objetivo es reducir la ejecución manual de cálculos actuariales y permitir que distintos escenarios puedan evaluarse desde una misma interfaz.

La herramienta contempla los siguientes productos:

- **Seguro temporal a `n` años**;
- **Seguro dotal puro a `n` años**;
- **Seguro dotal mixto**;
- **Seguro de vida entera**.

---

## 2. Metodología

La herramienta organiza el proceso de cálculo en diferentes componentes dentro del libro de Excel.

El flujo general es:

1. Seleccionar el producto de seguro de vida.
2. Capturar los datos del asegurado y los parámetros financieros.
3. Consultar las probabilidades biométricas correspondientes a la edad seleccionada.
4. Calcular los valores actuariales necesarios para el producto.
5. Determinar la prima neta correspondiente al riesgo asegurado.
6. Incorporar los parámetros de recargo definidos en la herramienta para obtener la prima bruta.
7. Validar automáticamente la consistencia de los datos de entrada.
8. Mostrar los resultados dentro del libro.
9. Permitir la generación de un reporte mediante las macros implementadas.

La lógica de cálculo se distribuye entre fórmulas de Excel y procedimientos desarrollados en VBA.

### Productos implementados

| Producto | Horizonte |
|---|---|
| Seguro temporal | Plazo determinado |
| Dotal puro | Plazo determinado |
| Dotal mixto | Plazo determinado |
| Vida entera | Vitalicio |

### Validaciones implementadas

La herramienta incorpora controles para detectar entradas inconsistentes antes de ejecutar la cotización, incluyendo:

- rangos de edad;
- plazo del seguro;
- edad límite de la tabla de mortalidad;
- tasa de interés;
- suma asegurada;
- y consistencia de los parámetros de recargo.

---

## 3. Datos utilizados

La base biométrica utilizada corresponde a la **Tabla de Mortalidad CNSF Experiencia 2000–2004**, incorporada directamente dentro del libro de Excel.

La tabla contiene las variables necesarias para construir las probabilidades utilizadas en los cálculos actuariales, incluyendo elementos como:

- edad;
- sobrevivientes;
- fallecimientos;
- probabilidad de fallecimiento;
- probabilidad de supervivencia.

La herramienta utiliza esta información para evaluar los beneficios contingentes asociados con cada producto.

No se utilizan datos personales reales de asegurados. Los parámetros de cotización son ingresados por el usuario de la calculadora para cada escenario.

---

## 4. Herramientas

| Herramienta | Aplicación |
|---|---|
| **Microsoft Excel** | Motor de cálculo, almacenamiento de la tabla biométrica y presentación de resultados |
| **VBA** | Automatización de procesos, validaciones, interfaz y generación de reportes |
| **Fórmulas de Excel** | Construcción de factores financieros y actuariales |
| **UserForm** | Captura interactiva de parámetros de cotización |

La solución fue diseñada como un libro habilitado para macros (`.xlsm`) para integrar los cálculos actuariales con una interfaz de usuario.

---

## 5. Resultados

La herramienta permite calcular de forma automatizada primas para los cuatro productos de seguro de vida implementados.

Entre sus principales resultados y funcionalidades se encuentran:

- cálculo de prima neta;
- cálculo de prima bruta;
- evaluación de diferentes edades y plazos;
- actualización de factores financieros ante cambios en la tasa de interés;
- selección del producto desde una interfaz gráfica;
- validación automática de parámetros;
- consulta de la tabla de mortalidad;
- y generación de un reporte desde el libro de Excel.

La implementación permite concentrar en una sola herramienta el flujo que va desde la captura de los supuestos hasta la presentación del resultado de la cotización.

---

## 6. Aprendizajes y limitaciones

### Aprendizajes

El proyecto permite demostrar de forma práctica:

- aplicación de matemáticas actuariales de vida;
- utilización de tablas de mortalidad;
- construcción de primas para diferentes beneficios contingentes;
- automatización de cálculos mediante VBA;
- diseño de controles de validación;
- creación de interfaces en Excel;
- separación entre parámetros, cálculos y presentación;
- y transformación de un modelo actuarial en una herramienta operativa.

### Limitaciones

La herramienta constituye una implementación académica y de portafolio. Entre sus principales limitaciones se encuentran:

- utiliza una única tabla de mortalidad;
- los supuestos biométricos son estáticos;
- la tasa de interés se considera bajo la estructura definida en el modelo;
- no incorpora modelos de decrementos múltiples;
- no modela cancelaciones o rescates;
- no incorpora selección médica ni segmentación adicional del riesgo;
- no constituye una nota técnica registrada;
- no incorpora todos los gastos, márgenes, impuestos, costos de capital o restricciones comerciales que podrían intervenir en una tarifa real;
- y no pretende sustituir los procesos de tarificación, suscripción o aprobación de una aseguradora.

Por lo anterior, las primas obtenidas deben interpretarse como resultados de un **modelo actuarial demostrativo**, no como cotizaciones comerciales.

---

## 7. Contenido del repositorio

```text
calculadora-primas-seguro-vida/
├── Calculadora_Primas_Vida.xlsm          # Calculadora actuarial en Excel y VBA
├── Calculadora_de_Primas_de_Vida.pdf     # Documentación matemática y actuarial
└── README.md                             # Descripción ejecutiva del proyecto
```

---

## 8. Documentación técnica

El desarrollo matemático, los fundamentos actuariales y la explicación detallada de los productos se encuentran en:

**[`Calculadora_de_Primas_de_Vida.pdf`](./Calculadora_de_Primas_de_Vida.pdf)**

El README funciona como una presentación ejecutiva de la herramienta y evita duplicar el contenido teórico disponible en dicho documento.

---

## 9. Cómo ejecutar el proyecto

### Requisitos

- Microsoft Excel de escritorio;
- soporte para libros habilitados para macros;
- macros de VBA habilitadas.

### Ejecución

1. Clonar o descargar el repositorio.
2. Abrir `Calculadora_Primas_Vida.xlsm`.
3. Habilitar el contenido y las macros cuando Excel lo solicite.
4. Abrir la calculadora mediante la macro correspondiente.
5. Seleccionar el producto.
6. Introducir la edad, suma asegurada, plazo y demás parámetros requeridos.
7. Ejecutar el cálculo.
8. Revisar las primas y resultados generados.
9. Utilizar la opción de reporte cuando sea necesario.

> **Seguridad:** únicamente deben habilitarse macros cuando el archivo provenga de una fuente conocida y haya sido revisado previamente.

---

## Autor

**Emiliano Guillén Medina**  
Licenciatura en Actuaría  
[GitHub](https://github.com/EmGM112002) · [LinkedIn](https://www.linkedin.com/in/emgm11)
