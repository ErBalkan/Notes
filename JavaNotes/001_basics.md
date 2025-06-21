# ✅ 1. Java Programının Genel Yapısı

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Merhaba Java!");
    }
}
```

## 🔍 Açıklaması:
1. `public class Main:` Java’da her şey bir class içinde yazılır. Class, bir yapıdır. Main bizim sınıfımızın adı.

2. `public static void main(String[] args):` Java programlarının çalıştığı ilk yer burasıdır. JVM (Java Virtual Machine) önce main metodunu bulur, sonra çalıştırır.

3. `public:` Her yerden erişilebilir (access modifier).

4. `static:` Nesne oluşturmadan çalıştırabilmek için kullanılır.

5. `void:` Bu metod geriye bir şey döndürmez.

6. `String[] args:` Komut satırından parametre almamıza olanak tanır (şimdilik kenarda dursun).

7. `System.out.println(...):` Konsola çıktı verir. Bu, Java'nın temel loglama/çıktı komutudur.


# ✅ 2. Java’da Noktalı Virgül ;
Java’da her ifade (statement) sonunda `;` gelir.

```java
int x = 10; // Doğru
System.out.println(x); // Doğru
```
Eğer noktalı virgülü unutursan:

```java
int x = 10   // Hata!
```

Bu, __compile-time error (derleme zamanı hatası)__ verir.

# ✅ 3. Java Büyük/Küçük Harf Duyarlılığı (Case Sensitive)

Java, büyük-küçük harf ayrımına duyarlıdır:

```java
int number = 5;
int Number = 10;
```

Bu iki değişken farklıdır. __System, system, SYSTEM__ hepsi farklıdır. Bu yüzden yazarken çok dikkatli olmalısın.

# ✅ 4. Yorum Satırları (Comments)

Kod okunabilirliği için yorumlar çok önemlidir:

```java
// Bu tek satırlık yorumdur

/*
 * Bu ise
 * çok satırlı
 * bir yorumdur
*/
```

Kod yazarken, neden o şekilde yazdığını belirtmek için yorumlar kritik önemdedir, özellikle ekip içinde çalışıyorsan.

# ✅ 5. Değişken Tanımlama (Variable Declaration)

```java
int age = 25;
String name = "Patron";
boolean isActive = true;
```

## 📌 Detaylar:
- Her değişkenin tipi bellidir: __int, String, boolean__, vs.
- Java strongly typed bir dildir. Tipi doğru vermek zorundasın.
- Tip uyuşmazlığı derleme hatasına sebep olur.

# ✅ 6. Anahtar Kelimeler (Keywords)

Java'da özel anlamı olan kelimelerdir, değişken ismi olarak kullanılamazlar:

Örnekler:

`class` | `static` | `public` | `void` | `int` | `if` | `else` | `return` | `new` | `try` | `catch` | `finally`

# ✅ 7. Bloklar {}

Java’da bloklar scope'ları yani kodun sınırlarını belirler:

```java
if (x > 0) {
    System.out.println("Pozitif");
}
```

Kod blokları her zaman `{}` içinde yazılır. Python gibi girintiyle çalışmaz, süslü parantezle çalışır.

# ✅ 8. Giriş Noktası: main() Metodu

Her çalıştırılabilir Java programı, bir `main()` metoduna ihtiyaç duyar.

```java
public static void main(String[] args) {
    // Kod burada başlar
}
```

Burayı silersen ya da yanlış yazarsan program çalışmaz.

# ✅ 9. Print/Output Komutları

Konsola veri yazdırmak için:

```java
System.out.print("Merhaba");
System.out.println(" Java");
```

- `print` : Satır sonuna geçmeden yazdırır.
- `println` : Yazdırır ve alt satıra geçer.

# ✅ 10. Dosya Adı ile Class Adı Aynı Olmalı (Public Class için)

Eğer bir sınıfı __public__ olarak tanımlarsan, dosya adının da aynı olması zorunludur.

```java
public class BlogApp { // --> Dosya adı: BlogApp.java
}
```

Eğer isimler uyuşmazsa, __derleyici (compiler)__ hata verir.

# ✅ 11. Java Derleme ve Çalıştırma Süreci
1. `.java` uzantılı dosya yazılır.

2. `javac DosyaAdi.java` __→__ Java Compiler, `.class` __(bytecode)__ dosyasını oluşturur.

3. `java DosyaAdi` __→__ JVM bu bytecode’u çalıştırır.

```
"Java syntax'ı bir dilin grameri gibidir. İyi konuşmak istiyorsan, önce kurallarını ezber değil, anlayarak öğrenmelisin. Bu temel seni kurumsal yazılım mimarisine kadar götürür."
```

