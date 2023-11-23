# Lab_05

## Zadanie 1

### A)

CREATE TABLE postac2(
id_postaci INT primary key auto_increment,
nazwa VARCHAR(50),
rodzaj enum('wiking','ptak','kobieta'),
data_ur date,
wiek INT unsigned
);

INSERT INTO postac2 VALUES(default, 'Bjorn', 'wiking', '1700-11-09', 45);
INSERT INTO postac2 VALUES(default, 'Wiking1', 'wiking', '1730-11-08', 40);
INSERT INTO postac2 VALUES(default, 'Wiking2', 'wiking', '1657-08-08', 35);
INSERT INTO postac2 VALUES(default, 'Wiking3', 'wiking', '1657-08-08', 38);

DELETE FROM postac WHERE rodzaj = 'wiking' and nazwa <> 'Bjorn' ORDER BY wiek asc limit 2;

### B)
ALTER TABLE postac drop primary key;

1) usunięcie atrybutu auto_increment:

ALTER TABLE postac CHANGE id_postaci id_postaci int;
ALTER TABLE postac MODIFY id_postaci INT;

2) usunięcie kluczy obcych:

ALTER TABLE walizka DROP foreign key walizka_ibfk_1;

3) wracamy do usunięcia auto_increment, ostateczne usunięcie klucza głównego:

ALTER TABLE postac DROP primary_key;

## Zadanie 2


### A)
ALTER TABLE postac ADD COLUMN pesel CHAR(11) primary key first;

ALTER TABLE postac ADD primary key(pesel);

UPDATE postac SET pesel = '76463625431' + id_postaci;

### B)
ALTER TABLE postac CHANGE rodzaj enum('wiking', 'ptak', 'kobieta', 'syrena');

### C)
INSERT INTO postac VALUES(26136167835, 4, 'Gertruda Nieszczera', 'syrena', 1657-08-08', 36);

## Zadanie 3

SELECT nazwa FROM postac WHERE nazwa LIKE '_r%';
SELECT nazwa FROM postac WHERE nazwa LIKE '__-___';

### B)

UPDATE statek SET max_ladownosc = max_ladownosc * 0.7 WHERE YEAR(data wodowania) BETWEEN 1901 AND 2000;

### C)

ALTER TABLE postac ADD CHECK (wiek <= 1000);

## Zadanie 4


### A)

ALTER TABLE postac CHANGE rodzaj enum('wiking', 'ptak', 'kobieta', 'syrena', 'wąż');

INSERT INTO postac VALUES(85630283714, 5, 'Loko', 'wąż', 1666-02-05, 30);

### B)

CREATE TABLE marynarz LIKE postac;

CREATE TABLE marynarz2 SELECT pesel. nazwa, rodzaj from postac;

INSERT INTO marynarz SELECT * FROM postac WHERE statek is NOT NULL;

### C)


## Zadanie 5

### A)

UPDATE postac SET funkcja = NULL;

### B)

UPDATE postac

### C)

DELETE FROM statek
