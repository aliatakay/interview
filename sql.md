
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
```
```sql
UPDATE Customers SET Name = 'Ali' WHERE Id = 1;
```
```sql
DELETE FROM Customers WHERE Id = 1;
```
```sql
INSERT INTO Customers (Id, Name, City) VALUES (1, 'Ali', 'Istanbul');
```



---

# SQL KOMUTLARI



```sql
SELECT * FROM Customers
```

<table>
  <tr>
    <th>Komut</th>
    <th>Anlam</th>
  </tr>
  <tr>
    <td>SELECT</td>
    <td>Tablodan satırları seçer.</td>
  </tr>
  <tr>
    <td>*</td>
    <td>Tüm kolonları seçer.</td>
  </tr>
  <tr>
    <td>FROM</td>
    <td>Hangi tablodan seçileceğini ifade eder.</td>
  </tr>
  <tr>
    <td>Customers</td>
    <td>Seçtiğimiz tablonun adıdır.</td>
  </tr>
</table>



```sql
SELECT Id, Name, City FROM Customers
```

- Sadece belirttiğimiz sütunların gelmesini istediğimiz için sütun isimlerini belirttik.
- Bu komut çalışınca, memory'de fake bir tablo oluşur. Bu tablo bize çıktı olarak gösterilir.



```sql
SELECT * FROM Customers WHERE City = 'London'
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
SELECT * FROM Products WHERE CategoryId = 1
SELECT * FROM Products WHERE UnitPrice > 10
SELECT * FROM Products WHERE UnitPrice < 20
SELECT * FROM Products WHERE UnitPrice >= 10
SELECT * FROM Products WHERE UnitPrice <= 10
SELECT * FROM Products WHERE UnitPrice <> 10 -- 10'dan farklı olanları getir.
```

---
