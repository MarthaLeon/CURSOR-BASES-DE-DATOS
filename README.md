# CURSOR-BASES-DE-DATOS
Tarea Programación de Bases de Datos


DELIMITER $$
CREATE PROCEDURE createlistaTipoProducto(
       INOUT listaTipoProducto varchar(5000)
)
BEGIN
       DECLARE finished INTEGER DEFAULT 0;
       DECLARE TipoProducto varchar(100) DEFAULT "";

       DECLARE tipoProdList
             CURSOR FOR
                         SELECT tipo_producto.nombreTipoProducto FROM tipo_producto

        DECLARE CONTINUE HANDLER
               FOR NOT FOUND SET finished = 1;

        OPEN tipoProdList;
        

getTipoProducto: LOOP
                                                FETCH tipoProdList INTO TipoProducto;
              IF finished = 1 THEN 
                                                                 LEAVE getTipoProducto;
                                                END IF;

                 SET listaTipoProducto=CONCAT(TipoProducto,";",listaTipoProducto)

                               END LOOP getTipoProducto;

        CLOSE tipoProdList;

END $$

DELIMITER;
