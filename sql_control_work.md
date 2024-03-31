1.Создайте функцию, которая принимает кол-во сек и далее переводит их в кол-во дней, часов, минут, секунд.
Пример: 123456 ->'1 days 10 hours 17 minutes 36 seconds '


DROP FUNCTION IF EXISTS times;
DELIMITER //
CREATE FUNCTION times(seconds INT)
RETURNS VARCHAR(255) 
BEGIN
    DECLARE days INT;
    DECLARE hours INT;
    DECLARE minutes INT;
    DECLARE message VARCHAR(255);
    
    SET days = seconds DIV (60*60*24);
    SET seconds = seconds MOD(60*60*24); 
    
	SET hours = seconds DIV (60*60);
    SET seconds = seconds MOD(60*60); 
    
	SET minutes = seconds DIV 60;
    SET seconds = seconds MOD 60; 
    
    -- SET message = (SELECT days, hours, minutes, seconds);
    
    SET message = CONCAT(days, 'days', hours, 'hours', minutes, 'minutes', seconds 'seconds');

RETURN message; 
END //
DELIMITER;
SELECT times(123456); 


2.Cоздайте процедуру, которая выведет только числа, делящиеся на 15 или 33 в промежутке от 1 до 1000.
Пример: 15,30,33,45...


DROP PROCEDURE IF EXISTS dividers;
DELIMITER //
CREATE PROCEDURE dividers(first_number INT, last_number INT)
BEGIN
    DECLARE result TEXT DEFAULT NULL;
    WHILE  first_number <=last_number DO
        IF first_number % 15 = 0 or first_number % 33 = 0 THEN
		IF result IS NULL THEN
			SET result = concat(first_number);
		ELSE
			SET result = concat(result, ', ', first_number);
		END IF;
		END IF;
            SET first_number = first_number + 1;
    END WHILE;
	SELECT result;
END //
DELIMITER ;
CALL dividers(1, 1000);