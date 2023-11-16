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
-  pojemnosc INT CHECK (pojemnosc >= 0),
-  kolor enum('różowy', 'czerwony', 'tęczowy', 'żółty') DEFAULT 'różowy',
-  id_wlasciciela INT FOREIGN KEY REFERENCES postac(id_postaci) CASCADE DELETE
-  <br>
);

**_Dodanie po 1 walizcje dla Bjorna i teściowej:_**

INSERT INTO walizka VALUES(default, 20, default, (SELECT id FROM postac WHERE imie = 'Bjorn'));

INSERT INTO walizka VALUES(default, 30, czerwony, (SELECT id FROM postac WHERE imie = 'Tesciowa'));

# Zad 3

**_Stworzenie tabeli:_**

CREATE TABLE izba (
-  adres_budynku VARCHAR(50),
-  nazwa_izby VARCHAR(50),
-  metraz INT CHECK (metraz >= 0),
-  wlasciciel VARCHAR(50) FOREIGN KEY REFERENCES postac(nazwa) ON DELETE SET NULL <br>
);

**_Dodanie pola kolor izby:_**

ALTER TABLE izba ADD VARCHAR(50) DEFAULT 'czarny' AFTER metraz;

**_Utworzenie izby spizarnia:_**

INSERT INTO izba VALUES(adres, spiżarnia, 20, default, "Bjorn");

