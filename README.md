# Calculadora de Costos Soldemi

Página web de una sola pieza para costear el inventario de Soldemi: se carga el
export de inventario en Excel y sale el listado con el PDV con descuento, la
utilidad y la comparación contra el costo de la competencia.

**Usar:** <https://dibasafioficina-lang.github.io/calculadora-costos-soldemi/>

También funciona sin servidor: descargá `index.html` y abrilo con doble clic.

## Qué hace

Del archivo lee estas seis columnas, por nombre de encabezado y, si el
encabezado cambiara, por posición (B, D, E, G, J y K):

| Columna | |
|---|---|
| `Item Number` | código de barras |
| `Nombre` | descripción del producto |
| `Marca` | |
| `InStock` | unidades |
| `Costo Prom. Nac.` | costo |
| `Precio Base` | precio de venta sin descuento |

Y agrega cinco columnas calculadas:

```
PDV con desc  = Precio Base × (1 − % desc)     ← 30% por defecto, editable
Utilidad      = PDV con desc − Costo Prom. Nac.
% Utilidad    = Utilidad ÷ PDV con desc
Dif. vs PDV   = Costo competencia − PDV con desc
```

`Costo competencia` es un campo que se llena a mano en cada fila. En la
diferencia, **verde** significa que la competencia está por encima de tu PDV
—tenés el precio más bajo— y **rojo** que está por debajo.

Además: buscador, filtro por marca, vistas por stock / comparados / alertas,
orden por cualquier columna, y exportación a Excel de lo que estés viendo
filtrado.

## Alertas

- **Barra roja** — costo en cero o negativo, o utilidad por debajo de cero.
- **Barra ámbar** — sin precio base cargado, o sin stock.

## Privacidad

Todo el procesamiento ocurre en el navegador. El archivo de inventario nunca
se sube a ningún servidor y la página no guarda nada: al cerrarla se pierden
los costos de competencia que hayas tipeado, así que exportá a Excel antes de
salir.

## Cómo está hecho

Un único `index.html` sin build ni dependencias que instalar. La lectura y
escritura de Excel usa [SheetJS](https://sheetjs.com) desde CDN; el resto es
HTML, CSS y JavaScript sin frameworks.
