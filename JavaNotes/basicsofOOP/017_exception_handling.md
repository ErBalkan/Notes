# 🚨 Java Exception Handling

## 1️⃣ Neden Exception Handling?

- Uygulamanın kontrol dışı hatalar yüzünden çökmesini önler.

- Hataları mantıklı bir şekilde yönetmek ve kullanıcıya düzgün geri bildirim vermek için kullanılır.

- Sistem güvenilirliğini ve kod kalitesini artırır.

- Büyük kurumsal projelerde mutlaka standartlaştırılması gereken bir altyapıdır.

## 2️⃣ Temel Kavramlar

| Terim                   | Açıklama                                                                               |
| ----------------------- | -------------------------------------------------------------------------------------- |
| **Exception**           | Program çalışırken oluşan beklenmedik durumlar, hata nesneleri                         |
| **Throwable**           | Exception ve Error sınıflarının üstü, tüm fırlatılabilir nesnelerin temel sınıfı       |
| **Error**               | JVM hataları (OutOfMemoryError gibi), program tarafından yakalanmaz genelde            |
| **Checked Exception**   | Derleme zamanında zorunlu olarak handle edilmesi gereken istisnalar (IOException gibi) |
| **Unchecked Exception** | RuntimeException’dan türeyen, zorunlu handle edilmeyen hatalar                         |


## Exception Handling Yapısı: try-catch-finally

```java
try {
    // Riskli kod bloğu
} catch (ExceptionTipi e) {
    // Hata yönetimi
} finally {
    // Her durumda çalışan temizlik kodu (opsiyonel)
}
```

`Örnek:`

```java
try {
    int[] arr = new int[5];
    System.out.println(arr[10]);  // ArrayIndexOutOfBoundsException
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Dizi sınırları dışında erişim!");
} finally {
    System.out.println("Temizlik işlemi yapılıyor.");
}
```

## Çoklu catch blokları

Java 7+ ile aynı blokta farklı exception tiplerini ayrı ayrı veya 
tek satırda yönetebilirsin.

```java
try {
    // riskli kod
} catch (IOException | SQLException e) {
    // Ortak hata yönetimi
} catch (Exception e) {
    // Diğer genel hatalar
}
```

## throw vs throws

| Terim      | Açıklama                                                                                                         |
| ---------- | ---------------------------------------------------------------------------------------------------------------- |
| **throw**  | Bir exception objesini açıkça fırlatmak için kullanılır (runtime içinde)                                         |
| **throws** | Metot imzasında, o metodun hangi exception’ları fırlatabileceğini belirtmek için kullanılır (compile-time bilgi) |

`Örnek:`

```java
void dosyaOku(String path) throws IOException {
    if (path == null) {
        throw new IllegalArgumentException("Dosya yolu null olamaz!");
    }
    // Dosya okuma işlemi
}
```

## Custom Exception (Özel İstisna Sınıfı)

Kurumsal projede, domain’e özel exception’lar yaratmak standarttır.

```java
public class UserNotFoundException extends Exception {
    public UserNotFoundException(String message) {
        super(message);
    }
}
```

## Best Practices – Kurumsal Perspektif

- Checked exceptions ile çalışırken anlamlı ve net mesajlar ver.

- catch bloklarında sadece gerekli işlemleri yap, hatayı üst katmana iletmek için logla ve re-throw et.

- finally bloğunu kaynakları (DB bağlantısı, file stream vs.) kapatmak için kullan.

- Gereksiz geniş catch(Exception e) kullanmaktan kaçın, exception’ları spesifik yakala.

- Custom exception kullanarak domain mantığını netleştir, hata ayıklamayı kolaylaştır.

## Hata Yönetiminde Öne Çıkan Kurumsal Tasarım Modelleri

- `Global Exception Handler (ControllerAdvice - Spring Framework):` API katmanında merkezi hata yönetimi.

- `Exception Translation:` Alt sistemden gelen exception’ları üst sistem için anlamlı hale getirme.

- `Fail Fast Principle:` Hata olduğunda mümkün olan en erken zamanda dur, problemi büyütme.

- `Circuit Breaker Pattern:` Özellikle mikroservis mimarilerinde hata izolasyonu ve yönetimi.


