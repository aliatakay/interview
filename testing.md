# Testing

### Unit Test nedir?

Herhangi bir **I/O işlemi gerçekleştirmeden**, sadece kodun logic'i ve algoritma test edilir.

Bunu yaparken, public, internal gibi erişilebilir metotlar test edilir. Public olan metotlar zaten private metotlara eriştiği için onlar da dolaylı yoldan test edilmiş olur.

Unit testler çok hızlı olmalıdır.

Bağımlılıkları olan metotlar test edilirken, bağımlılıkları sahteleriyle değiştirmek gerekmektedir. Aksi halde metotların, bağımlı olduğu yapıları da test etmemiz gerekir. Bu da birim metotları test etme mantığından uzaklaşır ve birçok birimi test etmeye dönüşür. Bu da istemediğimiz bir şeydir.

```c#
[Fact]
public void Sum_ShouldSumTwoNumbers()
{
     // Arrange
     var expected = 5;

     // Act
     var actual = Calculator.Sum(2, 3);

     // Assert
     Assert.Equal(expected, actual);
}
```

```c#
[Theory]
[InlineData(2, 3, 5)]
[InlineData(-3, -5, -8)]
public void Sum_ShouldSumTwoGivenNumbers(int number1, int number2, int expected)
{
     // Arrange

     // Act
     var actual = Calculator.Sum(number1, number2);

     // Assert
     Assert.Equal(expected, actual);
}
```

---

### Integration Test nedir?

---

### Mocking nedir?

Mock, Stub (Farklı kavramlar)

Sınıfımızın bağımlı olduğu sınıfları, sahteleriyle değiştirebilmemiz gerekiyor.

Bu noktada, Dependency Injection devreye giriyor.

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
