# Bazy Danych - Laboratorium 5

## Zadanie 1

```sql
CREATE TABLE kreatura AS SELECT * FROM wikingowie.kreatura;
CREATE TABLE zasob AS SELECT * FROM wikingowie.zasob;
CREATE TABLE ekwipunek AS SELECT * FROM wikingowie.ekwipunek;
```
```sql
SELECT * 
FROM zasob;
```
```sql
SELECT * 
FROM zasob
WHERE rodzaj = 'jedzenie';
```
```sql
SELECT idZasobu, ilosc
FROM ekwipunek
WHERE idKreatury IN (1,3,5);
```

## Zadanie 2

```sql
SELECT *
FROM kreatura
WHERE rodzaj != 'wiedzma' AND udzwig >= 50
```
```sql
SELECT *
FROM zasob
WHERE waga BETWEEN 2 AND 5;
```
```sql
SELECT *
FROM kreatura
WHERE nazwa LIKE '%or%' AND  (waga BETWEEN 30 AND 70)
```

## Zadanie 3

```sql
SELECT *
FROM zasob
WHERE MONTH(dataPozyskania) IN (7,8);
```
```sql
SELECT *
FROM zasob
WHERE rodzaj IS NOT NULL
ORDER BY waga;
```
```sql
SELECT *
FROM kreatura
ORDER BY dataUr
LIMIT 5;
```

## Zadanie 4

```sql
SELECT DISTINCT rodzaj
FROM zasob
WHERE rodzaj IS NOT NULL;
```
```sql
SELECT CONCAT(nazwa,'-',rodzaj)
FROM kreatura
WHERE rodzaj LIKE 'wi%';
```
```sql
SELECT *, ilosc*waga AS calkowitaWaga
FROM zasob
WHERE YEAR(dataPozyskania) BETWEEN 2000 AND 2007;
```

## Zadanie 5
```sql
SELECT *, waga*0.7 AS masaWlasciwa, waga*0.3 AS wagaOdpadkow
FROM zasob
WHERE rodzaj = 'jedzenie';
```
```sql
SELECT *
FROM zasob
WHERE rodzaj IS NULL;
```
```sql
SELECT DISTINCT rodzaj
FROM zasob
WHERE (nazwa LIKE 'Ba%' OR nazwa LIKE '%os') AND rodzaj IS NOT NULL
ORDER BY nazwa;
```