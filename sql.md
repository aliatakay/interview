
# SQL



**RDBMS** (Relational Database Management System)

- ilişkisel veri tabanlarına verilen isimdir.
- Sql Server, Oracle, MySql, PostgreSql



**NoSql**

- **not only sql** anlamına gelir.
- MongoDb, Firebase



## 4 temel komut

```sql
SELECT * FROM Customers

UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;

DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';

INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```



---

# SQL KOMUTLARI



```sql
SELECT * FROM Customers
```

**SELECT** 	      : Tablodan satırları seçer.
*****				       : Tüm satırları seç demektir.
**FROM** 			 : Hangi tablodan seçmek istediğimizi belirtmek için kullanırız.
**CUSTOMERS**  : Seçtiğimiz tablonun adıdır.



```sql
SELECT ContactName, CompanyName, City FROM Customers
```

- Sadece belirttiğimiz sütunların gelmesini istediğimiz için sütun isimlerini belirttik.
- Bu komut çalışınca, memory'de fake bir tablo oluşur. Bu tablo bize çıktı olarak gösterilir.



```sql
SELECT * FROM Customers WHERE City = ‘London’
```

**WHERE**			: Sorguya bir KOŞUL eklememizi sağlar.

* London şehrinde yaşayan tüm müşterileri getirmesini istemiş olduk.



```sql
Select * from Products where CategoryId = 1 or CategoryId = 3
```

**OR** 			: 'ya da' ifadesini sorguya eklemiş oluruz.

- CategoryId'si 1 VEYA 3 olanları seçer.



```sql
Select * from Products where CategoryId = 1 and UnitPrice >= 10
```

**AND** 			: 've' ifadesini sorguya eklemiş oluruz.

- CategoryId'si 1 VE 10'dan büyük olanları seçer.



```sql
Select * from Products where CategoryId = 1
Select * from Products where UnitPrice > 10
Select * from Products where UnitPrice < 20
Select * from Products where UnitPrice >= 10
Select * from Products where UnitPrice <= 10
Select * from Products where UnitPrice <> 10 -- 10'dan farklı olanları getir.
```

---
