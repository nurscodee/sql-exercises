# SQL TEMELLERI

## SQL ODEV 1

Bu odevde SELECT ile veri cekmeyi WHERE ile karsilastirma ve mantiksal operatorleriyle kosul atmayi ogrendim.

### 1- SELECT Kullanimi

```sql
SELECT title,description FROM Film;
```

### 2- WHERE Kullanimi

- 1:

```sql
SELECT * FROM Film
WHERE length > 60 AND length < 75;
```

- 2:

```sql
SELECT * FROM Film
WHERE rental_rate = 0.99 AND rental_rate = 12.99 OR rental_rate = 28.99;
```

(Burada and verilererine baktiktan sonra or verisi sanki tekrar basliyormus gibi oluyor)

- 3:

- Question: customer tablosunda bulunan first_name sütunundaki değeri 'Mary' olan müşterinin last_name sütunundaki değeri nedir?

- Answer: Smith

```sql
SELECT * FROM Customer
WHERE first_name = 'Mary';
```

- 4:

```sql
SELECT * FROM Film
WHERE (NOT length > 50) AND (rental_rate != 2.99 OR rental_rate != 4.99);
```

## SQL ODEV 2

Bu odevimde BETWEEN AND ve IN yapisini ogrendim. BETWEEN AND yapisi AND yapisina benzerken IN yapisi OR yapisina benzemektedir.

- 1:

```sql
SELECT * FROM Film
WHERE replacement_cost BETWEEN  12.99 AND 16.99;
```

- 2:

```sql
SELECT * FROM actor
WHERE first_name IN ('Penelope','Nick','Ed');
```

- 3:

```sql
SELECT * FROM Film
WHERE rental_rate IN (0.99,2.99,4.99) AND replacement_cost IN (12.99,15.99,28.99);
```

## SQL ODEV 3

Bu derste LIKE ve ILIKE yapisini ogrendim. Burada kullanilan wildcard sembolleri sayesinde kolayca veriler arasinda gezinebilir. %(yuzde) wildcard sembolu sifir,bir veya daha fazla karakteri temsil ederken \_(alt cizgi) wildcard sembolu bir karakteri temsil eder. ILIKE ise LIKE operatorunun case-insensitive versiyonudur.

- 1:

```sql
SELECT * FROM country
WHERE country LIKE 'A%a';
```

- 2:

```sql
SELECT * FROM country
WHERE country LIKE '_____n';
```

(Burada alti karakter icin her bir karakteri alt cizgi wildcard sembolu koyuldu).

- 3:

```sql
SELECT * FROM country
WHERE country ILIKE '%T%';
```

- 4:

```sql
SELECT * FROM Film
WHERE title LIKE 'C%' AND length > 90 AND rental_rate = 2.99;
```

## SQL ODEV 4

Bu derste distinct ve count yapisini ogrendim. DISTINCT yapisi sutunda birden fazla ayni olan degerleri tek bir tane(uniq) olarak gosterir. COUNT yapisi aggregate fonksiyonlar ilgili sorgu sonucunda olusan veri sayisini gosterir.

- 1:

```sql
SELECT DISTINCT replacement_cost FROM Film;
```

- 2:

```sql
SELECT COUNT(DISTINCT replacement_cost) FROM Film;
```

(21 tane veri vardir.)

- 3:

```sql
SELECT COUNT(*) FROM Film
WHERE title LIKE 'T%' AND rating = 'G';
```

(9 tane veri vardir.)

- 4:

```sql
SELECT COUNT(*) FROM Country
WHERE country LIKE '_____';
```

(13 tane veri vardir.)

- 5:

```sql
SELECT COUNT(*) FROM City
WHERE city ILIKE '%R';
```

(33 tane veri vardir.)

## SQL ODEV 5

Bu derste ORDER BY, LIMIT ve OFFSET yapilarini ogrendim. ORDER BY; herhangi bir sutunda bulunan degerlere gore artan veya azalan bir sekilde siralayabiliriz. (ASC: artan(default),DESC: azalan) LIMIT; kosullari saglayan verilerin tamamini degil belirli sayida olanlari siralamak icin kullanilirken OFFSET; bazi durumlarda veri grubu icerisinde bazilarini pass gecmek icin kullanilir.

- 1:

```sql
SELECT title FROM Film
WHERE title LIKE '%n'
ORDER BY length DESC
LIMIT 5;
```

- 2:

```sql
SELECT title FROM Film
WHERE title LIKE '%n'
ORDER BY length ASC
OFFSET 4
LIMIT 10;
```

- 3:

```sql
SELECT * FROM Customer
WHERE store_id = 1
ORDER BY last_name DESC
LIMIT 4;
```

## SQL ODEV 6

Bu derste Aggregate fonksiyonlarini ogrendim.

- AVG fonksiyonu; sayisal degerlerden olusan sutunun ortalamasini alir.
- SUM fonksiyonu; sayisal degerlerden olusan sutunun toplamini alir.
- MAX fonksiyonu; sayisal degerlerden olusan sutunun en yuksek degerini alir.
- MIN fonksiyonu; sayisal degerlerden olusan sutunun en dusuk degerini alir.

!! Aggregate fonksiyonlardan sonra sutun kullanimi olmaz

- 1:

```sql
SELECT ROUND(AVG(rental_rate),3) FROM Film;
```

(ROUND burada yuvarlamak icin kullanilir);

- 2:

```sql
SELECT COUNT(title) FROM Film
WHERE title LIKE 'C%';
```

- 3:

```sql
SELECT length FROM Film
WHERE rental_rate = 0.99
ORDER BY length DESC
LIMIT 1;
```

- 4:

```sql
SELECT COUNT(DISTINCT replacement_cost) FROM Film
WHERE length > 150;
```

## SQL ODEV 7

Bu derste GROUP BY, HAVING ve ALIAS(AS) kullanimini ogrendim. HAVING; kelime sayesinde gruplanmis verilere kosullar ekleyebiliriz. AS kullanimi, sorgular sonucu olusturdugumuz sanal tablo ve sutunlara gecici isimler verebiliriz.

- 1:

```sql
SELECT rating FROM Film
GROUP BY rating;
```

- 2:

```sql
SELECT replacement_cost FROM Film
GROUP BY replacement_cost
HAVING COUNT(*) > 50;
```

- 3:

```sql
SELECT store_id, COUNT(first_name) FROM Customer
GROUP BY store_id;
```

- 4:

```sql
SELECT country_id, COUNT(*) AS sehir_sayisi FROM City
GROUP BY country_id
ORDER BY sehir_sayisi DESC
LIMIT 1;
```

## SQL ODEV 8

Bu derste tablo olusturmayi, veri eklemeyi, eklenen veri uzerinde guncelleme veya silme islemi ve tablo silme komutlari ogrendim.

- 1:

```sql
CREATE DATABASE test;
```

- 2:

```sql
CREATE TABLE employee(
	id INTEGER,
	name VARCHAR(50),
	birthday DATE,
	email VARCHAR(100)
);
```

- 3:

```sql
insert into employee (id, name, birthday, email) values (1, 'Mindy', '1984-07-02', 'mburghall0@smh.com.au');
insert into employee (id, name, birthday, email) values (2, 'Cara', '1988-08-24', 'carnault1@myspace.com');
insert into employee (id, name, birthday, email) values (3, 'Vince', '1980-07-09', 'vgiacobilio2@arstechnica.com');
insert into employee (id, name, birthday, email) values (4, 'Lionello', '1983-07-12', 'lfaulkes3@ox.ac.uk');
insert into employee (id, name, birthday, email) values (5, 'Shepard', '1992-07-25', 'sthirsk4@purevolume.com');
insert into employee (id, name, birthday, email) values (6, 'Quinta', '1988-07-01', 'qrosewarne5@facebook.com');
insert into employee (id, name, birthday, email) values (7, 'Dulce', '1984-11-15', 'dconnue6@home.pl');
insert into employee (id, name, birthday, email) values (8, 'Mufinella', '1992-02-25', 'mmccallister7@ucla.edu');
insert into employee (id, name, birthday, email) values (9, 'Lutero', '1997-06-11', 'lbenedicte8@cbc.ca');
insert into employee (id, name, birthday, email) values (10, 'Cecile', '1989-10-03', 'cbailie9@imdb.com');
```

- 4:

```sql
UPDATE employee
SET name='Maria'
WHERE id=1;
```

- 5:

```sql
DELETE FROM employee
WHERE id=8;
```

## SQL ODEV 9

Bu derse INNER JOIN yapisini ogrendim. JOIN yapisi aslinda bir birlestirme yapisidir. INNER JOIN ise tablo1 ve tablo2 icin kesisen bilgileri alir ve birlestirir.

- 1:

```sql
SELECT city,country FROM city
INNER JOIN country ON city.country_id = country.country_id;
```

- 2:

```sql
SELECT payment_id, first_name, last_name FROM customer
INNER JOIN payment ON customer.customer_id = payment.customer_id;
```

- 3:

```sql
SELECT rental_id, first_name, last_name FROM customer
INNER JOIN rental ON customer.customer_id = rental.customer_id;
```

## SQL ODEV 10

Bu derste LEFT JOIN, RIGHT JOIN ve FULL JOIN ogrendim. LEFT JOIN yapisi tablo1'i referans alarak tablo1 de bulunan elemanlari hepsini yazdirir ve karsilik gelen bulunmadiginda NULL dondurur. RIGHT JOIN yapisi tablo2'yi referans alarak tablo2 de bulunan elemanlarin hepsini yazdirir ve karsilik gelen bulunmadiginda NULL dondurur. FULL JOIN ise tablo1 ile tablo2'nin birlesim kumelerini alir ve bastirir.

- 1:

```sql
SELECT country, city FROM country
LEFT JOIN city ON city.country_id = country.country_id;
```

- 2:

```sql
SELECT payment_id, first_name, last_name FROM customer
RIGHT JOIN payment ON payment.customer_id = customer.customer_id;
```

- 3:

```sql
SELECT rental_id, first_name, last_name FROM customer
FULL JOIN rental ON rental.customer_id = customer.customer_id;
```

## SQL ODEV 11

Bu derste UNION, INTERSECT ve EXCEPT yapilarini ogrendim. UNION operatoru sayesinde farkli SELECT sorgulariyla olusan sonuclari tek bir sonuc kumesi haline getiririz. INTERSECT operatoru sayesinde farkli SELECT sorgulariyla olusan sonuclarin kesisen verilerini tek bir sonuc kumesi haline getiririz. EXCEPT operatoru sayesinde ilk sorguda olup ikinci sorguda olmayan verileri gosterir.

!! Bu uc yapida tekrar eden verileri gostermez. Tekrar edenleri gormek icin UNION ALL, INTERSECT ALL ve EXCEPT ALL seklinde ALL yapisini kullaniriz.

!! Bu uc yapida kullanilacagi sorgularin, sutun sayisi ve sutunlardaki veri tipleri esit olmalidir.

- 1:

```sql
(
SELECT first_name FROM actor
)
UNION
(
SELECT first_name FROM customer
);
```

- 2:

```sql
(
SELECT first_name FROM actor
)
INTERSECT
(
SELECT first_name FROM customer
);
```

- 3:

```sql
(
SELECT first_name FROM actor
)
EXCEPT
(
SELECT first_name FROM customer
);
```

## SQL ODEV 12

Bu derste alt sorgu yapisini ve ANY ile ALL operatorunu ogrendim. Alt sorgu; bir sorgu icerisinde o sorgunun ihtiyac duydugu veri veya verileri getiren sorgulardir. ANY; alt sorgudan gelen herhangi bir deger kosulu saglamasi durumunda TRUE olarak ilgili degerin kosul saglamasini saglar. ALL; alt sorgudan gelen tum degerlerin kosulu saglamasi durumunda TRUE doner.

- 1:

```sql
SELECT COUNT(length) FROM film
WHERE length > (SELECT AVG(length) FROM film);
```

- 2:

```sql
SELECT COUNT(rental_rate) FROM film
WHERE rental_rate = (SELECT MAX(rental_rate) FROM film);
```

- 3:

```sql
SELECT title FROM film
WHERE rental_rate = (SELECT MIN(rental_rate) FROM film)
AND replacement_cost = (SELECT MIN(replacement_cost) FROM film);
```

- 4:

```sql
SELECT first_name, last_name, amount FROM customer
INNER JOIN payment ON payment.customer_id = customer.customer_id
ORDER BY amount DESC;
```

_Boylelikle sql sorgusu ve temel sql komutlarini ogrendim. Bu calisma [patika.dev](https://www.skillcamp.dev/tr/courses/sql/) de bulunan nodeJs patikasi icerisinde yer alan sql dersi ile ogrendigim temel sql yapisidir. PostgreSQL kullanildi ve terminal uzerinden de ogrenimim saglandi. Ornekler dvdrental veritabani uzerinden sorgulamalar gerceklestirilmistir. Bu veritabanina ulasmak icin [dvdrental](https://neon.com/postgresql/getting-started/sample-database) seklinde ulasabilirsiniz._
