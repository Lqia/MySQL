# Zad 1
### Wyświetl imię i nazwisko każdego pracownika i jego rok urodzenia:
```SQL
SELECT imie, nazwisko, YEAR(data_urodzenia) FROM pracownik;
```
# Zad 2
### Wyświetl imię i nazwisko pracowników oraz ich wiek w latach (bez uwzględniania miesiąca i dnia urodzenia):
```SQL
SELECT imie,nazwisko, YEAR(curdate())-YEAR(data_urodzenia) FROM pracownik;
```
# Zad 3
### Wyświetl nazwę działu i liczbę pracowników przypisanych do każdego z nich: :rage4:
```SQL
SELECT COUNT(DISTINCT(p.id_pracownika)), d.nazwa FROM pracownik p INNER JOIN dzial d ON p.dzial = d.id_dzialu GROUP BY d.id_dzialu;
```
# Zad 4
### Wyświetl nazwę kategorii oraz liczbę produktów w każdej z nich:
```SQL
SELECT COUNT(DISTINCT(t.id_towaru)), k.nazwa_kategori FROM towar t INNER JOIN kategoria k ON t.kategoria = k.id_kategori GROUP BY id_kategori;
```
# Zad 5
### Wyświetl nazwę kategorii i w kolejnej kolumnie listę wszystkich produktów należącej do każdej z nich:
```SQL
SELECT k.nazwa_kategori, group_concat(t.nazwa_towaru separator" ") FROM towar t INNER JOIN kategoria k ON t.kategoria = k.id_kategori GROUP BY id_kategori;
```
# Zad 6
### Wyświetl średnie zarobki pracowników za zaokrągleniem do 2 miejsc po przecinku:
```SQL
SELECT ROUND(AVG(pensja), 2) FROM pracownik;
```
# Zad 7
### Wyświetl średnie zarobki pracowników, którzy pracują co najmniej od 5 lat:
```SQL
SELECT ROUND(AVG(pensja), 2) FROM pracownik WHERE YEAR(curdate())-YEAR(data_zatrudnienia) >= 5;
```
# Zad 8
### Wyświetl 10 najczęściej sprzedawanych produktów:
```SQL
SELECT t.nazwa_towaru FROM towar t INNER JOIN pozycja_zamowienia pz ON t.id_towaru = pz.towar GROUP BY t.nazwa_towaru ORDER BY SUM(pz.ilosc) DESC LIMIT 10;
```
# Zad 9
### Wyświetl numer zamówienia, jego wartość (suma wartości wszystkich jego pozycji) zarejestrowanych w pierwszym kwartale 2017 roku:
```SQL

```
# Zad 10
### Wyświetl imie, nazwisko i sumę wartości zamówień, które dany pracownik dodał. Posortuj malejąco po sumie:
```SQL
SELECT p.imie, p.nazwisko, SUM(pz.ilosc*pz.cena) FROM zamowienie z
INNER JOIN pozycja_zamowienia pz ON z.id_zamowienia = pz.zamowienie
INNER JOIN pracownik p ON z.pracownik_id_pracownika = p.id_pracownika
GROUP BY p.id_pracownika;
```






