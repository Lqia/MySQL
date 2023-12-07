# Zad4:

### 2)
SELECT k.nazwa, k.dataUr, z.rodzaj FROM kreatura k INNER JOIN ekwipunek e ON k.idKreatury=e.idKreatury INNER JOIN zasob z ON e.idZasobu=z.idZasobu WHERE z.rodzaj = "jedzenie" ORDER BY k.dataUr DESC LIMIT 5;
