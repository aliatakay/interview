<h1>C# Soruları</h1>
<h2>Class Nedir?</h2>
<p>Class, object (nesne) üretmek için yazılan bir şablondur.</p>

```c#
public class Person
{
     public string Name { get; set; }
     public string City { get; set; }
}
```

<h2>Object Nedir?</h2>
<p>Object, class kullanılarak oluşturulur.</p>

```c#
var person = new Person();

person.Name = "Ali";
person.City = "Ankara";
```

<h2>Local Variable</h2>
<p>Bir metot veya blok içinde tanımlanan değişkenlerdir.</p>
<p>Bu değişkenler sadece bulunduğu blok içinde var olur.</p>
<p>Bu local değişkenlere, bulunduğu blok haricinde hiçbir yerden erişilemez.</p> 
<p>Bu yüzden değişkenin başında hiçbir access modifier tanımlanmaz.</p>

```c#
public bool IsTeenager(int age)
{
     var teenage = 18; //Bu değişkene yalnızca bulunduğu metot içinde erişilir.
     return age > teenage;
}
```

<h2>Field</h2>
<p>Bir class içinde, herhangi bir tipte, doğrudan tanımlanan değişkenlere denir.</p>
<p>Access modifier kullanılabilir. Fakat genelde hep private olarak kullanılır.</p>
<p>Çünkü bu değişkene dışarıdan doğrudan erişilmesini istemeyiz. Erişimi sağlamak için property'ler kullanırız.</p>

```c#
public class Person
{
     private string identity;
     private string nationality;
}
```

<h2>Property</h2>
<p>Private bir field'ın; read, write, compute işlemlerini yapmayı sağlayan yapıdır.</p>
<p>Property'nin kendisi değer tutmaz. Get ve set metotları ile ramdeki bir veriyi getirir.</p>
<p>Property sayesinde, private olan field'ı nasıl set edeceğimizi ve nasıl get edeceğimizi belirlemiş oluruz. Örneğin edge değeri 0'dan küçük olamaz.</p>

```c#
public class Square
{
     private int edge;

     public int Edge
     {
          get { return edge; }
      	  set
          {
               if (value > 0) edge = value;
               else throw new ArgumentException();
          }
     }
}
```

<h2>Auto Property</h2>
<p>Property ve Field ikilisini kısa şekilde yazmanın bir yöntemidir.</p>

```c#
public class Square
{
     public int Edge { get; set; }
}
```

---

### Boxing ve Unboxing nedir?

Boxing ve Unboxing, tip dönüşümü için kullanılır.

Boxing:       Value Type -> Reference Type

```c#
int number = 100;
Object obj = number;
```

Unboxing:   Reference Type -> Value Type

```c#
Object obj = 100;
int number = (int)obj;
```



---

### Struct ve Class farkları nelerdir?

<table>
	<tr>
		<th>Struct</th>
		<th>Class</th>
	</tr>
	<tr>
		<td>Struct bir değer tiptir.</td>
		<td>Class bir referans tiptir.</td>
	</tr>
	<tr>
		<td>Struct az sayıda data için kullanılır.</td>
		<td>Class çok sayıda data için kullanılır.</td>
	</tr>
	<tr>
		<td>Struct inherit edilemez.</td>
		<td>Class, diğer classlar tarafından inherit edilebilir.</td>
	</tr>
	<tr>
		<td>Struct abstract olamaz.</td>
		<td>Class abstract olabilir.</td>
	</tr>
	<tr>
		<td>Struct, Nesne türetirken new keyword kullanılmaz.</td>
		<td>Class, Nesne türetirken new keyword kullanılır.</td>
	</tr>
	<tr>
		<td>Struct, default constructor oluşturulamaz.</td>
		<td>Class, default constructor oluşturulabilir.</td>
	</tr>
</table>

---

### Interface Neden Kullanılır?

---

### Interface ve Abstract Class farkı nedir?

Abstract Class, ortak özellikleri olan nesneleri bir çatı altında toplamak için kullanılır.

Abstract Class, base class olarak kullanılır.

Bu ifadeyi anlaşılır kılmak için 'is a' ifadesi kullanılır.

Mesela **Mercedes is a Car** diyebiliriz. Car bir abstract class'tır.

Bir class sadece 1 tane abstract class'ı inherit alabilir.

Abstract class'lar new ile OLUŞTURAMAZLAR.

Zaten mantık olarak bunun olması anlamsızdır, çünkü içinde gövdesi olmayan metot imzaları barındırabilir.



- Interface içerisinde yalnıza method tanımları bulunur. İçerisine kod parçacığı yazılmaz.
- Interface başka bir interfaceden inherit olabilir.
- Interfaceler genelde **“can-do”** ilişkisine göre çalışır.
- “**new**” ile oluşturulamaz.
- Bir sınıf birden fazla interface implement edebilir.
- Interface içerisine yalnızca boş metot tanımlanabilir.
- Interface içerisinde özellik ve metodlarda erişim belirleyiciler kullanılmaz. Her şey **public** kabul edilir.



1-) Bir sınıf birden fazla interface’i inherit olarak alabilir ama bir sınıfa bir tane abstract class inherit alınabilir.

2-) Interface içerisinde boş metodlar tanımlanabilir ama abstract class’larda hem boş metodlar tanımlanabilir hemde içi dolu metodlar tanımlabilir.

3-) Abstract classları kullanmak hız açısından avantaj sağlar.

4-) Interface de yeni bir metod yazdığımız zaman bu interfaceden implement ettiğimiz tüm classlarda bu metodun içini tek tek doldurmak gerekiyor ancak abstract classlarda durum farklıdır burada bir metod tanımlayıp içini doldurduğumuzda abstract sınıfımızdan türetilmiş bütün sınıflar bu özelliği kazanmış olur.

5-) Interfaceler çoklu kalıtımı sağlamaya yardımcı abstract classlar ise çoklu kalıtımı desteklemez.

6-) Interface içerisindeki tüm nesnelerin “public” olması gerekirken Abstract classlarda tüm öğelerin “public” olması zorunlu değildir.

7-) Interface yapıcı metodlar(constructor) içermez. Abstract class yapıcı metodlar içerebilir.

8-)Interface metodlar **static** olamaz. Abstract class soyut olmayan metodlar **static** olarak tanımlanabilir.

Abstract Class, alt sınıfların kullanabileceği property'ler, field'lar ve metotlar içerir.

Interface ise metotların body'sini barındırmaz. Sadece imzalarını tutabilir.



---

### Enum nedir?

Enum, değer tiptir.

Değer tip olduğu için, Stack kısmında tutulur.

Bir rakam listesine karşılık gelen, sabit değerler listesidir.

```c#
enum Day {Sat, Sun, Mon, Tue, Wed, Thu, Fri}; 
```

---

### Continue ve Break statement farkı nedir?

Break komutu çalıştığı anda, o anki döngü tamamen sonlandırılır.

Continue komutu çalıştığı anda, o anki 1 iterasyon atlanır. Döngü diğer iterasyondan devam eder.

---

### Const ve Readonly farkı nedir?

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

runtime ve compile time farkı var bu konuda. buna dikkat et.

---

### ref ve out keyword farkı nedir?

---

### Accessors açıklayınız.

---

### String ve StringBuilder farkı nedir?

String bir değişkene yeni bir değer atanacağı zaman, memory'de yeni bir String instance oluşturulur.

Bu da bellekte performans kaybına yol açar.

System namespace'inden gelir.



StringBuilder kullanırken bir tane instance üretiriz.

Belli metotlar kullanarak string üzerinde, append veya replace işlemleri yapabiliriz.

System.Text.StringBuilder namespace'inden gelir.

---

### Sealed Class nedir?

Sealed anahtar kelimesi, bir class'ın başına yazılarak kullanılır.

```c#
sealed class Person {}
```

Sealed olarak tanımlanan bir class, inherit edilemez hale gelir.

---

### Partial Class nedir?



Aynı isimdeki bir class'ı partial anahtar kelimesini kullanarak birden çok parçaya böleriz.

Böldüğümüz bu farklı sınıflar, aynı isme sahip olur.

Ve compile time'da bu sınıflar birleştirilerek, tek bir sınıf olarak hareket eder.

Bir sınıfın içi çok karıştığında, sınıfı mantıklı parçalara bölmek isteyebiliriz.

Daha okunaklı ve anlaşılır olur, karmaşık kodlar düzene girer. Arkaplanda tek bir sınıf olmaya devam eder.

```c#
public partial class Person
{
     public int Id { get; set;}
     public string FirstName { get; set;}
     public string LastName { get; set;}
}

public partial class Person
{
     public string GetFullName()
     {
          return FirstName + " " + LastName;
     }
  
     public string SayHello()
     {
          return "Hello, " + FirstName + " " + LastName;
     }
} 
```



---

### IEnumerable<> nedir?

IEnumerable, bütün non-generic koleksiyonların ebeveyn interface'idir.

ArrayList, HashTable gibi generic olmayan koleksiyon yapıların ebeveyn interface'idir.

System.Collections namespace'inden gelir.



IEnumerable**<T>** ise, tüm generic olan koleksiyonların ebeveyn interface'idir.

List<> gibi generic olan koleksiyon yapıların ebeveyn interface'idir.

System.Collections.Generic namespace'inden gelir.

---

### Early Binding ve Late Binding nedir?

Early Binding => Compile Time Binding

Late Binding => Runtime Binding



**Static Type Binding** : Değişkenin tipi en başından beri bellidir.

```c#
Person p1;
```



**Dynamic Type Binding** : Tipi belli olmayan değişkendir. Atama yapılana kadar belirsizdir.

```c#
var a;
```



**Early Binding**

Nesne referanslarının, hangi nesneye bağlanacağına Compile Time anında belirlenir.

**Late Binding**

Geç bağlama olarak adlandırılır.

Late binding, polymorphism'in bir sonucu olarak ortaya çıkmaktadır.

Polymorphism'in olmadığı yerde Late Binding yoktur.

NOT: **var** tipi bu kuralın dışında kalıyor olabilir. Aşağıda yazan açıklama eski bir makaleden alındı.



Kişi sınıfından Personel türetelim, Personel sınıfından da Mühendis türetelim.

```c#
public class Person
{
     public virtual void WhoAmI()
     {
          Console.Write("I am a Person");
     }
}

public class Employee : Person
{
     public override void WhoAmI()
     {
          Console.Write("I am an Employee");
     }
}

public class Engineer : Employee
{
     public override void WhoAmI()
     {
          Console.Write("I am an Engineer");
     }
}

public class Main()
{
     public static void Main(string[] args)
     {
          Person human1   = new Person();
          Employee human2 = new Employee();
          Engineer human3 = new Engineer();
  	
      	  TellMeWhoIAm(human1); // I am a Person
          TellMeWhoIAm(human2); // I am an Employee
          TellMeWhoIAm(human3); // I am an Engineer
     }
  
     public static void TellMeWhoIAm(Person human) // önemli
     {
          human.WhoAmI();
     }
}

```

TellMeWhoIAm metodu sadece **PERSON sınıfından olan tipi parametre olarak kabul eder**.

Diğer sınıfları da parametre olarak kabul ederek, hata vermemesinin sebebi **tip dönüşümü** yapmasıdır.

Burada PERSON tipindeki parametre, yeri geldi PERSON tipinden bir nesneyi kabul etti, yeri geldi EMPLOYEE tipinden bir nesneyi kabul etti, yeri geldi ENGINEER tipinden bir nesneyi kabul etti.

**Parametrenin tipi ne ise, o tipe ait WhoAmI metodunu çalıştırdı**.

İŞTE BU POLYMORPHISM'dir.



Şimdi Late Binding kavramını anlayalım.

Polymorphism olduğunda, tüm child sınıflar, parent sınıfın tipi ile referans oluşturabilir.

Örneğin bir dizi oluşturalım.

```c#
List<Person> insanlar = new List<Person>();
```

Sonra bu listeye **random olarak** (person ya da employee ya da engineer ya da hepsinin kombinasyonunu) rastgele olarak atayalım.

Bu durumda, Compile time esnasında bu belirlenemez. Çünkü hangi tiplerin geleceği belli değildir. 

Random sayıların değerleri yalnızca Runtime esnasında belirlenir.

**Yani aslında, bir referansın hangi nesneye bağlanacağı, runtime anında belirlenir. Buna Late Binding denir**.

---

### IEnumerable\<T> ve IQueryable\<T> farkı nedir?

---

### Birden fazla Catch bloğu çalıştırılabilir mi?

C# programlama dilinde 1 try bloğunun ardından birden fazla catch bloğu **kullanılabilir**.

Bunun amacı, **birbirinden farklı exception'ları yönetebilmektir**.

Aynı exception tipinde catch blokları yazılırsa, compile-time error alınır.

Aslında bu da demektir ki, 1 tane catch bloğu çalışır. İlk catch bloğundaki exception ile eşleşirse, kalan catch blokları çalışmaz.



```c#
static void Main()
{
     int[] number = { 8, 17, 24, 5, 25 };
     int[] divisor = { 2, 0, 0, 5 };
  
     for (int j = 0; j < number.Length; j++)
     {
          try 
          {
               Console.WriteLine("Number: " + number[j]);
               Console.WriteLine("Divisor: " + divisor[j]);
               Console.WriteLine("Quotient: " + number[j] / divisor[j]);
          }
          catch (DivideByZeroException)
          {  
               Console.WriteLine("Not possible to Divide by zero");
          }
          catch (IndexOutOfRangeException)
          {
               Console.WriteLine("Index is Out of Range");
          }
     }          
}

// output
Number: 8
Divisor: 2
Quotient: 4
Number: 17
Divisor: 0
Not possible to Divide by zero
Number: 24
Divisor: 0
Not possible to Divide by zero
Number: 5
Divisor: 5
Quotient: 1
Number: 25
Index is Out of Range
```



---

### Indexers nedir?

---

### is ve as operatörleri farkı nedir?

---

### Nullable<> tipler nasıl kullanılır?

---

### Object Pool nedir?

---

### Generic nedir?

---

### Access Modifiers nelerdir?

- private
- public
- protected
- internal
- protected internal



```c#
class Customer
{
     // default olarak bulunan access modifier INTERNAL'dır.
}

//NOT: Bir yapının başında access modifier yazılmazsa, o yapı "alabileceği en düşük seviyedeki" belirteci alır default olarak.

// yani bir class "internal" alırken, bir field "private" alır.
```



Erişim belirteçleri, başka nesnelerin ulaşımını kısıtlamaya yöneliktir.

**internal** : Solution'daki diğer projeler, bizim projemizi referans alsalar bile, internal olan class'ı kullanamazlar. Aynı namespace içinde olan nesneler, bu class'a erişebilir.

**public** : Solution'daki diğer projeler, referans aldığı takdirde, public olan class'a erişebilirler.

**NOT**: bir class, sadece public ve internal olabilir. Çünkü bir class, kullanılmak için oluşturulur. Private veya protected olmasının hiçbir mantısı yoktur, bu nedenle private ve protected olamazlar. Ancak ve ancak, nested (iç içe) class'lar yazarsak, o durumda içte yer alan class private olabilir.

**private** : private tanımlanan bir yapı, sadece ve sadece **kendisini kapsayan bir üst süslü parantezler arasında** erişilebilirdir. Yani eğer bir metot private ise, o metoda yalnızca bulunduğu class erişebilir. Çünkü bir metodu kapsayan bir üst süslü parantezlere sahip yapı onu tutan classtır. Doğal olarak class'ın içindeki diğer metotlar, bu private metoda erişebilirler.

**NOT**: değişkenlerin default belirteci **private** olur.

```c#
int number = 10;
// aslında bu aşağıdaki gibidir.
private int number = 10;
// ve bu değişkene yalnızca onu kapsayan blok erişebilir.
```



**protected** : private'tan sadece tek bir farkı vardır. **inherit** verdiği classlar da erişebilir.

**protected internal** : 2 belirtecin birleşimidir. Sadece kendi projesi içinden erişilebilir. veya başka bir projeden erişilebilmesi için tek yöntem, inheritance uygulamaktır.



---

### Virtual Method nedir?

---

### Array ve ArrayList farkı nedir?

---

 ### Değer tip ve Referans Tip farkı nedir?

---

### Serialization nedir?

---

### using statement nasıl kullanılır?

---

### LINQ nedir?

---

### Lazy Loading ve Eager Loading nedir?



Entity Framework'ün, yazılan LINQ sorgularına bağlı olarak veriyi, database'den yüklemek için kullandığı 2 farklı Loading yöntemi vardır.

---
