# Bazy Danych - Praca Domowa
## 05.01.2023

### Zadanie 3
```sql
SELECT nazwa, COUNT(pracownik.id_pracownika)
FROM dzial
INNER JOIN pracownik ON dzial.id_dzialu=pracownik.dzial
GROUP BY nazwa;
```

### Zadanie 4
```sql
SELECT kategoria.nazwa_kategori, COUNT(*) AS ile
FROM kategoria
INNER JOIN towar
ON towar.kategoria = kategoria.id_kategori
GROUP BY kategoria.nazwa_kategori;
```

### Zadanie 5
```sql
SELECT kategoria.nazwa_kategori, group_concat(towar.nazwa_towaru)
FROM kategoria
INNER JOIN towar
ON towar.kategoria = kategoria.id_kategori
GROUP BY kategoria.nazwa_kategori;
```

### Zadanie 6
```sql
SELECT ROUND(AVG(pensja),2) AS srednia_pensja
FROM pracownik;
```

### Zadanie 7
```sql
SELECT ROUND(AVG(pensja),2) AS srednia_pensja
FROM pracownik
WHERE YEAR(CURDATE()) - YEAR(data_zatrudnienia)>=5;
```

### Zadanie 8
```sql
SELECT nazwa_towaru, COUNT(*)
FROM pozycja_zamowienia AS t1
INNER JOIN towar AS t2 ON t2.id_towaru = t1.towar
GROUP BY id_towaru
ORDER BY COUNT(*) DESC
LIMIT 10;
```

### Zadanie 9
```sql
SELECT t1.numer_zamowienia, SUM(t2.ilosc*t2.cena) AS wartosc
FROM zamowienie AS t1
INNER JOIN pozycja_zamowienia AS t2 ON t1.id_zamowienia = t2.zamowienie
WHERE (MONTH(t1.data_zamowienia) BETWEEN 1 AND 4) AND (YEAR(t1.data_zamowienia) = 2017)
GROUP BY t1.id_zamowienia;
```

### Zadanie 10
```sql
SELECT t3.imie,t3.nazwisko, SUM(t2.ilosc*t2.cena) AS wartosc
FROM zamowienie AS t1
INNER JOIN pozycja_zamowienia AS t2 ON t1.id_zamowienia = t2.zamowienie
INNER JOIN pracownik AS t3 ON t3.id_pracownika = t1.pracownik_id_pracownika
GROUP BY t3.id_pracownika
ORDER BY wartosc DESC
```