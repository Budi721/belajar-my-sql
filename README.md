#----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Intro to MySQL

### Untuk membuka MySQL
```
mysql -uroot -p
```

### Untuk menampilkan Database
```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.05 sec)
```

### Untuk menggunakan Database 
```
use belajar_mysql
```

### Untuk menampilkan Tabel
```
show tables;
+-------------------------+
| Tables_in_belajar_mysql |
+-------------------------+
| barang                  |
+-------------------------+
1 row in set (0.00 sec)
```

## Tabel di MySQL

### Untuk membuat tabel

```
CREATE TABLE barang (
    -> id INT,
    -> nama VARCHAR(100),
    -> harga INT,
    -> jumlah INT
    );
Query OK, 0 rows affected (0.08 sec)
```

### Alter Command 

#### Menambahkan Kolom
```
ALTER TABLE barang
    -> ADD COLUMN deskripsi TEXT;
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

#### Menghapus Kolom
```
ALTER TABLE barang 
    -> DROP COLUMN salah;
Query OK, 0 rows affected (0.10 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

#### Memodifikasi Tipe Data Kolom 
```
ALTER TABLE barang
    -> MODIFY nama VARCHAR(200) AFTER deskripsi;
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0

DESC barang;       
+-----------+--------------+------+-----+---------+-------+
| Field     | Type         | Null | Key | Default | Extra |
+-----------+--------------+------+-----+---------+-------+
| id        | int(11)      | YES  |     | NULL    |       |
| harga     | int(11)      | YES  |     | NULL    |       |
| jumlah    | int(11)      | YES  |     | NULL    |       |
| deskripsi | text         | YES  |     | NULL    |       |
| nama      | varchar(200) | YES  |     | NULL    |       |
+-----------+--------------+------+-----+---------+-------+
5 rows in set (0.00 sec)
```

#### Untuk menampilkan Tabel
```
SELECT * FROM barang 
    -> ;
+------+----+-------+--------+-----------+---------------------+
| nama | id | harga | jumlah | deskripsi | waktu_dibuat        |
+------+----+-------+--------+-----------+---------------------+
| Apel |  1 |     0 |      0 | NULL      | 2021-02-22 23:11:00 |
+------+----+-------+--------+-----------+---------------------+
1 row in set (0.00 sec)
```

#### Untuk menghapus Data di dalam Tabel (Tidak termasuk Tabelnya)
```
TRUNCATE barang;
Query OK, 0 rows affected (0.06 sec)
```

> Untuk menghapus tabel menggunakan command 
> ```DROP TABLE barang```

#### Untuk memasukkan Data ke dalam Tabel
```
INSERT INTO products (id, name, description, price, quantity)
    -> VALUES ('P0002', 'Mie Ayam Bakso Tahu', 'Mie Ayam Original + Bakso Tahu', 20000,100);
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM products;
+-------+---------------------+--------------------------------+-------+----------+---------------------+
| id    | name                | description                    | price | quantity | created_at          |
+-------+---------------------+--------------------------------+-------+----------+---------------------+
| P0001 | Mie Ayam Original   | NULL                           | 15000 |      100 | 2021-02-22 23:21:41 |
| P0002 | Mie Ayam Bakso Tahu | Mie Ayam Original + Bakso Tahu | 20000 |      100 | 2021-02-22 23:27:47 |
+-------+---------------------+--------------------------------+-------+----------+---------------------+
2 rows in set (0.00 sec)
```

## Auto Increment
```
CREATE TABLE admin
    -> (
    ->     id         INT          NOT NULL AUTO_INCREMENT,
    ->     first_name VARCHAR(100) NOT NULL,
    ->     last_name  VARCHAR(100) NOT NULL,
    ->     PRIMARY KEY (id)
    -> ) ENGINE = InnoDB;
Query OK, 0 rows affected (0.06 sec)
```

> Dengan menambahkan properti AUTO_INCREMENT ke kolom yang dituju

## String Fungsi 
```
SELECT id,
    ->        LOWER(name)  as 'Name Lower',
    ->        UPPER(name)  as 'Name Lower',
    ->        LENGTH(name) as 'Name Length'
    -> FROM products;
+-------+---------------------+---------------------+-------------+
| id    | Name Lower          | Name Lower          | Name Length |
+-------+---------------------+---------------------+-------------+
| P0001 | mie ayam original   | MIE AYAM ORIGINAL   |          17 |
| P0002 | mie ayam bakso tahu | MIE AYAM BAKSO TAHU |          19 |
| P0003 | mie ayam ceker      | MIE AYAM CEKER      |          14 |
| P0004 | mie ayam spesial    | MIE AYAM SPESIAL    |          16 |
| P0005 | mie ayam yamin      | MIE AYAM YAMIN      |          14 |
| P0006 | bakso rusuk         | BAKSO RUSUK         |          11 |
| P0007 | es jeruk            | ES JERUK            |           8 |
| P0008 | es campur           | ES CAMPUR           |           9 |
| P0009 | es teh manis        | ES TEH MANIS        |          12 |
| P0010 | kerupuk             | KERUPUK             |           7 |
| P0011 | keripik udang       | KERIPIK UDANG       |          13 |
| P0012 | es krim             | ES KRIM             |           7 |
| P0013 | mie ayam jamur      | MIE AYAM JAMUR      |          14 |
| P0014 | bakso telor         | BAKSO TELOR         |          11 |
| P0015 | bakso jando         | BAKSO JANDO         |          11 |
+-------+---------------------+---------------------+-------------+
15 rows in set (0.02 sec)
```

## Date Time Fungsi 
```
SELECT id,
    ->        created_at,
    ->        EXTRACT(YEAR FROM created_at)  as Year,
    ->        EXTRACT(MONTH FROM created_at) as Month
    -> FROM products;
+-------+---------------------+------+-------+
| id    | created_at          | Year | Month |
+-------+---------------------+------+-------+
| P0001 | 2021-02-23 14:21:41 | 2021 |     2 |
| P0002 | 2021-02-23 14:27:47 | 2021 |     2 |
| P0003 | 2021-02-23 14:31:03 | 2021 |     2 |
| P0004 | 2021-02-23 14:31:03 | 2021 |     2 |
| P0005 | 2021-02-23 14:31:03 | 2021 |     2 |
| P0006 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0007 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0008 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0009 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0010 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0011 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0012 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0013 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0014 | 2021-02-23 16:12:53 | 2021 |     2 |
| P0015 | 2021-02-23 16:12:53 | 2021 |     2 |
+-------+---------------------+------+-------+
15 rows in set (0.00 sec)

mysql> SELECT id, created_at, YEAR(created_at), MONTH(created_at)
    -> FROM products;
+-------+---------------------+------------------+-------------------+
| id    | created_at          | YEAR(created_at) | MONTH(created_at) |
+-------+---------------------+------------------+-------------------+
| P0001 | 2021-02-23 14:21:41 |             2021 |                 2 |
| P0002 | 2021-02-23 14:27:47 |             2021 |                 2 |
| P0003 | 2021-02-23 14:31:03 |             2021 |                 2 |
| P0004 | 2021-02-23 14:31:03 |             2021 |                 2 |
| P0005 | 2021-02-23 14:31:03 |             2021 |                 2 |
| P0006 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0007 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0008 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0009 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0010 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0011 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0012 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0013 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0014 | 2021-02-23 16:12:53 |             2021 |                 2 |
| P0015 | 2021-02-23 16:12:53 |             2021 |                 2 |
+-------+---------------------+------------------+-------------------+
15 rows in set (0.00 sec)
```

## Control Flow in MySQL
```
SELECT id,
    ->        category,
    ->        CASE category
    ->            WHEN 'Makanan' THEN 'Enak'
    ->            WHEN 'Minuman' THEN 'Segar'
    ->            ELSE 'Apa Itu?'
    ->            END AS 'Category'
    -> FROM products;
+-------+-----------+----------+
| id    | category  | Category |
+-------+-----------+----------+
| P0001 | Makanan   | Enak     |
| P0002 | NULL      | Apa Itu? |
| P0003 | Makanan   | Enak     |
| P0004 | NULL      | Apa Itu? |
| P0005 | NULL      | Apa Itu? |
| P0006 | Makanan   | Enak     |
| P0007 | Minuman   | Segar    |
| P0008 | Minuman   | Segar    |
| P0009 | Minuman   | Segar    |
| P0010 | Lain-Lain | Apa Itu? |
| P0011 | Lain-Lain | Apa Itu? |
| P0012 | Lain-Lain | Apa Itu? |
| P0013 | Makanan   | Enak     |
| P0014 | Makanan   | Enak     |
| P0015 | Makanan   | Enak     |
+-------+-----------+----------+
15 rows in set (0.00 sec)

SELECT id, price, IF(price <= 15000, 'Murah', 'Mahal') as 'Mahal ?' FROM products;; 
+-------+-------+---------+
| id    | price | Mahal ? |
+-------+-------+---------+
| P0001 | 15000 | Murah   |
| P0002 | 20000 | Mahal   |
| P0003 | 20000 | Mahal   |
| P0004 | 25000 | Mahal   |
| P0005 | 20000 | Mahal   |
| P0006 | 25000 | Mahal   |
| P0007 | 10000 | Murah   |
| P0008 | 15000 | Murah   |
| P0009 |  5000 | Murah   |
| P0010 |  2500 | Murah   |
| P0011 | 10000 | Murah   |
| P0012 |  5000 | Murah   |
| P0013 | 20000 | Mahal   |
| P0014 | 20000 | Mahal   |
| P0015 | 25000 | Mahal   |
+-------+-------+---------+
15 rows in set (0.00 sec)

ERROR:
No query specified

SELECT id, price, IF(price <= 15000, 'Murah', IF(price <= 20000, 'Mahal', 'Mahal Banget')) as 'Mahal ?' FROM products;; 
+-------+-------+--------------+
| id    | price | Mahal ?      |
+-------+-------+--------------+
| P0001 | 15000 | Murah        |
| P0002 | 20000 | Mahal        |
| P0003 | 20000 | Mahal        |
| P0004 | 25000 | Mahal Banget |
| P0005 | 20000 | Mahal        |
| P0006 | 25000 | Mahal Banget |
| P0007 | 10000 | Murah        |
| P0008 | 15000 | Murah        |
| P0009 |  5000 | Murah        |
| P0010 |  2500 | Murah        |
| P0011 | 10000 | Murah        |
| P0012 |  5000 | Murah        |
| P0013 | 20000 | Mahal        |
| P0014 | 20000 | Mahal        |
| P0015 | 25000 | Mahal Banget |
+-------+-------+--------------+
15 rows in set (0.00 sec)

ERROR:
No query specified

SELECT id, name, IFNULL(description, 'Kosong') as deskripsi FROM products;   
+-------+---------------------+--------------------------------+
| id    | name                | deskripsi                      |
+-------+---------------------+--------------------------------+
| P0001 | Mie Ayam Original   | Kosong                         |
| P0002 | Mie Ayam Bakso Tahu | Mie Ayam Original + Bakso Tahu |
| P0003 | Mie Ayam Ceker      | Mie Ayam + Ceker               |
| P0004 | Mie Ayam Spesial    | Kosong                         |
| P0005 | Mie Ayam Yamin      | Kosong                         |
| P0006 | Bakso Rusuk         | Kosong                         |
| P0007 | Es Jeruk            | Kosong                         |
| P0008 | Es Campur           | Kosong                         |
| P0009 | Es Teh Manis        | Kosong                         |
| P0010 | Kerupuk             | Kosong                         |
| P0011 | Keripik Udang       | Kosong                         |
| P0012 | Es Krim             | Kosong                         |
| P0013 | Mie Ayam Jamur      | Kosong                         |
| P0014 | Bakso Telor         | Kosong                         |
| P0015 | Bakso Jando         | Kosong                         |
+-------+---------------------+--------------------------------+
15 rows in set (0.02 sec)
```

## Agregate Fungsi 
```
mysql> SELECT SUM(quantity) AS 'Total Stock'
    -> FROM products;
+-------------+
| Total Stock |
+-------------+
|        3900 |
+-------------+
1 row in set (0.00 sec)

SELECT AVG(price) as 'Rata-Rata Harga'
    -> FROM products;
+-----------------+
| Rata-Rata Harga |
+-----------------+
|      15833.3333 |
+-----------------+
1 row in set (0.00 sec)

SELECT MIN(price) as 'Product Termurah'
    -> FROM products;
+------------------+
| Product Termurah |
+------------------+
|             2500 |
+------------------+
1 row in set (0.00 sec)

SELECT MAX(price) as 'Product Termahal'
    -> FROM products;
+------------------+
| Product Termahal |
+------------------+
|            25000 |
+------------------+
1 row in set (0.00 sec)

SELECT COUNT(id) as 'Total Product'
    -> FROM products;
+---------------+
| Total Product |
+---------------+
|            15 |
+---------------+
1 row in set (0.00 sec)
```

## Grouping
```
SELECT SUM(quantity) AS 'Total Stock', category FROM products GROUP BY category;
+-------------+-----------+
| Total Stock | category  |
+-------------+-----------+
|         900 | Makanan   |
|        1200 | Minuman   |
|        1500 | Lain-Lain |
+-------------+-----------+
3 rows in set (0.00 sec)

SELECT COUNT(id) as total,
    ->        category
    -> FROM products
    -> GROUP BY category
    -> HAVING total > 5;
+-------+----------+
| total | category |
+-------+----------+
|     6 | Makanan  |
+-------+----------+
1 row in set (0.00 sec)

```

## Constraint

### Unique Constraint
> Unique constraint agar isi di kolom yang kolom constraint tidak terdapat duplikasi data
> Secara otomatis ```PRIMARY KEY``` masuk ke dalam ```UNIQUE CONSTRAINT```

#### Perintah saat baru membuat tabel
```
CREATE TABLE customers(
    -> id INT NOT NULL AUTO_INCREMENT,
    -> email VARCHAR(100) NOT NULL,
    -> first_name VARCHAR(100) NOT NULL,
    -> last_name VARCHAR(100),
    -> PRIMARY KEY(id),
    -> UNIQUE KEY email_unique(email)
    -> ) ENGINE = InnoDB;
Query OK, 0 rows affected (0.05 sec)

mysql> DESCRIBE customers;
+------------+--------------+------+-----+---------+----------------+
| Field      | Type         | Null | Key | Default | Extra          |
+------------+--------------+------+-----+---------+----------------+
| id         | int(11)      | NO   | PRI | NULL    | auto_increment |
| email      | varchar(100) | NO   | UNI | NULL    |                |
| first_name | varchar(100) | NO   |     | NULL    |                |
| last_name  | varchar(100) | YES  |     | NULL    |                |
+------------+--------------+------+-----+---------+----------------+
4 rows in set (0.01 sec)
```

#### Menghapus dan Menambahkan Constraint saat tabel sudah dibuat
```
ALTER TABLE customers
    -> DROP CONSTRAINT email_unique;
```
> Untuk menambahkan tinggal ganti perintah ```DROP``` dengan ```ADD```

### Check Contraint
> Untuk memberikan syarat data untuk kolom tersebut 
```
 ALTER TABLE products
    ->     ADD CONSTRAINT price_check CHECK ( price >= 1000 );
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0
```
> Setelah dimasukkan perintah tersebut kolom price tidak boleh lebih dari 1000

## Index 

> Menyimpan data dalam B-Tree 
> Proses query menjadi lebih cepat, tetapi untuk memanipulasi data menjadi lebih lambat
> Ketika membuat primary key dan unique key tidak perlu menambahkan index

```
CREATE TABLE sellers
    -> (
    ->     id    INT          NOT NULL AUTO_INCREMENT,
    ->     name  VARCHAR(100) NOT NULL,
    ->     name2 VARCHAR(100) ,
    ->     name3 VARCHAR(100) ,
    ->     email VARCHAR(100) NOT NULL,
    ->     PRIMARY KEY (id),
    ->     UNIQUE KEY email_unique (email),
    ->     INDEX name_index (name),
    ->     INDEX name2_index (name2),
    ->     INDEX name3_index (name3),
    ->     INDEX name1_name2_name3_index (name, name2, name3)
    -> ) ENGINE = InnoDB;
Query OK, 0 rows affected (0.07 sec)

DESC sellers;
+-------+--------------+------+-----+---------+----------------+
| Field | Type         | Null | Key | Default | Extra          |
+-------+--------------+------+-----+---------+----------------+
| id    | int(11)      | NO   | PRI | NULL    | auto_increment |
| name  | varchar(100) | NO   | MUL | NULL    |                |
| name2 | varchar(100) | YES  | MUL | NULL    |                |
| name3 | varchar(100) | YES  | MUL | NULL    |                |
| email | varchar(100) | NO   | UNI | NULL    |                |
+-------+--------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)
```

## Full Text Search 

### Menambahkan FTS
```
ALTER TABLE products
    -> ADD FULLTEXT product_search(name, description);
Query OK, 0 rows affected, 1 warning (0.37 sec)
Records: 0  Duplicates: 0  Warnings: 1
```

### Menghapus FTS
```
ALTER TABLE products
    -> DROP INDEX product_search;
Query OK, 0 rows affected (0.10 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

### Contoh FTS dengan Tiga Mode Berbeda
```
 SELECT *
    -> FROM products
    -> WHERE MATCH(name, description)
    ->             AGAINST('ayam' IN NATURAL LANGUAGE MODE);
+-------+-------------------+----------+------------------+-------+----------+---------------------+
| id    | name              | category | description      | price | quantity | created_at          |
+-------+-------------------+----------+------------------+-------+----------+---------------------+
| P0003 | Mie Ayam Ceker    | Makanan  | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 |
| P0001 | Mie Ayam Original | Makanan  | NULL             | 15000 |      100 | 2021-02-23 14:21:41 |
| P0013 | Mie Ayam Jamur    | Makanan  | NULL             | 20000 |       50 | 2021-02-23 16:12:53 |
+-------+-------------------+----------+------------------+-------+----------+---------------------+
3 rows in set (0.01 sec)


 SELECT *
    -> FROM products
    -> WHERE MATCH(name, description)
    ->             AGAINST('+ayam -jamur' IN BOOLEAN MODE); 
+-------+-------------------+----------+------------------+-------+----------+---------------------+
| id    | name              | category | description      | price | quantity | created_at          |
+-------+-------------------+----------+------------------+-------+----------+---------------------+
| P0003 | Mie Ayam Ceker    | Makanan  | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 |
| P0001 | Mie Ayam Original | Makanan  | NULL             | 15000 |      100 | 2021-02-23 14:21:41 |
+-------+-------------------+----------+------------------+-------+----------+---------------------+
2 rows in set (0.00 sec)

 SELECT *
    -> FROM products
    -> WHERE MATCH(name, description)
    ->             AGAINST('bakso' WITH QUERY EXPANSION);
+-------+-------------+----------+-------------+-------+----------+---------------------+
| id    | name        | category | description | price | quantity | created_at          |
+-------+-------------+----------+-------------+-------+----------+---------------------+
| P0006 | Bakso Rusuk | Makanan  | NULL        | 25000 |      200 | 2021-02-23 16:12:53 |
| P0014 | Bakso Telor | Makanan  | NULL        | 20000 |      150 | 2021-02-23 16:12:53 |
| P0015 | Bakso Jando | Makanan  | NULL        | 25000 |      300 | 2021-02-23 16:12:53 |
+-------+-------------+----------+-------------+-------+----------+---------------------+
3 rows in set (0.00 sec)
```

## Tabel Relationship
```
CREATE TABLE wishlist
    -> (
    ->     id          INT         NOT NULL AUTO_INCREMENT,
    ->     id_product  VARCHAR(10) NOT NULL,
    ->     description TEXT,
    ->     PRIMARY KEY (id),
    ->     CONSTRAINT fk_wishlist_product
    ->         FOREIGN KEY (id_product) REFERENCES products (id)
    -> ) ENGINE = InnoDB;  
Query OK, 0 rows affected (0.04 sec)
```

> Dengan perintah tersebut kolom id_product harus sesuai dengan kolom id di tabel products
> Ketika id di products akan dihapus juga tidak bisa karena sedang digunakan tabel wishlist
> kecuali menggunakan opsi lain CASCADE, OPTION, NOTNULL

## Join 
### Macam-macam Join
#### Inner Join (Default)

```
SELECT customers.email, products.id, products.name, wishlist.description
    -> FROM wishlist
    -> JOIN products ON (products.id = wishlist.id_product)
    -> JOIN customers ON (customers.id = wishlist.id_customer);
+---------------+-------+-------------------+------------------+
| email         | id    | name              | description      |
+---------------+-------+-------------------+------------------+
| eko@gmail.com | P0001 | Mie Ayam Original | Makanan Kesukaan |
+---------------+-------+-------------------+------------------+
1 row in set (0.00 sec)
```
```
SELECT *
    -> FROM categories
    ->          INNER JOIN products ON (products.id_category = categories.id);
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
| id    | name      | id    | name              | description      | price | quantity | created_at          | id_category |
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
| C0001 | Makanan   | P0001 | Mie Ayam Original | NULL             | 15000 |      100 | 2021-02-23 14:21:41 | C0001       |
| C0001 | Makanan   | P0003 | Mie Ayam Ceker    | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 | C0001       |
| C0001 | Makanan   | P0006 | Bakso Rusuk       | NULL             | 25000 |      200 | 2021-02-23 16:12:53 | C0001       |
| C0002 | Minuman   | P0007 | Es Jeruk          | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0008 | Es Campur         | NULL             | 15000 |      500 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0009 | Es Teh Manis      | NULL             |  5000 |      400 | 2021-02-23 16:12:53 | C0002       |
| C0003 | Lain-Lain | P0010 | Kerupuk           | NULL             |  2500 |     1000 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0011 | Keripik Udang     | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0012 | Es Krim           | NULL             |  5000 |      200 | 2021-02-23 16:12:53 | C0003       |
| C0001 | Makanan   | P0013 | Mie Ayam Jamur    | NULL             | 20000 |       50 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0014 | Bakso Telor       | NULL             | 20000 |      150 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0015 | Bakso Jando       | NULL             | 25000 |      300 | 2021-02-23 16:12:53 | C0001       |
| C0003 | Lain-Lain | P0016 | Permen            | NULL             |  1000 |     1000 | 2021-02-24 10:08:39 | C0003       |
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
13 rows in set (0.00 sec)
```

#### Left Join
```
SELECT *
    -> FROM categories
    ->          LEFT JOIN products ON (products.id_category = categories.id);
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
| id    | name      | id    | name              | description      | price | quantity | created_at          | id_category |
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
| C0001 | Makanan   | P0001 | Mie Ayam Original | NULL             | 15000 |      100 | 2021-02-23 14:21:41 | C0001       |
| C0001 | Makanan   | P0003 | Mie Ayam Ceker    | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 | C0001       |
| C0001 | Makanan   | P0006 | Bakso Rusuk       | NULL             | 25000 |      200 | 2021-02-23 16:12:53 | C0001       |
| C0002 | Minuman   | P0007 | Es Jeruk          | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0008 | Es Campur         | NULL             | 15000 |      500 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0009 | Es Teh Manis      | NULL             |  5000 |      400 | 2021-02-23 16:12:53 | C0002       |
| C0003 | Lain-Lain | P0010 | Kerupuk           | NULL             |  2500 |     1000 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0011 | Keripik Udang     | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0012 | Es Krim           | NULL             |  5000 |      200 | 2021-02-23 16:12:53 | C0003       |
| C0001 | Makanan   | P0013 | Mie Ayam Jamur    | NULL             | 20000 |       50 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0014 | Bakso Telor       | NULL             | 20000 |      150 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0015 | Bakso Jando       | NULL             | 25000 |      300 | 2021-02-23 16:12:53 | C0001       |
| C0003 | Lain-Lain | P0016 | Permen            | NULL             |  1000 |     1000 | 2021-02-24 10:08:39 | C0003       |
| C0004 | Oleh-Oleh | NULL  | NULL              | NULL             |  NULL |     NULL | NULL                | NULL        |
| C0005 | Gadget    | NULL  | NULL              | NULL             |  NULL |     NULL | NULL                | NULL        |
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
15 rows in set (0.01 sec)
```

#### Right Join 
```
SELECT *
    -> FROM categories
    ->          RIGHT JOIN products ON (products.id_category = categories.id);
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
| id    | name      | id    | name              | description      | price | quantity | created_at          | id_category |
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
| C0001 | Makanan   | P0001 | Mie Ayam Original | NULL             | 15000 |      100 | 2021-02-23 14:21:41 | C0001       |
| C0001 | Makanan   | P0003 | Mie Ayam Ceker    | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 | C0001       |
| C0001 | Makanan   | P0006 | Bakso Rusuk       | NULL             | 25000 |      200 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0013 | Mie Ayam Jamur    | NULL             | 20000 |       50 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0014 | Bakso Telor       | NULL             | 20000 |      150 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0015 | Bakso Jando       | NULL             | 25000 |      300 | 2021-02-23 16:12:53 | C0001       |
| C0002 | Minuman   | P0007 | Es Jeruk          | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0008 | Es Campur         | NULL             | 15000 |      500 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0009 | Es Teh Manis      | NULL             |  5000 |      400 | 2021-02-23 16:12:53 | C0002       |
| C0003 | Lain-Lain | P0010 | Kerupuk           | NULL             |  2500 |     1000 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0011 | Keripik Udang     | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0012 | Es Krim           | NULL             |  5000 |      200 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0016 | Permen            | NULL             |  1000 |     1000 | 2021-02-24 10:08:39 | C0003       |
| NULL  | NULL      | X0001 | X Satu            | NULL             | 25000 |      200 | 2021-02-24 13:53:23 | NULL        |
| NULL  | NULL      | X0002 | X Dua             | NULL             | 10000 |      300 | 2021-02-24 13:53:23 | NULL        |
| NULL  | NULL      | X0003 | X Tiga            | NULL             | 15000 |      500 | 2021-02-24 13:53:23 | NULL        |
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
16 rows in set (0.00 sec)
```

#### Cross Join
```
SELECT *
    -> FROM categories
    ->          CROSS JOIN products;
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
| id    | name      | id    | name              | description      | price | quantity | created_at          | id_category |
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
| C0001 | Makanan   | P0001 | Mie Ayam Original | NULL             | 15000 |      100 | 2021-02-23 14:21:41 | C0001       |
| C0002 | Minuman   | P0001 | Mie Ayam Original | NULL             | 15000 |      100 | 2021-02-23 14:21:41 | C0001       |
| C0003 | Lain-Lain | P0001 | Mie Ayam Original | NULL             | 15000 |      100 | 2021-02-23 14:21:41 | C0001       |
| C0004 | Oleh-Oleh | P0001 | Mie Ayam Original | NULL             | 15000 |      100 | 2021-02-23 14:21:41 | C0001       |
| C0005 | Gadget    | P0001 | Mie Ayam Original | NULL             | 15000 |      100 | 2021-02-23 14:21:41 | C0001       |
| C0001 | Makanan   | P0003 | Mie Ayam Ceker    | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 | C0001       |
| C0002 | Minuman   | P0003 | Mie Ayam Ceker    | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 | C0001       |
| C0003 | Lain-Lain | P0003 | Mie Ayam Ceker    | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 | C0001       |
| C0004 | Oleh-Oleh | P0003 | Mie Ayam Ceker    | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 | C0001       |
| C0005 | Gadget    | P0003 | Mie Ayam Ceker    | Mie Ayam + Ceker | 20000 |      100 | 2021-02-23 14:31:03 | C0001       |
| C0001 | Makanan   | P0006 | Bakso Rusuk       | NULL             | 25000 |      200 | 2021-02-23 16:12:53 | C0001       |
| C0002 | Minuman   | P0006 | Bakso Rusuk       | NULL             | 25000 |      200 | 2021-02-23 16:12:53 | C0001       |
| C0003 | Lain-Lain | P0006 | Bakso Rusuk       | NULL             | 25000 |      200 | 2021-02-23 16:12:53 | C0001       |
| C0004 | Oleh-Oleh | P0006 | Bakso Rusuk       | NULL             | 25000 |      200 | 2021-02-23 16:12:53 | C0001       |
| C0005 | Gadget    | P0006 | Bakso Rusuk       | NULL             | 25000 |      200 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0007 | Es Jeruk          | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0007 | Es Jeruk          | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0002       |
| C0003 | Lain-Lain | P0007 | Es Jeruk          | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0002       |
| C0004 | Oleh-Oleh | P0007 | Es Jeruk          | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0002       |
| C0005 | Gadget    | P0007 | Es Jeruk          | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0002       |
| C0001 | Makanan   | P0008 | Es Campur         | NULL             | 15000 |      500 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0008 | Es Campur         | NULL             | 15000 |      500 | 2021-02-23 16:12:53 | C0002       |
| C0003 | Lain-Lain | P0008 | Es Campur         | NULL             | 15000 |      500 | 2021-02-23 16:12:53 | C0002       |
| C0004 | Oleh-Oleh | P0008 | Es Campur         | NULL             | 15000 |      500 | 2021-02-23 16:12:53 | C0002       |
| C0005 | Gadget    | P0008 | Es Campur         | NULL             | 15000 |      500 | 2021-02-23 16:12:53 | C0002       |
| C0001 | Makanan   | P0009 | Es Teh Manis      | NULL             |  5000 |      400 | 2021-02-23 16:12:53 | C0002       |
| C0002 | Minuman   | P0009 | Es Teh Manis      | NULL             |  5000 |      400 | 2021-02-23 16:12:53 | C0002       |
| C0003 | Lain-Lain | P0009 | Es Teh Manis      | NULL             |  5000 |      400 | 2021-02-23 16:12:53 | C0002       |
| C0004 | Oleh-Oleh | P0009 | Es Teh Manis      | NULL             |  5000 |      400 | 2021-02-23 16:12:53 | C0002       |
| C0005 | Gadget    | P0009 | Es Teh Manis      | NULL             |  5000 |      400 | 2021-02-23 16:12:53 | C0002       |
| C0001 | Makanan   | P0010 | Kerupuk           | NULL             |  2500 |     1000 | 2021-02-23 16:12:53 | C0003       |
| C0002 | Minuman   | P0010 | Kerupuk           | NULL             |  2500 |     1000 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0010 | Kerupuk           | NULL             |  2500 |     1000 | 2021-02-23 16:12:53 | C0003       |
| C0004 | Oleh-Oleh | P0010 | Kerupuk           | NULL             |  2500 |     1000 | 2021-02-23 16:12:53 | C0003       |
| C0005 | Gadget    | P0010 | Kerupuk           | NULL             |  2500 |     1000 | 2021-02-23 16:12:53 | C0003       |
| C0001 | Makanan   | P0011 | Keripik Udang     | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0003       |
| C0002 | Minuman   | P0011 | Keripik Udang     | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0011 | Keripik Udang     | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0003       |
| C0004 | Oleh-Oleh | P0011 | Keripik Udang     | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0003       |
| C0005 | Gadget    | P0011 | Keripik Udang     | NULL             | 10000 |      300 | 2021-02-23 16:12:53 | C0003       |
| C0001 | Makanan   | P0012 | Es Krim           | NULL             |  5000 |      200 | 2021-02-23 16:12:53 | C0003       |
| C0002 | Minuman   | P0012 | Es Krim           | NULL             |  5000 |      200 | 2021-02-23 16:12:53 | C0003       |
| C0003 | Lain-Lain | P0012 | Es Krim           | NULL             |  5000 |      200 | 2021-02-23 16:12:53 | C0003       |
| C0004 | Oleh-Oleh | P0012 | Es Krim           | NULL             |  5000 |      200 | 2021-02-23 16:12:53 | C0003       |
| C0005 | Gadget    | P0012 | Es Krim           | NULL             |  5000 |      200 | 2021-02-23 16:12:53 | C0003       |
| C0001 | Makanan   | P0013 | Mie Ayam Jamur    | NULL             | 20000 |       50 | 2021-02-23 16:12:53 | C0001       |
| C0002 | Minuman   | P0013 | Mie Ayam Jamur    | NULL             | 20000 |       50 | 2021-02-23 16:12:53 | C0001       |
| C0003 | Lain-Lain | P0013 | Mie Ayam Jamur    | NULL             | 20000 |       50 | 2021-02-23 16:12:53 | C0001       |
| C0004 | Oleh-Oleh | P0013 | Mie Ayam Jamur    | NULL             | 20000 |       50 | 2021-02-23 16:12:53 | C0001       |
| C0005 | Gadget    | P0013 | Mie Ayam Jamur    | NULL             | 20000 |       50 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0014 | Bakso Telor       | NULL             | 20000 |      150 | 2021-02-23 16:12:53 | C0001       |
| C0002 | Minuman   | P0014 | Bakso Telor       | NULL             | 20000 |      150 | 2021-02-23 16:12:53 | C0001       |
| C0003 | Lain-Lain | P0014 | Bakso Telor       | NULL             | 20000 |      150 | 2021-02-23 16:12:53 | C0001       |
| C0004 | Oleh-Oleh | P0014 | Bakso Telor       | NULL             | 20000 |      150 | 2021-02-23 16:12:53 | C0001       |
| C0005 | Gadget    | P0014 | Bakso Telor       | NULL             | 20000 |      150 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0015 | Bakso Jando       | NULL             | 25000 |      300 | 2021-02-23 16:12:53 | C0001       |
| C0002 | Minuman   | P0015 | Bakso Jando       | NULL             | 25000 |      300 | 2021-02-23 16:12:53 | C0001       |
| C0003 | Lain-Lain | P0015 | Bakso Jando       | NULL             | 25000 |      300 | 2021-02-23 16:12:53 | C0001       |
| C0004 | Oleh-Oleh | P0015 | Bakso Jando       | NULL             | 25000 |      300 | 2021-02-23 16:12:53 | C0001       |
| C0005 | Gadget    | P0015 | Bakso Jando       | NULL             | 25000 |      300 | 2021-02-23 16:12:53 | C0001       |
| C0001 | Makanan   | P0016 | Permen            | NULL             |  1000 |     1000 | 2021-02-24 10:08:39 | C0003       |
| C0002 | Minuman   | P0016 | Permen            | NULL             |  1000 |     1000 | 2021-02-24 10:08:39 | C0003       |
| C0003 | Lain-Lain | P0016 | Permen            | NULL             |  1000 |     1000 | 2021-02-24 10:08:39 | C0003       |
| C0004 | Oleh-Oleh | P0016 | Permen            | NULL             |  1000 |     1000 | 2021-02-24 10:08:39 | C0003       |
| C0005 | Gadget    | P0016 | Permen            | NULL             |  1000 |     1000 | 2021-02-24 10:08:39 | C0003       |
| C0001 | Makanan   | X0001 | X Satu            | NULL             | 25000 |      200 | 2021-02-24 13:53:23 | NULL        |
| C0002 | Minuman   | X0001 | X Satu            | NULL             | 25000 |      200 | 2021-02-24 13:53:23 | NULL        |
| C0003 | Lain-Lain | X0001 | X Satu            | NULL             | 25000 |      200 | 2021-02-24 13:53:23 | NULL        |
| C0004 | Oleh-Oleh | X0001 | X Satu            | NULL             | 25000 |      200 | 2021-02-24 13:53:23 | NULL        |
| C0005 | Gadget    | X0001 | X Satu            | NULL             | 25000 |      200 | 2021-02-24 13:53:23 | NULL        |
| C0001 | Makanan   | X0002 | X Dua             | NULL             | 10000 |      300 | 2021-02-24 13:53:23 | NULL        |
| C0002 | Minuman   | X0002 | X Dua             | NULL             | 10000 |      300 | 2021-02-24 13:53:23 | NULL        |
| C0003 | Lain-Lain | X0002 | X Dua             | NULL             | 10000 |      300 | 2021-02-24 13:53:23 | NULL        |
| C0004 | Oleh-Oleh | X0002 | X Dua             | NULL             | 10000 |      300 | 2021-02-24 13:53:23 | NULL        |
| C0005 | Gadget    | X0002 | X Dua             | NULL             | 10000 |      300 | 2021-02-24 13:53:23 | NULL        |
| C0001 | Makanan   | X0003 | X Tiga            | NULL             | 15000 |      500 | 2021-02-24 13:53:23 | NULL        |
| C0002 | Minuman   | X0003 | X Tiga            | NULL             | 15000 |      500 | 2021-02-24 13:53:23 | NULL        |
| C0003 | Lain-Lain | X0003 | X Tiga            | NULL             | 15000 |      500 | 2021-02-24 13:53:23 | NULL        |
| C0004 | Oleh-Oleh | X0003 | X Tiga            | NULL             | 15000 |      500 | 2021-02-24 13:53:23 | NULL        |
| C0005 | Gadget    | X0003 | X Tiga            | NULL             | 15000 |      500 | 2021-02-24 13:53:23 | NULL        |
+-------+-----------+-------+-------------------+------------------+-------+----------+---------------------+-------------+
80 rows in set (0.00 sec)
```
