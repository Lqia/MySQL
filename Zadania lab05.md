#Lab_05

#Zadanie 1

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
