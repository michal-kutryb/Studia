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
GROUP BY kreatura.nazwa;
```

```sql
SELECT kreatura.nazwa, zasob.nazwa
FROM kreatura
INNER JOIN ekwipunek ON ekwipunek.idKreatury = kreatura.idKreatury
INNER JOIN zasob ON ekwipunek.idZasobu = zasob.idZasobu
ORDER BY kreatura.nazwa;
```

```sql
SELECT kreatura.nazwa
FROM kreatura
LEFT JOIN ekwipunek ON ekwipunek.idKreatury = kreatura.idKreatury
WHERE idEkwipunku IS NULL;
```

## Zadanie 4

```sql
SELECT kreatura.nazwa,zasob.nazwa
FROM kreatura
NATURAL JOIN ekwipunek
INNER JOIN zasob ON ekwipunek.idZasobu = zasob.idZasobu
WHERE YEAR(kreatura.dataUr) BETWEEN 1670 AND 1679
ORDER BY kreatura.nazwa;
```

```sql
SELECT kreatura.nazwa
FROM kreatura
NATURAL JOIN ekwipunek
INNER JOIN zasob ON ekwipunek.idZasobu = zasob.idZasobu
WHERE zasob.rodzaj = 'jedzenie'
ORDER BY kreatura.dataUr DESC
LIMIT 5;
```

```sql
SELECT k1.nazwa,k2.nazwa
FROM kreatura AS k1
INNER JOIN kreatura AS k2 ON k1.idKreatury+5 = k2.idKreatury;
```

## Zadanie 5

```sql
SELECT t1.rodzaj, AVG(t2.ilosc * t3.ilosc * t3.waga)
FROM kreatura AS t1
INNER JOIN ekwipunek AS t2 ON t1.idKreatury = t2.idKreatury
INNER JOIN zasob AS t3 ON t3.idZasobu = t2.idZasobu
WHERE (t1.rodzaj != 'waz' OR t1.rodzaj != 'malpa') AND t2.ilosc < 30
GROUP BY rodzaj;
```

```sql
SELECT rodzaj,'Najstarszy' AS wiek , nazwa, dataUr
FROM kreatura
WHERE dataUR in
(SELECT min(dataUr) AS dataUr
FROM kreatura
GROUP BY rodzaj)
UNION ALL
SELECT rodzaj,'Najmlodszy' AS wiek ,nazwa, dataUr
FROM kreatura
WHERE dataUR in
(SELECT max(dataUr) AS dataUr
FROM kreatura
GROUP BY rodzaj)
ORDER BY rodzaj;
```