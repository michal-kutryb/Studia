# Bazy Danych - Laboratorium 4
## Zadanie 1
```sql
DELETE FROM postac 
WHERE wiek = 400 OR wiek = 357;
```
```sql
ALTER TABLE walizka DROP FOREIGN KEY walizka_ibfk_1 ;
ALTER TABLE przetwory DROP FOREIGN KEY przetwory_ibfk_1 ;
ALTER TABLE przetwory DROP FOREIGN KEY przetwory_ibfk_2 ;
ALTER TABLE postac MODIFY id_postaci INT NOT NULL;
ALTER TABLE postac DROP primary key;
```
## Zadanie 2
```sql
ALTER TABLE postac 
ADD pesel VARCHAR(11);

UPDATE postac SET pesel = '12345678912' WHERE id_postaci = 1;
UPDATE postac SET pesel = '22345678912' WHERE id_postaci = 2;
UPDATE postac SET pesel = '32345678912' WHERE id_postaci = 3;
UPDATE postac SET pesel = '42345678912' WHERE id_postaci = 4;
UPDATE postac SET pesel = '52345678912' WHERE id_postaci = 7;
UPDATE postac SET pesel = '62345678912' WHERE id_postaci = 8;

ALTER TABLE postac 
ADD PRIMARY KEY (pesel);
```
```sql
ALTER TABLE postac 
MODIFY COLUMN rodzaj 
ENUM('wiking','ptak','kobieta','syrena');
```
```sql
INSERT INTO postac
VALUES
(
9,'Gertruda Nieszczera','syrena','1515-12-12',515,DEFAULT,DEFAULT,'15151515151'
);
```
## Zadanie 3
```sql
UPDATE postac 
SET nazwa_statku = "Okret" 
WHERE nazwa LIKE '%a%';
```
```sql
UPDATE statek
SET max_ladownosc = 0.7 * max_ladownosc
WHERE data_wodowania BETWEEN '1901-01-01' AND '2000-12-31';
```
```sql
ALTER TABLE postac 
ADD CHECK (wiek<=1000);
```
## Zadanie 4
```sql
ALTER TABLE postac
MODIFY COLUMN rodzaj ENUM('wiking','ptak','kobieta','syrena','waz');

INSERT INTO postac 
VALUES
(
9,'Loko','waz','865-01-01',900,NULL,NULL,'91234567891'
);
```
```sql
CREATE TABLE marynarz AS 
    SELECT *
    FROM postac
    WHERE nazwa_statku IS NOT NULL;
```
```sql
ALTER TABLE marynarz 
ADD PRIMARY KEY (pesel);

ALTER TABLE marynarz 
ADD FOREIGN KEY (nazwa_statku) REFERENCES statek(nazwa);
```
## Zadanie 5
```sql
UPDATE marynarz 
SET nazwa_statku = NULL
WHERE nazwa_statku = 'Okret';

UPDATE postac 
SET nazwa_statku = NULL
WHERE nazwa_statku = 'Okret';
```
```sql
DELETE FROM marynarz WHERE nazwa = 'Ubba';

DELETE FROM postac WHERE nazwa = 'Ubba';
```
```sql
ALTER TABLE marynarz DROP FOREIGN KEY marynarz_ibfk_1;
ALTER TABLE postac DROP FOREIGN KEY postac_ibfk_1;

DELETE FROM statek;
```
```sql
DROP TABLE statek;
```
```sql
CREATE TABLE zwierz
(
id INT PRIMARY KEY AUTO_INCREMENT,
nazwa VARCHAR(40) NOT NULL,
wiek INT UNSIGNED NOT NULL
);
```
```sql
INSERT INTO zwierz
    SELECT id_postaci, nazwa, wiek
    FROM postac
    WHERE rodzaj = 'waz' OR rodzaj = 'ptak';
```