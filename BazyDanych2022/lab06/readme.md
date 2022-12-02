# Bazy Danych - Laboratorium 6

## Zadanie 1

```sql
SELECT AVG(waga)
FROM kreatura
WHERE rodzaj = 'wiking';
```

```sql
SELECT rodzaj, AVG(waga), COUNT(*)
FROM kreatura
GROUP BY rodzaj;
```

```sql
SELECT rodzaj, FLOOR(AVG(YEAR(CURDATE())-YEAR(dataUr))) AS sredniWiek
FROM kreatura
GROUP BY rodzaj;
```

## Zadanie 2

```sql
SELECT rodzaj, SUM(waga)
FROM zasob
GROUP BY rodzaj;
```

```sql
SELECT nazwa, AVG(waga)
FROM zasob
GROUP BY nazwa
HAVING SUM(ilosc)>=4 AND AVG(waga) > 10;
```

```sql
SELECT rodzaj, COUNT(DISTINCT(nazwa))
FROM zasob
GROUP BY rodzaj
HAVING MIN(ilosc)>1;
```

## Zadanie 3

```sql
SELECT kreatura.nazwa, SUM(ekwipunek.ilosc)
FROM kreatura
INNER JOIN ekwipunek ON ekwipunek.idKreatury = kreatura.idKreatury
GROUP BY kreatura.nazwa
```

```sql
SELECT kreatura.nazwa, zasob.nazwa
FROM kreatura
INNER JOIN ekwipunek ON ekwipunek.idKreatury = kreatura.idKreatury
INNER JOIN zasob ON ekwipunek.idZasobu = zasob.idZasobu
ORDER BY kreatura.nazwa
```

```sql
SELECT kreatura.nazwa
FROM kreatura
LEFT JOIN ekwipunek ON ekwipunek.idKreatury = kreatura.idKreatury
WHERE idEkwipunku IS NULL
```

## Zadanie 4

```sql
SELECT kreatura.nazwa,zasob.nazwa
FROM kreatura
NATURAL JOIN ekwipunek
INNER JOIN zasob ON ekwipunek.idZasobu = zasob.idZasobu
WHERE YEAR(kreatura.dataUr) BETWEEN 1670 AND 1679
ORDER BY kreatura.nazwa
```

```sql
SELECT kreatura.nazwa
FROM kreatura
NATURAL JOIN ekwipunek
INNER JOIN zasob ON ekwipunek.idZasobu = zasob.idZasobu
WHERE zasob.rodzaj = 'jedzenie'
ORDER BY kreatura.dataUr DESC
LIMIT 5
```

```sql
SELECT k1.nazwa,k2.nazwa
FROM kreatura AS k1
INNER JOIN kreatura AS k2 ON k1.idKreatury+5 = k2.idKreatury
```

## Zadanie 5

```sql

```

```sql

```