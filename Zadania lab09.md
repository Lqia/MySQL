#  Zad 1

### 1) Napisać wyzwalacz który przed wstawieniem lub modyfikacją tabeli kreatura sprawdzi czy waga jest większa od 0:
```SQL
DELIMITER //
CREATE TRIGGER waga_wieksza_od_0 
BEFORE INSERT ON kreatura FOR EACH ROW 
BEGIN
 IF NEW.waga <= 0
 THEN 
  SET NEW.waga = 1;
 END IF;
END
//
```

# Zad 2

### 1) Stwórz tabelę archiwum_wypraw z polami id_wyprawy, nazwa, data_rozpoczecia, data_zakonczenia, kierownik(varchar) do której będą wstawiane rekordy po usunięciu z tabeli wyprawa, Do kolumny kierownik wstawiana jest nazwa kreatury na podstawie usuwanego id_Kreatury:
```SQL
create table archiwum_wypraw(
id_wyprawy int primary key auto_increment,
nazwa varchar(55),
data_rozpoczecia date,
data_zakonczenia date,
kierownik varchar(55));

delimiter //
create trigger wyprawa_before_delete before delete on wyprawa
  for each row
  begin
    insert into archiwum_wypraw
    select w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa
    from wyprawa w join kreatura k on k.idKreatury=w.kierownik
    where id_wyprawy=old.id_wyprawy;
  end//
delimiter ;
```

# Zad 3

### 1) Napisz procedurę o nazwie "eliksir_sily" ktora bedzie podnosiła wartość pola udźwig z tabeli kreatura o 20% na podstawie id_kreatury przekazywanego jako parametr:
```SQL
delimiter //
create procedure eliksir_sily (in id int)
  begin
    update kreatura set udzwig = udzwig * 1.2 where idKreatury = id;
  end//
delimiter ;
```

### 2) Napisz funkcję która będzie pobierała tekst i zwracała go z wielkich liter
