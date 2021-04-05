# Trabajo Docker
## Capítulos 1,2,3
En estos 3 capítulos te introducen al curso de docker

## Capítulos 4,5,6
Las bases de datos almacenan y organizan los datos.

Se pueden llamar RDBMS. 

Debes elegir las RDBMS que se adapten a tus necesidades, por ejemplo con interfaz gráfica o sin interfaz gráfica

## Capítulo 7
Tiene 2 partes el que gestiona y el que almacena los datos.

## Capítulo 8
Los RDBMS ofrecen al cliente los datos que necesite.

## Capítulo 9
Vas a la página docker.com y instalas el docker adecuado para tu dispositivo.
En tu ordenador vas a descargas y ejecutas el iniciador de docker.

## Capítulo 10
Comandos de docker en el txt

 Microsoft SQL docker run --name SQLServer2019 -e "ACCEPT_EULA=Y" -E"SA_PASSWORD=Adam123456" -p 1404:1433 -d  -latest

 Postgre SQL docker run --name postgresql -p 5401:5432 -e postgres_PASSWORD=Adam123456 -d 

## Capítulo 11
Para microsoft sql usa este comando-it sqlserver2019 bash Ahora estas entro del contenedor /opt/mssql-tools/bin/sqlcmd -U sa -P Adam123456 
Asi se crea una base de tados :CREATE DATABASE mytestdb GO 

## Capítulos 12,13
Objetivo: crear un container 
Solucion en el bloc de notas de ayuda
View all runing containers docker ps

Stop a container docker stop MySecondSQLServer

View all containers docker ps -a

 Start a container docker start MySecondSQLServer

 Remove a container docker rm MySecondSQLServer

## Capítulo 14
Hay distintas interfaces gráficas para docker

## Capítulo 15
Para instalar azure data studio vas a la pagina y escoges el mas adecuado para tu dispositivo

## Capítulos 16,17
Azure data studio puedes configurarlo a tu gusto, sigue los pasos del video y conseguiras tenerlo a tu gusto

## Capítulo 18
Vete a ajustes y cambia el tab color, para que se muestre como una interfaz de comando 
Para hacer consultas en azure data studio haremos consultas con lenguaje sql

## Capítulo 19,20

Objetivo crear bases de datos kineteco como dicta en el video
Solucion :
MacOS & Linux: docker run --name kineteco -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Adam123456' -p 1411:1433 -d 
Connect in Azure Data Studio with the following settings Connection type: Microsoft SQL Server Server name: localhost User name: SA Password: Adam123456 Remember passowrd: checked Server group: SQL Server Name: KinetEco Advanced - Port: 1411

Create the database in a new query window CREATE DATABASE KinetEco;

## Capítulo 21
En docker hay 2 tipos de comandos DDL y DML

## Capítulos 22,23
Haz click derecho sobre data bases y crea una nueva consulta, sigue los pasos que indica en el video. Igual para postgueSQL

Para empezar a crear una base de datos debes tener en cuenta todos los datos 

## Capítulo 24
Abre el archivo de ayuda con calc o excel a partir de este archivo haremos consultas y crearemos tablas
`CREATE TABLE products.products ( SKU CHAR(7) NOR NULL PRIMARY KEY, ProductName CHAR(50) NOT NULL, CategoryID INT, Size INT, Price DECIMAL(5,2) NOT NULL ); En POSTGRESQL es exactamente igual
`
Este es el comando que usa para crear una tabla como en el video
## Capítulo 25
Comando crear tabla:

`CREATE TABLE products.categories ( CategoryID INt PRIMARY KEY, CategoryDescription CHAR(50) )`

## Capítulo 26
""estas comillas se usan para hacer referencia a nombres y datos de la tabla 


## Capítulos 27,28
Ojetivo crear una tabla llamada HumanResources 
Solucion:

`CREATE SCHEMA HumanResources;`

`CREATE TABLE HumanResources.Employees ( EmployeeID INT NOT NULL PRIMARY KEY, FirstName CHAR(50) NOT NULL, LastName CHAR(50) NOT NULL, Department CHAR(20) NOT NULL, HireDate DATE NOT NULL );`

## Capítulo 29
Las tablas tienen columnas y filas 

## Capítulo 30

Usa este comando dl video para añadir valores en la tabla

`INSERT INTO products.products VALUES ('FCP008', 'First Cold Press', 1, 8, 8.99);`

`INSERT INTO products.products VALUES ('BI008', 'Basil-Infused EVO', 2, 8, 10.99), ('GI016', 'Garlic-Infused EVO', 2, 16, 15.99);`

`Add rows by specifying columns`

`INSERT INTO products.products (SKU, ProductName, Price) VALUES ('OGEC004', 'Olive Glow Eye Cream', 18.99);`

## Capítulos31,32
Comando para modificar valores

`UPDATE products.products SET CategoryID = 3, Size = 4 WHERE SKU = 'OGEC004';`

Eliminar fila

`DELETE FROM products.products WHERE SKU = 'OGEC004';`

Presiona la x de cerrar y sal guardando todos los comandos, se guardara donde tu le mandes por ejemplo el excritorio en un bloc de notas.

## Capítulos 33,34,35
Vamos añadir datos a la tabla kineteco
En los videos se mostraran los comandos pertinentes

Como dije anteriormente seguiremos unsando lenguaje sql para hacer consultas

## Capítulo 36
Eliminar todas las filas 
`DELETE FROM products.products;`

Agregar datos a la tabla
`INSERT INTO products.products (SKU, ProductName, CategoryID, Size, Price)`

## Capítulos 37,38,39,40,41,42,43,44,45,46,47
En estos videos explicara como hacer consultas con sql, a continuacion pondre todo los comandos utilizados por el para dichas consultas
_____
`-- Renaming columns in the result set with the AS keyword
-- Exercise Files > Chapter 7 > AS_Start.sql
SELECT p.ProductName "Product Name",
    p.Size "Size (Ounces)",
    p.SKU "Product SKU",
    p.Price "Price (US Dollars)",
    c.CategoryDescription "Category Description",
    c.ProductLine "Product Line"
FROM products.products p
    JOIN products.categories c
        ON p.CategoryID = c.CategoryID`
;`
____
`-- Modify data with built-in functions
-- Exercise Files > Chapter 7 > Functions_Start.sql
SELECT Price
FROM products.products;`

`-- View statistical information about pricing
SELECT
    MAX(Price) AS "Maximum Price",
    MIN(Price) AS "Minimum Price",
    ROUND(AVG(Price), 2) AS "Average Price"
FROM products.products;`

`-- Find the products with the highest price
SELECT MAX(Price)
FROM products.products;`

`SELECT ProductName, Size, Price
FROM products.products
WHERE Price = 
    (SELECT MAX(Price)
     FROM products.products
    )`
;
_____
`-- Group data based on common attribute values
-- Exercise Files > Chapter 7 > GroupBy_Start.sql
SELECT
    categories.CategoryDescription,
    COUNT(products.SKU) AS "Number of SKUs",
    MAX(products.Price) AS "Maximum Price",
    MIN(products.Price) AS "Minimum Price",
    AVG(products.Price) AS "Average Price"
FROM products.products
    JOIN products.categories
    ON products.CategoryID = categories.CategoryID
GROUP BY CategoryDescription
ORDER BY COUNT(products.SKU) DESC
;`
_____
`-- Group data based on common attribute values
-- Exercise Files > Chapter 7 > GroupBy_Start.sql
SELECT
    categories.CategoryDescription,
    products.SKU
FROM products.products
    JOIN products.categories
    ON products.CategoryID = categories.CategoryID
;`
_____
`-- Filter groups with HAVING
-- Exercise Files > Chapter 7 > Having_Start.sql
SELECT categories.CategoryDescription,
    COUNT(products.SKU) AS "Number of SKUs"
FROM products.products
    JOIN products.categories
    ON products.CategoryID = categories.CategoryID
WHERE products.Price > 15
GROUP BY CategoryDescription
--HAVING CategoryDescription = 'Olive Oils'
--HAVING NOT CategoryDescription = 'Bath and Beauty'
HAVING COUNT(products.SKU) < 10
ORDER BY COUNT(products.SKU) DESC
;`
_____
`-- Filter groups with HAVING
-- Exercise Files > Chapter 7 > Having_Start.sql
SELECT categories.CategoryDescription,
    COUNT(products.SKU) AS "Number of SKUs"
FROM products.products
    JOIN products.categories
    ON products.CategoryID = categories.CategoryID
GROUP BY CategoryDescription
ORDER BY COUNT(products.SKU) DESC
;`
_____
`-- View related data in two tables
SELECT * FROM products.products
WHERE SKU = 'ALB008';`

`SELECT * FROM products.categories
WHERE CategoryID = 1;`

`-- Join columns together in a single query
SELECT products.ProductName,
    products.CategoryID,
    products.SKU,
    products.Price,
    categories.ProductLine
FROM products.products
    JOIN products.categories
        ON products.CategoryID = categories.CategoryID
WHERE SKU = 'ALB008';`
_____
`-- Retrieving only a specific number of rows
-- SQL Server uses the TOP keyword
SELECT TOP 5 *
FROM products.products
ORDER BY Price DESC;


-- PostgreSQL uses the LIMIT clause
SELECT *
FROM products.products
ORDER BY Price DESC
LIMIT 5;`
_____
`-- Add columns that calculate values
-- Exercise Files > Chapter 7 > Math_Start.sql
SELECT SKU,
    ProductName,
    CategoryID,
    Size,
    Price,
    '8.5%' AS TaxRate,
    Price * 0.085 AS SalesTax,
    Price + (Price * 0.085) AS TotalPrice
FROM products.products;`
____
`-- Add columns that calculate values
-- Exercise Files > Chapter 7 > Math_Start.sql
SELECT SKU,
    ProductName,
    CategoryID,
    Size,
    Price
FROM products.products;`
____
`-- Sort results on price
SELECT *
FROM products.products
WHERE Size = 8
ORDER BY Price;`

`-- Reverse the sort
SELECT *
FROM products.products
WHERE Size = 8
ORDER BY Price DESC;`

`-- Sort alphabetically on text
SELECT *
FROM products.products
WHERE Size = 8
ORDER BY ProductName;`

`-- Sort rows based on values in two columns
SELECT *
FROM products.products
WHERE Size = 8
ORDER BY Price DESC, ProductName;`
_______
`-- Retrieve selected columns
SELECT ProductName, Size, Price
FROM products.products;`

`-- Columns can be returned in any order
SELECT Size, Price, ProductName
FROM products.products;`

`-- Retrieve all columns from a table
SELECT *
FROM products.products;`
_____
`-- Q1: convert size from oz to ml
SELECT SKU, ProductName,
    Size AS "Size (Ounces)",
    Size * 29.57353 AS "Size (Milliliters)"
FROM products.products;`

`-- Q2: how many products are in each size
SELECT
    Size AS "Size (Ounces)",
    COUNT(SKU) AS "Number of Products"
FROM products.products
GROUP BY Size;`

`-- Q3: Highest priced product in cosmetic product line
SELECT MAX(Price)
FROM products.products
WHERE CategoryID = 3`

`SELECT SKU, ProductName, CategoryID, Size, Price
FROM products.products
WHERE PRICE =`
    `(SELECT MAX(Price)
     FROM products.products
     WHERE CategoryID = 3)
    AND CategoryID = 3`
_____
`-- Select everything from the table`
`SELECT *`
`FROM products.products;`

`-- Filter rows to category 2`
`SELECT *`
`FROM products.products`
`WHERE CategoryID = 2;`

`-- View all products above $25`
`SELECT *`
`FROM products.products`
`WHERE Price > 25;`

`-- View opposite set of results with NOT`
`SELECT *`
`FROM products.products`
`WHERE NOT Price > 25;`

`-- Combine criteria with AND`
`SELECT *`
`FROM products.products`
`WHERE Price > 10 AND Size < 12;`

`-- Use OR to filter two criteria on the same columns`
`SELECT *`
`FROM products.products`
`WHERE CategoryID = 2 OR CategoryID = 3;`

`-- Use single quotes for text matches`
`SELECT *`
`FROM products.products`
`WHERE ProductName = 'Pure';`

`-- Empty result sets occur when no matching rows exist`
`SELECT *`
`FROM products.products`
`WHERE Price > 100;`
____

## Capítulo 48
Fin

