# Kopiowanie tabel:

### Jeżeli wybrana baza to baza imienna:

CREATE TABLE kreatura AS SELECT * FROM wikingowie.kreatura;

### Jeżeli wybrana baza to wikingowie:

CREATE TABLE kropiak.kreatura SELECT * From kreatura

# Zad 1:

### 1) Kopiowanie tabel kreatura, zasob, ekwipunek z bazy wikingowie do swojej:
CREATE TABLE kreatura AS SELECT * FROM wikingowie.kreatura;

### 2) Wypisanie rekordow z tabeli zasob:
SELECT * FROM zasob;

### 3) Wypisanie rekordow z tabeli zasob gdzie typ to jedzenie:
SELECT * FROM zasob WHERE rodzaj = "jedzenie";

### 4) Wypisz idZasobu, ilosc dla kreatur o id 1,3,5:
SELECT idZasobu, ilosc FROM zasob, kreatura WHERE idKreatury in (1, 3, 5);

# Zad 2:

### 1) Wyświetl kreatury które nie są wiedźmą i dźwigają co najmniej 50kg:
SELECT * FROM kreatura WHERE rodzaj != "wiedzma" AND udzwig >= 50;

### 2) Wyświetl zasoby które ważą pomiędzy 2 a 5kg:
SELECT * FROM zasob WHERE waga > 2 AND waga < 5;

### 3) Wyświetl kreatury których nazwa zawiera or i które dźwigają między 30kg a 70kg:
SELECT * FROM kreatura WHERE nazwa LIKE "%or%" AND udzwig > 30 AND udzwig < 70;

# Zad 3:

### 1) Wyświetl zasoby które zostały pozyskane w miesiącu lipcu i sierpniu:
SELECT * FROM zasob WHERE MONTH(dataPozyskania) = 7 OR MONTH(dataPozyskania) = 8;

### 2) Wyświetl zasoby które mają zdefiniowany rodzaj od najlżejszego do najcięższego:
SELECT * FROM zasob WHERE rodzaj IS NOT NULL ORDER BY waga ASC;

### 3) Wyświetl 5 najstarszych kreatur:
SELECT * FORM kreatura ORDER BY dataUr DESC LIMIT 5;

# Zad 4:

### 1) Wyświetl unikalne rodzaje zasobów:
SELECT DISTINCT rodzaj FROM kreatura;

### 2) Wyświetl jako jedną kolumnę nazwę i rodzaj kreatury gdzie rodzaj rozpoczyna się od wi:
SELECT concat(nazwa, "to id=", idKreatury) form kreatura;

### 3) Wyświetl zasoby z całkowitą wagą danego zasobu (ilosc*waga) dla zasobow pozyskanych w latach 2000-2007:
SELECT * FROM  kreatura ORDER BY dataUr DESC LIMIT 5;

# Zad 5:

### 1) Zakładając że każdy rodzaj jedzenie to 30% odpadu wyświetl masę właściwego jedzenie oraz wagę odpadków:
SELECT nazwa, waga * 0,7 AS masa_netto, waga * 0,3 AS masa_odpadkow FROM zasob WHERE rodzaj = "jedzenie";

### 2) Wyświetl zasoby które nie mają rodzau:
SELECT * FROM zasob WHERE rodzaj IS NULL;

### 3) Wyświetl wszystke unikalne rodzaje zasobów których nazwa zaczyna się od ba lub kończy na os, posortuj alfabetycznie:
SELECT DISTINCT rodzaj FROM zasob WHERE rodzaj LIKE "Ba%" OR rodzaj LIKE "%os" ORDER BY rodzaj ASC;

