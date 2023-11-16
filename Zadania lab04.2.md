# Zadanie 1

CREATE TABLE postac(
id_postaci INT primary key auto_increment,
nazwa VARCHAR(50),
rodzaj enum('wiking','ptak','kobieta'),
data_ur date,
wiek INT unsigned
);


# Zadanie 4
 CREATE TABLE przetwory(
id_przetworu INT PRIMARY KEY ,
rok_produkcji INT DEFAULT 1654,
id_wykonawcy INT,
zawartosc VARCHAR(250),
dodatek VARCHAR(60) DEFAULT 'papryczka chilli',
id_konsumenta INT,
FOREIGN KEY(id_wykonawcy) REFERENCES postac(id_postaci),
FOREIGN KEY(id_konsumenta) REFERENCES postac(id_postaci)
 );
 

 # Zadanie 5
 
INSERT INTO postac VALUES(default, 'Bjorn', 'wiking', '1900-08-07', 40);
INSERT INTO postac VALUES(default, 'Wiking2', 'wiking', '1900-08-08', 41);
INSERT INTO postac VALUES(default, 'Wiking3', 'wiking', '1900-08-09', 42);
INSERT INTO postac VALUES(default, 'Wiking4', 'wiking', '1900-08-10', 43);
INSERT INTO postac VALUES(default, 'Wiking5', 'wiking', '1900-08-11', 44);
 
 #5.2
 
 CREATE TABLE statek(
 nazwa VARCHAR(50) PRIMARY KEY,
 rodzaj enum('maly', 'sredni', 'duzy'),
 data_wodowania date,
 max_ladownosc INT CHECK (max_ladownosc > 0)
 );
 
 #5.3
 
 INSERT INTO statek VALUES('statek1', 'sredni', '1940-08-08', 10) 
 INSERT INTO statek VALUES('statek2', 'maly', '1940-08-07', 5) 
 
 #5.4
 
 ALTER TABLE postac ADD funkcja VARCHAR(50);
 
 #5.5
 
 UPDATE postac SET funkcja = 'Kapitan' WHERE nazwa = 'Wiking1';
 
 #5.6

