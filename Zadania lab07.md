# Zad 1

### 1) Wyswietl srednia wage wszystkich wikingow:
SELECT ROUND(avg(waga), 2) as srednia_waga FROM kreatura WHERE rodzaj = 'wiking';

### 2) Wyswietl srednia wage oraz liczbe kreatur dla kazdego rodzaju:
SELECT round(avg(waga), 2) as srednia_waga, rodzaj, count(rodzaj) as ilosc FROM kreatura GROUP BY rodzaj;

### 3) Wyswietl sredni wiek dla kazdego rodzaju kreatury:
SELECT round(avg(year(dataUr)),2) as sredni_wiek, rodzaj FROM kreatura GROUP BY rodzaj;

# Zad 2

### 1) Dla kazdego rodzaju zasobu wyswietl sume wag tego zasobu:
SELECT sum(waga*ilosc) as suma_wag, rodzaj FROM zasob GROUP BY rodzaj;

### 2) Dla kazdej nazwy zasobu wyswietl srednia wage jescli ilosc jest rowna co najmniej 4 oraz jesli ta suma wag jest wieksza od 10:
SELECT nazwa, round(avg(waga*ilosc), 2) as srednia_waga FROM zasob where ilosc >= 4 GROUP BY nazwa HAVING srednia_waga > 10;

### 3) Wyswietl ile jest roznych nazw dla kazdego rodzaju zasobu jesli minimalna liczba zasobu jest wieksza od 1:
SELECT rodzaj, count(distinct(nazwa)) as nazwa FROM zasob GROUP BY rodzaj HAVING min(ilosc) > 1;****

# Zad 3

### 1) Wyswietl dla kazdej kreatury ilosc zasobow jakie niesie:
SELECT k.nazwa, sum(e.ilosc) as niesione_rzeczy FROM kreatura k, ekwipunek e WHERE k.idKreatury = e.idKreatury GROUP by k.nazwa;

### 2) Wyswietl dla kazdej kreatury nazwy zasobow jakie posiada:
SELECT k.nazwa, z.nazwa FROM kreatura k JOIN ekwipunek e ON k.idKreatury=e.idKreatury JOIN zasob z ON e.idZasobu=z.idZasobu;

### 3) Wyswietl kreatury ktore nie posiadaja zadnego ekwipunku:
SELECT * FROM kreatura k left join ekwipunek e on k.idKreatury = e.idKreatury WHERE e.idKreatury is NULL;
SELECT * from kreatura WHERE idKreatury not in (select distinct idKreatury FROM ekwipunek WHERE idKreatury is not null);

# Zad 4

### 1) Wyswietl nazwy wikingow ktorzy urodzili sie w latach 70-tych XVII wieku oraz nazwy zasobow ktore posiadaja:
SELECT k.dataUr, k.nazwa, z.nazwa from kreatura k JOIN ekwipunek e on k.idKreatury=e.idKreatury JOIN zasob z on e.idZasobu=z.idZasobu WHERE year(k.dataUr) between 1670 and 1679 AND k.rodzaj = 'wiking';

### 2) Wyswietl nazwy 5 najmlodszych kreatur ktore w ekwipunku posiadaja jedzenie:
SELECT k.nazwa, k.dataUr as dU, z.nazwa FROM kreatura k JOIN ekwipunek e on k.idKreatury = e.idKreatury JOIN zasob z on e.idZasobu = z.idZasobu WHERE z.rodzaj = 'jedzenie' ORDER BY dU desc limit 5;

### 3) Wypisz obok siebie nazwy kreatur ktorych numer idKreatury rozni sie o 5:
SELECT k1.nazwa, k2.nazwa FROM kreatura k1, kreatura k2 WHERE k1.idKreatury = k2.idKreatury + 5;

SELECT k2.idKreatury, concat(k2.nazwa, ' - ' ,k1.nazwa) AS nazwa, k1.idKreatury FROM kreatura k1 JOIN kreatura k2 ON k1.idKreatury = k2.idKreatury + 5;

# Zad 5

### 1) Dla kazdego rodzaju kreatury wyswietlic srednia wage zasobow jaka posiadaja w ekwipunku jesli kreatura nie jest malpa ani wezem i ilosc ekwipunku jest ponizej 30:
SELECT k.rodzaj, avg(z.waga*e.ilosc) AS s_waga from kreatura k, ekwipunek e, zasob z WHERE k.rodzaj not in ('malpa', 'waz') GROUP BY k.rodzaj having e.ilosc < 30;

SELECT k.rodzaj, avg(z.waga*e.ilosc) AS s_waga FROM kreatura k, ekwipunek e, zasob z WHERE k.idKreatury=e.idKreatury AND e.idZasobu=z.idZasobu GROUP BY k.rodzaj having s_waga < 30;
