# Bazy Danych - Laboratorium 3
## Zadanie 1
```sql
CREATE TABLE postac
(
id_postaci INT AUTO_INCREMENT PRIMARY KEY,
nazwa VARCHAR(40) NOT NULL,
rodzaj ENUM('wiking','ptak','kobieta') NOT NULL,
data_ur DATE NOT NULL,
wiek INT UNSIGNED
);
```
```sql
INSERT INTO postac
VALUES
(
default,'Bjorn','wiking','1657-10-28',300
),
(
default,'Drozd','ptak','1907-10-28',20
),
(
default,'Tesciowa','kobieta','0907-10-28',800
);
```
```sql
UPDATE postac 
SET wiek=88 
WHERE id_postaci = 3;
```
## Zadanie 2
```sql
CREATE TABLE walizka 
(
id_walizki INT AUTO_INCREMENT PRIMARY KEY,
pojemnosc INT UNSIGNED,
kolor ENUM('rozowy','czerwony','teczowy','zolty'),
id_wlasciciela INT,
FOREIGN KEY (id_wlasciciela) 
REFERENCES postac(id_postaci) 
ON DELETE CASCADE
);
```
```sql
ALTER TABLE walizka
ALTER kolor
SET DEFAULT 'rozowy';
```
```sql
INSERT INTO walizka
VALUES
(
DEFAULT,100,'zolty',1
),
(
DEFAULT,25,'czerwony',3
);
```
## Zadanie 3
```sql
CREATE TABLE izba
(
adres_budynku varchar(100),
nazwa_izby varchar(100),
metraz INT UNSIGNED,
wlasciciel INT,
PRIMARY KEY (adres_budynku, nazwa_izby),
FOREIGN KEY (wlasciciel)
REFERENCES postac(id_postaci)
ON DELETE SET NULL
);
```
```sql
ALTER TABLE izba 
ADD COLUMN kolor varchar(50) DEFAULT 'czarny'
AFTER metraz;
```
```sql
INSERT INTO izba 
VALUES 
(
'stumilowy las','spizarnia',10,DEFAULT,1
);
```
## Zadanie 4
```sql
CREATE TABLE przetwory
(
id_przetworu INT AUTO_INCREMENT PRIMARY KEY,
rok_produkcji INT(4) DEFAULT 1654,
id_wykonawcy INT NOT NULL,
zawartosc VARCHAR(64),
dodatek VARCHAR(32) DEFAULT 'papryczka chilli',
id_konsumenta INT,
FOREIGN KEY (id_wykonawcy) REFERENCES postac(id_postaci),
FOREIGN KEY (id_konsumenta) REFERENCES postac(id_postaci)
);
```
```sql
INSERT INTO przetwory
VALUES
(
default,default,1,'bigos z papryczka chilli',default,3
);
```
## Zadanie 5
```sql
INSERT INTO postac 
VALUES
(
default,'Ragnar','wiking','1620-02-12',345
),
(
default,'Ivar','wiking','1615-07-23',357
),
(
default,'Hvitserk','wiking','1600-01-02',400
),
(
default,'Ubba','wiking','1627-12-07',320
),
(
default,'Sigurd','wiking','1620-02-17',345
);
```
```sql
CREATE TABLE statek
(
nazwa VARCHAR(32) PRIMARY KEY,
rodzaj ENUM('Byrding', 'Drakkar', 'Knara', 'Langskip', 'Sneka') NOT NULL,
data_wodowania DATE,
max_ladownosc INT UNSIGNED
);
```
```sql
INSERT INTO statek
VALUES
(
'Lajba','Knara','1712-05-14',2000
),
(
'Okret','Langskip','1732-08-24',15000
);
```
```sql
ALTER TABLE postac ADD funkcja VARCHAR(32);
```
```sql
UPDATE postac 
SET funkcja = 'kapitan' 
WHERE id_postaci = 1;
```
```sql
ALTER TABLE postac ADD 
nazwa_statku varchar(32);

ALTER TABLE postac ADD
FOREIGN KEY (nazwa_statku) REFERENCES statek(nazwa);
```
```sql
UPDATE postac 
SET nazwa_statku = 'Okret' 
WHERE id_postaci=1 OR id_postaci=2 OR id_postaci BETWEEN 4 AND 6;

UPDATE postac 
SET nazwa_statku = 'Lajba' 
WHERE id_postaci BETWEEN 7 AND 8;
```
```sql
DELETE FROM izba WHERE nazwa_izby = 'spizarnia';
```
```sql
DROP TABLE izba;
```