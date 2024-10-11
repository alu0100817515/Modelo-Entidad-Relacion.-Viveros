# Modelo Entidad/Relación. Viveros.

## Miembros
1. Laura Álvarez Zamora **alu0101349824@ull.edu.es**
2. Pablo Fernández Herrera **alu0100817515@ull.edu.es**
---
## Descripción de las Entidades

1. **Empleado**
   - **Descripción:** Representa a los trabajadores de la empresa, quienes pueden desempeñar funciones como horticultors o vendedores.
   - **Atributos:**
     - `DNI` (Identificador): Número de identificación único del empleado. Ejemplo: `12345678X`.
     - `Nombre` (Descriptor): Nombre completo del empleado. Ejemplo: `Juan Pérez`.
     - `Productividad` (Calculado): Métrica calculada basada en los resultados de trabajo del empleado, como la cantidad de productos vendidos o tareas completadas en un periodo determinado. Ejemplo: 30 productos/hora.
     - `Historial` (Multivaluado y Compuesto): Registro de las asignaciones del empleado en distintos viveros y zonas en diferentes fechas. Ejemplo: El empleado trabajó en el vivero "Vivero Norte" en la zona "Exterior" el 01/01/2024.
         - **Atributos:**
           - Vivero (Descriptor): Vivero en el que trabaja el empleado. Ejemplo: "Vivero Norte".
           - Fecha (Descriptor): Fecha en la que se realizó el historial. Ejemplo: 01/01/2024.
           - Zona (Descriptor): Área específica dentro de un vivero donde trabaja el empleado. Ejemplo: Zona "Exterior".

2. **Horticultor**
   - **Descripción:** Entidad débil que representa a un empleado que trabaja en un vivero.

3. **Vendedor**
   - **Descripción:** Entidad débil que representa a un empleado que vende productos.
   - **Atributos:**
     - `Pedidos que gestiona a Tajinaste Plus` (Descriptor): Cantidad de pedidos que gestiona a Tajinaste Plus. Ejemplo: `15`.

4. **Vivero**
   - **Descripción:** Lugar físico donde se almacenan y venden los productos de la empresa.
   - **Atributos:**
     - `Código` (Identificador): Código único del vivero. Ejemplo: `VIV001`.
     - `Productividad` (Calculado): Índice de rendimiento del vivero basado en las ventas y la cantidad de productos manejados. Ejemplo: 30 productos/hora.
     - `Georreferencia` (Descriptor): Coordenadas del vivero. Ejemplo: `28.4682, -16.2546`.
         - **Atributos:**
           - Longitud (Descriptor): Es la distancia en grados desde cualquier punto de la Tierra hasta el meridiano de Greenwich, medida hacia el este o el oeste (horizontal). Ejemplo: `28.4682`.
           - Latitud (Descriptor): Es la distancia en grados desde cualquier punto de la Tierra hasta el ecuador, medida hacia el norte o el sur (vertical). Ejemplo: `-16.2546`.

5. **Zona**
   - **Descripción:** Área específica dentro de un vivero, como un almacén o una sección exterior.
   - **Atributos:**
     - `Código` (Identificador): Código único de la zona. Ejemplo: `ZON001`.
     - `Nombre` (Descriptor): Descripción de la zona. Ejemplo: `Almacén`.
     - `Productividad` (Calculado): Índice de productividad calculado en función del número de productos gestionados en la zona. Ejemplo: 30 productos/hora.
     - `Georreferencia` (Descriptor): Coordenadas del vivero. Ejemplo: `28.4682, -16.2546`.
         - **Atributos:**
           - Longitud (Descriptor): Es la distancia en grados desde cualquier punto de la Tierra hasta el meridiano de Greenwich, medida hacia el este o el oeste (horizontal). Ejemplo: `28.4682`.
           - Latitud (Descriptor): Es la distancia en grados desde cualquier punto de la Tierra hasta el ecuador, medida hacia el norte o el sur (vertical). Ejemplo: `-16.2546`.

6. **Producto**
   - **Descripción:** Bien que se ofrece a la venta, como plantas o herramientas de jardinería.
   - **Atributos:**
     - `Código` (Identificador): Código único del producto. Ejemplo: `PROD001`.
     - `Stock` (Descriptor): Cantidad disponible del producto en inventario. Ejemplo: `50 unidades`.
     - `Precio` (Descriptor): Precio de venta del producto. Ejemplo: `15.99 EUR`.
     - `Disponibilidad` (Descriptor): Indicación de si el producto está disponible para la venta. Ejemplo: `Disponible`, `Agotado`.

7. **Cliente**
   - **Descripción:** Persona que realiza compras en Tajinaste S.A.
   - **Atributos:**
     - `DNI` (Identificador): Número de identificación único del cliente. Ejemplo: `87654321Y`.
     - `Nombre` (Descriptor): Nombre completo del cliente. Ejemplo: `María González`.
     - `Pedidos` (Multivaluado y Compuesto): Registro de la cantidad de pedidos realizados por el cliente en diferentes momentos. Ejemplo: `5 pedidos en el año 2024`.
         - **Atributos:**
           - Importe (Calculado): Precio del pedido calculado a partir del precio de venta del producto multiplicuado por la cantidad del mismo. Ejemplo: `15.99 * 5 = 79.95 EUR`.
           - Fecha (Descriptor): Fecha en la que se realizó el pedido. Ejemplo: 01/01/2024.
           - Producto (Descriptor): Nombre del bien que se ofrece a la venta. Ejemplo: `Geranios`.
           - Cantidad (Descriptor): Es el número de pedidos vendidos de un producto. Ejemplo: `5`.

8. **Fidelizado**
   - **Descripción:** Entidad débil que representa a los clientes que forman parte del programa "Tajinaste Plus".
   - **Atributos:**
     - `Bonificaciones` (Calculado): Valor de las bonificaciones acumuladas en función de las compras realizadas. Ejemplo: `30 EUR`.
    
9. **Sin fidelizar**
   - **Descripción:** Entidad débil que representa a los clientes que no forman parte del programa "Tajinaste Plus".

## Relaciones

1. **Empleado - Horticultor**
   - **Descripción:** Un empleado puede desempeñar el rol de horticultor. Es una jerarquía solapada y total, un empleado puede ser simultáneamente horticultor y otro rol, como vendedor, y todos los empleados deben pertenecer al menos a un subtipo.
   - **Cardinalidad:** (1,1) - (0,1). Esto significa que cada empleado debe ser al menos un horticultor o cumplir con otro rol, pero no todos los horticultors tienen que estar asignados continuamente.
   - **Ejemplo:** Juan Pérez trabaja como horticultor durante ciertos periodos, pero también puede cumplir con otras funciones dentro de la empresa.
   - **Atributos:**
     - Función (Descriptivo): Indica el tipo de empleado. Ejemplo: `Horticultor`.

2. **Empleado - Vendedor**
   - **Descripción:** Un empleado puede desempeñar el rol de vendedor. Es una jerarquía solapada y total, un empleado puede ser simultáneamente vendedor y otro rol, como horticultor, y todos los empleados deben pertenecer al menos a un subtipo.
   - **Cardinalidad:** (1,1) - (0,1). Esto significa que cada empleado debe ser al menos un vendedor o cumplir con otro rol, pero no todos los vendedor tienen que estar asignados continuamente.
   - **Ejemplo:** Juan Pérez trabaja como vendedor durante ciertos periodos, pero también puede cumplir con otras funciones dentro de la empresa.
   - **Atributos:**
     - Función (Descriptivo): Indica el tipo de empleado. Ejemplo: `Vendedor`.

3. **Vivero - Zona**
   - **Descripción:** Un vivero puede estar dividido en varias zonas (1:N), y cada zona pertenece a un único vivero (1:1).
   - **Ejemplo:** El "Vivero Norte" tiene las zonas "Almacén" y "Exterior".
  
4. **Horticultor - Vivero - Zona**
   - **Descripción:** Un horticultor está destinado a un vivero y a una zona de ese vivero en una época del año.
       - **Atributos:**
         - `Época del año` (Descriptor): Periodo de tiempo en el que se asigna al horticultor a un vivero. Ejemplo: `Primavero, verano, otoño, invierno`.
       - **Restricción semántica:**
         - Un empleado nunca puede tener dos destinos en la misma época del año.
         - La zona en la que trabaja un empleado debe pertenecer al vivero en el que está destinado.
   - **Ejemplo:** El horticultor Juan Pérez está destinado al "Vivero Norte" en las zonas "Almacén" y "Exterior" en "primavera".

5. **Zona - Producto**
   - **Descripción:** Ninguno o varios productos pueden estar presentes en varias zonas (0:N), y una zona puede contener varios productos (1:N).
   - **Ejemplo:** La planta "Ficus" se encuentra tanto en la zona "Exterior" como en el "Invernadero".

6. **Producto - Cliente**
   - **Descripción:** Ninguno o varios productos pueden ser comprados por varios clientes (0:N) y un cliente puede comprar varios productos (1:N).
   - **Ejemplo:** María González compró una "Planta Ficus" y una "Maceta de cerámica".

7. **Cliente - Fidelizado**
   - **Descripción:** La relación indica que un cliente puede estar fidelizado o no, pero no ambas simultáneamente.
   - **Cardinalidad:** (1,1) - (0,1). Exclusiva y parcial: Un cliente puede estar fidelizado, pero no todos los cliente tienen que estarlo. La exclusividad indica que un cliente no puede estar simultáneamente fidelizado y no fidelizado.
   - **Ejemplo:** Juan Pérez está fidelizado en el programa "Tajinaste Plus".
   - **Atributos:**
     - Forma parte del programa Tajinaste Plus (Descriptivo): Indica si el cliente está fidelizado. Ejemplo: `Fidelizado`.

8. **Cliente - Sin fidelizar**
   - **Descripción:** La relación indica que un cliente puede estar no fidelizado o sí estarlo, pero no ambas simultáneamente.
   - **Cardinalidad:** (1,1) - (0,1). Exclusiva y parcial: Un cliente puede estar fidelizado, pero no todos los cliente tienen que estarlo. La exclusividad indica que un cliente no puede estar simultáneamente fidelizado y no fidelizado.
   - **Ejemplo:** Juan Pérez no está fidelizado en el programa "Tajinaste Plus".
   - **Atributos:**
     - Forma parte del programa Tajinaste Plus (Descriptivo): Indica si el cliente está fidelizado. Ejemplo: `No fidelizado`.

## Restricciones semánticas

1. Un empleado nunca puede tener dos destinos en la misma época del año.
2. La zona en la que trabaja un empleado debe pertenecer al vivero en el que está destinado.
