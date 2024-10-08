# Object-Oriented Programlama Soruları

Object-Oriented Programlama'nın 4 temel özelliği vardır.

<details>
<summary><h2>Encapsulation</h2></summary>

Birbiriyle iletişim kuran, farklı nesnelerin olduğu bir program düşünelim.

Herbir nesne, kendi state'lerini bir class içinde private tuttuğunda encapsulation gerçekleşir.

Diğer nesneler, bu state'lere doğrudan erişemezler.

Bunun yerine, public olarak tanımlanmış metotlara erişebilirler.

Nesne, kendi state'lerini yalnızca metotlar üzerinden yönetir. İzin verilmedikçe, başka classlar erişemez.

Nesne ile iletişim kurmak istendiğinde, sadece sağlanan metotlar ile bunu yaparsınız.

Ancak (default olarak) state'in kendisini değiştiremezsiniz.



Örneğin insanların ve bir tane kedinin olduğu bir oyun projesi düşünelim.

İnsanlar ve kedi birbirileriyle iletişim kuruyorlar.

Burada encapsulation uygulamamız gerekiyorsa, kediye ait tüm logic, Cat isimli bir class içine yazılır.

```c#
public class Cat
{
     private int mood;
     private int hungry;
     private int energy;
	
     private void Meow()
     {
          Console.Write("Meow");
     }
  
     public void Feed()
     {
          hungry--;
          mood++;
          Meow();
     }
}
```

Dışarıdan hiçbir class, Cat class'ındaki private field'lara erişemez.

Diğer classlar sadece Cat class'ında public olarak tanımlanmış Feed metoduna erişebilir.

Bu şekilde, Feed metodunu çağırarak, Cat class'ındaki private field ve metotlara erişim sağlanmış olur.

Ancak bu erişim, sadece Cat sınıfındaki public metotların izin verdiği kadardır.



Bunun dışında, private olan field'lar için **property** kullanmak da encapsulation yapmak demektir.

Property'ler sayesinde private olan field'ın get ve set metotlarını yönetiriz.

```c#
public class Person
{
     private string name;
     public string Name
     {
          get
          {
               return name;
          }
      	  set
          {
               name = value;
          }
     }
}
```

Özetle Encapsulation; bir class'ta bulunan field veya metotları diğer class'lara gizlemektir. Bu, yanlış kullanımları ve atamaları engellemek içindir. Diğer class'lar, private olan bu field'lara erişmek için public olan metotları kullanmak zorundadır. Doğrudan field'lar için oluşturulan property'ler üzerinden erişebilirler. Ya da class'ta bulunan başka public bir metot aracılığıyla erişebilirler.

```c#
public class AccountCreator
{
     public int Age;
     private string _country;
  
     public void CreateAccount(Account account)
     {
          this.Age = account.Age;
          this._country = account.Country;
          var accountEligible = CheckAge();
     } 
  
     private bool CheckAge()
     {
          if(_country == "USA")
          {
               this.Age++;
               return this.Age > 18;
          }
     }
}

static void Main(string[] args)
{
     var accountCreator = new AccountCreator();
     var account = getAccountFromAzure();
     accountCreator.CreateAccount(account);
     accountCreator.Age = 16; //Erişilebiliyor olması hatadır.
}
```



Burada Age field'ına müdahale edebildik. Bu tamamen anlamsızdır ve çok risklidir. Age field'ımız private olmalıydı. Çünkü AccountCreator sınıfında yer alan Age field'ı dışarıdan sadece sınıf içindeki public metot olan CreateAccount metodu kullanılarak manipüle edilebilir. Başka türlü edilememesi gerekmektedir. O yüzden private bir field olmalıydı.

---

</details>

<details>
<summary><h2>Abstraction</h2></summary>

Abstraction, Encapsulation prensibinin doğal bir uzantısı olarak görülebilir.

OOP tasarımda, programlar büyük ölçekli olur.

Nesneler birbiriyle fazlaca haberleşirler.

Proje büyüdükçe ve değiştikçe, yönetimi de zorlaşır.

Abstraction da bu problemi hafifletmeye çalışan bir yaklaşımdır.

Örneğin bir cep telefonunu düşünelim. Çok karmaşık bir yapısı vardır ancak kullanımı çok basittir.

Sadece birkaç tuşa basarak telefonla etkileşime geçeriz.

Arkada ne olduğunu bilmemize gerek yoktur.



Abstraction, bireysel olarak farklı olan yapıları, ortak olan bazı taraflarını almak suretiyle onları kategorize etmektir.

Mesela **Türkler** dediğimizde, birbirinden çok farklı olan milyonlarca insanı, ortak bir çatıda toplamış oluruz. Bu isimlendirme ile abstraction uygulamış oluruz.

Mesela araba kullanırken sadece pedalları, vitesi ve direksiyonu kullanırız. Halbuki arabada, bu 3 parçanın var olmasını sağlayan binlerce başka parça mevcuttur. Fakat onların hiçbirini bilmeyiz.

Şimdi yazılımdaki abstraction'ın ne olduğuna bakalım.

```c#
string text = "hello";
```

Aslında yukarıdaki tek satır kodda 'interface', 'abstract class' ya da 'inheritance' yok. Fakat aslında abstraction vardır.

**string** bir soyutlamadır. Metinsel ifadeleri tutan yapıdır. Bellekte ne kadar yer ayrılacağı, nasıl tutulacağı, operatörlere nasıl tepki vereceği vs. her şeyi bellidir. Bütün bunları 'string' kelimesi ile soyutlamıştır.

**=** işareti de bir soyutlamadır. Verinin atanması için gereken tüm adımları soyutlar.

**"hello"** bile bir soyutlamadır. Arka planda oluşma, saklanma ve 010101 verilerini soyutlar.

Bunları yaparken, hitap ettiğiniz asıl kitle, bu sınıfları kullanacak olan diğer insanlar. Arabalardaki gaz ve fren gibi kısımlar ile soyutlanan binlerce parça, arabayı nasıl daha kolay kullanılabilir hale getirdiyse, yazılımda da abstraction benzer etkiyi hem sizin için hem de sınıflarınızı kullanacak diğer mühendisler için yapar. Eğer mühendisler, arabanın nasıl çalıştığını bildiklerinden dolayı, onları üretirken herkesi kendileri gibi düşünüyor olsalardı, o zaman araba süren insan sayısı şimdikinin sizce kaçta kaçı kadar olurdu? Benzer şekilde, eğer yazılımda, abstraction çok gelişmiş bir konsept olmasaydı, şu an çoğumuz 010101 diye kod yazıyor olurduk.

```c#
class Animal
{
     public int Length { get; set; }
     public string Gender { get; set; }
}
class Dog : Animal
{
     public int TailLength { get; set; }
}
class Dolphin : Animal
{
     public string SpeedInWater { get; set; }
}
```



**Özetlemek gerekirse**: Abstraction, farklı kod parçalarının kompleks kısımlarını; sahip oldukları ortak davranışlar, amaçlar, karakteristik özellikler arkasında saklamak sayesinde daha anlaşılır ve kolay kullanılabilir kod yazmaktır.

---

</details>

<details>
<summary><h2>Inheritance</h2></summary>

Nesneler sıklıkla birbirine benzer.

Ortak bir logic paylaşırlar.

Ancak yüzde yüz aynı değildirler.

O halde ortak gözüken mantığı aynı tutup, farklılaşan kısımları ayrı sınıflara taşımalıyız.

Bunu da inheritance ile yaparız.

Bir parent sınıftan, bir child sınıf türetiriz.

Yani bir hiyerarşi kurarız.

Çocuk class, ebeveyne ait tüm özellikleri kullanabilir.

Aynı zamanda kendine has metot ve özellikleri de implemente edebilir.



Örneğin parent bir PERSON class'ı olur.

Teacher ve Student class'ları, Person class'ından türetilir.

PERSON class'ındaki 'Name' ve 'Email' fieldlarına, tüm çocuk sınıflar da sahip olmuş olur.

Ayrıca TEACHER classından da PrivateTeacher ve PublicTeacher gibi farklı çocuk sınıflar türetebiliriz.



Bu sayede her class, ortak olan logic bölümü parent sınıftan kullanabilir.

Ve her sınıf, kendine has ek logicleri de kendine ekleyebilir.

---

</details>

<details>
<summary><h2>Polymorphism</h2></summary>

En karmaşık prensiptir.

'Çok Biçimlilik' anlamına gelmektedir.

Inheritance birçok imkan sağlar ama bazı problemleri de yanında getirir.

Diyelim ki bir parent class var. Ve ondan türeyen child classlar var.

Bazen tüm bu sınıfları karışık halde tutan bir listeye ihtiyaç duyarız.

Bazen parent class için uyguladığımız bir metodu, çocuk sınıflar için de uygulamak isteriz.

Bu sorunlar Polymorphism kullanarak çözülür.

Parent class ya bir interface ya da bir abstract class olur.

Burada yer alan metotlar, çocuk sınıflar için birer şema görevindedir.

Örneğin parent yapıya, AlanHesapla metodu koyarız.

Üçgen, Kare, Daire isimli çocuk sınıflar, bu parent yapıyı implemete ederek, AlanHesapla metoduna sahip olurlar. Ve bu metodu kendi mantıklarına göre kullanırlar.

Bu parent yapı sayesinde, tüm çocuklar tek ve ortak bir nesne gibi kullanılabilir.

Aynı zamanda hangi sınıftan bir nesnenin Hesapla metodu çağrılıyorsa, o sınıfa ait Hesapla metodu çalışır.

Ya da her 3 sınıfa yönelik başka bir metot yazılacaksa, farklı parametre yollanan 3 farklı metot yazılmasına gerek yoktur. Figure isimli parent sınıfı yolladığınız bir metot yazarsınız. Bu metot, 3 çocuk sınıfı da parametre olarak alabilecektir.



**Inheritance**; bir child sınıfın, parent sınıfa ait metotlara ve fieldlara sahip olup, bunları kullanabilmesidir.

**Polymorphism**; child classın, parent classa ait olan metotları değiştirerek kullanabilmesidir.



```c#
Person p = new Student();
p.Read();

// Person, parent class'tır.
// Student, child class'tır.
// Bu örnek, eylem halindeki polymorphism örneğidir.

p.Read(); // dediğimiz zaman aslında STUDENT'a ait READ metodu çalışır.
```

---

</details>

### Object-Oriented Programlama nedir?

---

### Object-Oriented Diller Hangileridir?

Java

C#

C++

Python

JavaScript

PHP

---

### Dependency Injection Nedir?

Dependency Injection, Dependency Inversion prensibinin uygulanmasını içeren bir pattern'dir.

Dependency injection, sınıfların birbirine olan bağımlılıklarının kontrolü ve yönetimi için kullanılır.



A sınıfının, B sınıfının metotlarını kullanmak istediğini düşünelim. Bu bir bağımlılıktır.





```c#
public class Customer
{
     private MobileDeveloper developer;
  	
     public Customer()
     {
          developer = new MobileDeveloper();
     }
  
     public void CreateApp()
     {
          developer.MakeAnApplication();
     }
}
```

Yukarıda bir MobileDeveloper nesnesi üretildiğini görüyoruz.

Yani Customer nesnesi, MobileDeveloper nesnesini **oluşturmak zorunda**.

Bu durum **Sıkı Bağımlılık** (**Tight Coupling**) oluşturur. Çünkü Customer sınıfında, MobileDeveloper sınıfından bir nesne new'lememiz gerekmektedir.

Bu durumu gidermek için, Customer sınıfını, MobileDeveloper nesnesini new'leme sorumluluğundan kurtaralım.

```c#
public class Customer
{
     private MobileDeveloper developer;
  	
     public Customer(MobileDeveloper developer)
     {
          this.developer = developer;
     }
  
     public void CreateApp()
     {
          developer.MakeAnApplication();
     }
}
```

Artık Customer nesnesini kullanarak, yeni bir Application üreten metodu çalıştırmak için, Customer nesnesine bir MobileDeveloper enjekte etmek zorundayız.

```c#
public static void Main(string[] args)
{
     MobileDeveloper developer = new MobileDeveloper();
     Customer customer = new Customer(developer);
     customer.CreateApp();
}
```



Fakat müşteri, aynı uygulamanın Web versiyonunu da isteyebilir. Bu durumda yeni bir WebDeveloper eklememiz gerekir.

Ancak **Customer sınıfımızı MobileDeveloper'a bağımlı yazmıştık**. Bu bir sorun oluşturur.

Bu durumu çözmek için IDeveloper adında bir interface oluşturmamız gerekir.

````c#
public interface IDeveloper
{
     void MakeAnApplication();
}
````



Şimdi IDeveloper interface'ini hem MobileDeveloper hem de WebDeveloper sınıflarına implement ederiz.

````c#
public class MobileDeveloper : IDeveloper
{
     public MobileDeveloper() {}
  
     public void MakeAnApplication()
     {
          //Mobil uygulama üreten kodlar.
     }
}
````

````c#
public class WebDeveloper : IDeveloper
{
     public WebDeveloper() {}
  
     public void MakeAnApplication()
     {
          // Web uygulama üreten kodlar.
     }
}
````



Artık Customer sınıfındaki somut bağımlılığı düzelterek, interface üzerinden soyut bağımlı hale getirebiliriz. Bu sayede artık Customer sınıfı **Gevşek Bağımlı** (**Loosely Coupled**) hale dönüşmüş olur. Çünkü interface üzerinden bağımlı hale getirmiş oluruz. Bu sayede, Customer nesnesi oluştururken, istediğimiz türde bir Developer verebiliyor olacağız.

````c#
public class Customer
{
     private IDeveloper developer;
  	
     public Customer(IDeveloper developer)
     {
          this.developer = developer;
     }
  
     public void CreateApp()
     {
          developer.MakeAnApplication();
     }
}
````



Şimdi IDeveloper interface'inden implement edilmiş her somut sınıf, Customer nesnesine parametre olarak gönderilebilir.

```c#
public static void Main(string[] args)
{
     IDeveloper developer = new MobileDeveloper();
     //IDeveloper developer = new WebDeveloper();
     Customer customer = new Customer(developer);
     customer.CreateApp();
}
```



Bu sayede soyut yapılar üzerinden bağımlılık yaratarak, bağımlılığı azaltmış olduk.

Sıkı bağımlılık yerine Gevşek bağımlılık oluşturduk.

Bunu somut sınıfları enjekte etmek yerine soyut yapıları enjekte ederek sağladık.



Temel olarak 3 çeşit Dependency Injection yöntemi vardır.

- Constructor Injection
- Property (Setter) Injection
- Method Injection



Dependency Injection sayesinde;

- Loosely Coupled uygulamalar oluşturabiliriz.
- Uygulamada değişmesi gereken kodları minimum düzeye indirir.
- Test edilebilirliği artırır.



### Constructor Injection

Sınıfa ait bağımlılıkları, sınıfın constructor'ına parametre olarak geçerek uygulanır.

Bu sistem uygulandığında, sınıftan bir instance oluştururken mutlaka parametre olarak bağımlı olduğu değişkenin verilmesi gerekir.

````c#
public class PayrollSystem
{
     private BankingService _bankingService;
  
     public PayrollSystem(BankingService bankingService)
     {
          _bankingSystem = bankingSystem;
     }      
}
````

Yukarıdaki gibi bir class oluşturduğumuz zaman, bu sınıftan yaratılacak olan bir instance mutlaka BankingService tipinde bir değeri parametre olarak enjekte etmek zorundadır.

BankingService instance'ını parametre olarak geçmeden asla bir PayrollSystem instance'ı oluşturulamaz.

Aslında burada bir açık vardır. BankingService parametresini zorunlu tutmamıza rağmen, parametre olarak null bir değer verilebilir. Ve bu önlenmelidir. Null değer aldığında hata oluşacaktır.

````c#
public class PayrollSystem
{
     private BankingService _bankingService;
  
     public PayrollSystem(BankingService bankingService)
     {
          if(bankingService == null)
          {
               throw new ArgumentNullException();
          }
      	  _bankingSystem = bankingSystem;
     }      
}
````



**Constructor Injection ne zaman kullanılır?**

Sınıfın düzgün çalışabilmesi için mutlaka bir bağımlılığa ihtiyaç duyduğunda ctor injection uygulanır. Sınıf bağımlılık olmadan çalışamıyorsa, bu şekilde enjekte etmek gerekir. Sınıfın çalışması için 3 bağımlılığa ihtiyacı varsa, 3'ünü de bu şekilde ctor injection yapmalıyız.

Genelde sınıf içinde kullanılacak olan bağımlılık, birçok metotta kullanılıyorsa, ctor injection tercih edilmesi çok mantıklıdır. Eğer bağımlılık sadece tek bir metotta kullanılacaksa method injection kullanmak daha iyi bir tercih olacaktır.

Injection tanımlarken hataya yer vermemek için Guard Pattern uygulanması çok daha sağlıklı olur.



### Property Injection

Sınıfın bağımlılığa kesin olarak ihtiyacı varsa, Constructor Injection kullanmak gerekir demiştik.

Fakat bağımlılık, sınıf için gerekli değilse ne olacak?

Bazen sınıf için mutlak olarak gerekli olmayan ama eklendiği takdirde kullanabileceği bir bağımlılık olabilir.

Örnek olarak, bir Document sınıfı, grammar checker kullanabilir ya da kullanmayabilir. Eğer bir tane grammar checker var ise, sınıf bunu kullanır. Eğer yoksa class, placeholder olarak, default bir implementasyon dahil edebilir.

Bu tür bir durumdaki çözüm property injection uygulamaktır.

Sınıfınıza bir tane property eklersiniz. Bu property, sınıfın valid bir instance'ına set edilebilir olur.

Dependency bir property olduğundan, istenilen şekilde set edilebilir.

Eğer dependency istenmiyorsa ya da ihtiyaç duyulmuyorsa, olduğu gibi bırakılır.

Geçerli bir dependency varsa, onu property üzerinden kullanır. Geçerli bir dependency yoksa, sınıfın düzgün çalışabilmesi için default olarak valid (geçerli) bir implementasyon yaparız. Bu sayede sınıf hatasız şekilde çalışmaya devam eder.

Default olarak belirlenen değer null olmamalıdır. Valid bir implementasyon olmalıdır.



**Property Injection ne zaman kullanılır?**

Dependency, opsiyonel olduğu zamanlarda kullanılır.

Ya da sınıf, somut şekilde kullanılırken, değişken bir bağımlılık ihtimali varsa kullanılır. Kullanıcılar kendilerinin sağladığı implementasyonu kullandığı durumlarda, interface aracılığıyla sağlanır.

Property Injection bazen Setter Injection olarak da isimlendirilir.

Default implementasyon çoğunlukla fonksiyonsuz bir implementasyon olur. Ama böyle olmak zorunda da değildir. Eğer gerçekten çalışan ve bir şeyler yapan bir default implementasyon isteniyorsa, bu şekilde de kodlanabilir.



````c#
public interface IGrammarChecker
{
     void CheckGrammar();
}
````

Şimdi bu interface'i 2 kere implement edeceğiz. 

- Hiçbir şey yapmayan default versiyon
- Gerçek bir grammar checker olduğundaki versiyon



```c#
public class DefaultGrammarChecker : IGrammarChecker
{
     public void CheckGrammar()
     {
          Console.Write("Do nothing");
     }
}
```

```c#
public class RealGrammarChecker : IGrammarChecker
{
     public void CheckGrammar()
     {
          Console.Write("Grammar has been checked.");
     }
}
```



Şimdi property injection uygulayacağımız Document sınıfını yazalım.

```c#
public class Document
{
     private string _text;
     // property
     private IGrammarChecker _grammarChecker;
     public IGrammarChecker grammarChecker
     {
          set
          {
               if(value != null)
               {
                    _grammarChecker = value;
               }
          }
     }
  
  
     // ctor
     public Document(string text)
     {
          _text = text;
          _grammarChecker = new DefaultGrammarChecker();
     }
      
     public void CheckGrammar()
     {
          _grammarChecker.CheckGrammar();
     }
}
```



Bu kodla beraber, sınıf içindeki _grammarChecker field'ına, ctor içinde default olarak DefaultGrammarChecker tipinde bir instance atadık.

Yani bu Document sınıfından bir instance oluşturan kişi, default olarak DefaultGrammarChecker atamasına sahip olur.

Kullanıcı bunu istemiyorsa, istediği herhangi bir gerçek grammar checker instance'ını, sınıf içindeki _grammarChecker field'ına atayabilir.

```c#
public static void Main(string[] args)
{
     string text = "Bu örnek bir metindir.";
     Document document = new Document(text);
     document.CheckGrammar(); // Do nothing.
  	
     document.grammarChecker = new RealGrammarChecker();
     document.CheckGrammar(); // Grammar has been checked.
}
```



Property injection, bize **opsiyonel** bağımlılık imkanı sağlar.

**Eğer gerekliyse** bağımlılığı değiştirme imkanı sunar.

Örneğin dokümanlar farklı dillerde gelebilir. Bu nedenden dolayı haliyle farklı grammar checker'lar enjekte etmemiz gerekir. Property injection tam da bu sebepten dolayı kullanılır.





### Method Injection

Sınıfın ihtiyaç duyduğu bağımlılık çoğu zaman farklı olacaksa ne olur?

Bağımlılığı bir interface olarak oluştururuz ve farklı sınıflara implement ederiz. Ve sonrasında asıl sınıfımıza bağımlılık olarak ekleriz.

Mesela bunun için property injection kullanabiliriz. Ama böyle yaptığımız takdirde, sıkça değişecek olan bağımlılığı kullanan metodu çağırmadan önce, her zaman property'ye yeni atama yapmak durumunda kalırız. Bu durum, Temporal Coupling açısından bazı sorunlara yol açabilir.

(*Not: Temporal Coupling; bir sınıfın iki veya daha fazla metodu arasında, bu metotlardan birinin diğerinden önce çağırılmasını gerektiren örtülü bir ilişkisi bulunması durumunda ortaya çıkar. Bu şart, öğeleri zamansal boyutta sıkıca bağlaştırır. Mesela ardışık metot çağırmalarında hangisinin önce çağırılacağı önemliyse, söz konusu metotlar arasında zamansal bağlaşıklık vardır.*)



Constructor ve Property injection, bağımlılığın çok fazla değişmeyeceği durumlarda tercih edilir. Çok fazla implementasyon çeşitliliği varsa, method injection tercih edilir.

Method injection, tam da kullanım esnasında hangi bağımlılığı implement etmek istiyorsanız, onu edebileceğiniz bir imkanı sağlar.

```c#
public interface IFoodPreparer
{
     void PrepareFood(Recipe recipe);
}
```

```c#
public class Baker : IFoodPreparer
{
     public voic PrepareFood(Recipe recipe)
     {
          Console.Write("Use baking skills to do " + recipe.Text);
     }
}
```

```c#
public class FastOrderCook : IFoodPreparer
{
     public voic PrepareFood(Recipe recipe)
     {
          Console.Write("Use fast skills to do " + recipe.Text);
     }
}
```

```c#
public class Chef : IFoodPreparer
{
     public voic PrepareFood(Recipe recipe)
     {
          Console.Write("Use chef skills to do " + recipe.Text);
     }
}
```

```c#
public class Restaurant
{
     public string Name { get; set;}
  	
     public Restaurant(string name)
     {
          Name = name;
     }
  
     public void MakeFood(Recipe recipe, IFoodPreparer foodPreparer)
     {
          foodPreparer.PrepareFood(recipe);
     }
}
```



Tarifin ne olduğuna bağlı olarak, preparer nesnesi de değişiklik gösterir.

Bunu sadece metodu kullanacak olan kişi bilir. Hangi tarif için hangi preparer kullanılsın.

Bu tür bir durumda her defasında property injection ile atama yapmak da çok hantal kalacaktır.

Ve aynı zamanda devamlı property ataması yapmak, Temporal Coupling'e sebep olacaktır.

Burada en iyi çözüm, IFoodPreparer nesnesini kullanılacağı duruma göre metot parametresi olarak geçmektir.

Method injection, dependency'nin her kullanımda değişeceği durumlarda kullanılır. Ya da hangi durumda hangi dependency'nin geleceğinin önceden bilinmediği durumlarda kullanılır.



**Özetle**: Method injection 2 durumda kullanılır.

- Bağımlılığın sıkça değişme ihtimali olduğunda
- Her kullanımdan sonra bağımlılığın yenilenmesi gerektiğinde

Her 2 durumda da karar, metoda implementasyonu verecek olan kullanıcıya bağlıdır.

---

### Inversion of Control Nedir?

---

### IoC Container Nedir?

---





# SOLID Prensipleri

- Robert C. Martin tarafından tanımlanan prensiplerdir.
- Yazılımcıların birlikte çalışabileceği, anlaşılır, okunabilir, test edilebilir kodlar yazabilmek içindir.



Solid, 5 adet prensipten oluşur.

- **Single Responsibility Principle**
- **Open-Closed Principle**
- **Liskov Substitution Principle**
- **Interface Segregation Principle**
- **Dependency Inversion Principle**

---

### Single Responsibility

* Bir class **tek bir iş yapmalıdır**.

- Aynı zamanda bir class değişecekse, **sadece tek bir nedenden dolayı değişmelidir**.

Örneğin belli field'lar içeren bir Student entity sınıfı olsun. Bu sınıf yalnızca **data model** değişirse, değişebilir.



Farklı bir örnek düşünelim. 

Örneğin Kitap satışı yapılan bir proje geliştiriyoruz.

Fatura adında bir class var.

Burada Faura ile ilgili field'lar var.

Aynı sınıfta, Faturaya ait property'leri ekrana yazan bir PrintInvoice metodu da var.

Ve yine aynı sınıfta, Fatura bilgilerini bir dosyaya yazan SaveToFile metodu da var.

İşte burada Single Responsibility prensibini ihlal etmiş oluyoruz.

Bunun yerine InvoicePrinter isimli bir class oluşturup, ekrana yazma görevini o sınıfa vermeliyiz.

Ayrıca InvoicePersistence isimli bir class oluşturup, dosyaya yazma işlevini de o sınıfa vermeliyiz.

Fatura sınıfıyla alakalı bu 2 sınıfa, constructor injection ile Fatura nesnesini yollayabiliriz.

---

### Open-Closed Principle

Classlar **geliştirmelere açık** fakat **değişimlere kapalı** olmalıdır.

Yani class'a ait kodlara dokunmamamız gerekir.

Peki o zaman yeni bir özellik nasıl ekleyeceğiz?

Mesela fatura bilgilerini **dosyaya yazan bir sınıfımız ve içinde metodumuz vardı**.

Biz ek olarak aynı bilgileri **veritabanına yazan bir metot da olmasını istiyoruz**. Ne yaparız?

Dosyaya yazan sınıfın içine yeni bir metot ekleyip, database'e yazan bir metot eklemek YANLIŞTIR.

Onun yerine **Interface** veya **Abstract Class** kullanmalıyız.

```c#
interface IinvoicePersistence 
{
     void Save(Invoice invoice);
}
```

Bu şekilde bir Interface oluştururuz. Ve log işlemi yapacak olan sınıflara implemente ederiz.

```c#
public class DatabasePersistence : IinvoicePersistence 
{
     public void Save(Invoice invoice) 
     {
          // Save to DB
     }
}

public class FilePersistence : IinvoicePersistence 
{
     public void Save(Invoice invoice) 
     {
          // Save to File
     }
}
```



Interface oluşturmadan, doğrudan 2 farklı sınıf oluştursak da olmaz mıydı?

Olurdu ama hatalı olurdu.

Başka Manager sınıflarında, bu interface sayesinde artık loglama yapan sınıfları parametre olarak verirken, **Referans Tutucu** işlevinden faydalanabiliriz. Interface'i bir referans tutucu olacak kullanırız.

---

### Liskov Substitution

Child sınıflar, Base sınıfları yerine kullanılabilir olmalıdır.

Yani, Base sınıfı objesini parametre olarak geçebileceğimiz her yerde Child sınıfı objesini de kullanabiliyor olmamız gerekir.

Bunu uygularken hiçbir hata almamamız gerekir.

Zaten mantık olarak da bunun gerçekleşmesi beklenir.

Çünkü bir base sınıfı, bir child sınıfa inherit ederken, base sınıfın tüm özelliklerinin child sınıfa aktarılması beklenir. Bu durumda child class, base class'ın genişletilmiş bir versiyonudur.

---

### Interface Segregation

Bu prensip, interface'leri ayırmakla ilgilidir.

Bir class, ihtiyacı olmayan bir metodu kullanmaya zorlanmamalıdır.

Bundan dolayı interface'lerin de bölünmesi faydalıdır.

Bir otopark yazılımı örneği üzerinden düşünelim.

Park yeri interface'i oluşturalım.

```c#
public interface IParkingLot 
{
     void parkCar();
     void unparkCar();
     void getCapacity();	
}
```

```c#
public interface IFreeParkingLot : IParkingLot
{
  
}
```

```c#

public interface IUcretliParkingLot : IParkingLot
{
     double calculateFee(Car car);
     void doPayment(Car car);	
}
```





Araba hareketleri ve ödeme işlemi için bazı metot imzaları bulunuyor.

Bunu bir park yeri classına implemete edebiliriz.

Peki ya **ücretsiz otopark** sınıfı da oluşturmak istersek ne olacak?

Ücretsiz otopark sınıfı **CalculateFee** ve **DoPayment** metotlarını kullanmaz.

O halde hatalı bir interface tasarımı olmuş demektir.

Bunun çözümü olarak interface'i de parçalamalıyız.

**ParkYeri** adında bir parent interface olur.

Onu implemente eden 2 child interface olur.

**UcretliParkYeri** ve **FreeParkYeri** olarak 2 child interface oluşturmamız en mantıklısı olacaktır.

---

### Dependency Inversion

Sınıflar arası bağımlılıklar olabildiğince az olmalıdır.

Üst seviye sınıflar, **somut olan** alt seviye sınıflara bağımlı OLMAMALIDIR.

Alt sınıflarda yapılan değişiklikler, üst sınıfı ETKİLEMEMELİDİR.

Alt seviyedeki sınıflar, üst seviyedeki sınıfta yapılan değişikliklere UYUM SAĞLAMALIDIR.



Bu sorunları çözebilmek için;

Classlar, somut sınıflara ya da somut metotlara bağımlı **OLMAMALIDIR**.

Classlar, her zaman **soyut bağımlılıklar** ile bağlanmalıdır.

Üst seviye bir sınıfla, alt seviye sınıf arasına soyut bir yapı koymalıyız.

```c#
public class Email
{
     public void SendEmail()
     {
          // send email
     }
}
```

```c#
public class Sms
{
     public void SendSms()
     {
          // send sms
     }
}
```



Bildirim göndermek istediğimizde, 2 sınıfı da çalıştırması için oluşturduğumuz Notification sınıfını yazalım.

```c#
public class Notification
{
     private Email email = new Email();
     private Sms sms = new Sms();
  
     public void Sender()
     {
          email.SendEmail();
      	  sms.SendSms();
     }
}
```

Notification sınıfımız **yüksek seviyeli bir sınıf** olmasına rağmen, **düşük seviyeli email ve sms sınıflarına bağımlı hale gelmiştir**. 

Sms veya email sınıflarında bir değişiklik olduğu zaman, Notification sınıfında da değişiklik yapmamız gerekecek. Demek ki Dependency Inversion prensibine aykırı hareket etmiş olduk.

Bu somut bağımlılığı ortadan kaldırmak için soyutlama yapmamız gerekmektedir.

Bu çözümü uygulamak için Email ve Sms sınıflarını kapsayacak bir interface yazabiliriz.

```c#
public interface IMessage
{
     void SendMessage();
}
```

```c#
public class Email : IMessage
{
     public void SendMessage()
     {
          // Email gönder.
     }
}
```

```c#
public class Sms : IMessage
{
     public void SendMessage()
     {
          // Sms gönder.
     }
}
```



Şimdi Notification sınıfımızı yazalım.

```c#
public class Notification
{
     private List<Message> messages;
  	
     public Notification(List<Message> messages)
     {
          this.messages = messages;
     }
  
     public void Sender()
     {
          foreach(var message in messages)
          {
               message.SendMessage();
          }
     }
}
```

Yüksek seviyeli sınıfın, alt seviyeli sınıflara olan bağımlılıklarını kaldırdık.

artık soyut katman üzerinden işlemlerimizi yapabiliyoruz.

DIP sayesinde Loosely Coupled bir yapı sağladık.



---

# Design Pattern ve Architecture Soruları



### Microservice Mimarisi nedir?

Tek başına, bir tane sorumluluğu olan ve tek bir iş yapan (sadece o işe ait görevleri yürüten) modüler projelerdir.

Microserviceler, bir yazılım uygulamasında belirli özellik ya da fonksiyonu sağlayan, tek bir amaca hizmet eden, birbirinden bağımsız yazılım servislerdir. Bu hizmetlerin bağımsız olarak bakımı yapılabilir, izlenebilir ve dağıtılabilir.



Micrservice mimarisi, SOA (services oriented architecture) üzerine kurulmuş bir mimaridir.

Uygulamalar, tek bir ağ üzerinden birden çok makineye dağıtıldığında, bu servislerin sistemde iletişim kurmasını sağlayan mimarilerden biri SOA'dır.



Tek bir uygulama geliştirirken, modüler bir yapıda birçok küçük servis olarak düşünülebilir.

Her servis kendi işini ve kendi iletişimini yürütür.

Servisler karmaşık olmaz, başka servislere bağımlılığı az olur.

Her bir microservice diğer hizmetler ile (loosely coupled) oldukça az bağımlılığa sahip bir şekilde çalışmaktadır.

Farklı dillerle geliştirilebilirler, farklı database teknolojileri kullanabilirler.



Microservice mimarisine uygun geliştirilen herhangi bir servis üzerinde, geliştirici bağımsız olarak çalışabilir, böylece geliştirme aşaması da kolaylaştırılmış olur.



Avantajları:

- Bağımsız Deployment: servisler birbirinden bağımsız olarak, ayrı ayrı deploy edilebilir.
- Microserviceler, otomatize bir şekilde gerekli aşamalardan geçirilerek deploy edilmelidir. Bu aşamalar; unit tests, intergration tests, sonarqube, automation tests, vs) gibidir.
- Her servis, diğer servislerden bağımsız olarak geliştirilebilir.
- Hata İzolasyonu: projenin bir yerinde oluşan sorun, diğer bölümleri etkilemez. Projeler çalışmaya devam eder.
- Herhangi bir serviste oluşacak trafik tüm sistemin scale olmasını gerektirmeden, trafik altındaki servis çoklanarak sorun ortadan kaldırılabilir.
- Gereksinime göre, uygun olan teknolojiler kullanılarak servisler geliştirilir.
- Tüm microserviceler birbirleriyle REST veya Message Bus üzerinden haberleşmelidir. İkisi birden de kullanılabilir.



- **Decoupling** — Bir sistemdeki servisler büyük ölçüde birbirinden bağımsızdır.
- **Componentization** — Microserviceler, kolayca değiştirilebilen ve versiyonları artırılabilen bağımsız bileşenlerdir.
- **Business Capabilities** — Bir microservice basit bir yapıdadır ve tek bir göreve odaklanır.
- **Autonomy** — Geliştiriciler ve ekipler birbirlerinden bağımsız olarak çalışabilir, böylece hızlıca geliştirme ve test süreçleri yürütülebilir.
- **Continuous Delivery** — Yazılım geliştirme, test etme ve onaylama sistematik otomasyonu ile sık sık yazılım sürümlerini canlıya almaya otomatik bir biçimde izin verir. Servisler ayrı ayrı deploy edilebileceği için, deployment süresi kısalır ve maliyet zamanla azalır.
- **Decentralized Governance** — Odak, doğru iş için doğru aracı kullanmaktır. Bu, standart bir teknoloji veya yapıyı zorunlu kılmadığı anlamına gelir. Geliştiriciler, sorunlarını çözmek için en iyi teknolojiyi seçme özgürlüğüne sahiptir.
- **Agility** — Microserviceler çevikliği destekler. Herhangi bir yeni özellik hızla geliştirilip sisteme adapte edilebilir.

---

### Singleton Design Pattern nedir? 

Singleton Design Pattern; Creational Design Pattern kategorisindedir.

Bu tasarımdaki amaç, **bir class'tan sadece 1 instance yaratılmasını** sağlamaktır.

Yani bir class'tan bir instance yaratılmak istendiğinde, eğer daha önce yaratılmış bir instance yoksa, yeni bir tane yaratılır. Daha önce yaratılmış bir tane varsa, o instance kullanılır.



En yaygın singleton tasarım örneklerinden biri **Logger**'dır.



Bir class’ın singleton tasarım örüntüsüne uygun olması için temelde üç adım vardır;

- Constructor **private** olmalı. Bu yapılan işlem new ile nesne oluşturulmasını engeller.
- Class ile aynı türde **static bir member** oluşturulur.
  Örneğin;
  class **SingletonExample** 
- {
          private static **SingletonExample** instance;
  }
- **Static member**’a ulaşmak için **static bir metot** oluşturulmalıdır.
  Örneğin;
  public **static** Singleton getInstance() { … return **instance**; }

```c#
public class SingletonExample 
{
     private static SingletonExample instance;

     private SingletonExample(){}

     public static SingletonExample getInstance()
     {
          if (instance == null)
          {
               instance = new SingletonExample();
          }

          return instance;
    }
}
```



Bu sayede aslında herkes aynı instance'a erişir. ve global değişken yaratmaktan da kaçınmış oluruz.

---

### Run Time ve Compile Time nedir?

Compile-time: Kaynak kodun, executable koda dönüştürüldüğü zamandır.

Run-time: Executable kodun, çalışmaya başladığı zamandır.



Run-time ve Compile-time, farklı tipte hatalar oluşturur.



Compile-time errors: Yanlış syntax kullanıldığında oluşan hatalardır.

Eğer yanlış syntax veya semantic yazarsak, compile-time hataları derleyici tarafından alınır.

Compiler, tüm hatalar kaldırılana kadar, programın çalışmasına izin vermeyecektir.

Tüm hatalar kaldırıldığında Compiler, executable kodun oluşmasına izin verecektir.

Compile-time hataları 2 sebepten kaynaklanır.

- Syntax error
- Semantic error



Run-time error: Bu tip hatalar, derlemeden sonra oluşur.

Örneğin sıfıra bölme hatası bunlardan biridir.

Derleyici bu tür hatalara işaret etmez, o yüzden bu hataların bulunması kolay değildir.

---

### MVC nedir?

ASP.NET MVC olarak kullanılır.

MVC, bir tasarım desenidir. Microsoft'a özel bir şey değildir.

ASP.NET MVC Framework ise asp'nin mvc desenine göre yazılmış bir versiyonudur.



mvc, 3 tane bileşenler oluşur.

- model
- view
- controller



Bu desen, asla bir katmanlı mimari değildir.

Bu, arayüzler için bir tasarım desenidir.

Request ilk olarak geldiğinde, controller'a gelir.

Gelen isteğe göre ne yapılması gerekiyorsa, controller'da kodlanır.

İstek o anda ne ise, controller ona göre hareket eder. Her istek için her zaman 3 yapı da kullanılmaz. Örneğin controller'a gelen istek, sadece bir html sayfasının gösterilmesiyse, o halde controller doğrudan view'ı çağırır.

Hatta bazen gelen istek, sadece controller içinde halledilir.



Datalar ise model diye adlandırılan nesnelerdir.

Örneğin controller'a bir istek geldi. Tüm müşterilerin listelenmesi gerekiyor.

Controller, müşterileri bir view içinde listelemek durumundadır.

Controller, view'u açarken, ona bir de data (model) gönderir.



Kısaca;

**Controller**, istekleri karşılayan yapı.

**View**, html - css - javascript yani görüntülenecek sayfa.

**Model**, view'da gösterilecek olan datadır. ya da kullanıcının bilgileri doldurup, controller'a yolladığı datadır.

---
