# Zad 1

### 1) Skopiowac z bazy wikingowie tabele uczestnicy, etapy_wyprawy, sektor, wyprawa, kreatura

CREATE TABLE uczestnicy AS SELECT * FROM wikingowie.uczestnicy;

CREATE TABLE etapy_wyprawy AS SELECT * FROM wikingowie.etapy_wyprawy;

CREATE TABLE sektor AS SELECT * FROM wikingowie.sektor;

CREATE TABLE wyprawa AS SELECT * FROM wikingowie.wyprawa;

CREATE TABLE kreatura AS SELECT * FROM wikingowie.kreatura;

### 2) Wypisz nazwy kreatur które nie uczestniczyły w żadnej wyprawie:

SELECT nazwa FROM kreatura LEFT JOIN uczestnicy ON idKreatury = id_uczestnika WHERE id_uczestnika IS NULL;

### 3) Do każdej wyprawy wypisać jej nazwę oraz sumę ilości ekwipnku jaka została zebrana pzez uczestnikow tej wyprawy:

SELECT w.nazwa AS nazwa_wyprawy, sum(e.ilosc) AS niesione_rzeczy FROM kreatura k
JOIN ekwipunek e ON k.idKreatury=e.idKreatury
JOIN uczestnicy u ON k.idKreatury=u.id_uczestnika
JOIN wyprawa w ON u.id_wyprawy=w.id_wyprawy
GROUP BY w.nazwa;
