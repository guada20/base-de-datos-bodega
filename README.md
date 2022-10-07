# base-de-datos-bodega
bodega
--Hay que tener una base de datos donde almacenamos información 
CREATE DATABASE Bodega
--Indicar que base de datos vamos a usar
USE Bodega
--Crear la tabla Producto
CREATE TABLE Producto(
Id_Producto int Primary Key,
Descripcion varchar(40) NOT NULL,
Categoria varchar(30) NOT NULL,
Existencias int NOT NULL,
Precio_Compra int NOT NULL,
Precio_Venta int NOT NULL,
Ganancia as Precio_Venta - Precio_Compra, --Aquí estamos
--asignando un valor para el campo ganancia
check (Precio_Venta > Precio_Compra) )
--Comprobando que el valor que se envía en precio venta
--debe de ser mayor al valor de precio compra
--Crear la tabla Cliente
CREATE TABLE Cliente(
Identificacion_Cliente int Primary Key,
Nombre_Cliente varchar(30) NOT NULL,
Apellido_Cliente varchar(50) NOT NULL,
Telefono_Cliente bigint NOT NULL,
Direccion_Cliente varchar(50), 
Correo_Electronico varchar(50),
Fecha_Nacimiento date)

--Crear la tabla Pedido que una al producto y al cliente
CREATE TABLE Pedido(
Id_Pedido int Primary Key,
Identificacion_Cliente int FOREIGN KEY REFERENCES Cliente(Identificacion_Cliente),
Identificacion_Producto int FOREIGN KEY REFERENCES Producto(Id_Producto),
Cantidad int NOT NULL)

--Agregar Registros en la tabla Producto
Insert into Producto values (2360,'cocacola 1.5','bebidas',10,4.000,5.500)
Insert into Producto values (1502,'papas limom','mekato',15,2.000,3.000)
Insert into Producto values (1620,'bandeja fresas','frutas',6,3.500,5.000)
Insert into Producto values (1030,'Leche entera', 'lacteos', 7,2000,3500)
Insert into Producto values (5630,'Jamon colanta','Embutidos',13,9000,13000)
--Agregar Registros en la tabla Cliente
Insert into Cliente values(1033502315,'juan david','muñoz',3014569815,'cra30#10-15','juan@gmail.com','1995-05-01')
Insert into Cliente values(43590216,'eliana maria','avendaño',3128322768,'cllA#30-60','elioc@gmail.com','1974-12-10')
Insert into Cliente values(32302304,'Ruth','zapata',3215548965,'cra60#69-20','ruth@gmail.com','1945-10-24')
Insert into Cliente values(98644802,'alvaro','restrepo',3215524875,'cra10#56-20','alva@gmail.com','1975-05-13')
Insert into Cliente values(10334865,'ana','gonzalez',3014361259,'cll50#40-16','analdk@gmail.com','2000-01-22')
--Agregar Registros en la tabla Pedido, recordando que esta tabla tiene 2 claves foráneas
Insert into Pedido values(28605,1033502315,2360,3)
Insert into Pedido values(56905,43590216,1502,5)
Insert into Pedido values(89567,32302304,1620,6)
Insert into Pedido values(75481,98644802,1030,4)
Insert into Pedido values(32154,10334865,5630,10)

select*from Producto
select*from Cliente
select*from Pedido
update Producto set Precio_Compra=4000,Precio_Venta=5500 where Id_Producto=2360
update Producto set Precio_Compra=2000,Precio_Venta=3000 where Id_Producto=1502
update Producto set Precio_Compra=3500,Precio_Venta=5000 where Id_Producto=1620
update Producto set Precio_Compra=2000,Precio_Venta=3500 where Id_Producto=1030
update Producto set Precio_Compra=9000,Precio_Venta=13000 where Id_Producto=5630
--el cliente con id 10334865 cambio de direccion y telefono
update Cliente set Direccion_Cliente='call30#10-60',Telefono_Cliente=3014362158 where Identificacion_Cliente=10334865
--consultar los clientes que el nombre comience en a
select*from Cliente where Nombre_Cliente like 'A%'
--traer  de producto aquellos que su categoria sea mekato o gaseosa
select*from Producto where Categoria in('mekato','bebidas')
--de la tabla productos traer todos menos los que tengan como existencias 5,15 y 7
select*from Producto where Existencias not in(5,15,7)
--de la tabla cliente traer toods los que tengan gmail
select*from Cliente where Correo_Electronico like '%gmail%'
--de la tabl producto necesitamos solo los que baya la ganancia desde 1100 hasta 2000

select*from Producto where Ganancia between 1100 and 2000
