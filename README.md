# FunPro
Functional Programing with Scala
CREATE FUNCTION ConvertBase ( 
IN InputInteger INTEGER, 
IN InputRadix INTEGER 
) RETURNS CHARACTER 
BEGIN 
   DECLARE OutputText CHARACTER REPLICATE('0', 65); 
   DECLARE digitsArray CHARACTER '01234567890abcdefghijklmnopqrstuvwxyz'; 
    
   IF (InputRadix < 2) OR (InputRadix > 36) THEN 
      SET InputRadix = 10; 
   END IF; 
    
   DECLARE i INTEGER 65; 
   DECLARE j INTEGER 0; 
    
   IF InputInteger < 0 THEN 
      SET j = 1; 
   END IF; 
    
   IF j = 0 THEN 
      SET InputInteger = -InputInteger; 
   END IF; 
    
   DECLARE ReplaceString CHARACTER; 
   WHILE InputInteger <= -InputRadix DO 
      SET  ReplaceString = SUBSTRING ( digitsArray FROM -(MOD (InputInteger,InputRadix )-1) FOR 1); 
      SET OutputText = OVERLAY ( OutputText PLACING ReplaceString FROM i for 1 ); 
      SET InputInteger = InputInteger / InputRadix; 
      SET i = i - 1; 
   END WHILE; 
   SET  ReplaceString = SUBSTRING ( digitsArray FROM -(InputInteger-1) FOR 1); 
   SET OutputText = OVERLAY ( OutputText PLACING ReplaceString FROM i for 1 ); 
    
   IF j <> 0 THEN 
      SET i = i - 1; 
      SET OutputText = OVERLAY ( OutputText PLACING '-' FROM i for 1 ); 
   END IF; 
   RETURN SUBSTRING(OutputText FROM i); 
END;
