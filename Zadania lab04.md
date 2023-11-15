# Zad 1

**_Stworzenie tabeli postac:_**

CREATE TABLE postac (
-  id_postaci INT primary key auto_increment,
-  nazwa VARCHAR(40),
-  rodzaj enum('wiking', 'ptak', 'kobieta'),
-  data_ur date,
-  wiek INT unsigned <br>
);

**_Dodanie wartośći do tabeli:_**

INSERT INTO postac VALUES(default, 'Bjorn', 'wiking', '1700-11-09', 45);

INSERT INTO postac VALUES(default, 'Drozd', 'ptak', '1730-11-08', 15);

INSERT INTO postac VALUES(default, 'Tesciowa', 'kobieta', '1657-08-08', 19);

**_Modyfikacja wieku teściowej:_**

UPDATE postac SET wiek=88 WHERE nazwa = 'Tesciowa';

# Zad 2

**_Stworzenie tabeli walizka:_**

CREATE TABLE walizka (
-  id_walizki INT primary key auto_increment,
-  pojemnosc INT >= 0,
-  kolor enum('różowy', 'czerwony', 'tęczowy', 'żółty') DEFAULT 'różowy',
-  id_wlasciciela INT FOREIGN KEY REFERENCES postac(id_postaci) CASCADE DELETE <br>
);

INSERT INTO walizka VALUES(default, 20, default, default);
