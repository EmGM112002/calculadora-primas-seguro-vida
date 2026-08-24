# Portafolio Actuarial — Proyecto 01
## Calculadora de Primas de Seguros de Vida

![Excel](https://img.shields.io/badge/Excel-217346?style=flat&logo=microsoft-excel&logoColor=white)
![VBA](https://img.shields.io/badge/VBA-867DB1?style=flat&logo=microsoft&logoColor=white)
![LaTeX](https://img.shields.io/badge/LaTeX-008080?style=flat&logo=latex&logoColor=white)
![Área](https://img.shields.io/badge/Área-Matemáticas%20Actuariales-1B3A6B?style=flat)
![Tabla](https://img.shields.io/badge/Tabla-CNSF%202000--2004-2E6DB4?style=flat)

---

## ¿De qué trata este proyecto?

Este modelo calcula **primas netas y brutas** de seguros de vida individuales aplicando
la teoría de contingencias de vida sobre la **Tabla de Mortalidad CNSF Experiencia 2000–2004**,
tabla estándar del mercado mexicano regulado por la Comisión Nacional de Seguros y Fianzas.

El objetivo del proyecto es doble: demostrar solidez en matemáticas actuariales
y habilidad técnica en las herramientas más utilizadas en el área de pricing de vida.

---

## Productos cubiertos

| Producto | Notación | Descripción |
|---|---|---|
| Seguro temporal a n años | $A^1_{x:\overline{n}\|}$ | Paga si el asegurado muere dentro del plazo |
| Seguro dotal puro a n años | $_nE_x$ | Paga si el asegurado sobrevive el plazo |
| Seguro dotal mixto | $A_{x:\overline{n}\|}$ | Paga en muerte o supervivencia, lo que ocurra primero |
| Seguro de vida entera | $A_x$ | Paga sin importar cuándo ocurra la muerte |

---

## Fundamento teórico

El modelo implementa tres pilares de las matemáticas actuariales:

### 1. Tabla de Mortalidad
Construida sobre la **CNSF Experiencia 2000–2004** con raíz $l_0 = 100{,}000$
y edad límite $\omega = 99$. Las funciones derivadas son:

$$_tp_x = \frac{l_{x+t}}{l_x} \qquad _tq_x = 1 - {_tp_x}$$

### 2. Valor Actual Actuarial (NSP)
Valor presente esperado de los beneficios futuros. Para el seguro temporal:

$$A^1_{x:\overline{n}|} = \sum_{k=0}^{n-1} v^{k+1} \cdot {_kp_x} \cdot q_{x+k}$$

Para vida entera, la suma cubre toda la vida remanente ($k = 0, \ldots, \omega - x - 1$).

### 3. Principio de Equivalencia
Determina la prima igualando el valor esperado de ingresos y egresos:

$$P = \frac{\text{SA} \cdot \text{NSP}}{\ddot{a}_{x:\overline{n}|}}
\qquad
G = \frac{\text{SA} \cdot \text{NSP} + \alpha \cdot \text{SA}}{(1 - \beta - \gamma)\cdot\ddot{a}_{x:\overline{n}|}}$$

donde $\alpha$, $\beta$, $\gamma$ son recargos por gastos de adquisición,
administración y cobranza respectivamente.

---

## Estructura del repositorio

```
Proyecto01_Excel_VBA/
│
├── Proyecto01_Calculadora_Primas_Vida.xlsm   # Modelo principal con macros
├── Proyecto01_Excel_VBA_Primas_de_Vida.tex   # Documento teórico en LaTeX
├── Proyecto01_Excel_VBA_Primas_de_Vida.pdf   # Documento compilado (opcional)
└── README.md
```

---

## Contenido del archivo Excel (.xlsm)

El libro está organizado en **6 hojas** con responsabilidades claramente separadas:

| Hoja | Función |
|---|---|
| `PORTADA` | Dashboard de entrada con instrucciones y convención de colores |
| `TABLA_MORT` | Tabla CNSF completa — 100 edades, funciones $l_x$, $d_x$, $q_x$, $p_x$, $_tp_x$ |
| `PARAMETROS` | Entradas del asegurado con validación de datos integrada |
| `CALCULO` | Motor actuarial — NSP, anualidades, primas neta y bruta (820 fórmulas) |
| `REPORTE` | Plantilla de cotización exportable a PDF |
| `CODIGO_VBA` | Código fuente de los módulos VBA visible para revisión |

### Convención de colores (estándar financiero)

- 🔵 **Texto azul** — Entradas que el usuario modifica
- ⚫ **Texto negro** — Fórmulas calculadas, no modificar
- 🟢 **Texto verde** — Fórmulas que referencian otra hoja del libro
- 🟡 **Fondo amarillo** — Supuesto clave que requiere revisión periódica

---

## Módulos VBA

```
modPrimas         →  Motor de cálculo: NSP, anualidades, primas por producto
modValidacion     →  Validación de entradas (5 reglas de negocio)
modReporte        →  Exportación automática a PDF con nombre dinámico
frmCalculadora    →  UserForm interactivo con 4 secciones y resultados en tiempo real
```

### UserForm — funcionalidades

- **SpinButton** sincronizado con el campo de edad (rango 15–85)
- **v** y **d** se actualizan en tiempo real al modificar la tasa técnica
- **Select Case** por tipo de producto — cada uno usa su NSP correcto
- Vida entera calculada directamente desde `TABLA_MORT` para cubrir toda la vida remanente sin limitarse al plazo ingresado
- Validación antes de calcular: edad, plazo, $\omega$, tasa, suma asegurada y condición $\beta + \gamma < 1$
- Exportación a PDF con nombre automático: `PRIMA_[Tipo]_[Edad]a_[Plazo]n_[Fecha].pdf`

---

## Cómo usar el modelo

**Requisitos:** Microsoft Excel con macros habilitadas (guardar como `.xlsm`)

```
1. Abrir el archivo y hacer clic en "Habilitar contenido"
2. Alt + F8  →  AbrirCalculadora  →  Ejecutar
3. Ingresar datos del asegurado en el UserForm
4. Clic en "CALCULAR" para obtener NSP, anualidad, prima neta y bruta
5. Clic en "GENERAR REPORTE PDF" para exportar la cotización
```

---

## Documento teórico

El archivo `.tex` contiene el marco teórico completo del modelo:

- Tablas de mortalidad y sus funciones actuariales
- Matemáticas del interés (v, d, interés compuesto)
- Valor Actual Actuarial para cada tipo de seguro
- Anualidades de vida temporaria *due* y su relación con los seguros
- Principio de equivalencia — prima neta y prima bruta con gastos
- Descripción de la arquitectura del modelo Excel y los módulos VBA

Para compilar el PDF localmente:

```bash
pdflatex Proyecto01_Excel_VBA_Primas_de_Vida.tex
pdflatex Proyecto01_Excel_VBA_Primas_de_Vida.tex   # segunda pasada para TOC
```

O abre el `.tex` directamente en [Overleaf](https://www.overleaf.com) (compilador: pdfLaTeX).

---

## Referencias

- Bowers, N. L. et al. (1997). *Actuarial Mathematics* (2nd ed.). Society of Actuaries.
- Dickson, D. C. M., Hardy, M. R., & Waters, H. R. (2020). *Actuarial Mathematics for Life Contingent Risks* (3rd ed.). Cambridge University Press.
- Comisión Nacional de Seguros y Fianzas (2006). *Tabla de Mortalidad Experiencia CNSF 2000–2004*. Diario Oficial de la Federación.
- Jordan, C. W. (1991). *Life Contingencies* (2nd ed.). Society of Actuaries.

---
