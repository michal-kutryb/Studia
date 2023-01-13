# Bazy Danych - Laboratorium 13.01.2023

## Zadanie 1
```sql
SELECT dzial.nazwa, MIN(pensja),MAX(pensja),AVG(pensja)
FROM pracownik
INNER JOIN dzial ON dzial.id_dzialu = pracownik.dzial
GROUP BY dzial.id_dzialu
```

## Zadanie 2
```sql
SELECT t3.pelna_nazwa,SUM(t2.ilosc*t2.cena) AS wartosc
FROM zamowienie AS t1
INNER JOIN pozycja_zamowienia AS t2 ON t2.zamowienie = t1.id_zamowienia
INNER JOIN klient AS t3 ON t1.klient = t3.id_klienta
GROUP BY t3.id_klienta
ORDER BY wartosc DESC
LIMIT 10;
```

## Zadanie 3
```sql
SELECT YEAR(z.data_zamowienia) AS rok, SUM(p.ilosc*p.cena) AS wartosc
FROM zamowienie AS z
INNER JOIN pozycja_zamowienia AS p
ON p.zamowienie = z.id_zamowienia
WHERE z.status_zamowienia = 5 
GROUP BY rok
ORDER BY wartosc DESC;
```

## Zadanie 4
```sql
SELECT SUM(p.ilosc*p.cena) AS wartosc
FROM zamowienie AS z
INNER JOIN pozycja_zamowienia AS p
ON p.zamowienie = z.id_zamowienia
WHERE z.status_zamowienia = 6
```

## Zadanie 5
```sql
SELECT miejscowosc, COUNT(*) AS ile, SUM(p.ilosc*p.cena) AS wartosc
FROM zamowienie AS z
INNER JOIN pozycja_zamowienia AS p ON p.zamowienie = z.id_zamowienia
INNER JOIN klient AS k ON z.klient = k.id_klienta
INNER JOIN adres_klienta AS a ON a.klient = k.id_klienta
WHERE a.typ_adresu = 1
GROUP BY miejscowosc
```

## Zadanie 6
```sql
SELECT SUM(p.ilosc*p.cena) - SUM(p.ilosc*t.cena_zakupu) AS dochod
FROM zamowienie AS z
INNER JOIN pozycja_zamowienia AS p
ON p.zamowienie = z.id_zamowienia
INNER JOIN  towar as t
ON t.id_towaru = p.towar
WHERE z.status_zamowienia = 5 
```
## Zadanie 7
```sql
SELECT YEAR(z.data_zamowienia) AS rok,SUM(p.ilosc*p.cena) - SUM(p.ilosc*t.cena_zakupu) AS dochod
FROM zamowienie AS z
INNER JOIN pozycja_zamowienia AS p
ON p.zamowienie = z.id_zamowienia
INNER JOIN  towar as t
ON t.id_towaru = p.towar
WHERE z.status_zamowienia = 5 
GROUP BY rok
```

## Zadanie 8
```sql
SELECT k.nazwa_kategori, SUM(s.ilosc*t.cena_zakupu) AS wartosc
FROM towar AS t
INNER JOIN stan_magazynowy AS s ON s.towar = t.id_towaru
INNER JOIN kategoria AS k ON k.id_kategori = t.kategoria
GROUP BY k.nazwa_kategori
```

## Zadanie 9
```sql
SELECT MONTHNAME(data_urodzenia) AS Miesiac, COUNT(*) AS Liczba_pracownikow
FROM pracownik AS p
GROUP BY Miesiac
ORDER BY MONTH(data_urodzenia)
```

## Zadanie 10
```sql
SELECT p.imie,p.nazwisko, 
TIMESTAMPDIFF(MONTH,data_zatrudnienia,CURDATE()) * p.pensja AS koszt
FROM pracownik AS p
```