# Bazy Danych - Laboratorium 7

## Zadanie 1

#### Podpunkt 1
```sql
DELETE FROM kreatura;

INSERT INTO kreatura
SELECT * FROM wikingowie.kreatura;
```
```sql
CREATE TABLE uczestnicy 
AS (SELECT * FROM wikingowie.uczestnicy);
```
```sql
CREATE TABLE etapy_wyprawy 
AS (SELECT * FROM wikingowie.etapy_wyprawy);
```
```sql
CREATE TABLE sektor
AS (SELECT * FROM wikingowie.sektor);
```
```sql
CREATE TABLE wyprawa
AS (SELECT * FROM wikingowie.wyprawa);
```
#### Podpunkt 2
```sql
SELECT kreatura.nazwa
FROM kreatura LEFT OUTER JOIN uczestnicy 
ON kreatura.idKReatury = uczestnicy.id_uczestnika
WHERE id_wyprawy IS NULL;
```
#### Podpunkt 3
```sql
SELECT wyprawa.nazwa, SUM(ekwipunek.ilosc)
FROM wyprawa
INNER JOIN uczestnicy ON wyprawa.id_wyprawy = uczestnicy.id_wyprawy
INNER JOIN ekwipunek ON ekwipunek.idKreatury = uczestnicy.id_uczestnika
GROUP BY wyprawa.nazwa;
```
## Zadanie 2
#### Podpunkt 1
```sql
SELECT wyprawa.nazwa, COUNT(*), GROUP_CONCAT(kreatura.nazwa)
FROM wyprawa
INNER JOIN uczestnicy ON wyprawa.id_wyprawy = uczestnicy.id_wyprawy
INNER JOIN kreatura ON kreatura.idKreatury = uczestnicy.id_uczestnika
GROUP BY wyprawa.nazwa;
```
#### Podpunkt 2
```sql
SELECT wyprawa.nazwa AS nazwa_wyprawy,etap.idEtapu,sektor.nazwa AS nazwa_sektoru,kreatura.nazwa AS kierownik
FROM wyprawa
INNER JOIN etapy_wyprawy as etap ON etap.idWyprawy = wyprawa.id_wyprawy
INNER JOIN sektor ON sektor.id_sektora = etap.sektor
INNER JOIN kreatura ON wyprawa.kierownik = kreatura.idKreatury
ORDER BY wyprawa.data_rozpoczecia,wyprawa.id_wyprawy,etap.kolejnosc;
```