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

# Zad 2

### 1) Dla każdej wyprawy wypisz jej nazwę, liczbę uczestników oraz nazwy tych uczestników w jedej linii:
select w.nazwa, count(u.id_uczestnika) as liczba_uczestnikow, group_concat(k.nazwa separator ' - ') as uczestnicy from
wyprawa w join uczestnicy u on
w.id_wyprawy=u.id_wyprawy
join kreatura k on k.idKreatury=u.id_uczestnika
group by w.nazwa;

### 2) Wypisz kolejne etapy wraz z nazwami sektorów, stosując najpierw według daty początku wyprawy a następnie według kolejności występowania etapów, w każdym etapie okreść nazwę kierownika danej wyprawy:

SELECT w.data_rozpoczecia, ew.sektor, ew.kolejnosc, s.nazwa, k.nazwa, w.idWyprawy FROM etapy_wyprawy ew
INNER JOIN sektor s on ew.sektor=s.id_sektora
INNER JOIN wyprawa w ON w.id_wyprawy = ew.idWyprawy
INNER JOIN kreatura k ON k.idKreatury=w.kierownik
ORDER BY w.data_rozpoczecia asc, ew.kolejnosc asc;

# Zad 3

### 1) Wypisac ile razy dany sektor byl odwiedzany podczas wszystkich wypraw(nazwa sektora, ilosc odwiedzin), jeśli nie był odwiedzony ani razu wypisz zero:

SELECT s.nazwa, ifnull(count(ew.sektor), 0) FROM sektor s LEFT JOIN etapy_wyprawy ew ON s.id_sektora=ew.sektor 
GROUP BY s.nazwa;

### 2) W zaleznosci od ilosci wypraw w jakich brała udział dana kreatura wypisz: nazwa kreatury, "bral udzial w wyprawie" - gdy liczba > 0, "nie brał udziału w wyprawie" - gdy liczba równa 0:

SELECT k.nazwa, if(count(u.id_uczestnika)>0, "brał udział w wyprawie", "nie brał udziału w wyprawie") FROM uczestnicy u RIGHT JOIN kreatura k ON k.idKreatury=u.id_uczestnika
GROUP BY k.nazwa;

# Zad 4

### 1) Dla kazdej wyprawy wypisz jej nazwę oraz sumę liczby znaków które zostały użyte przy pisaniu dziennika jeśli ta liczba znaków jest mniejsza od 400: 

SELECT w.nazwa, sum(length(ew.dziennik)) FROM wyprawa w INNER JOIN etapy_wyprawy ew WHERE length(ew.dziennik) < 400 GROUP BY w.nazwa;

### 2) Dla każdej wyprawy podaj średnią wagę zasobów jakie były niesione przez  uczestników tej wyprawy:

select w.nazwa as nazwa_wyprawy,
       sum(z.waga*e.ilosc)/count(distinct(u.id_uczestnika)) as niesione_rzeczy
from kreatura k
join ekwipunek e on k.idKreatury=e.idKreatury
join uczestnicy u on k.idKreatury=u.id_uczestnika
join wyprawa w on u.id_wyprawy=w.id_wyprawy
join zasob z on z.idZasobu=e.idZasobu
group by w.nazwa;

# Zad 5

### 1) Wypisac nazwe kreatury oraz ile miala dni (wiek w dniach) w momencie rozpoczęcia wyprawy dla wypraw które przechodziły przez chatkę dziadka:

SELECT w.nazwa, k.nazwa, datediff(w.data_rozpoczecia, k.dataUr) AS roznica FROM kreatura k 
INNER JOIN uczestnicy u ON u.id_uczestnika=k.idKreatury
INNER JOIN wyprawa w ON u.id_wyprawy = w.id_wyprawy
INNER JOIN etapy_wyprawy ew ON ew.idWyprawy=w.id_wyprawy
WHERE ew.sektor = 7 GROUP BY w.id_wyprawy, k.idKreatury;






