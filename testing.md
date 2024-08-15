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
