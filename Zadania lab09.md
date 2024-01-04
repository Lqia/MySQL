#  Zad 1

### 1) Napisać wyzwalacz który przed wstawieniem lub modyfikacją tabeli kreatura sprawdzi czy waga jest większa od 0:
```SQL
DELIMITER //
CREATE TRIGGER waga_wieksza_od_0 
BEFORE INSERT ON kreatura FOR EACH ROW 
BEGIN
 IF NEW.waga <= 0
 THEN 
  SET NEW.waga = 1;
 END IF;
END
//

```
