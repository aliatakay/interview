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

    public static SingletonExample getInstance(){

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

# C# Soruları



### Object nedir?

---

### Local Variable - Field - Property - Auto Property

**Local Variable**: Bir metot ya da blok içinde tanımlanan değişkenlerdir. Bu değişkenler sadece bulunduğu blok içinde var olur. Bu local değişkenlere, bulunduğu blok haricinde hiçbir yerden **erişilemez**. Bu yüzden hiçbir access modifier almaz.

```c#

public bool CheckIfPassed(double average)
{
     int passingScore = 50; //bu değişkene sadece bu metot içinde erişilir.
     if(average >= passingScore) return true;
     return false;
}

```



**Field**: Bir class içinde, herhangi bir tipte, doğrudan tanımlanan değişkenlere denir. Access modifier kullanılabilir. Fakat genelde hep private olarak kullanılır. Çünkü bu değişkene dışarıdan doğrudan erişilmesini istemeyiz. Erişimi sağlamak için property'ler kullanırız.

```c#
public class Rectangle
{
  	private int shortEdge;
  	private int longEdge;
  //...
}
```



**Property**: Private bir field'ın; read, write, compute işlemlerini yapmayı sağlayan yapıdır. Property'lerin kendisi değer tutmazlar. Get ve set metotları ile ramdeki bir veriyi getirir. Property sayesinde, private olan field'ı nasıl set edeceğimizi ve nasıl get edeceğimizi belirlemiş oluruz. Örneğin shortEdge değeri 0'dan küçük olamaz.

```c#
public class Rectangle
{
  	private int _shortEdge;
  	public int shortEdge
    {
      	get
        {
          	return _shortEdge;
        }
      	set
        {
          	if(value > 0) _shortEdge = value;
          	else throw new ArgumentException();
        }
    }
}
```



**Auto Property**: Property ve Field ikilisini kısa şekilde yazmanın bir yöntemidir.

```c#
public class Rectangle
{
  	public int ShortEdge { get; set; }
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
            catch (DivideByZeroException) {  
                Console.WriteLine("Not possible to Divide by zero");
            }
            catch (IndexOutOfRangeException) {
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

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

---



# Git Soruları



Git, 3 adet çalışma ağacına sahiptir.

- Working Directory
- Staging Area / Index
- Repository
- Remote Repository ( 3 ağacın sonunda GitHub gibi remote repository'ye pushlanır.)



### Git Komutları



**git clone <*url*>** 					Remote bir repoyu, local bilgisayara klonlamak için

**git status** 			 				Bulunduğumuz branch'i görmek için

​                              				Working Tree'deki değişiklikleri görmek için

**git add <*filename*>** 	 		Untracked (izlenmeyen) bir dosyayı, git'in takip etmesini sağlar.

​											  Aynı zamanda bu komut ile dosyalar, Staging Area'ya taşınmış olur.

**git commit -m <*mesaj*>** 	  Stage'deki dosyaları repository'ye taşır.

​											   Tüm dosyalar hala local repo'da bulunmaktadır.

**git push origin master** 		Repo'daki dosyaları, remote repo'ya gönderir. (GitHub gibi)



---



# Testing



### Unit Test nedir?

Herhangi bir **I/O işlemi gerçekleştirmeden**, sadece kodun logic'i ve algoritma test edilir.

Bunu yaparken, public, internal gibi ulaşılabilir metotlar / birimler test edilir. Public olan metotlar da zaten private yapılara erişiyordur mutlaka.

Unit testler çok hızlı olmalıdır.

Bağımlılıkları olan birimler test edilirken, bağımlılıkları sahteleriyle değiştirmek gerekmektedir. Aksi halde metotların, bağımlı olduğu yapıları da test etme işine girişmeye başlıyoruz. Bu da unitleri yani birim halindeki metotları test etme mantığından uzaklaşıyor, birçok birimi test etmeye dönüşür. Bu da istenmez.



Mock, Stub (fakeler oluştururken devreye giren sahte dependency'ler, aralarında fark var.)

Sınıfımızın bağımlı olduğu sınıfları, sahteleriyle değiştirebilmemiz gerekiyor.

Bundan dolayı, dependency injection kavramı devreye giriyor.



```c#
				[Fact]
        public void Add_SimpleValuesShouldCalculate_1()
        {
            // Arrange
            double expected = 5;

            // Act
            double actual = Calculator.Add(2, 3);

            // Assert
            Assert.Equal(expected, actual);
        }
```



XUNit kullandım!!!!!



```c#
[Theory]
[InlineData(4,5,9)]
[InlineData(-10,-55,-65)]
[InlineData(0,0,0)]
public void Add_SimpleValuesShouldCalculate(double number1, double number2, double expected)
{
       // Arrange

       // Act
       double actual = Calculator.Add(number1, number2);

       // Assert
       Assert.Equal(expected, actual);
}
```



---

### Integration Test nedir?

---

### Mocking nedir?

---

### TDD  Test-Driven Development nedir?

Önce test yazılmasını öneren sistemin, genişletilmiş sistemsel bir halidir.



1. Bir test yazılır.
2. Test başarısız olur.
3. Test başarılı hale getirilir.
4. Mevcut bütün testlerin başarılı olması sağlanır.
5. Kod refactor edilir. Yani kodda iyileştirme ve(ya) temizleme yapılır.

Ve birinci adıma geri dönülür. Bu döngü sürekli olarak devam eder.



TDD'de mutlaka ve mutlaka test, koddan önce yazılmalıdır.

---

### 

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

# Docker



Örneğin belli kapasitede donanımlara sahip bir makinemiz var.

Bu makinenin, sahip olduğu RAM, harddisk ve bir adet işletim sistemi var.

Bu makineyi, **hypervisor** sayesinde sanal makinelere bölebiliyoruz.

Herbir sanal makineye, istediğimiz kapasitede ram, harddisk ayırabiliyoruz. Ve herbir sanal makineye istediğimiz işletim sistemini de kurabiliyoruz.

![virtual](https://cdn-media-1.freecodecamp.org/images/1*RKPXdVaqHRzmQ5RPBH_d-g.png)

Hypervisor sayesinde, makinemize sanal makineler kurabildik.

Bu sanal makinelere, istediğimiz işletim sistemlerini kurabildik.

Bu işletim sistemlerine de ihtiyaç duyulan sürümleri (java, python vs) kurabildik.

Bu sayede istediğimiz uygulamaları da çalıştırabildik.



Fakat yöntemde de sorunlar var. 

Örneğin biz 10 mb uygulama çalıştırmak için, bir sanal makineye farklı bir işletim sistemi kuracağız. Ama işletim sistemi 30 gb yer kaplıyor.

Bu büyük bir sorundur. İşte Docker sayesinde bu sorunu ortadan kaldırıyoruz.

![docker](https://cdn-media-1.freecodecamp.org/images/1*V5N9gJdnToIrgAgVJTtl_w.png)

Bu yapıda Docker Engine sayesinde, Guest olan işletim sistemlerini kurmaya artık gerek kalmıyor.

Dolayısıyla bir windows için 30gb ayırmamıza gerek yok.



Docker Engine, doğrudan **Host işletim sistemini kullanarak sanallaştırma** yapıyor.



**Container** : izole edilmiş ortam demektir.

Docker, host olan işletim sistemi üzerinde, parça parça işletim sistemleri oluşturuyor ve ihtiyaca göre donanımları ayırıyor.

Bu sanallaşan işletim sistemleri, diğer container'lardaki işletim sistemlerinin process'lerini görmüyor, donanım gereksinimlerini görmüyor.



Docker aynı zamanda şunu sağlıyor; yazılımcının bilgisayarında çalışan projenin, diğer bilgisayarlarda da sorunsuz çalışacağının garantisini veriyor.

Çünkü docker sayesinde, geliştirilen projenin ortamını her şeyiyle beraber taşıyabiliyorsun.

Bu tür bir yapıyı kullanmak genel olarak DevOps görevindeki kişiler için faydalıdır.
